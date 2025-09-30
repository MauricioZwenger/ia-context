---
{
  "created_at": "0001-01-01T00:00:00Z",
  "description": "Indicates the basic structure of an asynchronous repository",
  "modified_at": "0001-01-01T00:00:00Z"
}
---
# Guide and Template for .NET 8 Repositories with Dapper

This document contains the guidelines and best practices for building a repository, culminating in a ready-to-use code template that exemplifies all the points described.

---

## Implementation Guide

#### **Objective**
To create a reusable C# repository class template for a .NET 8 application using Dapper, focusing on modern patterns, readability, and best practices.

#### **Core Requirements**

* **Naming and Style Conventions**
    * **Private Fields:** Use an underscore prefix (`_`) for all private field names (e.g., `_tenantConnection`, `_columnMapping`).
    * **Descriptive Names:** Employ clear and descriptive names for all variables, constants, and methods to ensure code clarity.

* **C# 12 Syntax**
    * **Primary Constructors:** Use for dependency injection (e.g., `ITenantConnection`).
    * **File-Scoped Namespaces:** Implement for a cleaner code structure.
    * **Collection Expressions:** Use for initializing collections (e.g., `[.. result]`).

* **Dapper Implementation**
    * **Asynchronous Operations:** All data access methods must be async, accept a `CancellationToken`, and use `ConfigureAwait(false)`.
    * **Secure and Efficient Queries:** Use `Dapper.DynamicParameters` and `Dapper.CommandDefinition`.

* **Structure**
    * **SQL Constants:** Extract all fixed parts of SQL queries (base SELECTs, JOINs, etc.) into `private const string` fields at the class level.
    * **Base Query for Pagination:** A base select constant (e.g., `_selectBaseQuery`) **must** include `TotalRows = COUNT(*) OVER()` for efficient pagination.
    * **Column Mapping:** Maintain a `private readonly Dictionary<string, string> _columnMapping` to map entity properties to DB columns for safe dynamic sorting. This is optional and only needed if there are methods with pagination.

#### **Example Method Patterns**

* **Single Record Retrieval (e.g., `GetByIdAsync`)**
    * **Signature:** `Task<EntityClass> GetByIdAsync(int id, CancellationToken cancellationToken)`
    * **Logic:** Append a `WHERE` clause to a base query constant and execute with `QueryFirstOrDefaultAsync`.

* **Paginated List Retrieval (e.g., `GetAsync`)**
    * **Signature:** `Task<PaginatedResult<EntityClass>> GetAsync(EntityFilter filter, PageFilter pageFilter, CancellationToken cancellationToken)`
    * **Logic:**
        * Dynamically build the `WHERE` clause from the `filter` object.
        * Use a helper method like `PaginationSqlHelper.ApplyOrderAndPagination` to add the final sorting and pagination clauses to the query.
        * Use Dapper's multi-mapping (`QueryAsync<Entity, int, Entity>`) with `splitOn: "Id, TotalRows"` to get the data and total count in a single call.
        * Return a populated `PaginatedResult` object.

---

## Example Code Template

This is the concrete implementation of the guide above, ready to be adapted to your project.

```csharp
using Dapper;
using System.Threading;
using System.Threading.Tasks;

// Use a file-scoped namespace for cleaner code.
namespace [YourProject.DataAccess.Repositories];

public class [EntityName]Repository(ITenantConnection _tenantConnection) : I[EntityName]Repository
{
    // Optional: This mapping is only necessary if methods with pagination and dynamic sorting are implemented.
    // Maps property aliases to actual DB columns for safe sorting.
    // Prevents SQL injection in the ORDER BY clause.
    private readonly Dictionary<string, string> _columnMapping = new()
    {
        { "Id", "e.Id" },
        { "Name", "e.EntityName" },
        // Add more mappings according to your entity.
    };

    // Constant for the fixed part of the SELECT query.
    // It's crucial to include COUNT(*) OVER() to get the total row count for pagination.
    private const string _selectBaseQuery = @"
        SELECT
            e.Id,
            e.EntityName AS Name,
            TotalRows = COUNT(*) OVER()
        FROM [TableName] e";

    public async Task<[EntityName]> GetByIdAsync(int id, CancellationToken cancellationToken = default)
    {
        // The method-specific SQL is defined in a local constant.
        const string sql = _selectBaseQuery + " WHERE e.Id = @Id";

        var parameters = new DynamicParameters();
        parameters.Add("Id", id);

        var command = new CommandDefinition(sql, parameters, cancellationToken: cancellationToken);

        using var connection = await _tenantConnection.NewConnectionAsync(cancellationToken).ConfigureAwait(false);
        return await connection.QueryFirstOrDefaultAsync<[EntityName]>(command).ConfigureAwait(false);
    }

    public async Task<PaginatedResult<[EntityName]>> GetAsync([EntityName]Filter filter, PageFilter pageFilter, CancellationToken cancellationToken = default)
    {
        var whereClause = " WHERE 1=1";
        var parameters = new DynamicParameters();

        // Dynamic construction of the WHERE clause and parameters.
        if (!string.IsNullOrEmpty(filter.Name))
        {
            whereClause += " AND e.EntityName LIKE @Name";
            parameters.Add("Name", $"%{filter.Name}%");
        }

        // The helper is used to add sorting and pagination to the SQL.
        var sql = PaginationSqlHelper.ApplyOrderAndPagination(
            baseSql: _selectBaseQuery + whereClause, // The base query with filters.
            parameters: parameters,                  // Dapper parameters for the filters.
            pageFilter: pageFilter,                  // The object with pagination and sorting info.
            orderByFieldsMapping: _columnMapping,    // The dictionary for safe sorting.
            defaultOrderField: "Id"                  // The default sort field.
        );

        var command = new CommandDefinition(sql, parameters, cancellationToken: cancellationToken);

        using var connection = await _tenantConnection.NewConnectionAsync(cancellationToken).ConfigureAwait(false);

        var totalRows = 0;
        var result = await connection.QueryAsync<[EntityName], int, [EntityName]>(
            command,
            map: (entity, totalCount) =>
            {
                totalRows = totalCount; // Captures the total row count from the first record.
                return entity;
            },
            splitOn: "TotalRows") // Dapper splits the result on the "TotalRows" column.
            .ConfigureAwait(false);

        // The paginated result object is returned.
        return new PaginatedResult<[EntityName]>()
        {
            PaginatedList = [.. result], // C# 12 collection expression.
            Quantity = totalRows,
            PageNumber = pageFilter.PageNumber,
            PageSize = pageFilter.PageSize
        };
    }
}
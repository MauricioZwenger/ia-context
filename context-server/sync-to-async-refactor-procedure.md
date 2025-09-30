---
{
  "created_at": "0001-01-01T00:00:00Z",
  "description": "Procedure to refactor synchronous methods to asynchronous equivalents.",
  "modified_at": "0001-01-01T00:00:00Z"
}
---
### Sync-to-Async Refactoring Procedure (Non-TDD)

**Objective**: Convert synchronous methods to asynchronous, ensuring immediate testing after creation.

**Testing Scope**: Default to **Unit Tests**. Do not write integration tests unless explicitly required for a specific method.

**CRITICAL NAMING AND COMPATIBILITY RULES:**
- **NEVER** modify the name of public methods except to add the `Async` suffix.
- **NEVER** modify the return type or data returned by the original public method.
- The refactored service **MUST** return exactly the same data as the original version functionally.
- Preserve all existing method signatures, parameter types, and return types for public methods.

**1. Planning**
- Identify all synchronous methods for conversion.
- Create an `.md` file listing each target method with its full file path.

**2. Refactoring Cycle (for each method)**
- **a. Create Async Method**: Write the new `async` version of the method.
- **b. Immediate Unit Test**: Create a new **unit test** for the `async` method. Run it immediately and confirm it passes.
- **c. Mark Obsolete**: Mark the original synchronous method as `[Obsolete]`.
- **d. Update References**: Replace all calls to the old method with the new `async` version.
- **e. Handle Old Tests**: Disable or delete the unit tests for the obsolete method.

**3. Finalization**
- **a. Build Solution**: Verify the entire solution builds successfully.
- **b. Run All Tests**: Execute the full test suite and ensure all tests pass.
- **c. Cleanup**: Search for remaining references to obsolete methods. If none exist:
  - **Private/Internal methods**: Delete the obsolete methods and their associated test files.
  - **Public methods**: DO NOT DELETE - proceed to step 4 for proper refactoring.

**4. Public Synchronous Method Preservation**
- **NEVER DELETE** existing public synchronous methods - they must remain for backward compatibility.
- **Refactor synchronous methods** to internally call the new asynchronous versions using deadlock-safe patterns:
  - Use `ConfigureAwait(false)` on all `await` calls
  - Use `.GetAwaiter().GetResult()` instead of `.Result` or `.Wait()`
  - Consider using `Task.Run()` for CPU-bound operations if needed
- **Example pattern**:
  ```csharp
  // Original synchronous method (KEEP - refactor implementation)
  [Obsolete("Use GetDocumentAsync instead")]
  public DocumentDto GetDocument(int id)
  {
      return GetDocumentAsync(id).ConfigureAwait(false).GetAwaiter().GetResult();
  }
  
  // New asynchronous method
  public async Task<DocumentDto> GetDocumentAsync(int id)
  {
      // Actual async implementation here
  }
  ```
- This ensures that existing consumers continue to work while new code can benefit from async patterns.
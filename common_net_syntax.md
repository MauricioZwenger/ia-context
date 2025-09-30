---
{
  "created_at": "0001-01-01T00:00:00Z",
  "description": "Common instructions for .NET",
  "modified_at": "0001-01-01T00:00:00Z"
}
---
Refactor the provided C# code to align with .NET 8 and C# 12 best practices.

**Constraints:**

- **Syntax:** Employ modern C# 12 features, including primary constructors, collection expressions, and file-scoped namespaces.
- **Public API:** DO NOT modify any public method signatures or parameter names.
- **Structure & Naming:**
    - Position all private, class-level fields at the top of the class, prefixed with an underscore (`_`).
    - Use descriptive names for internal variables and private methods.
- **Code Quality:**
    - Prioritize simple, readable, and performant code. Avoid over-engineering.
    - Adhere to security best practices, such as input validation.
- **Comments:** Omit all documentation and code comments.
    - **Exception:** Unit tests MUST include `// Arrange`, `// Act`, and `// Assert` comments to structure test phases.
- **Output:** Provide only the final, refactored C# code without any explanations or surrounding text.
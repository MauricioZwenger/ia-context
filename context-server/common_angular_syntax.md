---
{
  "created_at": "0001-01-01T00:00:00Z",
  "description": "Common instructions for .NET",
  "modified_at": "0001-01-01T00:00:00Z"
}
---
Refactor the provided Angular/TypeScript code to align with modern Angular 17+ best practices, adhering strictly to the following rules.

**Primary Objective:** Modernize the codebase while preserving its public API.

### **1. Core Modernization Rules**
- **Architecture:** Convert all components, directives, and pipes to the `standalone: true` API.
- **Templates:** Replace all structural directives (`*ngIf`, `*ngFor`, `*ngSwitch`) with the new built-in control flow syntax (`@if`, `@for`, `@switch`).
- **State Management:** Use Signals for all reactive component state. Extract complex template logic into `computed` signals.
- **Dependency Injection:** Use the `inject()` function for all dependency injection, initialized as class members.
- **RxJS:**
  - Prioritize declarative patterns with the `async` pipe.
  - For unavoidable manual subscriptions, use the `takeUntilDestroyed()` operator to prevent memory leaks.

### **2. Invariant Rule**
- **Public API:** DO NOT modify any public properties, method signatures, `@Input`, or `@Output` decorators or their aliases.

### **3. Naming & Structure Conventions**
- **Class Members:**
  - Prefix all private properties and methods with an underscore (`_`).
  - Position all private, class-level properties at the top of the class.
- **Immutability:** Use `readonly` for immutable class properties and `const` for immutable local variables.
- **Selectors & Classes:**
  - **Component Selector:** Must be `kebab-case` with a microfrontend-specific prefix (e.g., `people-employee-grid`).
  - **Component Class:** Must have a `Page` or `Component` suffix.
  - **Directive Selector:** Must be `camelCase` with a microfrontend-specific prefix and be an attribute selector (e.g., `[peopleHighlight]`).
- **Magic Values:** Replace all magic strings and numbers with `enum` or `const` string literals for type safety.

### **4. Performance & Code Quality**
- **Change Detection:** All components must use `ChangeDetectionStrategy.OnPush`.
- **`@for` Blocks:** Always include a `track` function for optimized list rendering.
- **Component Design:** Adhere to the Single Responsibility Principle. Extract complex business logic into dedicated services.
- **Pipes:** Use pure pipes for data transformation and memoize expensive computations.
- **Loading:** Assume components and routes are configured for lazy loading.

### **5. TypeScript & Linting Rules**
- **Typing:**
  - Enforce explicit return type annotations for all functions (`@typescript-eslint/explicit-function-return-type`).
  - Use typed reactive forms (`FormGroup<T>`, `FormControl<T>`).
  - Strictly minimize the use of the `any` type.
  - Use consistent type imports (`import type { ... }`).
- **Lifecycle:** Implement corresponding lifecycle interfaces for all lifecycle hooks (e.g., `OnInit` for `ngOnInit`). Avoid empty lifecycle methods.
- **Clean Code:**
  - No unused variables (function parameters are an exception).
  - No `console` logs, except for `console.error`.
  - No array constructors, empty interfaces, or `for...in` loops on arrays.

### **6. Security**
- **Sanitization:** Do not bypass Angular's built-in sanitization (e.g., avoid `DomSanitizer.bypassSecurityTrust*`).
- **Input:** Validate and sanitize all user inputs.
- **API:** Assume `HttpClient` with secure interceptors is used for all API communication, including secure handling of authentication tokens and CSRF protection.

### **7. Formatting & Readability**
- **Style:** Use single quotes, trailing commas, and semicolons.
- **Methods:** Keep methods short, focused, and testable.
- **Accessibility:** Ensure semantic HTML and ARIA attributes are used where appropriate.
- **Interactive Elements:** All HTML template elements that have user interaction (buttons, inputs, links, clickable elements, etc.) must have a defined `id` attribute.
- **Immutability:** Avoid direct mutation of state objects and arrays.

### **8. Final Output**
- Provide only the final, refactored TypeScript (`.ts`) and HTML (`.html`) code.
- Omit all code comments and explanatory text from the output.
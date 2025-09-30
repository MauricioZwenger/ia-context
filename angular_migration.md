# Angular Migration Guide: v11 to v17

This document provides a consolidated context for migrating an Angular application from version 11 through 17. It synthesizes official Angular update guides into a single, optimized prompt.

## General Pre-Migration Steps

**Before starting the migration process for any version, ensure the following:**

1.  **Node.js Version:** Use a supported version of Node.js as specified in the official Angular documentation for the target version.
2.  **TypeScript Version:** Update to the required TypeScript version *before* updating Angular.
3.  **Clean State:** Ensure your working directory is clean (no uncommitted changes in git).
4.  **Dependencies:** Update third-party libraries to versions compatible with the target Angular version.

---

## Migration Steps & Key Changes by Version

### **Version 11 to 12**

* **Command:** `ng update @angular/core@12 @angular/cli@12`
* **Key Changes & Actions:**
    * **Strict Mode:** Production builds are now default (`ng build` is equivalent to `ng build --prod`).
    * **Webpack 5:** Angular CLI now uses Webpack 5.
    * **TypeScript:** Requires TypeScript 4.2.
    * **IE11 Support:** Deprecated.
    * **Styling:**
        * `ng update` will migrate Sass/CSS to use the new `@use` syntax instead of `@import`.
        * Update component styles to no longer use `::ng-deep` as it is deprecated.
    * **Forms:** `min` and `max` attributes now result in `null` being set for `Validators.min` and `Validators.max` if the value is invalid.

### **Version 12 to 13**

* **Command:** `ng update @angular/core@13 @angular/cli@13`
* **Key Changes & Actions:**
    * **Ivy Engine:** View Engine is completely removed. All applications are now Ivy-only. `ngcc` is no longer needed.
    * **Node.js:** Requires Node.js v12.20.0 or later.
    * **TypeScript:** Requires TypeScript 4.4.
    * **RxJS:** Requires RxJS v7.4 or later. Run `npm install rxjs@7.4`
    * **Router:**
        * `routerLink` with `undefined` or `null` is now equivalent to an empty string, preventing navigation.
        * The `relativeLinkResolution` configuration option in `RouterModule.forRoot()` is removed (default is now 'corrected').
    * **Forms:** `FormControlStatus` is now a union of strings (`'VALID'`, `'INVALID'`, etc.) instead of a string literal type.
    * **IE11 Support:** Removed.

### **Version 13 to 14**

* **Command:** `ng update @angular/core@14 @angular/cli@14`
* **Key Changes & Actions:**
    * **Standalone Components:** Introduction of standalone components, directives, and pipes.
    * **Typed Forms:** `FormGroup`, `FormControl`, and `FormArray` now have generic types to provide better type safety. This is the biggest change and may require significant refactoring.
        * `ng update` will attempt to migrate your forms automatically. Manually update any complex forms that could not be migrated.
    * **TypeScript:** Requires TypeScript 4.6 or later.
    * **Page Titles:** `RouterModule.forRoot()` now provides a `title` property for defining page titles.
    * **Environment Initializers:** New `ENVIRONMENT_INITIALIZER` provider to run code during app bootstrap.

### **Version 14 to 15**

* **Command:** `ng update @angular/core@15 @angular/cli@15`
* **Key Changes & Actions:**
    * **Standalone APIs are Stable:** Standalone components, directives, and pipes are now out of developer preview.
    * **Node.js:** Requires Node.js v14.20.x, v16.13.x, or v18.10.x.
    * **TypeScript:** Requires TypeScript 4.8 or later.
    * **NgModules are Optional:** You can now bootstrap an application using a standalone component.
    * **Directive Composition API:** Allows for applying directives to a component's host element from within the component's decorator.
    * **Image Directive:** The `NgOptimizedImage` directive is now stable.
    * **`providedIn: 'root'` is Default:** The `providedIn` property for `@Injectable()` is no longer required for tree-shakable providers (defaults to `'root'`).
    * **`@angular/flex-layout` Deprecated:** This library is now deprecated.

### **Version 15 to 16**

* **Command:** `ng update @angular/core@16 @angular/cli@16`
* **Key Changes & Actions:**
    * **Signals:** Introduction of Signals as a new reactivity model (developer preview).
    * **Required Inputs:** Component inputs can now be marked as required.
    * **Non-destructive Hydration:** Developer preview of improved server-side rendering (SSR) hydration.
    * **esbuild Dev Server:** Experimental support for using esbuild for the development server (`ng serve`).
    * **TypeScript:** Requires TypeScript 4.9 or later.
    * **Zone.js:** The `zone.js` import should now be `import 'zone.js';` in `polyfills.ts`.
    * **Router:** Can now bind router information (like route params, query params) directly to component inputs.

### **Version 16 to 17**

* **Command:** `ng update @angular/core@17 @angular/cli@17`
* **Key Changes & Actions:**
    * **New Control Flow:** Introduction of new, built-in control flow syntax (`@if`, `@for`, `@switch`) that replaces `*ngIf`, `*ngFor`, and `NgSwitch`. This is a major syntactical change.
    * **Vite and esbuild are Default:** New projects use Vite for the development server and esbuild for builds by default.
    * **Standalone is Default:** `ng new` now generates standalone applications by default.
    * **View Transitions API:** Built-in support for the View Transitions API in the router.
    * **Deferred Loading:** New `@defer` block for declarative, deferred loading of component dependencies.
    * **Node.js:** Requires Node.js v18.13.0 or later.
    * **TypeScript:** Requires TypeScript 5.2 or later.

---

## Post-Migration

After running each `ng update` command and before moving to the next version:
1.  **Run Tests:** Execute your unit and end-to-end tests to ensure the application is stable.
2.  **Manually Review:** Check the console for deprecation notices and address them.
3.  **Commit Changes:** Commit the successful migration before starting the next one.
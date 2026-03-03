---
Language: Clsx
Version: 2.1.1
Fidelity: 100% (Physical Disk Reference + Deep d.ts Analysis)
State_ID:  BigInt(0x1)
LSP_Discovery_Root: "@root/node_modules/clsx/package.json"
Grammar_Lock: "@root/hashes/grammar/clsx.hash.md"
---

/** [Project].Grammar.Clsx - Lightweight Utility Logic **/

## [SDK_Discovery_Map]
/** === clsx (Core) === */
/** @Ref: @root/node_modules/clsx/clsx.d.ts */

## [SDK_Imports / Namespaces]
```ts
import clsx from "clsx"
// Or CommonJS:
// const clsx = require("clsx")
```

## [Core_Primitives]
```ts
// clsx.d.ts: The complete type system. Recursive ClassValue enables arbitrary nesting.
declare namespace clsx {
  // ClassValue: The union of ALL acceptable input types.
  // string — direct class name ("text-red-500").
  // number — coerced to string. Truthy numbers become class names, 0 is falsy (ignored).
  // bigint — coerced to string.
  // boolean — true/false. false, null, undefined are ignored (falsy filtering).
  // null | undefined — silently ignored.
  // ClassDictionary — object mapping class names to boolean conditions.
  // ClassArray — recursive array of ClassValues (arbitrary nesting depth).
  type ClassValue = ClassArray | ClassDictionary | string | number | bigint | null | boolean | undefined;

  // ClassDictionary: Object where keys are class names and values are boolean conditions.
  // Truthy values include the key as a class. Falsy values exclude it.
  type ClassDictionary = Record<string, any>;

  // ClassArray: Recursive array type. Enables deep nesting: clsx([["a", ["b", "c"]]]).
  type ClassArray = ClassValue[];

  // Main function: Variadic. Accepts ANY number of ClassValue arguments.
  function clsx(...inputs: ClassValue[]): string;
}

// Default export: The clsx function itself.
declare function clsx(...inputs: clsx.ClassValue[]): string;
export = clsx;
```

## [Architectural_Laws]
- **Immutability_Law**: `clsx` returns a new string; it NEVER modifies input objects or arrays.
- **Falsy_Filtering_Law**: `null`, `undefined`, `false`, `0`, `""` are automatically ignored during concatenation.
- **Recursive_Merge_Law**: Nested arrays are flattened recursively. `clsx(["a", ["b", ["c"]]])` → `"a b c"`.
- **Dictionary_Conditional_Law**: Object keys with truthy values are included. `{ "active": true, "disabled": false }` → `"active"`.
- **String_Concatenation_Law**: Output is a space-separated string of all truthy arguments. No duplicates are removed — that is `tailwind-merge`'s job.
- **Zero_Dependency_Law**: clsx has ZERO runtime dependencies. ~228 bytes gzipped.
- **Ordering_Law**: Classes appear in the output in the order they are provided as arguments.

## [Syntax_Rules] | [Naming_Conventions]
- `cn`: The industry-standard alias for `twMerge(clsx(...))`. Combines clsx's class merging with tailwind-merge's conflict resolution.
- `inputs`: Variadic argument list `...inputs: ClassValue[]`.
- `clsx(base, conditional, override)`: Common 3-argument pattern for building class strings.

## [Prohibited_Patterns]
- NO manual template literals for complex conditional classes — use `clsx({ "class": condition })` for readability and type safety.
- NO relying on clsx for Tailwind conflict resolution — clsx does NOT understand Tailwind utilities. Use `tailwind-merge` for that.
- NO using clsx to deduplicate class names — it preserves ALL truthy inputs, duplicates included.

## [Tactical_Patterns]

### Conditional Styling
- **Object Syntax**: `clsx({ 'text-red-500': isError, 'text-green-500': isSuccess })` — reactive conditional classes.
- **Ternary Inline**: `clsx(isActive ? "bg-blue-500" : "bg-gray-200")` — simple binary toggle.
- **Nullable Safety**: `clsx(maybeClass)` — if `maybeClass` is undefined/null, safely ignored.

### Composable Class Building
- **Base + Variant**: `clsx("btn", variant === "primary" && "btn-primary", size === "lg" && "btn-lg")`.
- **Array Spreading**: `clsx(baseStyles, ...conditionalStyles)` — merge base with optional overrides.
- **Props Forwarding**: `<div className={clsx("container", className)} />` — merge component defaults with consumer overrides.

### Integration with tailwind-merge (cn pattern)
```ts
// The canonical "cn" utility — combines clsx's flexibility with tailwind-merge's conflict resolution:
import { clsx, type ClassValue } from "clsx"
import { twMerge } from "tailwind-merge"

function cn(...inputs: ClassValue[]): string {
  return twMerge(clsx(...inputs))
}
// Usage: cn("px-2 py-1", condition && "px-4") → "py-1 px-4" (conflict resolved by twMerge).
```

## [Standard_Library_Signatures]
```ts
// Main function — the ONLY export.
function clsx(...inputs: ClassValue[]): string;
```

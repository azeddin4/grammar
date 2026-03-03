---
Language: Tailwind Merge
Version: 3.5.0
Fidelity: 100% (Physical Disk Reference + Deep d.ts Analysis)
State_ID:  BigInt(0x1)
LSP_Discovery_Root: "@root/node_modules/tailwind-merge/package.json"
Grammar_Lock: "@root/hashes/grammar/tailwind-merge.hash.md"
---

/** [Project].Grammar.TailwindMerge - Conflict Resolution Logic **/

## [SDK_Discovery_Map]
/** === tailwind-merge (Core) === */
/** @Ref: @root/node_modules/tailwind-merge/dist/types.d.ts */

## [SDK_Imports / Namespaces]
```ts
import { twMerge, extendTailwindMerge, createTailwindMerge, getDefaultConfig, twJoin, type ClassNameValue, type Config } from "tailwind-merge"
```

## [Core_Primitives]
```ts
// types.d.ts: The complete Config type system for class group resolution.

// ClassNameValue: Input type for twMerge. Matches clsx's ClassValue for compatibility.
type ClassNameValue = string | null | undefined | 0 | false | ClassNameValue[];

// TailwindMerge: The function signature of twMerge and custom mergers.
type TailwindMerge = (...classLists: ClassNameValue[]) => string;

// Config: Full configuration for the merge engine.
interface Config<ClassGroupIds extends string = string, ThemeGroupIds extends string = string> {
  cacheSize: number;                                    // LRU cache size (default: 500).
  prefix?: string;                                      // Tailwind prefix (e.g., "tw-").
  separator?: string;                                   // Modifier separator (default: ":").
  experimentalParseClassName?: (param: ExperimentalParseClassNameParam) => ParsedClassName;
  override?: Partial<OverrideConfig<ClassGroupIds, ThemeGroupIds>>;
  extend?: Partial<ExtendConfig<ClassGroupIds, ThemeGroupIds>>;
  theme: Record<ThemeGroupIds, ClassGroup<ClassGroupIds>[]>;
  classGroups: Record<ClassGroupIds, ClassGroup<ClassGroupIds>[]>;
  conflictingClassGroups: Record<ClassGroupIds, ClassGroupIds[]>;
  conflictingClassGroupModifiers?: Record<ClassGroupIds, ClassGroupIds[]>;  // Postfix modifiers (e.g., font-size/leading → leading).
  orderSensitiveModifiers?: string[];  // Modifiers whose order changes targets (e.g., group-hover, peer-focus).
}

// ExperimentalParseClassNameParam: Hook into class parsing pipeline.
interface ExperimentalParseClassNameParam {
  className: string;
  parseClassName(className: string): ParsedClassName;
}

// ParsedClassName: Result of class parsing. Controls how twMerge treats individual classes.
interface ParsedClassName {
  isExternal?: boolean;                    // If true, class is not a Tailwind class; passes through unchanged.
  modifiers: string[];                     // e.g., ['hover', 'dark'] for `hover:dark:bg-gray-100`.
  hasImportantModifier: boolean;           // e.g., true for `hover:dark:!bg-gray-100`.
  baseClassName: string;                   // e.g., 'bg-gray-100' for `hover:dark:bg-gray-100`.
  maybePostfixModifierPosition?: number;   // Position of '/' in class (e.g., 11 for `bg-gray-100/50`).
}

// ClassDefinition: Defines how classes map to groups. Can be string, validator function, ThemeGetter, or object.
type ClassDefinition<T> = string | ClassValidator | ThemeGetter | ClassObject<T>;
type ClassValidator = (classPart: string) => boolean;  // Custom validation for arbitrary values.
interface ThemeGetter { (theme: ThemeObject): ClassGroup; isThemeGetter: true; }  // Resolves from theme scale.

// DefaultClassGroupIds: 300+ built-in class groups covering ALL Tailwind CSS utilities.
// Includes: 'accent' | 'align-content' | 'align-items' | 'animate' | 'aspect' | 'auto-cols' | 'auto-rows' |
//   'backdrop-blur' | 'basis' | 'bg-attachment' | 'bg-clip' | 'bg-color' | 'bg-image' | 'bg-origin' |
//   'bg-position' | 'bg-repeat' | 'bg-size' | 'blur' | 'border-collapse' | 'border-color' | 'border-style' |
//   'border-w' | 'box' | 'break' | 'brightness' | 'caption' | 'clear' | 'col-end' | 'col-start' | 'columns' |
//   'container' | 'content' | 'contrast' | 'cursor' | 'display' | 'divide-color' | 'divide-style' | 'divide-x' |
//   'divide-y' | 'drop-shadow' | 'duration' | 'ease' | 'flex-direction' | 'flex-wrap' | 'flex' | 'float' |
//   'font-family' | 'font-size' | 'font-style' | 'font-weight' | 'gap-x' | 'gap-y' | 'gap' | 'gradient-from' |
//   'gradient-to' | 'gradient-via' | 'grid-cols' | 'grid-flow' | 'grid-rows' | 'grow' | 'h' | 'inset' |
//   'justify-content' | 'leading' | 'left' | 'line-clamp' | 'm' | 'max-h' | 'max-w' | 'min-h' | 'min-w' |
//   'mix-blend' | 'object-fit' | 'object-position' | 'opacity' | 'order' | 'outline-color' | 'outline-style' |
//   'overflow' | 'p' | 'perspective' | 'place-content' | 'pointer-events' | 'position' | 'resize' |
//   'ring-color' | 'ring-offset-color' | 'ring-w' | 'rotate' | 'rounded' | 'saturate' | 'scale' |
//   'scroll-behavior' | 'select' | 'shadow-color' | 'shadow' | 'shrink' | 'size' | 'snap-align' |
//   'space-x' | 'space-y' | 'sr' | 'stroke' | 'table-layout' | 'text-alignment' | 'text-color' |
//   'text-decoration' | 'text-overflow' | 'text-transform' | 'text-wrap' | 'top' | 'tracking' |
//   'transform' | 'transition' | 'translate' | 'visibility' | 'w' | 'whitespace' | 'will-change' | 'z'
//   ... and 200+ more groups for responsive, interaction, and layout utilities.

// DefaultThemeGroupIds: Theme scale keys used in configuration.
type DefaultThemeGroupIds = 'animate' | 'aspect' | 'blur' | 'breakpoint' | 'color' | 'container' |
  'drop-shadow' | 'ease' | 'font-weight' | 'font' | 'inset-shadow' | 'leading' | 'perspective' |
  'radius' | 'shadow' | 'spacing' | 'text' | 'text-shadow' | 'tracking';
```

## [Architectural_Laws]
- **Last_Wins_Resolution**: In class group conflicts, the LAST defined class always wins. `twMerge("px-2 px-4")` → `"px-4"`.
- **Group_Awareness**: twMerge understands Tailwind CSS class groups (e.g., `text-color`, `bg-color`, `border-w`). It resolves conflicts WITHIN groups, not between them. `twMerge("text-red-500 bg-blue-500")` → `"text-red-500 bg-blue-500"` (no conflict — different groups).
- **Arbitrary_Value_Support**: Supports `[arbitrary]` values (e.g., `grid-cols-[1fr,auto]`, `text-[#ff0000]`). These participate in conflict resolution.
- **Modifier_Awareness**: Understands responsive (`sm:`, `md:`, `lg:`) and state (`hover:`, `focus:`, `active:`) modifiers. `twMerge("sm:px-2 sm:px-4")` → `"sm:px-4"`. Different modifiers are separate groups: `twMerge("px-2 sm:px-4")` → `"px-2 sm:px-4"`.
- **Conflicting_Group_Rules**: Some class groups conflict transitively. E.g., `ring-w` and `ring-w-inset` are conflicting. Defined in `conflictingClassGroups` config.
- **LRU_Cache_Law**: twMerge uses an internal LRU cache (default: 500 entries) for performance. Repeated calls with identical inputs hit the cache. Configurable via `cacheSize`.
- **Prefix_Awareness**: If Tailwind uses a prefix (e.g., `tw-`), configure `prefix: "tw-"` in the config. Without it, conflict detection WILL FAIL.

## [Syntax_Rules] | [Naming_Conventions]
- `twMerge`: The standard default function. Uses the default Tailwind CSS config.
- `extendTailwindMerge`: Factory to create a custom merge function with extended/overridden class groups and themes.
- `createTailwindMerge`: Low-level factory for total config control. Takes config creator functions.
- `twJoin`: Simple class joiner WITHOUT conflict resolution. Faster than twMerge. Use when no Tailwind conflicts are possible.
- `getDefaultConfig`: Returns a read-only snapshot of the default configuration.

## [Prohibited_Patterns]
- NO manual regex for style conflicts — always defer to `twMerge` to handle complex Tailwind edge cases.
- NO using `twMerge` for non-Tailwind class names — it only understands Tailwind's utility naming convention. Regular CSS classes pass through unchanged.
- NO setting `cacheSize: 0` in production — this disables caching and severely impacts performance.
- NO forgetting `prefix` config if your Tailwind setup uses one — merging will silently fail to detect conflicts.

## [Tactical_Patterns]

### Basic Conflict Resolution
- **Spacing**: `twMerge("p-2 p-4")` → `"p-4"`. Works for all spacing utilities (m, p, gap, inset, etc.).
- **Colors**: `twMerge("text-red-500 text-blue-500")` → `"text-blue-500"`.
- **Layout**: `twMerge("flex grid")` → `"grid"` (display group conflict).
- **Responsive**: `twMerge("md:p-2 md:p-4")` → `"md:p-4"`. Modifiers are scoped independently.

### Customization Patterns
```ts
// extendTailwindMerge: Add custom class groups or theme values.
const customTwMerge = extendTailwindMerge({
  extend: {
    theme: {
      spacing: ["sm", "md", "lg"],     // Custom spacing scale.
    },
    classGroups: {
      "custom-group": ["custom-a", "custom-b"],  // Custom conflicting classes.
    },
  },
});

// createTailwindMerge: Full control over config pipeline.
const totalCustomMerge = createTailwindMerge(() => ({
  cacheSize: 1000,
  prefix: "tw-",
  theme: { ... },
  classGroups: { ... },
  conflictingClassGroups: { ... },
}));
```

### Integration with clsx (cn pattern)
```ts
// The canonical utility — requires both packages:
import { clsx, type ClassValue } from "clsx"
import { twMerge } from "tailwind-merge"

function cn(...inputs: ClassValue[]): string {
  return twMerge(clsx(...inputs))
}
// clsx handles: conditionals, arrays, objects, falsy filtering.
// twMerge handles: Tailwind utility conflict resolution.
```

### Performance Optimization
- **twJoin**: When you know there are NO Tailwind conflicts, use `twJoin` for faster string concatenation.
- **Cache Tuning**: Increase `cacheSize` for applications with many unique class combinations (e.g., large design systems).
- **Memoization**: twMerge's internal LRU cache handles memoization automatically. No need for external memoization.

## [Standard_Library_Signatures]
```ts
// Default merge function (uses default Tailwind CSS config).
function twMerge(...classLists: ClassNameValue[]): string;

// Simple class joiner (no conflict resolution). Faster.
function twJoin(...classLists: ClassNameValue[]): string;

// Extension factory — extends the default config.
function extendTailwindMerge<AdditionalClassGroupIds extends string = never, AdditionalThemeGroupIds extends string = never>(
  ...configs: Array<Partial<Config<DefaultClassGroupIds | AdditionalClassGroupIds, DefaultThemeGroupIds | AdditionalThemeGroupIds>>>
): TailwindMerge;

// Low-level factory — complete config control.
function createTailwindMerge(createConfigFirst: () => Config, ...createConfigRest: Array<(config: Config) => Config>): TailwindMerge;

// Config inspector.
function getDefaultConfig(): Config<DefaultClassGroupIds, DefaultThemeGroupIds>;
```

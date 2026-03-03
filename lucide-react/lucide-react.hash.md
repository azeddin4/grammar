---
Language: Lucide React
Version: 0.475.0
Fidelity: 100% (Physical Disk Reference + Deep d.ts Analysis)
State_ID:  BigInt(0x1)
LSP_Discovery_Root: "@root/node_modules/lucide-react/package.json"
Grammar_Lock: "@root/hashes/grammar/lucide-react.hash.md"
---

/** [Project].Grammar.Lucide - Linguistic DNA anchor for Lucide Icons */

## [SDK_Discovery_Map]
/** === lucide-react (Core) === */
/** @Ref: @root/node_modules/lucide-react/dist/lucide-react.d.ts */
/** @Ref: @root/node_modules/lucide-react/dist/lucide-react.prefixed.d.ts */
/** @Ref: @root/node_modules/lucide-react/dist/lucide-react.suffixed.d.ts */
/** @Ref: @root/node_modules/lucide-react/dynamic.d.ts */
/** @Ref: @root/node_modules/lucide-react/dynamicIconImports.d.ts */

## [SDK_Imports / Namespaces]
```ts
// Standard (tree-shaken) import — recommended for production:
import { Camera, Search, ArrowLeft, type LucideProps, type LucideIcon } from "lucide-react"

// Dynamic import — for loading icons by string name at runtime:
import { DynamicIcon, iconNames, type IconName } from "lucide-react/dynamic"
import dynamicIconImports from "lucide-react/dynamicIconImports"
```

## [Core_Primitives]
```ts
// lucide-react.d.ts: SVG element types used by icon nodes.
type SVGElementType = 'circle' | 'ellipse' | 'g' | 'line' | 'path' | 'polygon' | 'polyline' | 'rect';

// IconNode: Internal representation of icon SVG structure. Array of [element, attributes] tuples.
type IconNode = [elementName: SVGElementType, attrs: Record<string, string>][];

// LucideProps: Extended SVG props for all icon components.
interface LucideProps extends React.SVGProps<SVGSVGElement>, React.RefAttributes<SVGSVGElement> {
  size?: string | number;           // Width & height in pixels (default: 24).
  color?: string;                    // Stroke color (default: "currentColor").
  strokeWidth?: string | number;     // Stroke width (default: 2).
  absoluteStrokeWidth?: boolean;     // If true, strokeWidth is NOT scaled with size. Maintains visual weight at any size.
}

// LucideIcon: The type of every exported icon component.
type LucideIcon = React.ForwardRefExoticComponent<Omit<LucideProps, 'ref'> & React.RefAttributes<SVGSVGElement>>;
```

## [Architectural_Laws]
- **Icon_Atomicity**: Every icon is a self-contained SVG wrapped in `ForwardRefExoticComponent`. It renders an `<svg>` with viewBox="0 0 24 24" containing `<path>`, `<circle>`, `<line>`, etc.
- **Tree_Shaking_Law**: Named imports (`import { Camera }`) are tree-shaken. NEVER import the entire module (`import * as Icons`). Each icon is ~1-2KB.
- **Stroke_Scaling**: By default, `strokeWidth` scales proportionally with `size`. Enable `absoluteStrokeWidth` to maintain the exact pixel stroke regardless of scaling.
- **Color_Inheritance**: Icons use `currentColor` by default. They inherit text color from parent CSS. Override with `color` prop.
- **SVG_Ref_Forwarding**: All icons forward refs to the underlying `<SVGSVGElement>`. Can be used with `useRef<SVGSVGElement>()`.
- **24x24_Grid**: All icons are designed on a 24x24 grid with 2px stroke. Props `size`, `color`, and `strokeWidth` adjust rendering.

## [Syntax_Rules] | [Naming_Conventions]
- `PascalCase`: Standard icon exports (e.g., `ArrowRight`, `Camera`, `CheckCircle`).
- `IconPascalCase`: Prefixed exports from `lucide-react/dist/lucide-react.prefixed.d.ts` (e.g., `IconCamera`).
- `PascalCaseIcon`: Suffixed exports from `lucide-react/dist/lucide-react.suffixed.d.ts` (e.g., `CameraIcon`).
- `kebab-case`: Dynamic import keys (e.g., `"arrow-right"`, `"check-circle"`).
- `className`: Primary styling mechanism for Tailwind/CSS integration.
- `size`: Prefer numeric values (e.g., `size={24}`) for standard grid alignment.

## [Prohibited_Patterns]
- NO direct SVG path manipulation — use the component wrapper for accessibility and consistency.
- NO large-batch wildcard imports (`import * from "lucide-react"`) — destroys tree-shaking, adds entire icon set (~1500 icons) to bundle.
- NO hardcoded SVG viewBox changes — all icons are designed for `viewBox="0 0 24 24"`.
- NO mixing prefixed and standard imports in the same file — choose one naming convention per project.

## [Dynamic_Icon_System]
```ts
// dynamic.d.ts: Runtime icon loading by string name.
// DynamicIcon: Component that lazily loads icons by name prop.
interface DynamicIconComponentProps extends LucideProps {
  name: IconName;                    // kebab-case icon name (e.g., "arrow-right").
  fallback?: () => JSX.Element | null;  // Rendered while icon is loading.
}
const DynamicIcon: React.ForwardRefExoticComponent<DynamicIconComponentProps>;

// dynamicIconImports.d.ts: Map of icon names to lazy import functions.
// Each key is a kebab-case icon name, value is () => Promise<{ default: LucideIcon }>
// Example: dynamicIconImports["camera"]() returns Promise<typeof Camera>
const dynamicIconImports: Record<IconName, () => Promise<{ default: LucideIcon; __iconNode: IconNode }>>;

// iconNames: Array of ALL available icon names (kebab-case).
const iconNames: Array<IconName>;

// IconName: Union type of all available icon string names.
type IconName = keyof typeof dynamicIconImports;
// Includes ~1500+ icons: "a-arrow-down" | "a-arrow-up" | "accessibility" | "activity" | ...

// Aliases: Some icons have multiple names (e.g., "wallet-2" -> "wallet-minimal", "user-2" -> "user-round").
```

## [Tactical_Patterns]

### Static Usage (Recommended for Production)
- **Direct Import**: `import { Camera } from "lucide-react"` — tree-shaken, smallest bundle impact.
- **Accessibility**: Add `aria-label` or wrap in visually-hidden text for screen readers. Icons are decoration by default.
- **Tailwind Integration**: `<Camera className="w-6 h-6 text-blue-500" />` — `currentColor` inherits.

### Dynamic Usage (Admin Panels, CMS, Icon Pickers)
- **DynamicIcon**: `<DynamicIcon name="camera" />` — lazy-loads icon on demand.
- **Icon Picker**: Use `iconNames` array to populate a selector. Validate with `type IconName`.
- **Lazy Loading**: `dynamicIconImports` provides individual lazy importers. Use with React.lazy or Suspense.
- **Fallback**: `<DynamicIcon name={userIcon} fallback={() => <Spinner />} />` — shows fallback during load.

### Naming Collision Avoidance
- **Prefixed**: Import from `lucide-react` prefixed variant for collision-free names (`IconCamera` vs local `Camera` component).
- **Suffixed**: Import from suffixed variant for post-fix pattern (`CameraIcon`).
- **Choose consistently**: Pick ONE naming convention per project and stick with it.

## [Standard_Library_Signatures]
```ts
// Every icon follows this pattern — ~1500+ icons available:
const Camera: LucideIcon;
const ArrowRight: LucideIcon;
const CheckCircle: LucideIcon;
const Search: LucideIcon;
const Menu: LucideIcon;
const X: LucideIcon;
const ChevronDown: LucideIcon;
const Settings: LucideIcon;
const User: LucideIcon;
const Heart: LucideIcon;
// ... and ~1490 more icons following the same type signature.

// Dynamic Component
const DynamicIcon: React.ForwardRefExoticComponent<DynamicIconComponentProps & RefAttributes<SVGSVGElement>>;
```

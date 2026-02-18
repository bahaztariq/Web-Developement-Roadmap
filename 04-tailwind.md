# 🌊 Tailwind CSS - Utility-First CSS Framework

> A utility-first CSS framework for rapidly building custom designs. Instead of pre-built components, Tailwind provides low-level utility classes that let you build completely custom designs.

---

## 1. Introduction

**Definition:** Tailwind CSS is a utility-first CSS framework that provides low-level utility classes to build custom designs directly in HTML markup, eliminating the need to write custom CSS or fight against pre-built component styles.

### What is Tailwind CSS?

**Definition:** Tailwind CSS is a utility-first CSS framework that provides low-level, single-purpose CSS classes (utilities) that you compose directly in HTML to build any design. Unlike component-based frameworks (Bootstrap), Tailwind doesn't provide pre-built components — instead it gives you building blocks like `flex`, `pt-4`, `text-center`, and `rotate-90` that you combine to create custom designs without writing custom CSS.

Tailwind CSS is a **utility-first** CSS framework that provides a comprehensive set of low-level utility classes. Rather than writing custom CSS or using pre-designed components, you compose designs directly in your HTML using utility classes.

### Introduction UML: Tailwind CSS Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                  TAILWIND CSS ARCHITECTURE                      │
└─────────────────────────────────────────────────────────────────┘

┌──────────────────────┐         ┌──────────────────────┐
│   UTILITY-FIRST      │         │   COMPONENT-BASED    │
│     (Tailwind)       │         │   (Bootstrap, etc)   │
└──────────────────────┘         └──────────────────────┘

┌──────────────────────┐         ┌──────────────────────┐
│ • Single-purpose     │         │ • Pre-built widgets  │
│   classes            │         │ • Limited styling    │
│ • Compose in HTML    │         │ • Override conflicts │
│ • Infinite variety   │         │ • Cookie-cutter look │
│ • Custom by default  │         │ • Faster initial dev │
└──────────────────────┘         └──────────────────────┘
         │                                  │
         ▼                                  ▼
┌──────────────────────┐         ┌──────────────────────┐
│   HTML EXAMPLE       │         │   HTML EXAMPLE       │
│                      │         │                      │
│ <button class="      │         │ <button class="      │
│   bg-blue-500        │         │   btn                │
│   hover:bg-blue-700  │         │   btn-primary        │
│   text-white         │         │   btn-lg">           │
│   font-bold          │         │   Click me           │
│   py-2 px-4          │         │ </button>            │
│   rounded">          │         │                      │
│   Click me           │         │ Result: Generic      │
│ </button>            │         │       blue button    │
│                      │         │                      │
│ Result: Custom,      │         │ Override required    │
│       branded        │         │ for customization    │
└──────────────────────┘         └──────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│              HOW TAILWIND GENERATES CSS                         │
└─────────────────────────────────────────────────────────────────┘

┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│  Scan Files  │───▶│  JIT Engine  │───▶│ Generate CSS │
│   (content)  │    │  (v3+ only)  │    │  (output.css)│
└──────────────┘    └──────────────┘    └──────────────┘
       │                   │                   │
       ▼                   ▼                   ▼
• HTML files          • Parse classes        • Base styles
• JS/JSX/TSX          • Generate rules       • Components
• Vue components      • Minimize output      • Utilities
• Templates           • Tree-shake unused    • Variants
• Markdown            • Arbitrary values     • Custom config

┌─────────────────────────────────────────────────────────────────┐
│  WORKFLOW: Source ▶ JIT Engine ▶ Generated CSS ▶ Browser        │
│                                                                 │
│  input.css ──┐                                                  │
│              ├──▶ Tailwind CLI ──▶ output.css ──▶ Browser      │
│  config.js ──┘                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Key Philosophy:

**Definition:** Tailwind's core philosophy is that utility classes in HTML are more maintainable than custom CSS because: (1) you never need to invent class names, (2) CSS doesn't grow with your project since utilities are reused, (3) changes are local to the HTML element so you always know what will change, and (4) the design system is enforced through a constrained set of values.

Tailwind CSS is a **utility-first** CSS framework that provides a comprehensive set of low-level utility classes. Rather than writing custom CSS or using pre-designed components, you compose designs directly in your HTML using utility classes.

**Key Philosophy:**
- Utility-first over component-based
- Highly customizable
- Mobile-first responsive design
- Small production bundle (purgeCSS removes unused styles)

### Utility-First vs Component-Based

**Definition:** Utility-first frameworks (Tailwind) apply many small, single-purpose classes directly in HTML. Component-based frameworks (Bootstrap) provide pre-styled components (`.btn`, `.card`, `.navbar`) that you apply to elements. Utility-first gives more design flexibility and avoids specificity battles; component-based is faster for standard UI patterns but harder to customize.

**Component-Based (Bootstrap, Bulma):**
```html
<!-- Pre-built component - limited customization -->
<button class="btn btn-primary btn-lg">Click me</button>
```

**Utility-First (Tailwind):**
```html
<!-- Build exactly what you need with utilities -->
<button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
    Click me
</button>
```

**Comparison:**

| Aspect | Component-Based | Utility-First |
|--------|----------------|---------------|
| Learning curve | Low | Moderate |
| Customization | Limited | Unlimited |
| Design consistency | High | Depends on discipline |
| File size | Larger | Smaller (with purge) |
| Development speed | Fast initially | Fast after learning |

### Pros and Cons

**Definition:** Tailwind's advantages include rapid prototyping, no context switching between HTML and CSS, no naming conflicts, and excellent PurgeCSS integration for tiny production bundles. Its disadvantages include verbose HTML (many classes per element), a learning curve for memorizing utility names, and potential readability issues in large templates without component extraction.

**Advantages:**
- No naming convention wars (no `.btn-wrapper__inner--active`)
- Consistent spacing and color scales
- Responsive design is effortless
- Dark mode support built-in
- Small production bundles
- No context switching between HTML and CSS files
- Easy to maintain (delete HTML = delete styles)

**Disadvantages:**
- HTML can become verbose ("class soup")
- Learning curve for all utility names
- Need to learn the framework's naming conventions
- Can be repetitive without component extraction
- Initial build configuration required

### When to Use Tailwind

**Definition:** Tailwind is ideal for: custom designs that don't fit a standard component library, teams that want design consistency enforced by a token system, projects where CSS bundle size matters (Tailwind's PurgeCSS removes unused utilities), and developers who prefer co-locating styles with markup. It's less ideal for rapid prototyping with standard UI patterns or teams unfamiliar with CSS fundamentals.

**Perfect for:**
- Custom designs (not cookie-cutter layouts)
- Teams wanting design consistency
- Rapid prototyping
- Projects requiring unique branding
- Applications with responsive requirements

**Consider alternatives when:**
- Building many similar admin dashboards (consider component libraries)
- Team prefers separation of concerns (HTML/CSS)
- Need pixel-perfect control over every style
- Working on very small projects (CDN overhead)

---

## 2. Installation & Setup

**Definition:** The Installation & Setup process configures Tailwind CSS to scan your project's files, process utility classes through the JIT (Just-In-Time) engine, and generate an optimized CSS file containing only the styles you actually use.

**Context:** Proper installation ensures Tailwind works efficiently with your build process, provides IDE autocomplete support, and generates optimized production CSS with unused styles removed.

### Installation Flow Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                 TAILWIND INSTALLATION WORKFLOW                  │
└─────────────────────────────────────────────────────────────────┘

    ┌─────────────┐
    │   Install   │
    │  npm packages│
    └──────┬──────┘
           │ npm install -D tailwindcss postcss autoprefixer
           ▼
    ┌─────────────┐
    │   Initialize │
    │    Config    │
    └──────┬──────┘
           │ npx tailwindcss init -p
           ▼
    ┌─────────────┐
    │   Configure  │
    │    Content   │
    └──────┬──────┘
           │ content: ["./src/**/*.{html,js}"]
           ▼
    ┌─────────────┐
    │   Create     │
    │  Input CSS   │
    └──────┬──────┘
           │ @tailwind directives
           ▼
    ┌─────────────┐     ┌─────────────┐
    │    Build     │────▶│   Output    │
    │   Process    │     │    CSS      │
    └─────────────┘     └─────────────┘
           │                   │
           ▼                   ▼
    ┌─────────────┐     ┌─────────────┐
    │ Development │     │ Production  │
    │   --watch   │     │  --minify   │
    └─────────────┘     └─────────────┘

┌─────────────────────────────────────────────────────────────────┐
│                    FILE STRUCTURE                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  project/                                                       │
│  ├── tailwind.config.js     ← Configuration & customization    │
│  ├── postcss.config.js      ← PostCSS plugins                   │
│  ├── src/                                                     │
│  │   ├── input.css          ← @tailwind directives             │
│  │   ├── components/        ← React/Vue/HTML files             │
│  │   └── pages/             ← Templates                        │
│  └── dist/                                                    │
│      └── output.css         ← Generated CSS file               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### CDN (Quick Start - Development Only)

**Definition:** The Tailwind CDN link loads the full Tailwind CSS stylesheet from a content delivery network. It's only suitable for quick prototyping and learning — it includes all utilities (large file size), doesn't support customization via `tailwind.config.js`, and doesn't tree-shake unused styles. For production, always use the CLI or PostCSS build process.

```html
<!DOCTYPE html>
<html>
<head>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body>
    <h1 class="text-3xl font-bold text-blue-500">Hello Tailwind!</h1>
</body>
</html>
```

**⚠️ Warning:** CDN is for development only. It includes all 10,000+ classes.

### NPM Installation (Production)

```bash
# Using npm
npm install -D tailwindcss postcss autoprefixer

# Using yarn
yarn add -D tailwindcss postcss autoprefixer

# Using pnpm
pnpm add -D tailwindcss postcss autoprefixer
```

### Initialize Tailwind

**Definition:** Running `npx tailwindcss init` creates a `tailwind.config.js` file in your project root. This configuration file controls which files Tailwind scans for class names (the `content` array), custom theme extensions (colors, fonts, spacing), and plugins. The `content` array is critical — Tailwind uses it to determine which utility classes to include in the production build.

```bash
# Create tailwind.config.js and postcss.config.js
npx tailwindcss init -p
```

### Configure Content (tailwind.config.js)

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./src/**/*.{html,js,jsx,ts,tsx,vue}",
    "./public/index.html",
    // Add all files that use Tailwind classes
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

**Content Configuration Tips:**
```javascript
content: [
  // React/Vue/Angular components
  "./src/**/*.{js,jsx,ts,tsx,vue}",
  
  // HTML files
  "./public/**/*.html",
  
  // Include specific paths
  "./pages/**/*.{js,ts,jsx,tsx}",
  "./components/**/*.{js,ts,jsx,tsx}",
  
  // Exclude node_modules
  "!./node_modules",
]
```

### Create CSS Entry File

**Definition:** The Tailwind CSS entry file uses three `@tailwind` directives to inject Tailwind's generated styles: `@tailwind base` (Preflight — a CSS reset based on modern-normalize), `@tailwind components` (any component classes from plugins or `@layer components`), and `@tailwind utilities` (all utility classes). This file is processed by the Tailwind CLI or PostCSS to generate the final CSS output.

```css
/* src/input.css */
@tailwind base;      /* Reset + base styles */
@tailwind components; /* Component classes */
@tailwind utilities;  /* Utility classes */

/* Add custom base styles */
@layer base {
  h1 {
    @apply text-2xl font-bold;
  }
}

/* Add custom components */
@layer components {
  .btn-primary {
    @apply bg-blue-500 text-white px-4 py-2 rounded;
  }
}
```

### Build Process

**Definition:** The Tailwind build process scans all files listed in the `content` array of `tailwind.config.js`, finds every Tailwind class used, and generates a CSS file containing only those classes. In development, use `--watch` for automatic rebuilding. In production, Tailwind automatically minifies and removes all unused utilities, resulting in CSS files typically under 10KB.

```json
// package.json
{
  "scripts": {
    "build:css": "tailwindcss -i ./src/input.css -o ./dist/output.css",
    "watch:css": "tailwindcss -i ./src/input.css -o ./dist/output.css --watch",
    "prod:css": "tailwindcss -i ./src/input.css -o ./dist/output.css --minify"
  }
}
```

```bash
# Run once
npm run build:css

# Watch for changes
npm run watch:css

# Production build
npm run prod:css
```

### VS Code Extensions

**Definition:** The **Tailwind CSS IntelliSense** VS Code extension (by Tailwind Labs) provides autocomplete for utility class names, hover previews showing the generated CSS, linting for invalid classes, and syntax highlighting. It dramatically speeds up development by eliminating the need to memorize class names and showing the exact CSS each utility generates.

**Essential Extensions:**
1. **Tailwind CSS IntelliSense** - Autocomplete, linting, hover info
2. **Headwind** - Opinionated class sorter (enforces consistent order)
3. **Tailwind Shades** - Generate color shades

**Settings (settings.json):**
```json
{
  "tailwindCSS.includeLanguages": {
    "javascript": "javascript",
    "html": "HTML"
  },
  "tailwindCSS.emmetCompletions": true,
  "editor.quickSuggestions": {
    "strings": true
  }
}
```

### Framework Integration

**Definition:** Tailwind integrates with JavaScript frameworks by adding it to the build pipeline: in **Vite** projects (React, Vue, Svelte), install as a PostCSS plugin; in **Next.js**, it's supported out of the box with `create-next-app --tailwind`; in **Laravel**, use the Vite plugin. The integration ensures Tailwind scans framework component files for class names during the build.

**Vite:**
```javascript
// vite.config.js
import { defineConfig } from 'vite'

export default defineConfig({
  css: {
    postcss: './postcss.config.js',
  },
})
```

**Next.js:**
```javascript
// next.config.js
module.exports = {
  // Tailwind is automatically configured
}
```

**Laravel:**
```javascript
// tailwind.config.js
module.exports = {
  content: [
    "./resources/**/*.blade.php",
    "./resources/**/*.js",
    "./resources/**/*.vue",
  ],
}
```

---

## 3. Core Concepts

**Definition:** Core Concepts are the fundamental principles that govern how Tailwind CSS works—utility classes (single-purpose atomic classes), responsive prefixes (mobile-first breakpoints), state variants (hover, focus, etc.), dark mode support, and arbitrary values for one-off customizations.

**Context:** Understanding these concepts is essential for effectively using Tailwind. They form the foundation for writing efficient, maintainable, and responsive CSS without leaving your HTML.

### Utility-First Workflow Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│              UTILITY-FIRST WORKFLOW                             │
└─────────────────────────────────────────────────────────────────┘

  TRADITIONAL CSS WORKFLOW                    TAILWIND WORKFLOW
  ┌─────────────────────┐                    ┌─────────────────────┐
  │ 1. Write HTML       │                    │ 1. Write HTML       │
  │                     │                    │    + Classes        │
  └──────────┬──────────┘                    └──────────┬──────────┘
             │                                          │
             ▼                                          ▼
  ┌─────────────────────┐                    ┌─────────────────────┐
  │ 2. Create CSS file  │                    │ 2. No CSS needed    │
  │    .card {          │                    │    (mostly)         │
  │      padding: 1rem; │                    │                     │
  │      border: 1px    │                    │                     │
  │        solid #ccc;  │                    │                     │
  │    }                │                    │                     │
  └──────────┬──────────┘                    └──────────┬──────────┘
             │                                          │
             ▼                                          ▼
  ┌─────────────────────┐                    ┌─────────────────────┐
  │ 3. Name classes     │                    │ 3. Done! Classes    │
  │    .card-wrapper    │                    │    self-document    │
  │    .card__inner     │                    │                     │
  │    .card--active    │                    │                     │
  └──────────┬──────────┘                    └──────────┬──────────┘
             │                                          │
             ▼                                          ▼
  ┌─────────────────────┐                    ┌─────────────────────┐
  │ 4. Maintain BEM     │                    │ 4. Maintain HTML    │
  │    naming           │                    │    Delete = Clean   │
  └─────────────────────┘                    └─────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│           UTILITY CLASS COMPOSITION EXAMPLE                     │
└─────────────────────────────────────────────────────────────────┘

  Single Utility Classes                    Combined Result
  ┌────────────────────┐
  │ bg-blue-500        │──┐
  │ text-white         │──┤
  │ font-bold          │──┼──▶┌──────────────────────────┐
  │ py-2               │──┤   │   Styled Button          │
  │ px-4               │──┤   │   [Blue bg, white text]  │
  │ rounded            │──┤   │   "Click me"             │
  │ hover:bg-blue-700  │──┤   └──────────────────────────┘
  │ transition-colors  │──┘
  └────────────────────┘
```

### Utility Classes

Utility classes are single-purpose classes that apply one CSS property.

```html
<!-- Each class does one thing -->
<div class="bg-blue-500 text-white p-4 rounded-lg">
    <!-- bg-blue-500: background-color: rgb(59 130 246) -->
    <!-- text-white: color: rgb(255 255 255) -->
    <!-- p-4: padding: 1rem (16px) -->
    <!-- rounded-lg: border-radius: 0.5rem (8px) -->
</div>
```

**Common Utility Patterns:**
```html
<!-- Layout -->
<div class="block">display: block</div>
<div class="flex">display: flex</div>
<div class="grid">display: grid</div>
<div class="hidden">display: none</div>

<!-- Spacing -->
<div class="m-4">margin: 1rem</div>
<div class="p-4">padding: 1rem</div>
<div class="px-4">padding-left/right: 1rem</div>
<div class="py-2">padding-top/bottom: 0.5rem</div>

<!-- Colors -->
<div class="bg-red-500">background: red-500</div>
<div class="text-blue-600">color: blue-600</div>
<div class="border-gray-300">border-color: gray-300</div>
```

### Responsive Prefixes (Mobile-First)

**Definition:** Responsive prefixes allow you to apply styles at specific breakpoints using a mobile-first approach. Base styles apply to all screen sizes, and prefixes like `md:`, `lg:` add or override styles for larger screens.

**Context:** Mobile-first means you design for the smallest screen first, then progressively enhance for larger screens. This aligns with how most users browse the web and ensures core functionality works everywhere.

#### Responsive Breakpoint Flow (Mobile-First)

```
┌─────────────────────────────────────────────────────────────────┐
│              MOBILE-FIRST BREAKPOINT FLOW                       │
└─────────────────────────────────────────────────────────────────┘

   ┌─────────┐     ┌─────────┐     ┌─────────┐     ┌─────────┐
   │   BASE  │────▶│   sm:   │────▶│   md:   │────▶│   lg:   │
   │ (0px+)  │     │ (640px+)│     │ (768px+)│     │(1024px+)│
   └────┬────┘     └────┬────┘     └────┬────┘     └────┬────┘
        │               │               │               │
        ▼               ▼               ▼               ▼
   ┌─────────┐     ┌─────────┐     ┌─────────┐     ┌─────────┐
   │ Mobile  │     │  Large  │     │ Tablets │     │ Laptops │
   │ Phones  │     │ Phones  │     │         │     │         │
   └─────────┘     └─────────┘     └─────────┘     └─────────┘
        │               │               │               │
        └───────────────┴───────────────┴───────────────┘
                          │
                          ▼
                   ┌─────────────┐
                   │    xl:      │
                   │  (1280px+)  │
                   │  Desktops   │
                   └──────┬──────┘
                          │
                          ▼
                   ┌─────────────┐
                   │   2xl:      │
                   │  (1536px+)  │
                   │ Large Screens│
                   └─────────────┘

┌─────────────────────────────────────────────────────────────────┐
│  EXAMPLE: Responsive Grid                                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  class="grid-cols-1 sm:grid-cols-2 lg:grid-cols-4"              │
│                                                                 │
│  Mobile (0-639px):    1 column  ┌───┐                           │
│                                 │   │                           │
│                                 ├───┤                           │
│                                 │   │                           │
│                                 ├───┤                           │
│                                 │   │                           │
│                                 └───┘                           │
│                                                                 │
│  Tablet (768-1023px): 2 columns ┌───┬───┐                       │
│                                 │   │   │                       │
│                                 ├───┼───┤                       │
│                                 │   │   │                       │
│                                 └───┴───┘                       │
│                                                                 │
│  Desktop (1024px+):   4 columns ┌───┬───┬───┬───┐               │
│                                 │   │   │   │   │               │
│                                 └───┴───┴───┴───┘               │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

Tailwind uses a **mobile-first** approach. Base styles apply to all screens, breakpoints add styles for larger screens.

```html
<!-- Mobile-first example -->
<div class="w-full md:w-1/2 lg:w-1/3">
    <!-- Mobile: width: 100% -->
    <!-- md (768px+): width: 50% -->
    <!-- lg (1024px+): width: 33.333% -->
</div>

<!-- Another example -->
<div class="text-sm md:text-base lg:text-lg">
    <!-- Mobile: 0.875rem (14px) -->
    <!-- md: 1rem (16px) -->
    <!-- lg: 1.125rem (18px) -->
</div>
```

**Default Breakpoints:**

| Prefix | Min-width | CSS Equivalent |
|--------|-----------|----------------|
| (none) | 0px | Base styles |
| `sm:` | 640px | `@media (min-width: 640px)` |
| `md:` | 768px | `@media (min-width: 768px)` |
| `lg:` | 1024px | `@media (min-width: 1024px)` |
| `xl:` | 1280px | `@media (min-width: 1280px)` |
| `2xl:` | 1536px | `@media (min-width: 1536px)` |

**Practical Responsive Layout:**
```html
<!-- Card grid that adapts to screen size -->
<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4">
    <div class="bg-white p-4 rounded shadow">Card 1</div>
    <div class="bg-white p-4 rounded shadow">Card 2</div>
    <div class="bg-white p-4 rounded shadow">Card 3</div>
    <div class="bg-white p-4 rounded shadow">Card 4</div>
</div>
```

### State Variants

**Definition:** State variants are prefixes that apply styles based on an element's state or context, such as `hover:`, `focus:`, `active:`, `disabled:`, `first:`, `last:`, and more. They enable interactive designs without writing custom CSS.

**Context:** State variants allow you to respond to user interactions and element relationships directly in your utility classes, making it easy to create dynamic, accessible interfaces.

#### State Variants Hierarchy

```
┌─────────────────────────────────────────────────────────────────┐
│                 STATE VARIANTS HIERARCHY                        │
└─────────────────────────────────────────────────────────────────┘

  USER INTERACTION STATES                    STRUCTURAL STATES
  ┌─────────────────────────┐                ┌─────────────────────────┐
  │ hover:                  │                │ first:                  │
  │   Mouse over element    │                │   First child           │
  │                         │                │                         │
  │ focus:                  │                │ last:                   │
  │   Element focused       │                │   Last child            │
  │                         │                │                         │
  │ focus-visible:          │                │ odd: / even:            │
  │   Keyboard focused      │                │   Alternating children  │
  │                         │                │                         │
  │ focus-within:           │                │ only:                   │
  │   Child has focus       │                │   Only child            │
  │                         │                │                         │
  │ active:                 │                │ empty:                  │
  │   Being clicked         │                │   No children           │
  │                         │                │                         │
  │ disabled:               │                │ required:               │
  │   Element disabled      │                │   Required field        │
  │                         │                │                         │
  │ checked:                │                │ invalid:                │
  │   Checkbox/radio on     │                │   Invalid input         │
  │                         │                │                         │
  │ visited:                │                │ valid:                  │
  │   Link visited          │                │   Valid input           │
  └─────────────────────────┘                └─────────────────────────┘

  RESPONSIVE STATES                          GROUP/PEER STATES
  ┌─────────────────────────┐                ┌─────────────────────────┐
  │ sm: / md: / lg: / xl:   │                │ group-hover:            │
  │   Breakpoint prefixes   │                │   Parent being hovered  │
  │                         │                │                         │
  │ dark:                   │                │ group-focus:            │
  │   Dark mode             │                │   Parent focused        │
  │                         │                │                         │
  │ print:                  │                │ peer-hover:             │
  │   Print media           │                │   Sibling being hovered │
  │                         │                │                         │
  │ motion-safe:            │                │ peer-focus:             │
  │   No preference         │                │   Sibling focused       │
  │                         │                │                         │
  │ motion-reduce:          │                │ peer-invalid:           │
  │   Reduced motion        │                │   Sibling invalid       │
  │                         │                │                         │
  │ landscape: / portrait:  │                │ peer-checked:           │
  │   Orientation           │                │   Sibling checked       │
  └─────────────────────────┘                └─────────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│  COMBINING VARIANTS                                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Order: Responsive ▶ Dark ▶ State ▶ Base Class                  │
│                                                                 │
│  Example:                                                       │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │  md:dark:hover:bg-blue-600                              │    │
│  │  │   │   │    │                                        │    │
│  │  │   │   │    └─ Base utility                          │    │
│  │  │   │   └────── Hover state                           │    │
│  │  │   └────────── Dark mode                             │    │
│  │  └────────────── Medium breakpoint (768px+)            │    │
│  └─────────────────────────────────────────────────────────┘    │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

Apply styles based on element state.

```html
<!-- Hover state -->
<button class="bg-blue-500 hover:bg-blue-700">
    Hover over me
</button>

<!-- Focus state -->
<input class="border-gray-300 focus:border-blue-500 focus:ring-2">

<!-- Active state -->
<button class="bg-blue-500 active:bg-blue-800">
    Click me
</button>

<!-- Disabled state -->
<button class="bg-blue-500 disabled:opacity-50 disabled:cursor-not-allowed" disabled>
    Disabled Button
</button>

<!-- First/Last child -->
<ul>
    <li class="first:mt-0 last:mb-0">Item 1</li>
    <li class="first:mt-0 last:mb-0">Item 2</li>
    <li class="first:mt-0 last:mb-0">Item 3</li>
</ul>

<!-- Odd/Even -->
<ul>
    <li class="odd:bg-gray-100 even:bg-white">Item 1</li>
    <li class="odd:bg-gray-100 even:bg-white">Item 2</li>
    <li class="odd:bg-gray-100 even:bg-white">Item 3</li>
</ul>
```

**Common State Variants:**
- `hover:` - Mouse over
- `focus:` - Element focused
- `active:` - Element being clicked
- `disabled:` - Disabled elements
- `visited:` - Visited links
- `checked:` - Checked checkboxes/radio buttons
- `first:` - First child
- `last:` - Last child
- `odd:` / `even:` - Odd/even children
- `empty:` - Elements with no children

### Dark Mode

**Definition:** Tailwind's dark mode support adds a `dark:` variant that applies styles only when dark mode is active. With `darkMode: 'class'` in config, dark mode activates when a `dark` class is on the `<html>` element (toggled by JavaScript). With `darkMode: 'media'`, it follows the OS preference via the `prefers-color-scheme` media query. Prefix any utility with `dark:` to apply it in dark mode.

Tailwind supports dark mode with the `dark:` prefix.

```javascript
// tailwind.config.js
module.exports = {
  darkMode: 'class', // 'media' for system preference, 'class' for manual toggle
  // ...
}
```

```html
<!-- Toggle dark mode by adding 'dark' class to html element -->
<html class="dark">
<body class="bg-white dark:bg-gray-900 text-gray-900 dark:text-white">
    <div class="bg-gray-100 dark:bg-gray-800">
        <h1 class="text-black dark:text-white">Hello World</h1>
    </div>
</body>
</html>
```

**Dark Mode Toggle (React example):**
```jsx
function DarkModeToggle() {
    const [dark, setDark] = useState(false);
    
    useEffect(() => {
        if (dark) {
            document.documentElement.classList.add('dark');
        } else {
            document.documentElement.classList.remove('dark');
        }
    }, [dark]);
    
    return (
        <button 
            onClick={() => setDark(!dark)}
            className="p-2 rounded bg-gray-200 dark:bg-gray-700"
        >
            {dark ? '🌙' : '☀️'}
        </button>
    );
}
```

### Arbitrary Values

Use square brackets for one-off custom values.

```html
<!-- Arbitrary sizes -->
<div class="w-[100px] h-[50px]"></div>
<div class="top-[117px] left-[20%]"></div>

<!-- Arbitrary colors -->
<div class="bg-[#1da1f2] text-[rgb(255,0,0)]"></div>

<!-- Arbitrary spacing -->
<div class="p-[3rem] m-[10px]"></div>

<!-- Arbitrary in responsive -->
<div class="md:w-[500px] lg:w-[800px]"></div>

<!-- Arbitrary with calc() -->
<div class="w-[calc(100%-2rem)]"></div>

<!-- Arbitrary animations -->
<div class="animate-[bounce_1s_infinite]"></div>
```

**Best Practices:**
- Use arbitrary values sparingly
- If you use the same value 3+ times, add it to config
- Prefer standard utilities when possible

### Important Modifier

**Definition:** The `!` prefix in Tailwind (e.g., `!text-red-500`) adds `!important` to the generated CSS declaration, overriding any other styles including inline styles. Use it sparingly — only when you need to override styles from third-party libraries or legacy CSS that you cannot modify. Overusing `!important` makes styles harder to debug and maintain.

Add `!` to make any utility `!important`.

```html
<!-- Force override -->
<div class="text-blue-500 !text-red-500">
    This text will be red, overriding other styles
</div>

<!-- Useful for component overrides -->
<button class="bg-blue-500 !bg-green-500">
    Force green background
</button>
```

---

## 4. Layout & Spacing

**Definition:** Layout & Spacing utilities control how elements are positioned and spaced on the page. This includes containers for centering content, display properties (block, flex, grid), positioning (static, relative, absolute, fixed, sticky), padding, margin, and overflow handling.

**Context:** These utilities form the structural foundation of your designs. Proper use of layout and spacing creates visual hierarchy, improves readability, and ensures responsive behavior across different screen sizes.

#### Box Model Utilities Mapping

```
┌─────────────────────────────────────────────────────────────────┐
│                    BOX MODEL UTILITIES                          │
└─────────────────────────────────────────────────────────────────┘

                    ┌─────────────────────┐
                    │      margin (m)     │  ← Outside spacing
                    │   ┌─────────────┐   │     m-4 = 1rem
                    │   │   border    │   │  ← Border width
                    │   │ ┌─────────┐ │   │     border-2
                    │   │ │ padding │ │   │  ← Inside spacing
                    │   │ │┌───────┐│ │   │     p-4 = 1rem
                    │   │ ││CONTENT││ │   │
                    │   │ │└───────┘│ │   │
                    │   │ └─────────┘ │   │
                    │   └─────────────┘   │
                    └─────────────────────┘

┌─────────────────────────────────────────────────────────────────┐
│  SPACING SCALE                                                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Space Outside (Margin)           Space Inside (Padding)        │
│                                                                 │
│  ┌──────────────┬────────────┐    ┌──────────────┬────────────┐ │
│  │ Class        │ Value      │    │ Class        │ Value      │ │
│  ├──────────────┼────────────┤    ├──────────────┼────────────┤ │
│  │ m-0          │ 0          │    │ p-0          │ 0          │ │
│  │ m-1          │ 0.25rem    │    │ p-1          │ 0.25rem    │ │
│  │ m-2          │ 0.5rem     │    │ p-2          │ 0.5rem     │ │
│  │ m-4          │ 1rem       │    │ p-4          │ 1rem       │ │
│  │ m-6          │ 1.5rem     │    │ p-6          │ 1.5rem     │ │
│  │ m-8          │ 2rem       │    │ p-8          │ 2rem       │ │
│  └──────────────┴────────────┘    └──────────────┴────────────┘ │
│                                                                 │
│  Direction Modifiers:                                           │
│  • mt-, mr-, mb-, ml-  = Specific sides                        │
│  • mx-, my-            = Horizontal / Vertical                 │
│  • -m-4                = Negative margin                       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Container

**Definition:** The `container` utility sets a fixed `max-width` that matches the current breakpoint's minimum width, centering content within the viewport. By default it's not centered — add `mx-auto` to center it. Configure `container` in `tailwind.config.js` to add automatic centering and horizontal padding. It's the standard way to constrain page content width in Tailwind layouts.

The container class centers content and adds responsive max-widths.

```html
<!-- Basic container -->
<div class="container mx-auto px-4">
    <!-- Content centered with auto margins -->
</div>

<!-- Container with breakpoints -->
<div class="container mx-auto px-4 sm:px-6 lg:px-8">
    <!-- Responsive padding -->
</div>

<!-- Full-width with max constraints -->
<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <!-- Max-width 80rem (1280px) -->
</div>
```

**Container Sizes:**
```html
<div class="container sm:max-w-xl">640px</div>
<div class="container md:max-w-3xl">768px</div>
<div class="container lg:max-w-5xl">1024px</div>
<div class="container xl:max-w-7xl">1280px</div>
```

### Display

**Definition:** Tailwind's display utilities control the CSS `display` property: `block`, `inline-block`, `inline`, `flex`, `inline-flex`, `grid`, `inline-grid`, `hidden` (`display: none`), and `contents`. These are the most fundamental layout utilities — `flex` and `grid` are the primary tools for building modern layouts in Tailwind.

```html
<!-- Block display -->
<div class="block">Block element</div>

<!-- Inline -->
<span class="inline">Inline element</span>

<!-- Inline block -->
<span class="inline-block">Inline but with block properties</span>

<!-- Flex container -->
<div class="flex">Flex container</div>

<!-- Grid container -->
<div class="grid">Grid container</div>

<!-- Hidden -->
<div class="hidden">Not visible</div>
<div class="hidden md:block">Hidden on mobile, visible on md+</div>

<!-- Contents (useful for grid children) -->
<div class="contents">Removes wrapper from layout</div>
```

### Position

**Definition:** Tailwind's position utilities set the CSS `position` property: `static`, `relative`, `absolute`, `fixed`, `sticky`. Use `relative` on a parent to establish a positioning context for `absolute` children. Combine with inset utilities (`top-`, `right-`, `bottom-`, `left-`, `inset-`) to control the exact placement of positioned elements.

```html
<!-- Static (default) -->
<div class="static">Normal flow</div>

<!-- Relative -->
<div class="relative">
    Positioned relative to normal position
    <div class="absolute top-0 right-0">Absolutely positioned child</div>
</div>

<!-- Absolute -->
<div class="absolute top-4 left-4">Positioned relative to nearest positioned ancestor</div>

<!-- Fixed -->
<div class="fixed top-0 left-0 w-full">Fixed to viewport</div>

<!-- Sticky -->
<header class="sticky top-0 z-50">Sticks when scrolling</header>
```

**Position Values:**
```html
<!-- Inset (shorthand for top/right/bottom/left) -->
<div class="absolute inset-0">Fill parent</div>
<div class="absolute inset-x-0">Full width, auto height</div>
<div class="absolute inset-y-0">Full height, auto width</div>

<!-- Specific positioning -->
<div class="absolute top-0 left-0">Top left corner</div>
<div class="absolute bottom-4 right-4">Bottom right with spacing</div>
<div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2">Centered</div>
```

### Padding & Margin

**Definition:** Tailwind's spacing utilities use a numeric scale where each unit equals 4px (e.g., `p-4` = `padding: 16px`). Padding classes: `p-` (all sides), `px-` (horizontal), `py-` (vertical), `pt-`/`pr-`/`pb-`/`pl-` (individual sides). Margin classes follow the same pattern with `m-`. Use `mx-auto` for horizontal centering. Negative margins use the `-m-` prefix.

**Padding:**
```html
<!-- All sides -->
<div class="p-0">0px</div>
<div class="p-1">4px</div>
<div class="p-2">8px</div>
<div class="p-4">16px</div>
<div class="p-8">32px</div>

<!-- Specific sides -->
<div class="pt-4">Padding top</div>
<div class="pr-4">Padding right</div>
<div class="pb-4">Padding bottom</div>
<div class="pl-4">Padding left</div>

<!-- Horizontal/Vertical -->
<div class="px-4">Padding left + right</div>
<div class="py-4">Padding top + bottom</div>
```

**Margin:**
```html
<!-- All sides -->
<div class="m-4">16px margin</div>
<div class="m-auto">Auto margin (centers block)</div>

<!-- Negative margins (use - prefix) -->
<div class="-m-4">Negative 16px margin</div>
<div class="-mt-2">Negative margin top</div>

<!-- Specific sides -->
<div class="mt-4">Margin top</div>
<div class="mr-auto">Push element left</div>
<div class="ml-auto">Push element right</div>

<!-- Center horizontally -->
<div class="mx-auto">Horizontal centering</div>
```

**Spacing Scale:**
| Class | Value | Pixels |
|-------|-------|--------|
| `p-0` | 0 | 0px |
| `p-0.5` | 0.125rem | 2px |
| `p-1` | 0.25rem | 4px |
| `p-2` | 0.5rem | 8px |
| `p-3` | 0.75rem | 12px |
| `p-4` | 1rem | 16px |
| `p-5` | 1.25rem | 20px |
| `p-6` | 1.5rem | 24px |
| `p-8` | 2rem | 32px |
| `p-10` | 2.5rem | 40px |
| `p-12` | 3rem | 48px |

### Space Between

**Definition:** The `space-x-` and `space-y-` utilities add margin between child elements of a flex or block container using CSS sibling selectors (`> * + *`). `space-x-4` adds `margin-left: 16px` to all children except the first. This is a convenient alternative to adding individual margins to each child element. Use `gap-` instead when working with flex or grid containers.

Add horizontal or vertical space between child elements.

```html
<!-- Horizontal spacing (for flex/grid row) -->
<div class="flex space-x-4">
    <div>Item 1</div>  <!-- No left margin -->
    <div>Item 2</div>  <!-- margin-left: 1rem -->
    <div>Item 3</div>  <!-- margin-left: 1rem -->
</div>

<!-- Vertical spacing (for flex/grid column) -->
<div class="flex flex-col space-y-4">
    <div>Item 1</div>  <!-- No top margin -->
    <div>Item 2</div>  <!-- margin-top: 1rem -->
    <div>Item 3</div>  <!-- margin-top: 1rem -->
</div>

<!-- Responsive spacing -->
<div class="flex flex-col md:flex-row md:space-x-4 space-y-4 md:space-y-0">
    <!-- Vertical on mobile, horizontal on desktop -->
</div>

<!-- Reverse space -->
<div class="flex flex-row-reverse space-x-4 space-x-reverse">
    <!-- Spaces items correctly in reverse order -->
</div>
```

### Overflow

```html
<!-- Visible (default) -->
<div class="overflow-visible">Content can overflow</div>

<!-- Hidden -->
<div class="overflow-hidden">Overflow is clipped</div>

<!-- Scroll -->
<div class="overflow-scroll">Always show scrollbars</div>

<!-- Auto -->
<div class="overflow-auto">Scrollbars when needed</div>

<!-- Specific axis -->
<div class="overflow-x-auto">Horizontal scroll only</div>
<div class="overflow-y-hidden">Hide vertical overflow</div>

<!-- Truncate (single line ellipsis) -->
<div class="truncate">Long text that will be truncated...</div>

<!-- Line clamp (multi-line ellipsis) -->
<div class="line-clamp-3">
    This text will be limited to 3 lines 
    and then truncated with an ellipsis...
</div>
```

---

## 5. Flexbox & Grid

**Definition:** Flexbox & Grid utilities provide powerful layout systems for arranging elements. Flexbox excels at one-dimensional layouts (rows OR columns) with alignment control, while CSS Grid handles two-dimensional layouts (rows AND columns) with precise placement.

**Context:** These are the primary tools for creating complex, responsive layouts. Flexbox is ideal for navigation bars, card components, and centering content. Grid is perfect for page layouts, photo galleries, and dashboard designs.

#### Flexbox Alignment Matrix

```
┌─────────────────────────────────────────────────────────────────┐
│              FLEXBOX ALIGNMENT MATRIX                           │
└─────────────────────────────────────────────────────────────────┘

  JUSTIFY CONTENT (Main Axis - Horizontal in Row)
  ┌──────────────────────────────────────────────────────────────┐
  │                                                              │
  │  justify-start (default)          justify-center             │
  │  ┌────┬──────┬────┐              ┌──────┬────┬──────┐        │
  │  │A   │      │   B│              │      │AB  │      │        │
  │  └────┴──────┴────┘              └──────┴────┴──────┘        │
  │                                                              │
  │  justify-end                      justify-between            │
  │  ┌──────┬────┬────┐              ┌────┬──────────┬────┐      │
  │  │      │      AB│              │A   │          │   B│      │
  │  └──────┴────┴────┘              └────┴──────────┴────┘      │
  │                                                              │
  │  justify-around                   justify-evenly             │
  │  ┌──┬────┬──┬────┬──┐            ┌────┬────┬────┬────┐       │
  │  │  │ A  │  │ B  │  │            │    │ A  │ B  │    │       │
  │  └──┴────┴──┴────┴──┘            └────┴────┴────┴────┘       │
  │                                                              │
  └──────────────────────────────────────────────────────────────┘

  ALIGN ITEMS (Cross Axis - Vertical in Row)
  ┌──────────────────────────────────────────────────────────────┐
  │                                                              │
  │  items-start                      items-center               │
  │  ┌──────────────────┐            ┌──────────────────┐        │
  │  │A                 │            │                  │        │
  │  │B                 │            │       AB         │        │
  │  │                  │            │                  │        │
  │  └──────────────────┘            └──────────────────┘        │
  │                                                              │
  │  items-end                        items-stretch (default)    │
  │  ┌──────────────────┐            ┌──────────────────┐        │
  │  │                  │            │▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓│        │
  │  │                  │            │▓▓▓A▓▓▓▓▓▓▓▓▓B▓▓▓│        │
  │  │                 B│            │▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓│        │
  │  └──────────────────┘            └──────────────────┘        │
  │                                                              │
  └──────────────────────────────────────────────────────────────┘

  COMMON PATTERNS
  ┌──────────────────────────────────────────────────────────────┐
  │                                                              │
  │  Center Everything                Sidebar Layout             │
  │  ┌──────────────────┐            ┌──────────────────┐        │
  │  │                  │            │▓▓▓▓│             │        │
  │  │       [X]        │            │▓▓▓▓│             │        │
  │  │                  │            │▓▓▓▓│             │        │
  │  └──────────────────┘            └──────────────────┘        │
  │  flex justify-center             flex                        │
  │       items-center               ├─ aside: w-64              │
│                                    └─ main: flex-1             │
  │                                                              │
  └──────────────────────────────────────────────────────────────┘
```

#### Grid System Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                  GRID SYSTEM OVERVIEW                           │
└─────────────────────────────────────────────────────────────────┘

  GRID TEMPLATE COLUMNS
  ┌──────────────────────────────────────────────────────────────┐
  │                                                              │
  │  grid-cols-2                     grid-cols-3                 │
  │  ┌──────────┬──────────┐        ┌──────┬──────┬──────┐       │
  │  │          │          │        │      │      │      │       │
  │  │    A     │    B     │        │  A   │  B   │  C   │       │
  │  │          │          │        │      │      │      │       │
  │  ├──────────┼──────────┤        ├──────┼──────┼──────┤       │
  │  │          │          │        │      │      │      │       │
  │  │    C     │    D     │        │  D   │  E   │  F   │       │
  │  │          │          │        │      │      │      │       │
  │  └──────────┴──────────┘        └──────┴──────┴──────┘       │
  │                                                              │
  │  Responsive: grid-cols-1 md:grid-cols-2 lg:grid-cols-3       │
  │                                                              │
  └──────────────────────────────────────────────────────────────┘

  GRID SPANNING
  ┌──────────────────────────────────────────────────────────────┐
  │                                                              │
  │  col-span-2 (spans 2 columns)                                │
  │  ┌──────────────────┬──────────┐                             │
  │  │                  │          │                             │
  │  │    FEATURED      │    B     │                             │
  │  │                  │          │                             │
  │  ├──────────┬───────┼──────────┤                             │
  │  │          │       │          │                             │
  │  │    C     │   D   │    E     │                             │
  │  │          │       │          │                             │
  │  └──────────┴───────┴──────────┘                             │
  │                                                              │
  │  row-span-2 (spans 2 rows)                                   │
  │  ┌──────────┬──────────┐                                     │
  │  │          │▓▓▓▓▓▓▓▓▓▓│                                     │
  │  │    A     │▓▓▓▓B▓▓▓▓▓│                                     │
  │  │          │▓▓▓▓▓▓▓▓▓▓│                                     │
  │  ├──────────┤▓▓▓▓▓▓▓▓▓▓│                                     │
  │  │          │▓▓▓▓▓▓▓▓▓▓│                                     │
  │  │    C     │▓▓▓▓▓▓▓▓▓▓│                                     │
  │  │          │▓▓▓▓▓▓▓▓▓▓│                                     │
  │  └──────────┴──────────┘                                     │
  │                                                              │
  └──────────────────────────────────────────────────────────────┘

  DASHBOARD LAYOUT (12-column system)
  ┌──────────────────────────────────────────────────────────────┐
  │ HEADER (col-span-12)                                         │
  │ ████████████████████████████████████████████████████████████ │
  ├────────────┬─────────────────────────────────────────────────┤
  │            │                                                 │
  │ SIDEBAR    │  MAIN CONTENT                                   │
  │ (col-span-3│  (col-span-9)                                   │
  │  or fixed) │                                                 │
  │            │  ┌──────────────┐ ┌──────────────┐              │
  │            │  │   Card 1     │ │   Card 2     │              │
  │            │  └──────────────┘ └──────────────┘              │
  │            │                                                 │
  └────────────┴─────────────────────────────────────────────────┘

  AUTO-FIT GRID (Responsive without breakpoints)
  ┌──────────────────────────────────────────────────────────────┐
  │                                                              │
  │  grid-cols-[repeat(auto-fit,minmax(250px,1fr))]             │
  │                                                              │
  │  Mobile:                         Desktop:                    │
  │  ┌────────────┐                 ┌─────┬─────┬─────┬─────┐   │
  │  │  Card 1    │                 │ C1  │ C2  │ C3  │ C4  │   │
  │  ├────────────┤                 ├─────┴─────┴─────┴─────┤   │
  │  │  Card 2    │                 │ C5  │ C6  │ C7  │     │   │
  │  ├────────────┤                 └─────┴─────┴─────┴─────┘   │
  │  │  Card 3    │                                              │
  │  └────────────┘                                              │
  │                                                              │
  └──────────────────────────────────────────────────────────────┘
```

### Flexbox

**Definition:** Tailwind's flexbox utilities wrap CSS Flexbox. Start with `flex` to create a flex container, then control direction (`flex-row`, `flex-col`), wrapping (`flex-wrap`), alignment (`items-center`, `justify-between`), and child sizing (`flex-1`, `flex-none`, `flex-auto`). Flexbox is ideal for one-dimensional layouts (rows or columns) and aligning items within a container.

**Flex Direction:**
```html
<!-- Row (default) -->
<div class="flex flex-row">Horizontal layout</div>

<!-- Column -->
<div class="flex flex-col">Vertical layout</div>

<!-- Row reverse -->
<div class="flex flex-row-reverse">Right to left</div>

<!-- Column reverse -->
<div class="flex flex-col-reverse">Bottom to top</div>
```

**Justify Content (main axis):**
```html
<div class="flex justify-start">    <!-- Align to start (left) -->
<div class="flex justify-end">      <!-- Align to end (right) -->
<div class="flex justify-center">   <!-- Center horizontally -->
<div class="flex justify-between">  <!-- Space between items -->
<div class="flex justify-around">   <!-- Space around items -->
<div class="flex justify-evenly">   <!-- Even spacing -->
```

**Align Items (cross axis):**
```html
<div class="flex items-start">      <!-- Align to top -->
<div class="flex items-end">        <!-- Align to bottom -->
<div class="flex items-center">     <!-- Center vertically -->
<div class="flex items-stretch">    <!-- Stretch to fill (default) -->
<div class="flex items-baseline">   <!-- Align text baselines -->
```

**Align Content (multi-line):**
```html
<div class="flex flex-wrap content-start">
<div class="flex flex-wrap content-end">
<div class="flex flex-wrap content-center">
<div class="flex flex-wrap content-between">
```

**Flex Wrap:**
```html
<div class="flex flex-nowrap">     <!-- No wrapping (default) -->
<div class="flex flex-wrap">       <!-- Wrap to next line -->
<div class="flex flex-wrap-reverse"> <!-- Wrap in reverse -->
```

**Flex Grow, Shrink, Basis:**
```html
<!-- Flex grow -->
<div class="flex">
    <div class="flex-grow">Takes remaining space</div>
    <div class="flex-grow-0">Fixed size</div>
</div>

<!-- Flex shrink -->
<div class="flex">
    <div class="flex-shrink">Can shrink</div>
    <div class="flex-shrink-0">Won't shrink</div>
</div>

<!-- Flex basis -->
<div class="flex">
    <div class="basis-1/4">25% initial size</div>
    <div class="basis-1/2">50% initial size</div>
</div>

<!-- Shorthand -->
<div class="flex-1">   <!-- flex: 1 1 0% -->
<div class="flex-auto"> <!-- flex: 1 1 auto -->
<div class="flex-initial"> <!-- flex: 0 1 auto -->
<div class="flex-none">   <!-- flex: none -->
```

**Common Flexbox Patterns:**
```html
<!-- Center content perfectly -->
<div class="flex items-center justify-center min-h-screen">
    <div>Centered content</div>
</div>

<!-- Sidebar layout -->
<div class="flex">
    <aside class="w-64 flex-shrink-0">Sidebar</aside>
    <main class="flex-grow">Main content</main>
</div>

<!-- Card with footer at bottom -->
<div class="flex flex-col h-64">
    <div class="flex-grow">Content</div>
    <footer>Footer always at bottom</footer>
</div>

<!-- Navigation -->
<nav class="flex items-center justify-between px-4 py-2">
    <div class="logo">Logo</div>
    <div class="flex space-x-4">
        <a href="#">Link 1</a>
        <a href="#">Link 2</a>
        <a href="#">Link 3</a>
    </div>
</nav>
```

### CSS Grid

**Definition:** Tailwind's grid utilities wrap CSS Grid Layout. Use `grid` to create a grid container, `grid-cols-{n}` to define columns, `gap-` for gutters, and `col-span-{n}` on children to span multiple columns. Grid is ideal for two-dimensional layouts. Combine with responsive prefixes (`md:grid-cols-3`) to create responsive grid layouts without media query boilerplate.

**Grid Template Columns:**
```html
<!-- Basic columns -->
<div class="grid grid-cols-1">   <!-- 1 column -->
<div class="grid grid-cols-2">   <!-- 2 equal columns -->
<div class="grid grid-cols-3">   <!-- 3 equal columns -->
<div class="grid grid-cols-4">   <!-- 4 equal columns -->

<!-- Fractional columns -->
<div class="grid grid-cols-[2fr_1fr]">  <!-- 2:1 ratio -->

<!-- Repeat notation -->
<div class="grid grid-cols-[repeat(3,1fr)]">  <!-- 3 equal columns -->

<!-- Responsive columns -->
<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4">
    <!-- 1 col mobile, 2 col tablet, 3 col desktop, 4 col large -->
</div>

<!-- Auto-fit with minmax (responsive without breakpoints) -->
<div class="grid grid-cols-[repeat(auto-fit,minmax(250px,1fr))]">
    <!-- As many columns as fit with 250px minimum -->
</div>
```

**Grid Template Rows:**
```html
<div class="grid grid-rows-3">   <!-- 3 equal rows -->
<div class="grid grid-rows-[auto_1fr_auto]">  <!-- Header, content, footer -->
```

**Column/Row Span:**
```html
<!-- Column span -->
<div class="col-span-1">1 column wide</div>
<div class="col-span-2">2 columns wide</div>
<div class="col-span-full">Full width</div>

<!-- Row span -->
<div class="row-span-2">Spans 2 rows</div>

<!-- Start/End -->
<div class="col-start-1 col-end-3">Columns 1-2</div>
<div class="col-start-2 col-span-2">Start at 2, span 2</div>
```

**Gap:**
```html
<!-- Both axes -->
<div class="grid grid-cols-3 gap-4">  <!-- 16px gap -->

<!-- Specific axes -->
<div class="grid grid-cols-3 gap-x-4 gap-y-2">  <!-- Horizontal & vertical -->

<!-- Responsive gaps -->
<div class="grid grid-cols-3 gap-2 md:gap-4 lg:gap-6">
```

**Common Grid Patterns:**
```html
<!-- Photo gallery -->
<div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4">
    <img src="photo1.jpg" class="w-full h-48 object-cover">
    <img src="photo2.jpg" class="w-full h-48 object-cover">
    <!-- ... more photos -->
</div>

<!-- Dashboard layout -->
<div class="grid grid-cols-12 gap-4">
    <header class="col-span-12">Header</header>
    <aside class="col-span-12 md:col-span-3">Sidebar</aside>
    <main class="col-span-12 md:col-span-9">Main Content</main>
</div>

<!-- Card layout with featured item -->
<div class="grid grid-cols-3 gap-4">
    <div class="col-span-3 md:col-span-2">Featured</div>
    <div class="col-span-3 md:col-span-1">Side 1</div>
    <div class="col-span-3 md:col-span-1">Side 2</div>
</div>

<!-- Auto-fill cards -->
<div class="grid grid-cols-[repeat(auto-fill,minmax(300px,1fr))] gap-4">
    <div class="card">Card 1</div>
    <div class="card">Card 2</div>
    <div class="card">Card 3</div>
    <!-- Automatically wraps to new rows -->
</div>
```

---

## 6. Typography

**Definition:** Typography utilities control text appearance, including font families, sizes, weights, colors, alignment, line height, letter spacing, text decoration, and text overflow handling.

**Context:** Typography establishes the visual hierarchy and readability of your content. Well-designed typography guides users through information, conveys brand personality, and ensures accessibility across different devices.

**Key Concepts:**
- **Font Family**: Define typefaces (sans, serif, mono, custom)
- **Font Size**: Control text scale (xs through 9xl)
- **Font Weight**: Adjust thickness (thin through black)
- **Text Color**: Apply color utilities with opacity support
- **Line Height**: Control vertical spacing (leading-tight through leading-loose)
- **Letter Spacing**: Adjust character spacing (tracking-tight through tracking-widest)
- **Text Alignment**: Position text (left, center, right, justify)
- **Text Decoration**: Underlines, strikethroughs, and styling
- **Text Overflow**: Handle long text (truncate, line-clamp)

### Font Family

**Definition:** Tailwind provides utility classes for setting the `font-family` property. By default, it includes `font-sans` (inter/system-ui), `font-serif` (merriweather/georgia), and `font-mono` (fira code/consolas). You can customize these in your configuration. These utilities typically set a stack of fallback fonts to ensure consistent rendering across operating systems.

```html
<!-- Sans-serif (default) -->
<p class="font-sans">Inter, system-ui, sans-serif</p>

<!-- Serif -->
<p class="font-serif">Georgia, Cambria, serif</p>

<!-- Monospace -->
<code class="font-mono">Consolas, Monaco, monospace</code>
```

**Custom Fonts (tailwind.config.js):**
```javascript
module.exports = {
  theme: {
    extend: {
      fontFamily: {
        'sans': ['Inter', 'system-ui', 'sans-serif'],
        'display': ['Poppins', 'sans-serif'],
        'body': ['Open Sans', 'sans-serif'],
      },
    },
  },
}
```

```html
<h1 class="font-display">Display Font</h1>
<p class="font-body">Body Font</p>
```

### Font Size

**Definition:** Tailwind's `text-{size}` utilities control `font-size` and usually a corresponding `line-height` to ensure readable typography out of the box. Sizes range from `text-xs` (0.75rem) to `text-9xl` (8rem). The scale is designed to provide a harmonious typographic hierarchy without perfect pixel pushing.

```html
<p class="text-xs">    12px - Extra small</p>
<p class="text-sm">    14px - Small</p>
<p class="text-base">  16px - Base (default)</p>
<p class="text-lg">    18px - Large</p>
<p class="text-xl">    20px - Extra large</p>
<p class="text-2xl">   24px - 2X large</p>
<p class="text-3xl">   30px - 3X large</p>
<p class="text-4xl">   36px - 4X large</p>
<p class="text-5xl">   48px - 5X large</p>
<p class="text-6xl">   60px - 6X large</p>
<p class="text-7xl">   72px - 7X large</p>
<p class="text-8xl">   96px - 8X large</p>
<p class="text-9xl">   128px - 9X large</p>
```

### Font Weight

**Definition:** Tailwind's `font-{weight}` utilities set the `font-weight` property. They use semantic names like `font-thin` (100), `font-normal` (400), `font-bold` (700), and `font-black` (900). This abstraction makes it easier to remember weights and ensures consistency across the application.

```html
<p class="font-thin">      100 - Thin</p>
<p class="font-extralight">200 - Extra Light</p>
<p class="font-light">     300 - Light</p>
<p class="font-normal">    400 - Normal (default)</p>
<p class="font-medium">    500 - Medium</p>
<p class="font-semibold">  600 - Semi Bold</p>
<p class="font-bold">      700 - Bold</p>
<p class="font-extrabold">800 - Extra Bold</p>
<p class="font-black">     900 - Black</p>
```

### Text Color

**Definition:** Tailwind uses the `text-{color}` format to set the `color` property. It utilizes the same extensive color palette as backgrounds and borders. You can also control the opacity of text with the `/` modifier (e.g., `text-blue-500/50`). Hover and focus states work seamlessly with standard variant prefixes (`bover:text-blue-700`).

```html
<!-- Basic colors -->
<p class="text-transparent">Transparent</p>
<p class="text-current">Current color (inherits)</p>
<p class="text-black">Black</p>
<p class="text-white">White</p>

<!-- Gray scale -->
<p class="text-gray-50">  Lightest gray</p>
<p class="text-gray-100"> Very light</p>
<p class="text-gray-500"> Medium gray</p>
<p class="text-gray-900"> Darkest gray</p>

<!-- Colors with shades (50-950) -->
<p class="text-blue-500">Blue 500</p>
<p class="text-red-600">Red 600</p>
<p class="text-green-400">Green 400</p>

<!-- With opacity -->
<p class="text-blue-500/50">50% opacity</p>
<p class="text-blue-500/[0.75]">75% opacity</p>
```

**Color Palette Preview:**
- Slate, Gray, Zinc, Neutral, Stone (grays)
- Red, Orange, Amber, Yellow (warm)
- Lime, Green, Emerald, Teal (greens)
- Cyan, Sky, Blue, Indigo, Violet (blues/purples)
- Purple, Fuchsia, Pink, Rose (pinks)

### Text Alignment

**Definition:** Tailwind provides utilities for `text-align` customization: `text-left`, `text-center`, `text-right`, and `text-justify`. These are essential for controlling how text flows within its container. Responsive variants (e.g., `md:text-left`) are frequently used to change alignment on different screen sizes.

```html
<p class="text-left">    Left aligned</p>
<p class="text-center">  Center aligned</p>
<p class="text-right">   Right aligned</p>
<p class="text-justify"> Justified</p>
<p class="text-start">   Start (LTR=left, RTL=right)</p>
<p class="text-end">     End (LTR=right, RTL=left)</p>

<!-- Responsive alignment -->
<p class="text-center md:text-left">Center mobile, left desktop</p>
```

### Line Height (Leading)

**Definition:** Tailwind's `leading-{size}` utilities control the `line-height` property. Line height is critical for readability. Tailwind provides relative line heights (like `leading-tight`, `leading-normal`, `leading-loose`) and fixed line heights. `leading-none` (1) is often used for headings to prevent unwanted vertical spacing, while `leading-relaxed` improves readability of long paragraphs.

```html
<p class="leading-none">    1 - No extra space</p>
<p class="leading-tight">   1.25 - Tight</p>
<p class="leading-snug">    1.375 - Snug</p>
<p class="leading-normal">  1.5 - Normal (default)</p>
<p class="leading-relaxed"> 1.625 - Relaxed</p>
<p class="leading-loose">   2 - Loose</p>

<!-- With font size utilities -->
<p class="text-xl leading-relaxed">Large relaxed text</p>
```

### Letter Spacing (Tracking)

**Definition:** Tailwind's `tracking-{size}` utilities control `letter-spacing`. Adjusting tracking improves legibility, especially for uppercase headings (`tracking-widest`) or dense interfaces (`tracking-tight`). While subtle, correct letter spacing significantly impacts the polished feel of typography.

```html
<p class="tracking-tighter"> -0.05em - Very tight</p>
<p class="tracking-tight">   -0.025em - Tight</p>
<p class="tracking-normal">   0 - Normal (default)</p>
<p class="tracking-wide">     0.025em - Wide</p>
<p class="tracking-wider">    0.05em - Wider</p>
<p class="tracking-widest">   0.1em - Widest</p>
```

### Text Decoration & Transform

**Definition:** Utilities like `underline`, `line-through`, `no-underline` control `text-decoration`. `uppercase`, `lowercase`, and `capitalize` control `text-transform`. These are commonly used for links, pricing (strikethrough), and headings to enforce consistent casing regardless of the backend data.

```html
<!-- Decoration -->
<p class="underline">Underlined</p>
<p class="overline">Overline</p>
<p class="line-through">Strikethrough</p>
<p class="no-underline">No decoration</p>

<!-- Style -->
<p class="underline decoration-solid">Solid (default)</p>
<p class="underline decoration-double">Double</p>
<p class="underline decoration-dotted">Dotted</p>
<p class="underline decoration-wavy">Wavy</p>

<!-- Color -->
<p class="underline decoration-blue-500">Blue underline</p>

<!-- Thickness -->
<p class="underline decoration-2">2px thick</p>

<!-- Offset -->
<p class="underline underline-offset-4">4px offset from text</p>

<!-- Transform -->
<p class="uppercase">UPPERCASE</p>
<p class="lowercase">lowercase</p>
<p class="capitalize">Capitalize Each Word</p>
<p class="normal-case">Normal case</p>
```

### Text Overflow & Truncation

**Definition:** Tailwind provides utilities like `truncate` (which sets `overflow: hidden`, `text-overflow: ellipsis`, `white-space: nowrap`) to handle text that exceeds its container's width. For multi-line truncation, the `line-clamp-{n}` plugin (now built-in) is used to limit text to a specific number of lines before ellipsizing.

```html
<!-- Truncate (single line) -->
<p class="truncate">
    This long text will be truncated with an ellipsis...
</p>

<!-- Multi-line clamp -->
<p class="line-clamp-3">
    This text will be limited to exactly three lines 
    and then truncated with an ellipsis if it exceeds 
    that limit...
</p>

<!-- Overflow -->
<p class="overflow-ellipsis overflow-hidden whitespace-nowrap">
    Legacy truncate syntax
</p>

<!-- Whitespace -->
<p class="whitespace-normal">Normal wrapping</p>
<p class="whitespace-nowrap">No wrapping</p>
<p class="whitespace-pre">Respects whitespace</p>
<p class="whitespace-pre-line">Preserves newlines</p>
```

### Complete Typography Examples

```html
<!-- Article typography -->
<article class="prose lg:prose-xl max-w-none">
    <h1 class="text-4xl font-bold text-gray-900 mb-4">
        Article Title
    </h1>
    <p class="text-lg text-gray-600 leading-relaxed mb-6">
        Lead paragraph with relaxed line height and subtle color.
    </p>
    <p class="text-base text-gray-800 leading-normal">
        Body text with comfortable reading experience.
    </p>
</article>

<!-- Pricing table -->
<div class="text-center">
    <p class="text-sm font-medium text-gray-500 uppercase tracking-wide">
        Starter Plan
    </p>
    <p class="text-5xl font-extrabold text-gray-900">
        $29
    </p>
    <p class="text-lg text-gray-500">
        per month
    </p>
</div>

<!-- Quote/Blockquote -->
<blockquote class="border-l-4 border-blue-500 pl-4 italic text-gray-700">
    "Tailwind CSS makes styling websites incredibly fast."
</blockquote>
```

---

## 7. Backgrounds, Borders & Effects

**Definition:** Background, border, and effects utilities control the visual styling of elements. This includes background colors, gradients, images, borders (width, style, color, radius), box shadows, opacity, and visual filters (blur, brightness, grayscale).

**Context:** These utilities add depth, emphasis, and visual interest to your designs. They help create card components, buttons, overlays, glassmorphism effects, and establish visual hierarchy through layering and contrast.

**Key Concepts:**
- **Background Color**: Solid colors with opacity support
- **Background Gradients**: Linear, radial, and conic gradients
- **Background Images**: Position, size, repeat, attachment
- **Borders**: Width, style, color, and radius (rounded corners)
- **Outline**: Focus indicators separate from borders
- **Box Shadow**: Depth and elevation effects
- **Opacity**: Transparency control
- **Filters**: Visual effects like blur, brightness, saturation
- **Backdrop Filters**: Glassmorphism and blur-behind effects

### Background Color

**Definition:** The `bg-{color}` utilities set the `background-color` of an element. They support the full color palette and opacity modifiers (e.g., `bg-red-500/20`). Background colors are fundamental for creating layout structure, buttons, cards, and visual hierarchy.

```html
<div class="bg-white">White background</div>
<div class="bg-black">Black background</div>
<div class="bg-transparent">Transparent</div>
<div class="bg-current">Current color</div>

<!-- Gray scale -->
<div class="bg-gray-50">Very light</div>
<div class="bg-gray-100">Light</div>
<div class="bg-gray-500">Medium</div>
<div class="bg-gray-900">Dark</div>

<!-- Colors -->
<div class="bg-blue-500">Blue</div>
<div class="bg-red-600">Red</div>
<div class="bg-green-400">Green</div>

<!-- With opacity -->
<div class="bg-blue-500/50">50% opacity</div>
<div class="bg-blue-500/[0.25]">25% opacity</div>
```

### Background Gradients

**Definition:** Tailwind makes creating linear gradients easy with three utilities: `bg-gradient-to-{direction}` (sets gradient angle), `from-{color}` (start color), and `to-{color}` (end color). You can optionally add `via-{color}` for a middle stop. Gradients add depth and modern aesthetics to backgrounds and buttons.

```html
<!-- Linear gradients -->
<div class="bg-gradient-to-r from-blue-500 to-purple-600">
    Left to right gradient
</div>

<div class="bg-gradient-to-br from-cyan-400 via-blue-500 to-purple-600">
    Diagonal with middle color
</div>

<!-- Direction keywords -->
<div class="bg-gradient-to-t">Bottom to top</div>
<div class="bg-gradient-to-tr">Bottom-left to top-right</div>
<div class="bg-gradient-to-r">Left to right</div>
<div class="bg-gradient-to-br">Top-left to bottom-right</div>
<div class="bg-gradient-to-b">Top to bottom</div>

<!-- Multiple colors -->
<div class="bg-gradient-to-r from-red-500 via-yellow-500 to-green-500">
    Rainbow gradient
</div>

<!-- With stops -->
<div class="bg-gradient-to-r from-blue-500 from-10% via-purple-500 via-30% to-pink-500 to-90%">
    Custom color stops
</div>

<!-- Radial gradient -->
<div class="bg-[radial-gradient(ellipse_at_center,_var(--tw-gradient-stops))] from-purple-400 to-blue-500">
    Radial gradient (arbitrary)
</div>

<!-- Conic gradient -->
<div class="bg-[conic-gradient(at_top,_var(--tw-gradient-stops))] from-orange-400 via-red-500 to-orange-400">
    Conic gradient
</div>
```

### Background Size, Position & Repeat

**Definition:** These utilities control `background-size` (`bg-cover`, `bg-contain`, `bg-auto`), `background-position` (`bg-center`, `bg-top`, etc.), and `background-repeat` (`bg-no-repeat`, `bg-repeat`). They are essential when working with background images to ensure they scale and position correctly within their container.

```html
<!-- Size -->
<div class="bg-auto">    Original size</div>
<div class="bg-cover">   Cover entire element</div>
<div class="bg-contain"> Fit within element</div>

<!-- Position -->
<div class="bg-center">  Center</div>
<div class="bg-top">     Top</div>
<div class="bg-bottom">  Bottom</div>
<div class="bg-left">    Left</div>
<div class="bg-right">   Right</div>
<div class="bg-top-right">Top right corner</div>

<!-- Repeat -->
<div class="bg-repeat">       Repeat both directions</div>
<div class="bg-no-repeat">    No repeat</div>
<div class="bg-repeat-x">     Repeat horizontally</div>
<div class="bg-repeat-y">     Repeat vertically</div>
<div class="bg-repeat-round"> Round to fit</div>
<div class="bg-repeat-space"> Space evenly</div>

<!-- Attachment -->
<div class="bg-fixed">   Fixed to viewport</div>
<div class="bg-local">   Scrolls with element</div>
<div class="bg-scroll">  Scrolls with viewport</div>
```

### Border Width & Style

**Definition:** Tailwind provides `border-{width}` utilities (`border`, `border-0`, `border-2`, `border-4`, `border-8`) to set `border-width`. `border-{side}-{width}` sets individual sides. `border-{style}` utilities (`border-solid`, `border-dashed`, `border-dotted`) control the `border-style`. Borders delineate content areas and interactive elements.

```html
<!-- Width -->
<div class="border-0">    No border</div>
<div class="border">      1px border (all sides)</div>
<div class="border-2">    2px border</div>
<div class="border-4">    4px border</div>
<div class="border-8">    8px border</div>

<!-- Specific sides -->
<div class="border-t">    Top border</div>
<div class="border-r">    Right border</div>
<div class="border-b">    Bottom border</div>
<div class="border-l">    Left border</div>
<div class="border-x">    Left & right borders</div>
<div class="border-y">    Top & bottom borders</div>

<!-- Style -->
<div class="border-solid">  Solid (default)</div>
<div class="border-dashed"> Dashed</div>
<div class="border-dotted"> Dotted</div>
<div class="border-double"> Double</div>
<div class="border-hidden"> Hidden</div>
<div class="border-none">   No border</div>
```

### Border Color

**Definition:** The `border-{color}` utilities set the `border-color`. Like text and background colors, they support the full palette and opacity modifiers. Defining border colors separately from widths allows for cleaner responsive overrides (e.g., changing color on hover while keeping width constant).

```html
<div class="border-gray-300">Gray border</div>
<div class="border-blue-500">Blue border</div>
<div class="border-red-500">Red border</div>
<div class="border-transparent">Transparent border</div>

<!-- Individual sides -->
<div class="border-t-blue-500 border-b-red-500">
    Blue top, red bottom
</div>
```

### Border Radius

**Definition:** Tailwind's `rounded-{size}` utilities control `border-radius`, softening the corners of elements. Sizes range from `rounded-sm` to `rounded-full` (creates circles or pills). You can also target specific corners (e.g., `rounded-t-lg` for top corners only), commonly used in card designs and buttons.

```html
<!-- All corners -->
<div class="rounded-none"> 0px (no radius)</div>
<div class="rounded-sm">   2px</div>
<div class="rounded">      4px (default)</div>
<div class="rounded-md">   6px</div>
<div class="rounded-lg">   8px</div>
<div class="rounded-xl">   12px</div>
<div class="rounded-2xl">  16px</div>
<div class="rounded-3xl">  24px</div>
<div class="rounded-full"> 9999px (circle/pill)</div>

<!-- Specific corners -->
<div class="rounded-t-lg">     Top corners</div>
<div class="rounded-r-lg">     Right corners</div>
<div class="rounded-b-lg">     Bottom corners</div>
<div class="rounded-l-lg">     Left corners</div>
<div class="rounded-tl-lg">    Top-left</div>
<div class="rounded-tr-lg">    Top-right</div>
<div class="rounded-br-lg">    Bottom-right</div>
<div class="rounded-bl-lg">    Bottom-left</div>
```

### Outline

**Definition:** While borders take up space in the box model, `outline` draws a line outside the element without affecting layout. Tailwind facilitates accessible focus states using `outline-{width}`, `outline-{color}`, and `outline-offset`. Custom outlines are crucial for keyboard navigation visibility.

```html
<!-- Outline width -->
<div class="outline-0">No outline</div>
<div class="outline-1">1px outline</div>
<div class="outline-2">2px outline</div>
<div class="outline-4">4px outline</div>

<!-- Outline style -->
<div class="outline">        Default outline</div>
<div class="outline-none">   No outline</div>
<div class="outline-dashed"> Dashed outline</div>
<div class="outline-dotted"> Dotted outline</div>
<div class="outline-double"> Double outline</div>

<!-- Outline color -->
<div class="outline-blue-500">Blue outline</div>

<!-- Outline offset -->
<div class="outline-2 outline-offset-2 outline-blue-500">
    Outline with 2px gap
</div>

<!-- Focus ring (common pattern) -->
<input class="focus:outline-none focus:ring-2 focus:ring-blue-500">
```

### Box Shadow

**Definition:** The `shadow-{size}` utilities apply `box-shadow` depth effects, from `shadow-sm` (subtle) to `shadow-2xl` (deep). `shadow-inner` applies an inset shadow. Shadows create elevation and z-axis hierarchy in material-like designs, helping distinct elements pop from the background.

```html
<!-- Default shadows -->
<div class="shadow-none">    No shadow</div>
<div class="shadow-sm">      0 1px 2px 0 rgb(0 0 0 / 0.05)</div>
<div class="shadow">         0 1px 3px 0 rgb(0 0 0 / 0.1)</div>
<div class="shadow-md">      0 4px 6px -1px rgb(0 0 0 / 0.1)</div>
<div class="shadow-lg">      0 10px 15px -3px rgb(0 0 0 / 0.1)</div>
<div class="shadow-xl">      0 20px 25px -5px rgb(0 0 0 / 0.1)</div>
<div class="shadow-2xl">     0 25px 50px -12px rgb(0 0 0 / 0.25)</div>
<div class="shadow-inner">   Inset shadow</div>

<!-- Colored shadows -->
<div class="shadow-lg shadow-blue-500/50">Blue tinted shadow</div>

<!-- Custom shadow (config) -->
```

**Custom Shadow Example (tailwind.config.js):**
```javascript
module.exports = {
  theme: {
    extend: {
      boxShadow: {
        'card': '0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06)',
        'glow': '0 0 20px rgba(59, 130, 246, 0.5)',
      }
    }
  }
}
```

### Opacity

**Definition:** Tailwind's `opacity-{value}` utilities set the element's overall opacity (0 to 100). Unlike color opacity modifiers (which affect only the background or text color), `opacity` affects the entire element and its children. It is often used for disabled states (`opacity-50`) or fade-in/out transitions.

```html
<div class="opacity-0">   0% (invisible)</div>
<div class="opacity-25">  25%</div>
<div class="opacity-50">  50%</div>
<div class="opacity-75">  75%</div>
<div class="opacity-100"> 100% (fully visible)</div>

<!-- Hover opacity -->
<div class="opacity-75 hover:opacity-100 transition-opacity">
    Fades in on hover
</div>

<!-- Disabled state -->
<button class="opacity-50 cursor-not-allowed" disabled>
    Disabled button
</button>
```

### Blur & Filters

**Definition:** Tailwind includes filter utilities like `blur`, `brightness`, `contrast`, `grayscale`, `invert`, `saturate`, and `sepia`. These rely on the CSS `filter` property. `blur-{amount}` is particularly popular for creating "frosted glass" effects (backdrop blur) in modern UI overlays.

```html
<!-- Blur -->
<div class="blur-none">No blur</div>
<div class="blur-sm">  4px blur</div>
<div class="blur">     8px blur (default)</div>
<div class="blur-md">  12px blur</div>
<div class="blur-lg">  16px blur</div>
<div class="blur-xl">  24px blur</div>
<div class="blur-2xl"> 40px blur</div>
<div class="blur-3xl"> 64px blur</div>

<!-- Backdrop blur (for glassmorphism) -->
<div class="backdrop-blur-md bg-white/30">
    Glassmorphism effect
</div>

<!-- Other filters -->
<div class="brightness-50">   50% brightness</div>
<div class="contrast-125">    125% contrast</div>
<div class="grayscale">       Black & white</div>
<div class="sepia">           Sepia tone</div>
<div class="hue-rotate-90">   Rotate hue 90deg</div>
<div class="invert">          Invert colors</div>
<div class="saturate-150">    150% saturation</div>

<!-- Combined filters -->
<div class="grayscale hover:grayscale-0 transition-all">
    Grayscale that turns to color on hover
</div>
```

### Visual Examples

```html
<!-- Card with complete styling -->
<div class="bg-white rounded-xl shadow-lg border border-gray-200 overflow-hidden">
    <div class="h-48 bg-gradient-to-br from-blue-400 to-purple-600"></div>
    <div class="p-6">
        <h3 class="text-xl font-bold text-gray-900">Card Title</h3>
        <p class="text-gray-600 mt-2">Card description here.</p>
    </div>
</div>

<!-- Button with hover effects -->
<button class="bg-blue-500 hover:bg-blue-600 text-white px-6 py-3 rounded-lg 
               shadow-md hover:shadow-lg transition-all duration-200
               border border-blue-600">
    Click Me
</button>

<!-- Glassmorphism card -->
<div class="bg-white/10 backdrop-blur-md rounded-2xl border border-white/20 
            shadow-xl p-6 text-white">
    <h2 class="text-2xl font-bold">Glass Card</h2>
    <p class="mt-2 opacity-80">Modern glassmorphism effect</p>
</div>
```

---

## 8. Sizing

**Definition:** Sizing utilities control the dimensions of elements, including width, height, minimum/maximum sizes, and aspect ratios. These utilities use a consistent spacing scale and support percentages, viewport units, and fixed values.

**Context:** Proper sizing ensures elements display correctly across different screen sizes and content types. Sizing utilities work with the box model to create responsive layouts, maintain aspect ratios for media, and constrain content to readable widths.

**Key Concepts:**
- **Width**: Fixed (0-96), percentages (1/2, 1/3, full), viewport (screen), auto
- **Height**: Fixed, percentages, viewport, auto
- **Min/Max Width/Height**: Constraints for responsive design
- **Aspect Ratio**: Maintain proportional dimensions (square, video, custom)
- **Prose Width**: Optimal reading width (max-w-prose = 65ch)

### Width (w-)

**Definition:** Tailwind's `w-{size}` utilities set element width. They use a comprehensive scale: fixed values (`w-1` = 0.25rem), percentages (`w-1/2` = 50%), viewport units (`w-screen` = 100vw), and special keywords (`w-auto`, `w-full`, `w-min`, `w-max`, `w-fit`). The percentage scale is particularly useful for building responsive grid-like layouts without CSS Grid.

```html
<!-- Fixed widths -->
<div class="w-0">     0px</div>
<div class="w-px">    1px</div>
<div class="w-1">     4px</div>
<div class="w-4">     16px</div>
<div class="w-8">     32px</div>
<div class="w-16">    64px</div>
<div class="w-32">    128px</div>
<div class="w-64">    256px</div>
<div class="w-96">    384px</div>

<!-- Percentage widths -->
<div class="w-1/2">   50%</div>
<div class="w-1/3">   33.333%</div>
<div class="w-2/3">   66.666%</div>
<div class="w-1/4">   25%</div>
<div class="w-3/4">   75%</div>
<div class="w-full">  100%</div>

<!-- Special widths -->
<div class="w-screen">  100vw (viewport width)</div>
<div class="w-auto">    Auto</div>
<div class="w-fit">     Fit content</div>
<div class="w-min">     Min content</div>
<div class="w-max">     Max content</div>
```

### Height (h-)

**Definition:** Tailwind's `h-{size}` utilities set element height using the same scale as width. Special height utilities include `h-screen` (100vh), `h-full` (100% of parent), and `h-auto`. Setting heights is essential for sticky footers, full-screen hero sections, and image aspect ratios.

```html
<!-- Fixed heights -->
<div class="h-0">     0px</div>
<div class="h-1">     4px</div>
<div class="h-4">     16px</div>
<div class="h-8">     32px</div>
<div class="h-16">    64px</div>
<div class="h-32">    128px</div>
<div class="h-64">    256px</div>
<div class="h-96">    384px</div>

<!-- Percentage heights -->
<div class="h-1/2">   50% of parent</div>
<div class="h-full">  100% of parent</div>

<!-- Special heights -->
<div class="h-screen">  100vh (viewport height)</div>
<div class="h-auto">    Auto</div>
<div class="h-fit">     Fit content</div>
<div class="h-min">     Min content</div>
<div class="h-max">     Max content</div>
```

### Min/Max Sizing

**Definition:** Utilities like `min-w-0`, `max-w-md`, `min-h-screen`, and `max-h-full` control the constraints of an element's size. `max-w-{size}` is crucial for readable typography (e.g., `max-w-prose`) and responsive containers (`max-w-7xl mx-auto`). `min-h-screen` is the standard pattern for full-page layouts that stretch to fill the viewport but can grow with content.

```html
<!-- Min width -->
<div class="min-w-0">       0px minimum</div>
<div class="min-w-full">    100% minimum</div>
<div class="min-w-min">     Min-content</div>
<div class="min-w-max">     Max-content</div>
<div class="min-w-fit">     Fit-content</div>

<!-- Max width -->
<div class="max-w-0">       0rem</div>
<div class="max-w-xs">      20rem (320px)</div>
<div class="max-w-sm">      24rem (384px)</div>
<div class="max-w-md">      28rem (448px)</div>
<div class="max-w-lg">      32rem (512px)</div>
<div class="max-w-xl">      36rem (576px)</div>
<div class="max-w-2xl">     42rem (672px)</div>
<div class="max-w-3xl">     48rem (768px)</div>
<div class="max-w-4xl">     56rem (896px)</div>
<div class="max-w-5xl">     64rem (1024px)</div>
<div class="max-w-6xl">     72rem (1152px)</div>
<div class="max-w-7xl">     80rem (1280px)</div>
<div class="max-w-full">    100%</div>
<div class="max-w-none">    No max width</div>

<!-- Max width prose (for readability) -->
<div class="max-w-prose">   65ch (optimal reading width)</div>

<!-- Min height -->
<div class="min-h-0">       0px minimum</div>
<div class="min-h-full">    100% minimum</div>
<div class="min-h-screen">  100vh minimum</div>

<!-- Max height -->
<div class="max-h-0">       0rem</div>
<div class="max-h-96">      24rem</div>
<div class="max-h-full">    100%</div>
<div class="max-h-screen">  100vh</div>
```

### Aspect Ratio

**Definition:** The `aspect-{ratio}` utilities (e.g., `aspect-video`, `aspect-square`) facilitate controlling the width-to-height ratio of an element, replacing the old "padding-bottom hack". This is native browser functionality via the `aspect-ratio` CSS property, invaluable for responsive images, video embeds, and card thumbnails.

```html
<!-- Square -->
<div class="aspect-square">  1:1 aspect ratio</div>

<!-- Video -->
<div class="aspect-video">   16:9 aspect ratio</div>

<!-- Auto -->
<div class="aspect-auto">    Natural aspect ratio</div>

<!-- Custom ratio (arbitrary) -->
<div class="aspect-[4/3]">   4:3 aspect ratio</div>
<div class="aspect-[21/9]">  21:9 ultrawide</div>
<div class="aspect-[3/4]">   3:4 portrait</div>
```

**Aspect Ratio Plugin (tailwind.config.js):**
```javascript
module.exports = {
  theme: {
    extend: {
      aspectRatio: {
        '4/3': '4 / 3',
        '3/4': '3 / 4',
        '21/9': '21 / 9',
      },
    },
  },
}
```

### Sizing Examples

```html
<!-- Full-height hero section -->
<section class="min-h-screen flex items-center justify-center bg-gray-900">
    <div class="text-center text-white">
        <h1 class="text-5xl font-bold">Hero Title</h1>
    </div>
</section>

<!-- Responsive image container -->
<div class="w-full max-w-4xl mx-auto aspect-video">
    <img src="video-thumbnail.jpg" class="w-full h-full object-cover">
</div>

<!-- Sidebar layout with min/max constraints -->
<div class="flex min-h-screen">
    <aside class="w-64 min-w-[250px] max-w-xs bg-gray-800">
        Sidebar
    </aside>
    <main class="flex-grow p-8">
        Main content
    </main>
</div>

<!-- Container with readable width -->
<article class="max-w-prose mx-auto px-4">
    <!-- Content with optimal reading width -->
</article>

<!-- Grid of equal height cards -->
<div class="grid grid-cols-3 gap-4">
    <div class="h-64 bg-blue-500">Card 1</div>
    <div class="h-64 bg-blue-500">Card 2</div>
    <div class="h-64 bg-blue-500">Card 3</div>
</div>
```

---

## 9. Transitions & Animations

**Definition:** Transitions and animations utilities add motion and interactivity to your designs. Transitions smoothly change property values over time (hover effects), while animations create complex, keyframe-based movements.

**Context:** Motion enhances user experience by providing feedback, guiding attention, and creating a sense of polish. Use transitions for subtle state changes and animations for attention-grabbing effects or loading indicators.

**Key Concepts:**
- **Transitions**: Property, duration, timing function (easing), delay
- **Transforms**: Scale, rotate, translate, skew
- **Transform Origin**: Change the pivot point for transformations
- **Built-in Animations**: spin, ping, pulse, bounce
- **Custom Animations**: Define keyframes in config
- **Stagger**: Delay animations for sequential effects

### Transition Properties

**Definition:** Tailwind provides sensible default transitions via `transition` (all common properties), `transition-colors`, `transition-opacity`, and `transition-transform`. These utilities set `transition-property` and default duration/timing, enabling smooth state changes (hover/focus) with a single class. Add `transition-none` to disable animations.

```html
<!-- Transition all properties -->
<div class="transition-all duration-300">
    Animates all properties
</div>

<!-- Specific properties -->
<div class="transition-colors">     Background, border, color, etc.</div>
<div class="transition-opacity">    Opacity only</div>
<div class="transition-transform">  Transform only</div>
<div class="transition-shadow">     Box-shadow only</div>

<!-- Multiple properties -->
<div class="transition-colors transition-transform">
    Colors and transforms
</div>

<!-- No transition -->
<div class="transition-none">
    Instant changes
</div>
```

### Duration

**Definition:** The `duration-{ms}` utilities control how long a transition or animation takes to complete, ranging from `duration-75` (fast) to `duration-1000` (slow). Matching durations to the type of interaction (quick for hovers, slower for modals) is key to a polished "native" feel.

```html
<div class="duration-75">   75ms</div>
<div class="duration-100">  100ms</div>
<div class="duration-150">  150ms</div>
<div class="duration-200">  200ms</div>
<div class="duration-300">  300ms (default)</div>
<div class="duration-500">  500ms</div>
<div class="duration-700">  700ms</div>
<div class="duration-1000"> 1000ms</div>

<!-- Usage with transition -->
<button class="transition-colors duration-300">
    300ms color transition
</button>
```

### Timing Function (Easing)

**Definition:** The `ease-{type}` utilities control the acceleration curve of a transition (`transition-timing-function`). Common options: `ease-linear` (constant speed), `ease-in` (slow start), `ease-out` (slow end - best for entering UI), and `ease-in-out` (slow start and end). Proper easing makes animations feel natural and less robotic.

```html
<div class="ease-linear">      Linear (constant speed)</div>
<div class="ease-in">          Slow start, fast end</div>
<div class="ease-out">         Fast start, slow end</div>
<div class="ease-in-out">      Slow start and end</div>

<!-- With transition -->
<button class="transition-all duration-300 ease-in-out">
    Smooth transition
</button>
```

### Delay

**Definition:** The `delay-{ms}` utilities add a wait time before a transition or animation starts. This is useful for staggering animations (e.g., list items fading in one by one) or preventing accidental hover triggers by adding a small delay.

```html
<div class="delay-75">   75ms delay</div>
<div class="delay-100">  100ms delay</div>
<div class="delay-150">  150ms delay</div>
<div class="delay-200">  200ms delay</div>
<div class="delay-300">  300ms delay</div>
<div class="delay-500">  500ms delay</div>
<div class="delay-700">  700ms delay</div>
<div class="delay-1000"> 1000ms delay</div>

<!-- Staggered animations -->
<div class="delay-100">Item 1</div>
<div class="delay-200">Item 2</div>
<div class="delay-300">Item 3</div>
```

### Transform (Scale, Rotate, Translate)

**Definition:** Tailwind's transform utilities (e.g., `scale-105`, `rotate-45`, `translate-x-4`) use CSS transforms to modify an element's appearance without affecting layout flow. Since Tailwind v3, these can be used independently without the `transform` class. They are GPU-accelerated and ideal for hover effects and interactive animations.

**Scale:**
```html
<div class="scale-0">    Scale to 0 (invisible)</div>
<div class="scale-50">   50% size</div>
<div class="scale-75">   75% size</div>
<div class="scale-90">   90% size</div>
<div class="scale-95">   95% size</div>
<div class="scale-100">  Original size (default)</div>
<div class="scale-105">  105% size</div>
<div class="scale-110">  110% size</div>
<div class="scale-125">  125% size</div>
<div class="scale-150">  150% size</div>

<!-- Axis-specific -->
<div class="scale-x-50">   50% width</div>
<div class="scale-y-150">  150% height</div>

<!-- Hover scale effect -->
<button class="transition-transform hover:scale-105">
    Scales up on hover
</button>
```

**Rotate:**
```html
<div class="rotate-0">     0deg</div>
<div class="rotate-45">    45deg</div>
<div class="rotate-90">    90deg</div>
<div class="rotate-180">   180deg</div>

<!-- Negative rotation -->
<div class="-rotate-45">   -45deg</div>
<div class="-rotate-90">   -90deg</div>

<!-- Hover rotate -->
<div class="transition-transform hover:rotate-12">
    Rotates on hover
</div>
```

**Translate:**
```html
<!-- X axis -->
<div class="translate-x-0">     0px</div>
<div class="translate-x-4">     16px right</div>
<div class="-translate-x-4">    16px left</div>
<div class="translate-x-1/2">   50% of width</div>
<div class="translate-x-full">  100% of width</div>

<!-- Y axis -->
<div class="translate-y-0">     0px</div>
<div class="translate-y-4">     16px down</div>
<div class="-translate-y-4">    16px up</div>
<div class="translate-y-1/2">   50% of height</div>

<!-- Combined -->
<div class="translate-x-4 -translate-y-4">
    Right and up
</div>

<!-- Center absolute element -->
<div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2">
    Perfectly centered
</div>
```

**Skew:**
```html
<div class="skew-x-0">     No skew</div>
<div class="skew-x-3">     3deg skew X</div>
<div class="skew-x-6">     6deg skew X</div>
<div class="skew-x-12">    12deg skew X</div>
<div class="-skew-x-12">   -12deg skew X</div>

<div class="skew-y-3">     3deg skew Y</div>
<div class="skew-y-6">     6deg skew Y</div>
<div class="-skew-y-12">   -12deg skew Y</div>
```

**Origin:**
```html
<div class="origin-center">    Transform from center (default)</div>
<div class="origin-top">       Transform from top</div>
<div class="origin-bottom">    Transform from bottom</div>
<div class="origin-left">      Transform from left</div>
<div class="origin-right">     Transform from right</div>
<div class="origin-top-left">  Transform from top-left</div>

<!-- Usage -->
<div class="origin-top-left rotate-45">
    Rotates around top-left corner
</div>
```

### Built-in Animations

**Definition:** Tailwind includes four keyframe animations out of the box: `animate-spin` (loading spinners), `animate-pulse` (skeleton loading states), `animate-bounce` (attention-grabbing indicators), and `animate-ping` (notification badges). These handle infinite loops and common UI patterns with zero configuration.

```html
<!-- Spin (for loading indicators) -->
<svg class="animate-spin h-5 w-5 text-blue-500" viewBox="0 0 24 24">
    <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
    <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4z"></path>
</svg>

<!-- Ping (for notifications/badges) -->
<span class="relative flex h-3 w-3">
    <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-red-400 opacity-75"></span>
    <span class="relative inline-flex rounded-full h-3 w-3 bg-red-500"></span>
</span>

<!-- Pulse (for skeletons/loading) -->
<div class="animate-pulse">
    <div class="h-4 bg-gray-400 rounded w-3/4"></div>
    <div class="h-4 bg-gray-400 rounded mt-2"></div>
</div>

<!-- Bounce (for arrows/scrolling indicators) -->
<div class="animate-bounce">
    ↓ Scroll down
</div>
```

### Custom Animations

**Definition:** For animations beyond the built-in set, you can define custom keyframes in `tailwind.config.js` or use arbitrary values (`animate-[wiggle_1s_ease-in-out_infinite]`). This allows you to create complex, brand-specific motion whilst still keeping styles co-located in your HTML.

**Add to tailwind.config.js:**
```javascript
module.exports = {
  theme: {
    extend: {
      animation: {
        'fade-in': 'fadeIn 0.5s ease-out',
        'slide-up': 'slideUp 0.5s ease-out',
        'wiggle': 'wiggle 1s ease-in-out infinite',
      },
      keyframes: {
        fadeIn: {
          '0%': { opacity: '0' },
          '100%': { opacity: '1' },
        },
        slideUp: {
          '0%': { transform: 'translateY(20px)', opacity: '0' },
          '100%': { transform: 'translateY(0)', opacity: '1' },
        },
        wiggle: {
          '0%, 100%': { transform: 'rotate(-3deg)' },
          '50%': { transform: 'rotate(3deg)' },
        },
      },
    },
  },
}
```

**Usage:**
```html
<div class="animate-fade-in">Fades in</div>
<div class="animate-slide-up">Slides up</div>
<div class="animate-wiggle">Continuous wiggle</div>
```

### Animation Examples

```html
<!-- Button with hover effects -->
<button class="bg-blue-500 text-white px-6 py-3 rounded-lg
               transition-all duration-300 ease-in-out
               hover:bg-blue-600 hover:scale-105 hover:shadow-lg
               active:scale-95">
    Hover Me
</button>

<!-- Card hover lift -->
<div class="bg-white rounded-xl shadow-md p-6
            transition-all duration-300
            hover:-translate-y-2 hover:shadow-xl">
    <h3>Card Title</h3>
    <p>Card content...</p>
</div>

<!-- Image zoom on hover -->
<div class="overflow-hidden rounded-lg">
    <img src="photo.jpg" 
         class="transition-transform duration-500 hover:scale-110">
</div>

<!-- Modal fade in -->
<div class="fixed inset-0 flex items-center justify-center
            transition-opacity duration-300"
     :class="show ? 'opacity-100' : 'opacity-0 pointer-events-none'">
    <div class="bg-white rounded-lg p-6 transform transition-transform duration-300"
         :class="show ? 'scale-100' : 'scale-95'">
        Modal content
    </div>
</div>

<!-- Staggered list animation -->
<ul>
    <li class="opacity-0 animate-[fadeIn_0.5s_ease-out_forwards]" style="animation-delay: 0.1s">Item 1</li>
    <li class="opacity-0 animate-[fadeIn_0.5s_ease-out_forwards]" style="animation-delay: 0.2s">Item 2</li>
    <li class="opacity-0 animate-[fadeIn_0.5s_ease-out_forwards]" style="animation-delay: 0.3s">Item 3</li>
</ul>
```

---

## 10. Building Components

**Definition:** Building Components demonstrates how to combine multiple Tailwind utility classes into reusable UI patterns like buttons, cards, navigation bars, forms, and modals. Components are created by composing utilities rather than writing custom CSS.

**Context:** While Tailwind is utility-first, you'll often reuse certain combinations. This section shows patterns for extracting components when appropriate—through framework components (React/Vue), template partials (Laravel), or carefully using @apply in CSS.

#### Component Composition Example

```
┌─────────────────────────────────────────────────────────────────┐
│              COMPONENT COMPOSITION PATTERN                      │
└─────────────────────────────────────────────────────────────────┘

  BUTTON COMPONENT BREAKDOWN
  ┌──────────────────────────────────────────────────────────────┐
  │                                                              │
  │  ┌─────────────────────────────────────────────────────────┐ │
  │  │                 BUTTON COMPONENT                        │ │
  │  │                                                         │ │
  │  │  Layout:     inline-flex items-center justify-center    │ │
  │  │                                                         │ │
  │  │  Spacing:    px-6 py-3                                  │ │
  │  │                                                         │ │
  │  │  Typography: font-semibold text-white                   │ │
  │  │                                                         │ │
  │  │  Visual:    bg-blue-600 rounded-lg shadow-md            │ │
  │  │                                                         │ │
  │  │  States:    hover:bg-blue-700 focus:ring-2              │ │
  │  │                                                         │ │
  │  │  Motion:    transition-all duration-200                 │ │
  │  │                                                         │ │
  │  └─────────────────────────────────────────────────────────┘ │
  │                                                              │
  │  RESULT: A reusable, accessible, interactive button          │
  │                                                              │
  └──────────────────────────────────────────────────────────────┘

  CARD COMPONENT LAYERS
  ┌──────────────────────────────────────────────────────────────┐
  │                                                              │
  │  Layer 1: Container                                          │
  │  ┌─────────────────────────────────────────────────────────┐ │
  │  │ bg-white rounded-xl shadow-lg overflow-hidden           │ │
  │  │                                                         │ │
  │  │ Layer 2: Image Section                                  │ │
  │  │ ┌─────────────────────────────────────────────────────┐ │ │
  │  │ │ w-full h-48 object-cover                            │ │ │
  │  │ │                                                     │ │ │
  │  │ │ [Image]                                             │ │ │
  │  │ └─────────────────────────────────────────────────────┘ │ │
  │  │                                                         │ │
  │  │ Layer 3: Content Section                                │ │
  │  │ ┌─────────────────────────────────────────────────────┐ │ │
  │  │ │ p-6                                                 │ │ │
  │  │ │                                                     │ │ │
  │  │ │ ┌───────────────────────────────────────────────┐   │ │ │
  │  │ │ │ Category (text-sm text-blue-600)              │   │ │ │
  │  │ │ └───────────────────────────────────────────────┘   │ │ │
  │  │ │ ┌───────────────────────────────────────────────┐   │ │ │
  │  │ │ │ Title (text-xl font-bold mt-2)                │   │ │ │
  │  │ │ └───────────────────────────────────────────────┘   │ │ │
  │  │ │ ┌───────────────────────────────────────────────┐   │ │ │
  │  │ │ │ Description (text-gray-600 mt-2)              │   │ │ │
  │  │ │ └───────────────────────────────────────────────┘   │ │ │
  │  │ │ ┌───────────────────────────────────────────────┐   │ │ │
  │  │ │ │ CTA Button (mt-4 inline-flex...)              │   │ │ │
  │  │ │ └───────────────────────────────────────────────┘   │ │ │
  │  │ └─────────────────────────────────────────────────────┘ │ │
  │  │                                                         │ │
  │  └─────────────────────────────────────────────────────────┘ │
  │                                                              │
  └──────────────────────────────────────────────────────────────┘

  WHEN TO EXTRACT COMPONENTS
  ┌──────────────────────────────────────────────────────────────┐
  │                                                              │
  │  ┌──────────────┐              ┌──────────────┐              │
  │  │  KEEP AS     │              │  EXTRACT TO  │              │
  │  │  UTILITIES   │              │  COMPONENT   │              │
  │  └──────┬───────┘              └──────┬───────┘              │
  │         │                             │                      │
  │  • Simple (<5 classes)         • Used 3+ times               │
  │  • Used 1-2 times              • Complex (>10 classes)       │
  │  • Style varies                • Needs internal logic         │
  │  • One-off designs             • Team consistency needed     │
  │         │                             │                      │
  │         ▼                             ▼                      │
  │  ┌──────────────┐              ┌──────────────┐              │
  │  │ Write in HTML│              │ Framework    │              │
  │  │ directly     │              │ Component    │              │
  │  │              │              │              │              │
  │  └──────────────┘              │ - React      │              │
  │                                │ - Vue        │              │
  │                                │ - Laravel    │              │
  │                                └──────────────┘              │
  │                                                              │
  └──────────────────────────────────────────────────────────────┘
```

### Buttons

**Definition:** Buttons are interactive elements that trigger actions. In Tailwind, buttons are built by combining utilities for spacing (`px-4 py-2`), background color (`bg-blue-500`), text color (`text-white`), border radius (`rounded`), and interactive states (`hover:bg-blue-600`, `focus:ring`). There is no `.btn` class — you compose the button style from scratch or extract it to a component.

```html
<!-- Primary button -->
<button class="bg-blue-600 hover:bg-blue-700 text-white font-semibold 
               py-2 px-4 rounded-lg transition-colors duration-200
               focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2">
    Primary Button
</button>

<!-- Secondary button -->
<button class="bg-white hover:bg-gray-50 text-gray-700 font-semibold 
               py-2 px-4 border border-gray-300 rounded-lg
               transition-colors duration-200
               focus:outline-none focus:ring-2 focus:ring-gray-500 focus:ring-offset-2">
    Secondary Button
</button>

<!-- Danger button -->
<button class="bg-red-600 hover:bg-red-700 text-white font-semibold 
               py-2 px-4 rounded-lg transition-colors duration-200
               focus:outline-none focus:ring-2 focus:ring-red-500 focus:ring-offset-2">
    Delete
</button>

<!-- Ghost button -->
<button class="text-gray-600 hover:text-gray-900 hover:bg-gray-100 
               font-medium py-2 px-4 rounded-lg transition-colors duration-200">
    Cancel
</button>

<!-- Icon button -->
<button class="inline-flex items-center justify-center p-2 rounded-full
               bg-blue-600 hover:bg-blue-700 text-white
               transition-colors duration-200">
    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"></path>
    </svg>
</button>

<!-- Button with icon and text -->
<button class="inline-flex items-center bg-blue-600 hover:bg-blue-700 
               text-white font-semibold py-2 px-4 rounded-lg
               transition-colors duration-200">
    <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"></path>
    </svg>
    Download
</button>

<!-- Disabled button -->
<button disabled class="bg-gray-300 text-gray-500 font-semibold 
                        py-2 px-4 rounded-lg cursor-not-allowed">
    Disabled
</button>

<!-- Loading button -->
<button disabled class="inline-flex items-center bg-blue-600 text-white 
                        font-semibold py-2 px-4 rounded-lg opacity-75 cursor-wait">
    <svg class="animate-spin -ml-1 mr-3 h-5 w-5 text-white" fill="none" viewBox="0 0 24 24">
        <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
        <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4z"></path>
    </svg>
    Loading...
</button>
```

### Cards

**Definition:** Cards are flexible containers used to group related information. A typical Tailwind card uses utilities for background (`bg-white`), shadow (`shadow-md`), border radius (`rounded-lg`), overflow handling (`overflow-hidden`), and padding. They often contain an image, a title, a description, and an action button.

```html
<!-- Basic card -->
<div class="bg-white rounded-lg shadow-md overflow-hidden">
    <div class="p-6">
        <h3 class="text-lg font-semibold text-gray-900 mb-2">Card Title</h3>
        <p class="text-gray-600">Card content goes here.</p>
    </div>
</div>

<!-- Card with image -->
<div class="bg-white rounded-xl shadow-lg overflow-hidden max-w-sm">
    <img src="card-image.jpg" alt="Card" class="w-full h-48 object-cover">
    <div class="p-6">
        <div class="text-sm text-blue-600 font-semibold mb-2">Category</div>
        <h3 class="text-xl font-bold text-gray-900 mb-2">Card Title</h3>
        <p class="text-gray-600 mb-4">
            This is a description of the card content.
        </p>
        <button class="text-blue-600 hover:text-blue-800 font-semibold">
            Read more →
        </button>
    </div>
</div>

<!-- Horizontal card -->
<div class="flex bg-white rounded-lg shadow-md overflow-hidden max-w-2xl">
    <img src="card-image.jpg" alt="Card" class="w-48 h-full object-cover">
    <div class="p-6 flex flex-col justify-between">
        <div>
            <h3 class="text-xl font-bold text-gray-900 mb-2">Card Title</h3>
            <p class="text-gray-600">Card description here.</p>
        </div>
        <div class="flex items-center mt-4">
            <span class="text-sm text-gray-500">5 min read</span>
            <button class="ml-auto text-blue-600 hover:text-blue-800 font-semibold">
                Learn more
            </button>
        </div>
    </div>
</div>

<!-- Pricing card -->
<div class="bg-white rounded-2xl shadow-xl border border-gray-200 p-8 max-w-sm">
    <div class="text-center">
        <h3 class="text-2xl font-bold text-gray-900">Pro Plan</h3>
        <div class="mt-4">
            <span class="text-5xl font-extrabold text-gray-900">$29</span>
            <span class="text-gray-500">/month</span>
        </div>
        <p class="mt-4 text-gray-600">Perfect for growing teams</p>
    </div>
    <ul class="mt-8 space-y-4">
        <li class="flex items-center">
            <svg class="w-5 h-5 text-green-500 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
            </svg>
            <span>Unlimited projects</span>
        </li>
        <li class="flex items-center">
            <svg class="w-5 h-5 text-green-500 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
            </svg>
            <span>Priority support</span>
        </li>
        <li class="flex items-center">
            <svg class="w-5 h-5 text-green-500 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
            </svg>
            <span>Advanced analytics</span>
        </li>
    </ul>
    <button class="w-full mt-8 bg-blue-600 hover:bg-blue-700 text-white font-semibold 
                   py-3 px-6 rounded-lg transition-colors duration-200">
        Get Started
    </button>
</div>
```

### Navigation Bars

**Definition:** Navigation bars guide users through the application. In Tailwind, navbars are typically built using a flex container (`flex`, `justify-between`, `items-center`) with a logo on one side and navigation links on the other. Responsive navbars often use a hidden menu on mobile (`hidden md:flex`) that toggles with JavaScript.

```html
<!-- Simple navbar -->
<nav class="bg-white shadow">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex justify-between h-16">
            <div class="flex items-center">
                <a href="#" class="text-xl font-bold text-gray-900">Logo</a>
            </div>
            <div class="flex items-center space-x-8">
                <a href="#" class="text-gray-600 hover:text-gray-900">Home</a>
                <a href="#" class="text-gray-600 hover:text-gray-900">About</a>
                <a href="#" class="text-gray-600 hover:text-gray-900">Contact</a>
            </div>
        </div>
    </div>
</nav>

<!-- Navbar with dropdown -->
<nav class="bg-gray-800">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex items-center justify-between h-16">
            <div class="flex items-center">
                <a href="#" class="text-white text-xl font-bold">Brand</a>
                <div class="hidden md:block ml-10">
                    <div class="flex items-baseline space-x-4">
                        <a href="#" class="bg-gray-900 text-white px-3 py-2 rounded-md text-sm font-medium">Dashboard</a>
                        <a href="#" class="text-gray-300 hover:bg-gray-700 hover:text-white px-3 py-2 rounded-md text-sm font-medium">Team</a>
                        <a href="#" class="text-gray-300 hover:bg-gray-700 hover:text-white px-3 py-2 rounded-md text-sm font-medium">Projects</a>
                    </div>
                </div>
            </div>
            <div class="hidden md:block">
                <div class="flex items-center">
                    <button class="bg-gray-800 p-1 rounded-full text-gray-400 hover:text-white">
                        <span class="sr-only">View notifications</span>
                        <svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9"></path>
                        </svg>
                    </button>
                </div>
            </div>
        </div>
    </div>
</nav>

<!-- Mobile-responsive navbar with hamburger -->
<nav class="bg-white shadow">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex justify-between h-16">
            <div class="flex items-center">
                <span class="text-xl font-bold">Logo</span>
            </div>
            <!-- Desktop menu -->
            <div class="hidden md:flex items-center space-x-8">
                <a href="#" class="text-gray-700 hover:text-gray-900">Home</a>
                <a href="#" class="text-gray-700 hover:text-gray-900">About</a>
                <a href="#" class="text-gray-700 hover:text-gray-900">Services</a>
                <a href="#" class="bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700">
                    Sign Up
                </a>
            </div>
            <!-- Mobile menu button -->
            <div class="flex items-center md:hidden">
                <button type="button" class="text-gray-700 hover:text-gray-900">
                    <svg class="h-6 w-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
                    </svg>
                </button>
            </div>
        </div>
    </div>
    <!-- Mobile menu -->
    <div class="md:hidden">
        <div class="px-2 pt-2 pb-3 space-y-1">
            <a href="#" class="block px-3 py-2 rounded-md text-base font-medium text-gray-700 hover:text-gray-900 hover:bg-gray-50">Home</a>
            <a href="#" class="block px-3 py-2 rounded-md text-base font-medium text-gray-700 hover:text-gray-900 hover:bg-gray-50">About</a>
            <a href="#" class="block px-3 py-2 rounded-md text-base font-medium text-gray-700 hover:text-gray-900 hover:bg-gray-50">Services</a>
        </div>
    </div>
</nav>
```

### Forms

**Definition:** Forms collect user input. Tailwind provides the `form-input`, `form-textarea`, etc. classes via the `@tailwindcss/forms` plugin to reset browser defaults, but you can also style inputs directly using border (`border-gray-300`), padding, and focus ring utilities (`focus:ring`, `focus:border-blue-500`).

```html
<!-- Basic form -->
<form class="space-y-6 max-w-md">
    <div>
        <label for="email" class="block text-sm font-medium text-gray-700">Email</label>
        <input type="email" id="email" name="email" 
               class="mt-1 block w-full rounded-md border-gray-300 shadow-sm
                      focus:border-blue-500 focus:ring-blue-500">
    </div>
    
    <div>
        <label for="password" class="block text-sm font-medium text-gray-700">Password</label>
        <input type="password" id="password" name="password"
               class="mt-1 block w-full rounded-md border-gray-300 shadow-sm
                      focus:border-blue-500 focus:ring-blue-500">
    </div>
    
    <button type="submit" 
            class="w-full flex justify-center py-2 px-4 border border-transparent 
                   rounded-md shadow-sm text-sm font-medium text-white 
                   bg-blue-600 hover:bg-blue-700 focus:outline-none 
                   focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">
        Sign in
    </button>
</form>

<!-- Form with floating labels -->
<div class="relative">
    <input type="text" id="floating" 
           class="block px-2.5 pb-2.5 pt-4 w-full text-sm text-gray-900 
                  bg-transparent rounded-lg border border-gray-300 
                  appearance-none focus:outline-none focus:ring-0 
                  focus:border-blue-600 peer" placeholder=" " />
    <label for="floating" 
           class="absolute text-sm text-gray-500 duration-300 
                  transform -translate-y-4 scale-75 top-2 z-10 origin-[0] 
                  bg-white px-2 peer-focus:px-2 peer-focus:text-blue-600 
                  peer-placeholder-shown:scale-100 peer-placeholder-shown:-translate-y-1/2 
                  peer-placeholder-shown:top-1/2 peer-focus:top-2 
                  peer-focus:scale-75 peer-focus:-translate-y-4 left-1">
        Floating label
    </label>
</div>

<!-- Select dropdown -->
<div>
    <label for="country" class="block text-sm font-medium text-gray-700">Country</label>
    <select id="country" name="country"
            class="mt-1 block w-full rounded-md border-gray-300 shadow-sm
                   focus:border-blue-500 focus:ring-blue-500">
        <option>United States</option>
        <option>Canada</option>
        <option>Mexico</option>
    </select>
</div>

<!-- Checkbox group -->
<div class="space-y-2">
    <div class="flex items-center">
        <input id="comments" name="comments" type="checkbox"
               class="h-4 w-4 rounded border-gray-300 text-blue-600 focus:ring-blue-500">
        <label for="comments" class="ml-2 block text-sm text-gray-900">Comments</label>
    </div>
    <div class="flex items-center">
        <input id="candidates" name="candidates" type="checkbox"
               class="h-4 w-4 rounded border-gray-300 text-blue-600 focus:ring-blue-500">
        <label for="candidates" class="ml-2 block text-sm text-gray-900">Candidates</label>
    </div>
</div>

<!-- Radio group -->
<div class="space-y-2">
    <div class="flex items-center">
        <input id="small" name="size" type="radio" value="small"
               class="h-4 w-4 border-gray-300 text-blue-600 focus:ring-blue-500">
        <label for="small" class="ml-2 block text-sm text-gray-900">Small</label>
    </div>
    <div class="flex items-center">
        <input id="medium" name="size" type="radio" value="medium"
               class="h-4 w-4 border-gray-300 text-blue-600 focus:ring-blue-500">
        <label for="medium" class="ml-2 block text-sm text-gray-900">Medium</label>
    </div>
</div>

<!-- File input -->
<div class="flex items-center justify-center w-full">
    <label for="dropzone-file" class="flex flex-col items-center justify-center w-full h-64 
                                        border-2 border-gray-300 border-dashed rounded-lg 
                                        cursor-pointer bg-gray-50 hover:bg-gray-100">
        <div class="flex flex-col items-center justify-center pt-5 pb-6">
            <svg class="w-10 h-10 mb-3 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"></path>
            </svg>
            <p class="mb-2 text-sm text-gray-500"><span class="font-semibold">Click to upload</span> or drag and drop</p>
            <p class="text-xs text-gray-500">SVG, PNG, JPG or GIF (MAX. 800x400px)</p>
        </div>
        <input id="dropzone-file" type="file" class="hidden" />
    </label>
</div>
```

### Modals

**Definition:** Modals are overlay dialogs that require user attention. A Tailwind modal consists of a backdrop (`fixed inset-0 bg-black/50`) and a centered content container (`absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2`). Managing `z-index` and accessibility (focus trapping) is critical when building custom modals.

```html
<!-- Modal overlay -->
<div class="fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full 
            flex items-center justify-center z-50">
    <!-- Modal content -->
    <div class="relative bg-white rounded-lg shadow-xl max-w-md w-full mx-4">
        <!-- Header -->
        <div class="flex items-center justify-between p-6 border-b">
            <h3 class="text-xl font-semibold text-gray-900">Modal Title</h3>
            <button class="text-gray-400 hover:text-gray-500">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
                </svg>
            </button>
        </div>
        
        <!-- Body -->
        <div class="p-6">
            <p class="text-gray-600">
                Are you sure you want to delete this item? 
                This action cannot be undone.
            </p>
        </div>
        
        <!-- Footer -->
        <div class="flex justify-end space-x-3 p-6 border-t bg-gray-50 rounded-b-lg">
            <button class="px-4 py-2 text-gray-700 bg-white border border-gray-300 
                           rounded-lg hover:bg-gray-50">
                Cancel
            </button>
            <button class="px-4 py-2 text-white bg-red-600 rounded-lg 
                           hover:bg-red-700">
                Delete
            </button>
        </div>
    </div>
</div>

<!-- Animated modal (with transitions) -->
<div class="fixed inset-0 z-50 overflow-y-auto" aria-labelledby="modal-title" role="dialog" aria-modal="true">
    <!-- Backdrop -->
    <div class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0">
        <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity" aria-hidden="true"></div>
        <span class="hidden sm:inline-block sm:align-middle sm:h-screen" aria-hidden="true">&#8203;</span>
        
        <!-- Modal panel -->
        <div class="inline-block align-bottom bg-white rounded-lg text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-lg sm:w-full">
            <div class="bg-white px-4 pt-5 pb-4 sm:p-6 sm:pb-4">
                <div class="sm:flex sm:items-start">
                    <div class="mx-auto flex-shrink-0 flex items-center justify-center h-12 w-12 rounded-full bg-red-100 sm:mx-0 sm:h-10 sm:w-10">
                        <svg class="h-6 w-6 text-red-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z"></path>
                        </svg>
                    </div>
                    <div class="mt-3 text-center sm:mt-0 sm:ml-4 sm:text-left">
                        <h3 class="text-lg leading-6 font-medium text-gray-900" id="modal-title">
                            Deactivate account
                        </h3>
                        <div class="mt-2">
                            <p class="text-sm text-gray-500">
                                Are you sure you want to deactivate your account? 
                                All of your data will be permanently removed.
                            </p>
                        </div>
                    </div>
                </div>
            </div>
            <div class="bg-gray-50 px-4 py-3 sm:px-6 sm:flex sm:flex-row-reverse">
                <button type="button" class="w-full inline-flex justify-center rounded-md border border-transparent shadow-sm px-4 py-2 bg-red-600 text-base font-medium text-white hover:bg-red-700 focus:outline-none sm:ml-3 sm:w-auto sm:text-sm">
                    Deactivate
                </button>
                <button type="button" class="mt-3 w-full inline-flex justify-center rounded-md border border-gray-300 shadow-sm px-4 py-2 bg-white text-base font-medium text-gray-700 hover:bg-gray-50 focus:outline-none sm:mt-0 sm:ml-3 sm:w-auto sm:text-sm">
                    Cancel
                </button>
            </div>
        </div>
    </div>
</div>
```

---

## 11. Customization

**Definition:** Customization allows you to extend Tailwind's default configuration to match your design system. This includes adding custom colors, fonts, spacing, breakpoints, animations, and creating your own utility classes or components.

**Context:** Tailwind's defaults are just a starting point. Most projects need to customize the theme to match brand colors, typography, spacing scales, and add project-specific utilities. The configuration file is the single source of truth for your design system.

#### Customization Config Hierarchy

```
┌─────────────────────────────────────────────────────────────────┐
│              TAILWIND CONFIG HIERARCHY                          │
└─────────────────────────────────────────────────────────────────┘

  CONFIGURATION STRUCTURE
  ┌──────────────────────────────────────────────────────────────┐
  │                                                              │
  │  module.exports = {                                          │
  │    content: ['./src/**/*.{html,js}'],  ← File paths to scan │
  │    theme: {                                                  │
  │      extend: {          ← Add customizations here          │
  │        colors: {        ← Colors                           │
  │          brand: {...}                                        │
  │        },                                                    │
  │        fontFamily: {    ← Typography                       │
  │          sans: [...]                                         │
  │        },                                                    │
  │        spacing: {       ← Spacing scale                    │
  │          '18': '4.5rem'                                      │
  │        },                                                    │
  │        animation: {     ← Animations                       │
  │          'fade-in': '...'                                    │
  │        },                                                    │
  │        boxShadow: {     │ Visual effects                    │
  │          'card': '...'                                       │
  │        },                                                    │
  │        borderRadius: {  └───────────────                     │
  │          '4xl': '2rem'                                       │
  │        }                                                     │
  │      }                                                       │
  │    },                                                        │
  │    plugins: [           ← Third-party plugins                │
  │      require('@tailwindcss/forms')                           │
  │    ]                                                         │
  │  }                                                           │
  │                                                              │
  └──────────────────────────────────────────────────────────────┘

  CUSTOMIZATION PRIORITY
  ┌──────────────────────────────────────────────────────────────┐
  │                                                              │
  │  Level 1: Tailwind Defaults                                  │
  │  ┌─────────────────────────────────────────────────────────┐ │
  │  │ • Default colors (slate, blue, red, etc.)               │ │
  │  │ • Default spacing scale (1 = 0.25rem)                   │ │
  │  │ • Default breakpoints (sm: 640px)                       │ │
  │  │ • Default fonts (system-ui, sans-serif)                 │ │
  │  └─────────────────────────────────────────────────────────┘ │
  │                            │                                 │
  │                            ▼                                 │
  │  Level 2: Theme Extend (ADDS to defaults)                    │
  │  ┌─────────────────────────────────────────────────────────┐ │
  │  │ theme: {                                                │ │
  │  │   extend: {                                             │ │
  │  │     colors: { brand: {...} }  ← Adds to colors         │ │
  │  │   }                                                     │ │
  │  │ }                                                       │ │
  │  └─────────────────────────────────────────────────────────┘ │
  │                            │                                 │
  │                            ▼                                 │
  │  Level 3: Theme Override (REPLACES defaults)                 │
  │  ┌─────────────────────────────────────────────────────────┐ │
  │  │ theme: {                                                │ │
  │  │   colors: {  ← Replaces ALL colors                     │ │
  │  │     primary: {...}                                      │ │
  │  │   }                                                     │ │
  │  │ }                                                       │ │
  │  └─────────────────────────────────────────────────────────┘ │
  │                            │                                 │
  │                            ▼                                 │
  │  Level 4: @layer utilities (CSS custom utilities)            │
  │  ┌─────────────────────────────────────────────────────────┐ │
  │  │ @layer utilities {                                      │ │
  │  │   .text-shadow {                                        │ │
  │  │     text-shadow: 0 2px 4px rgba(0,0,0,0.1);            │ │
  │  │   }                                                     │ │
  │  │ }                                                       │ │
  │  └─────────────────────────────────────────────────────────┘ │
  │                                                              │
  └──────────────────────────────────────────────────────────────┘

  CUSTOM DESIGN SYSTEM EXAMPLE
  ┌──────────────────────────────────────────────────────────────┐
  │                                                              │
  │  Colors:                                                     │
  │  ┌─────────┬─────────┬─────────┬─────────┬─────────┐        │
  │  │Primary  │Secondary│Success  │Warning  │Error    │        │
  │  │ 500     │ 500     │ 500     │ 500     │ 500     │        │
  │  │ ██████  │ ██████  │ ██████  │ ██████  │ ██████  │        │
  │  │ #3B82F6 │ #8B5CF6 │ #10B981 │ #F59E0B │ #EF4444 │        │
  │  └─────────┴─────────┴─────────┴─────────┴─────────┘        │
  │                                                              │
  │  Usage:                                                      │
  │  • bg-primary-500                                            │
  │  • text-secondary-600                                        │
  │  • border-success-400                                        │
  │  • ring-warning-500                                          │
  │  • shadow-error-500/50                                       │
  │                                                              │
  └──────────────────────────────────────────────────────────────┘
```

### Extending the Config

**Basic structure:**
```javascript
// tailwind.config.js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ['./src/**/*.{html,js}'],
  theme: {
    extend: {
      // Add customizations here
    },
  },
  plugins: [],
}
```

### Custom Colors

**Definition:** You can extend Tailwind's default color palette in `tailwind.config.js` under `theme.extend.colors`. This allows you to add brand-specific colors (e.g., `brand: '#ff5733'`) that automatically generate utilities like `bg-brand`, `text-brand`, and `border-brand`. Defining colors here ensures consistency across the entire project.

```javascript
module.exports = {
  theme: {
    extend: {
      colors: {
        // Single color
        'brand': '#3b82f6',
        
        // Color with shades (using CSS variables or direct values)
        'brand': {
          50: '#eff6ff',
          100: '#dbeafe',
          200: '#bfdbfe',
          300: '#93c5fd',
          400: '#60a5fa',
          500: '#3b82f6',
          600: '#2563eb',
          700: '#1d4ed8',
          800: '#1e40af',
          900: '#1e3a8a',
          950: '#172554',
        },
        
        // Using CSS variables
        'primary': 'rgb(var(--color-primary) / <alpha-value>)',
      },
    },
  },
}
```

**Usage:**
```html
<div class="bg-brand-500 text-brand-100">
    Custom brand colors
</div>
<div class="bg-primary text-primary/50">
    CSS variable colors
</div>
```

### Custom Fonts

**Definition:** Custom fonts are added in `tailwind.config.js` under `theme.extend.fontFamily`. You map a utility name (e.g., `sans`, `heading`) to an array of font family names. This allows you to use classes like `font-heading` to apply your custom typeface stack defined in the configuration.

```javascript
module.exports = {
  theme: {
    extend: {
      fontFamily: {
        'sans': ['Inter', 'system-ui', 'sans-serif'],
        'serif': ['Merriweather', 'serif'],
        'mono': ['Fira Code', 'monospace'],
        'display': ['Poppins', 'sans-serif'],
      },
    },
  },
}
```

**Load fonts in CSS/HTML:**
```html
<!-- Google Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Poppins:wght@600;700&display=swap" rel="stylesheet">
```

```css
/* @import in CSS */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');
```

**Usage:**
```html
<h1 class="font-display">Display Heading</h1>
<p class="font-sans">Body text</p>
<code class="font-mono">Code snippet</code>
```

### Custom Spacing

**Definition:** If the default spacing scale (0.25rem increments) doesn't fit your design system, you can extend it in `theme.extend.spacing`. Adding a key like `'128': '32rem'` generates utilities like `w-128`, `p-128`, and `m-128`. This is useful for large layouts or specific fixed-size elements.

```javascript
module.exports = {
  theme: {
    extend: {
      spacing: {
        '18': '4.5rem',     // 72px
        '88': '22rem',      // 352px
        '128': '32rem',     // 512px
      },
    },
  },
}
```

**Usage:**
```html
<div class="p-18">4.5rem padding</div>
<div class="w-88">22rem width</div>
<div class="h-128">32rem height</div>
```

### Custom Breakpoints

**Definition:** Tailwind's default breakpoints (`sm`, `md`, `lg`, `xl`, `2xl`) can be customized in `theme.screens`. You can change existing values, add new ones (e.g., `3xl`), or rename them completely. This controls when responsive variants like `md:text-center` activate.

```javascript
module.exports = {
  theme: {
    screens: {
      'xs': '475px',
      'sm': '640px',
      'md': '768px',
      'lg': '1024px',
      'xl': '1280px',
      '2xl': '1536px',
      // Custom breakpoints
      'tall': { 'raw': '(min-height: 800px)' },
    },
  },
}
```

### Custom Animations

**Definition:** You can define reusable custom animations in `theme.extend.keyframes` and `theme.extend.animation`. This allows you to create named animation utilities (e.g., `animate-wiggle`) that can be used just like the built-in ones, keeping your HTML clean and your animations consistent.

```javascript
module.exports = {
  theme: {
    extend: {
      animation: {
        'fade-in': 'fadeIn 0.5s ease-out',
        'fade-out': 'fadeOut 0.5s ease-out',
        'slide-up': 'slideUp 0.5s ease-out',
        'slide-down': 'slideDown 0.5s ease-out',
        'bounce-slight': 'bounceSlight 2s infinite',
      },
      keyframes: {
        fadeIn: {
          '0%': { opacity: '0' },
          '100%': { opacity: '1' },
        },
        fadeOut: {
          '0%': { opacity: '1' },
          '100%': { opacity: '0' },
        },
        slideUp: {
          '0%': { transform: 'translateY(20px)', opacity: '0' },
          '100%': { transform: 'translateY(0)', opacity: '1' },
        },
        slideDown: {
          '0%': { transform: 'translateY(-20px)', opacity: '0' },
          '100%': { transform: 'translateY(0)', opacity: '1' },
        },
        bounceSlight: {
          '0%, 100%': { transform: 'translateY(-5%)' },
          '50%': { transform: 'translateY(0)' },
        },
      },
    },
  },
}
```

### Custom Box Shadows

**Definition:** Custom shadows are defined in `theme.extend.boxShadow`. This allows you to implement specific elevation styles or glow effects that match your design system (e.g., `glow: '0 0 10px rgba(0, 255, 0, 0.5)'`). These become available as `shadow-glow`.

```javascript
module.exports = {
  theme: {
    extend: {
      boxShadow: {
        'card': '0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06)',
        'card-hover': '0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04)',
        'glow': '0 0 20px rgba(59, 130, 246, 0.5)',
        'inner-lg': 'inset 0 2px 4px 0 rgba(0, 0, 0, 0.06)',
      },
    },
  },
}
```

### Custom Border Radius

**Definition:** You can extend `theme.extend.borderRadius` to add custom radius values. For example, adding `4xl: '2rem'` creates `rounded-4xl`. This is useful for unique card shapes or ensuring border radius consistency with design requirements.

```javascript
module.exports = {
  theme: {
    extend: {
      borderRadius: {
        '4xl': '2rem',
        '5xl': '2.5rem',
      },
    },
  },
}
```

### Adding Utilities with @layer

```css
/* In your input.css file */
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer utilities {
  /* Custom utility classes */
  .text-shadow {
    text-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
  
  .text-shadow-lg {
    text-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  }
  
  .scrollbar-hide {
    -ms-overflow-style: none;
    scrollbar-width: none;
  }
  
  .scrollbar-hide::-webkit-scrollbar {
    display: none;
  }
}

@layer components {
  /* Reusable component classes */
  .btn {
    @apply px-4 py-2 rounded font-medium transition-colors duration-200;
  }
  
  .btn-primary {
    @apply btn bg-blue-600 text-white hover:bg-blue-700;
  }
  
  .btn-secondary {
    @apply btn bg-gray-200 text-gray-800 hover:bg-gray-300;
  }
  
  .card {
    @apply bg-white rounded-lg shadow-md overflow-hidden;
  }
}
```

### Custom Variants

**Definition:** Plugins allow you to register custom variants (pseudo-classes or media queries) that work like `hover:` or `md:`. For example, you can create a `landscape:` variant to target landscape orientation, or a `hocus:` variant that targets both hover and focus states.

```javascript
// tailwind.config.js
module.exports = {
  plugins: [
    function({ addVariant }) {
      // Add hocus variant (hover + focus)
      addVariant('hocus', ['&:hover', '&:focus'])
      
      // Add group-hocus variant
      addVariant('group-hocus', ['.group:hover &', '.group:focus &'])
      
      // Add optional variant (based on :optional pseudo-class)
      addVariant('optional', '&:optional')
      
      // Add peer-invalid variant
      addVariant('peer-invalid', ':merge(.peer):invalid ~ &')
    }
  ],
}
```

**Usage:**
```html
<button class="bg-blue-500 hocus:bg-blue-700">
    Hover or focus changes color
</button>
```

---

## 12. Plugins & Best Practices

**Definition:** Plugins extend Tailwind's functionality with pre-built components, form resets, typography styles, and more. Best practices include knowing when to use utilities vs components, organizing classes consistently, and optimizing for production builds.

**Context:** The Tailwind ecosystem offers powerful plugins that solve common problems. Following best practices ensures maintainable code, consistent styling across your team, and optimal performance in production.

**Key Concepts:**
- **Official Plugins**: Forms, Typography, Aspect Ratio, Container Queries
- **Community Plugins**: Scrollbar, Animated, DaisyUI
- **Component Extraction**: When and how to create reusable components
- **Class Organization**: Consistent ordering with Headwind
- **Performance**: Purging unused styles, optimization tips

### Official Plugins

**@tailwindcss/forms - Better form element styling:**
```bash
npm install -D @tailwindcss/forms
```

```javascript
// tailwind.config.js
module.exports = {
  plugins: [
    require('@tailwindcss/forms'),
  ],
}
```

**Benefits:**
- Resets form controls to a consistent base
- Makes form elements easy to override with utilities
- Works with checkboxes, radios, inputs, selects

**@tailwindcss/typography - Beautiful prose content:**
```bash
npm install -D @tailwindcss/typography
```

```javascript
// tailwind.config.js
module.exports = {
  plugins: [
    require('@tailwindcss/typography'),
  ],
}
```

```html
<!-- Usage -->
<article class="prose lg:prose-xl">
    <h1>Article Title</h1>
    <p>Your content here...</p>
    <!-- Automatically styled headings, paragraphs, lists, etc. -->
</article>

<!-- Dark mode support -->
<article class="prose dark:prose-invert">
    <!-- Works with dark mode -->
</article>
```

**@tailwindcss/aspect-ratio:**
```bash
npm install -D @tailwindcss/aspect-ratio
```

```html
<div class="aspect-w-16 aspect-h-9">
    <iframe src="..." class="w-full h-full"></iframe>
</div>
```

**@tailwindcss/container-queries:**
```bash
npm install -D @tailwindcss/container-queries
```

```html
<div class="@container">
    <div class="@md:text-lg @lg:text-xl">
        <!-- Responsive based on container, not viewport -->
    </div>
</div>
```

### Community Plugins (Popular)

```bash
# Tailwind Scrollbar
npm install -D tailwind-scrollbar

# Tailwind CSS Animated
npm install -D tailwindcss-animated

# DaisyUI (Component library)
npm install -D daisyui

# Tailwind Merge (for merging classes programmatically)
npm install tailwind-merge
```

### When to Extract Components

**Definition:** "Extraction" means moving repeated utility patterns into a reusable component (like a Vue/React component or a CSS class with `@apply`). You should extract components when a pattern is used in multiple places and updating it independently would be tedious. Don't extract prematurely — duplication is often better than the wrong abstraction.

**Use utility classes directly when:**
- Component is simple (< 5-7 classes)
- Used only 1-2 times
- Style varies between instances

**Extract to a component when:**
- Used 3+ times
- Complex styling (> 10 classes)
- Needs internal logic/state
- Team needs consistency

**Extraction methods:**

1. **@apply in CSS (limited use):**
```css
.btn-primary {
  @apply bg-blue-600 text-white px-4 py-2 rounded-lg 
         hover:bg-blue-700 transition-colors duration-200;
}
```

2. **Framework components (React/Vue/etc):**
```jsx
// Button.jsx
function Button({ children, variant = 'primary', ...props }) {
  const baseStyles = 'px-4 py-2 rounded-lg font-medium transition-colors duration-200';
  const variants = {
    primary: 'bg-blue-600 text-white hover:bg-blue-700',
    secondary: 'bg-gray-200 text-gray-800 hover:bg-gray-300',
    danger: 'bg-red-600 text-white hover:bg-red-700',
  };
  
  return (
    <button className={`${baseStyles} ${variants[variant]}`} {...props}>
      {children}
    </button>
  );
}
```

3. **Template partials (Laravel/Blade):**
```blade
{{-- components/button.blade.php --}}
@props(['variant' => 'primary'])

@php
$classes = match($variant) {
    'primary' => 'bg-blue-600 text-white hover:bg-blue-700',
    'secondary' => 'bg-gray-200 text-gray-800 hover:bg-gray-300',
    default => 'bg-blue-600 text-white hover:bg-blue-700',
};
@endphp

<button {{ $attributes->merge(['class' => "px-4 py-2 rounded-lg font-medium transition-colors duration-200 {$classes}"]) }}>
    {{ $slot }}
</button>
```

### Organizing Classes

**Use consistent ordering (Headwind extension helps):**

1. Layout (display, position, z-index)
2. Box model (width, height, margin, padding)
3. Background & borders
4. Typography
5. Visual effects (shadow, opacity)
6. Interactivity (cursor, user-select)
7. Transforms & animations
8. Responsive prefixes
9. State variants

**Example:**
```html
<div class="
    /* Layout */
    relative flex items-center
    /* Box Model */
    w-full h-12 px-4 py-2
    /* Background & Borders */
    bg-white border border-gray-300 rounded-lg
    /* Typography */
    text-sm text-gray-900 placeholder-gray-400
    /* Visual */
    shadow-sm
    /* Interactive */
    cursor-text
    /* States */
    focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500
    /* Responsive */
    md:w-96 md:text-base
">
```

**Or use one line for simpler elements:**
```html
<button class="bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 px-4 rounded-lg transition-colors duration-200">
    Click me
</button>
```

### Best Practices Summary

**DO:**
- Use mobile-first responsive design
- Leverage JIT (Just-In-Time) engine for arbitrary values
- Use @apply sparingly - prefer component extraction
- Configure your design system in tailwind.config.js
- Use the `prose` class for content-heavy areas
- Enable purging for production (automatic in v3+)
- Use VS Code extensions for autocomplete

**DON'T:**
- Use arbitrary values for frequently-used values
- Override base styles unnecessarily
- Mix Tailwind with heavy custom CSS
- Forget to configure `content` paths
- Use CDN in production
- Write CSS that fights against Tailwind

**Performance Tips:**
- Use the smallest color palette you need
- Remove unused configuration values
- Use `optimizeUniversalDefaults` for faster builds
- Consider using CSS variables for dynamic theming

---

## Quick Reference

### Common Class Combinations

**Definition:** Certain utility combinations appear frequently together, forming standard UI patterns. For example, `flex justify-center items-center` centers content, and `absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2` centers positioned elements. Recognizing these combinations speeds up development.

```html
<!-- Perfect centering -->
<div class="flex items-center justify-center min-h-screen">

<!-- Card shadow -->
<div class="bg-white rounded-lg shadow-md">

<!-- Button primary -->
<button class="bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 px-4 rounded-lg">

<!-- Input field -->
<input class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500">

<!-- Responsive grid -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">

<!-- Truncate text -->
<p class="truncate">

<!-- Aspect ratio container -->
<div class="aspect-video">

<!-- Glassmorphism -->
<div class="bg-white/10 backdrop-blur-md border border-white/20">
```

### Responsive Breakpoint Cheat Sheet

| Prefix | Min-Width | Description |
|--------|-----------|-------------|
| Default | 0px+ | Mobile (portrait) |
| `sm` | 640px+ | Large phones / small tablets |
| `md` | 768px+ | Tablets (iPad portrait) |
| `lg` | 1024px+ | Laptops / iPad landscape |
| `xl` | 1280px+ | Desktops |
| `2xl` | 1536px+ | Large Screens |


### Spacing Scale Reference

| Scale | Rem | Pixels |
|-------|-----|--------|
| `1` | 0.25rem | 4px |
| `2` | 0.5rem | 8px |
| `3` | 0.75rem | 12px |
| `4` | 1rem | 16px |
| `5` | 1.25rem | 20px |
| `6` | 1.5rem | 24px |
| `8` | 2rem | 32px |
| `10` | 2.5rem | 40px |
| `12` | 3rem | 48px |
| `16` | 4rem | 64px |
| `20` | 5rem | 80px |
| `24` | 6rem | 96px |
| `32` | 8rem | 128px |
| `40` | 10rem | 160px |
| `48` | 12rem | 192px |
| `64` | 16rem | 256px |


---

## Resources

- **Official Documentation:** https://tailwindcss.com/docs
- **Cheat Sheet:** https://tailwindcomponents.com/cheatsheet
- **Component Library:** https://tailwindui.com (official, paid)
- **Community Components:** https://tailwindcomponents.com
- **Color Generator:** https://tailwindcolor.com
- **Playground:** https://play.tailwindcss.com
- **VS Code Extension:** Tailwind CSS IntelliSense
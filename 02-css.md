# 🎨 CSS - Cascading Style Sheets

> CSS controls the presentation, layout, and styling of HTML documents. It separates content from design.

---

## 📊 CSS Architecture - UML Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                    CSS PROCESS FLOW                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  HTML Document ────→ Browser ────→ Rendered Page                │
│       │                                ▲                        │
│       │                                │                        │
│       ▼                                │                        │
│  ┌─────────────────────────────────┐   │                        │
│  │         CSS STYLESHEET          │   │                        │
│  ├─────────────────────────────────┤   │                        │
│  │  1. SELECTORS                   │   │                        │
│  │     ├─ Element (p, div)         │   │                        │
│  │     ├─ Class (.btn)             │───┤                        │
│  │     ├─ ID (#header)             │   │                        │
│  │     └─ Attribute ([type=text])  │   │                        │
│  │                                 │   │                        │
│  │  2. CASCADING ORDER             │   │                        │
│  │     ├─ Browser defaults         │   │                        │
│  │     ├─ External CSS             │   │                        │
│  │     ├─ Internal CSS             │   │                        │
│  │     ├─ Inline CSS               │   │                        │
│  │     └─ !important               │   │                        │
│  │                                 │   │                        │
│  │  3. BOX MODEL                   │   │                        │
│  │     ├─ Content                  │   │                        │
│  │     ├─ Padding                  │   │                        │
│  │     ├─ Border                   │   │                        │
│  │     └─ Margin                   │   │                        │
│  └─────────────────────────────────┘   │                        │
│                                         │                        │
└─────────────────────────────────────────────────────────────────┘
```

---

## 1. CSS Basics

### Definition
**CSS (Cascading Style Sheets)** is a stylesheet language used to describe the presentation of a document written in HTML. The term "cascading" refers to the priority scheme that determines which style rules apply when multiple rules target the same element.

### How CSS Works

**Definition:** CSS (Cascading Style Sheets) works by selecting HTML elements using selectors and applying style declarations (property: value pairs) to them. The browser parses CSS rules, resolves conflicts using the cascade (specificity + source order + inheritance), and applies the computed styles to build the visual render tree.

```
┌──────────────────────────────────────────────────────────────┐
│                   CSS WORKFLOW                               │
├──────────────────────────────────────────────────────────────┤
│                                                               │
│  Step 1: LOAD                                                │
│  ├─ Browser reads HTML                                       │
│  └─ Finds <link> or <style> tags                             │
│                                                               │
│  Step 2: PARSE                                               │
│  ├─ CSS rules parsed into selectors + declarations           │
│  └─ Specificity calculated for each rule                     │
│                                                               │
│  Step 3: MATCH                                               │
│  ├─ Selectors matched to DOM elements                        │
│  └─ Cascade determines which rule wins                       │
│                                                               │
│  Step 4: APPLY                                               │
│  ├─ Computed styles calculated                               │
│  └─ Visual rendering tree created                            │
│                                                               │
│  Step 5: RENDER                                              │
│  └─ Page painted to screen                                   │
│                                                               │
└──────────────────────────────────────────────────────────────┘
```

### Ways to Add CSS

**Definition:** CSS can be added to HTML in three ways: **inline** (via the `style` attribute directly on an element — highest specificity, hardest to maintain), **internal** (via a `<style>` block in the `<head>` — good for single pages), and **external** (via a linked `.css` file — best practice for maintainability and caching).

```html
<!-- 1. Inline CSS (avoid when possible) -->
<p style="color: red; font-size: 16px;">This is red text</p>

<!-- 2. Internal CSS (in <head>) -->
<head>
    <style>
        p {
            color: blue;
            font-size: 18px;
        }
    </style>
</head>

<!-- 3. External CSS (BEST PRACTICE) -->
<head>
    <link rel="stylesheet" href="styles.css">
</head>
```

### CSS Syntax

```
┌─────────────────────────────────────────────────────────┐
│                   CSS RULE STRUCTURE                     │
├─────────────────────────────────────────────────────────┤
│                                                          │
│   selector {                                             │
│       property: value;                                   │
│       ↓        ↓     ↓                                   │
│       │        │     └─ The value to apply              │
│       │        └─ The style aspect to change            │
│       └─ The element(s) to target                       │
│   }                                                      │
│                                                          │
│   Example:                                               │
│   h1 {                                                   │
│       color: blue;        ← Declaration                 │
│       font-size: 24px;    ← Declaration                 │
│   }                                                      │
│   ↑                                                      │
│   Selector                                               │
│                                                          │
└─────────────────────────────────────────────────────────┘
```

```css
/* Basic Structure */
selector {
    property: value;
    another-property: value;
}

/* Example */
h1 {
    color: blue;
    font-size: 24px;
    text-align: center;
}

/* Multiple selectors */
h1, h2, h3 {
    color: navy;
    font-family: Arial, sans-serif;
}

/* Class selector */
.btn {
    padding: 10px 20px;
    background-color: #007bff;
}

/* ID selector */
#header {
    background: #333;
    color: white;
}

/* Descendant selector */
nav ul li a {
    text-decoration: none;
}

/* Comments */
/* This is a CSS comment */
/* 
   Multi-line
   comment
*/
```

---

## 2. CSS Selectors

### Definition
**Selectors** are patterns used to select and style HTML elements. **Specificity** is the algorithm browsers use to determine which CSS rule takes precedence when multiple rules apply to the same element.

### Selector Types Diagram

```
SELECTOR HIERARCHY (Specificity)
│
├── Universal (*)
│   └── Specificity: (0,0,0,0)
│
├── Element (p, div, h1)
│   └── Specificity: (0,0,0,1)
│
├── Class (.btn), Attribute ([type]), Pseudo-class (:hover)
│   └── Specificity: (0,0,1,0)
│
├── ID (#header)
│   └── Specificity: (0,1,0,0)
│
├── Inline Style (style="")
│   └── Specificity: (1,0,0,0)
│
└── !important
    └── Overrides everything
```

### Basic Selectors

**Definition:** Basic CSS selectors are the fundamental patterns used to target HTML elements for styling. They include the universal selector (`*`), type/element selectors (`div`, `p`), class selectors (`.classname`), ID selectors (`#id`), and attribute selectors (`[attr]`). Each has a different specificity weight and use case.

```css
/* Universal selector - lowest specificity (0,0,0,0) */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

/* Element selector (0,0,0,1) */
p {
    line-height: 1.6;
}

/* Class selector (0,0,1,0) */
.highlight {
    background-color: yellow;
}

/* ID selector (0,1,0,0) */
#unique-element {
    border: 2px solid red;
}

/* Attribute selector */
input[type="text"] {
    border: 1px solid #ccc;
}

a[href^="https"] {   /* Starts with */
    color: green;
}

a[href$=".pdf"] {    /* Ends with */
    background: url(pdf-icon.png) no-repeat right;
}

a[href*="example"] { /* Contains */
    font-weight: bold;
}
```

### Combinator Selectors

**Definition:** Combinator selectors define relationships between elements. The descendant combinator (space) targets any nested descendant, the child combinator (`>`) targets only direct children, the adjacent sibling (`+`) targets the immediately following sibling, and the general sibling (`~`) targets all following siblings at the same level.

```
COMBINATOR TYPES
│
├── Descendant (space)
│   └── div p { }
│       Selects all <p> inside <div> at any level
│
├── Child (>)
│   └── ul > li { }
│       Selects only direct <li> children of <ul>
│
├── Adjacent Sibling (+)
│   └── h2 + p { }
│       Selects <p> immediately after <h2>
│
└── General Sibling (~)
    └── h2 ~ p { }
        Selects all <p> siblings after <h2>
```

```css
/* Descendant selector (space) */
article p {
    color: #333;  /* All paragraphs inside article */
}

/* Child selector (>) */
ul > li {
    list-style: disc;  /* Only direct children */
}

/* Adjacent sibling (+) */
h2 + p {
    margin-top: 0;  /* Paragraph immediately after h2 */
}

/* General sibling (~) */
h2 ~ p {
    color: #666;  /* All paragraphs after h2 (siblings) */
}

/* Grouping selector */
h1, h2, h3 {
    font-family: Georgia, serif;
}
```

### Pseudo-classes

```
PSEUDO-CLASSES CATEGORIES
│
├── State
│   ├── :hover - Mouse over
│   ├── :focus - Element focused
│   ├── :active - Being activated
│   ├── :visited - Visited link
│   └── :checked - Checked checkbox/radio
│
├── Structural
│   ├── :first-child - First child
│   ├── :last-child - Last child
│   ├── :nth-child(n) - nth child
│   ├── :nth-of-type(n) - nth of type
│   └── :only-child - Only child
│
├── Form
│   ├── :valid - Valid input
│   ├── :invalid - Invalid input
│   ├── :required - Required field
│   ├── :disabled - Disabled element
│   └── :placeholder-shown - Showing placeholder
│
└── Logical
    ├── :not() - Negation
    ├── :is() - Matching any
    └── :where() - Matching any (0 specificity)
```

```css
/* State pseudo-classes */
.btn:hover {
    background-color: #0056b3;
}

input:focus {
    outline: 2px solid blue;
    border-color: blue;
}

a:visited {
    color: purple;
}

button:active {
    transform: scale(0.98);
}

input:checked {
    background-color: green;
}

input:disabled {
    opacity: 0.5;
    cursor: not-allowed;
}

/* Structural pseudo-classes */
li:first-child {
    font-weight: bold;
}

li:last-child {
    border-bottom: none;
}

li:nth-child(odd) {
    background: #f5f5f5;
}

li:nth-child(even) {
    background: white;
}

li:nth-child(3n) {
    margin-right: 0;  /* Every 3rd item */
}

p:only-child {
    text-align: center;
}

/* Negation */
li:not(.exclude) {
    color: black;
}

/* Matching pseudo-classes */
:is(h1, h2, h3) span {
    color: blue;  /* Matches span inside any h1, h2, or h3 */
}

:where(h1, h2, h3) {
    margin-bottom: 1rem;  /* Same as :is but with 0 specificity */
}

/* Has selector (parent selector) */
article:has(img) {
    /* Articles that contain images */
    padding: 20px;
}

/* Form pseudo-classes */
input:valid {
    border-color: green;
}

input:invalid {
    border-color: red;
}

input:required {
    background: #fff3cd;
}

input:optional {
    background: white;
}
```

### Pseudo-elements

```
PSEUDO-ELEMENTS
│
├── Content Insertion
│   ├── ::before - Insert before element
│   └── ::after - Insert after element
│
├── Text Styling
│   ├── ::first-line - First line of text
│   ├── ::first-letter - First letter
│   └── ::selection - Selected text
│
├── Form Elements
│   └── ::placeholder - Input placeholder
│
└── Lists
    └── ::marker - List bullet/number
```

```css
/* ::before and ::after */
.quote::before {
    content: '"';
    font-size: 2em;
    color: #ccc;
}

.quote::after {
    content: '"';
    font-size: 2em;
    color: #ccc;
}

/* First line and first letter */
p::first-line {
    font-weight: bold;
}

p::first-letter {
    font-size: 3em;
    float: left;
    margin-right: 8px;
}

/* Placeholder */
input::placeholder {
    color: #999;
    font-style: italic;
}

/* Selection */
::selection {
    background: #007bff;
    color: white;
}

/* Marker (list bullets) */
li::marker {
    color: red;
    font-size: 1.2em;
}
```

---

## 3. Specificity & Cascade

### Definition
**Specificity** is the weight applied to CSS declarations based on the components of the selector. **Cascade** is the algorithm that determines which styles are applied when multiple rules could apply to an element.

### Specificity Calculation

**Definition:** Specificity is the algorithm browsers use to determine which CSS rule wins when multiple rules target the same element. It is calculated as a four-part score (inline, ID, class/attribute/pseudo-class, element/pseudo-element). Higher specificity always wins regardless of source order; equal specificity falls back to the last rule declared.

```
┌─────────────────────────────────────────────────────────────────┐
│              SPECIFICITY CALCULATION                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Format: (a, b, c, d)                                           │
│                                                                  │
│  a = Inline styles (1 or 0)                                     │
│  b = ID selectors                                               │
│  c = Class selectors, attribute selectors, pseudo-classes       │
│  d = Element selectors, pseudo-elements                         │
│                                                                  │
│  Examples:                                                      │
│  ├─ * {}                   = (0,0,0,0)                         │
│  ├─ p {}                   = (0,0,0,1)                         │
│  ├─ .class {}              = (0,0,1,0)                         │
│  ├─ #id {}                 = (0,1,0,0)                         │
│  ├─ #id .class p {}        = (0,1,1,1)                         │
│  └─ <p style="...">        = (1,0,0,0)                         │
│                                                                  │
│  Higher number wins!                                            │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

```css
/* Specificity: (0,0,0,1) */
p {
    color: black;
}

/* Specificity: (0,0,1,0) */
.text {
    color: blue;
}

/* Specificity: (0,1,0,0) */
#header {
    color: green;
}

/* Specificity: (0,1,1,1) */
#header .nav a:hover {
    color: red;
}

/* Specificity: (1,0,0,0) - Inline style wins */
/* <p style="color: purple;">Text</p> */
```

### The !important Rule

**Definition:** The `!important` declaration overrides all other specificity rules, forcing a style to apply regardless of any other competing rules. It should be used sparingly — only as a last resort (e.g., overriding third-party styles) — because it breaks the natural cascade and makes debugging and maintenance significantly harder.

```css
/* Use sparingly - overrides everything */
.text {
    color: red !important;
}

/* Cascade order (lowest to highest priority):
   1. User agent styles (browser defaults)
   2. User styles
   3. Author styles (your CSS)
   4. !important author styles
   5. !important user styles
*/
```

### Inheritance

**Definition:** CSS inheritance is the mechanism by which certain property values set on a parent element are automatically passed down to their child elements. Typography-related properties (color, font-family, font-size, line-height) are inherited by default, while box model properties (margin, padding, border, width) are not. The `inherit`, `initial`, and `unset` keywords give explicit control over inheritance.

```
┌─────────────────────────────────────────────────────────────────┐
│              CSS INHERITANCE                                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  INHERITED PROPERTIES                                            │
│  ├─ color                                                        │
│  ├─ font-family, font-size, font-weight                          │
│  ├─ line-height                                                  │
│  ├─ letter-spacing, word-spacing                                 │
│  ├─ text-align, text-indent                                      │
│  └─ visibility                                                   │
│                                                                  │
│  NOT INHERITED (must be set explicitly)                          │
│  ├─ background-color, background-image                           │
│  ├─ border, margin, padding                                      │
│  ├─ width, height                                                │
│  ├─ display, position                                            │
│  └─ float, clear                                                 │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

```css
/* Inherited properties (flow to children) */
body {
    font-family: Arial, sans-serif;  /* Inherited */
    color: #333;                      /* Inherited */
    line-height: 1.6;                 /* Inherited */
}

/* Non-inherited properties (must be set explicitly) */
.parent {
    border: 1px solid black;    /* NOT inherited */
    margin: 20px;               /* NOT inherited */
    padding: 10px;              /* NOT inherited */
    background: #f0f0f0;        /* NOT inherited */
}

/* Force inheritance */
.child {
    border: inherit;            /* Inherit from parent */
    color: inherit;
}

/* Inheritance keywords */
.element {
    color: inherit;     /* Use parent's value */
    color: initial;     /* Browser default */
    color: unset;       /* Inherit if inherited, otherwise initial */
    color: revert;      /* Roll back to previous cascade layer */
}
```

---

## 4. The Box Model

### Definition
The **Box Model** is a fundamental concept in CSS that describes how every HTML element is rendered as a rectangular box consisting of content, padding, border, and margin layers.

### Box Model Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                            MARGIN                               │
│                     (outside the border)                        │
│                     transparent space                           │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │                         BORDER                            │  │
│  │                  (surrounds padding)                      │  │
│  │  ┌─────────────────────────────────────────────────────┐  │  │
│  │  │                       PADDING                       │  │  │
│  │  │                (surrounds content)                  │  │  │
│  │  │  ┌───────────────────────────────────────────────┐  │  │  │
│  │  │  │                                               │  │  │  │
│  │  │  │                 CONTENT                       │  │  │  │
│  │  │  │            (text, images, etc.)               │  │  │  │
│  │  │  │                                               │  │  │  │
│  │  │  │     width × height                            │  │  │  │
│  │  │  │     (actual content size)                     │  │  │  │
│  │  │  │                                               │  │  │  │
│  │  │  └───────────────────────────────────────────────┘  │  │  │
│  │  └─────────────────────────────────────────────────────┘  │  │
│  └───────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘

Total Width = width + padding-left + padding-right + border-left + border-right + margin-left + margin-right

With box-sizing: border-box:
Total Width = width (includes padding and border) + margin
```

```css
/* Box Model Properties */
.box {
    /* Content dimensions */
    width: 300px;
    height: 200px;
    
    /* Padding (inside the border) */
    padding: 20px;                    /* All sides */
    padding: 10px 20px;               /* Vertical Horizontal */
    padding: 10px 20px 15px;          /* Top Horizontal Bottom */
    padding: 10px 20px 15px 25px;     /* Top Right Bottom Left */
    
    /* Individual padding */
    padding-top: 10px;
    padding-right: 20px;
    padding-bottom: 15px;
    padding-left: 25px;
    
    /* Border */
    border: 2px solid #333;           /* Shorthand */
    /* Or detailed: */
    border-width: 2px;
    border-style: solid;              /* solid, dashed, dotted, double, groove, ridge */
    border-color: #333;
    
    /* Individual borders */
    border-top: 1px solid red;
    border-right: 2px dashed blue;
    border-bottom: 3px dotted green;
    border-left: 4px double orange;
    
    /* Border radius */
    border-radius: 8px;               /* All corners */
    border-radius: 8px 16px;          /* Top-left/Bottom-right Top-right/Bottom-left */
    border-radius: 8px 16px 24px 32px; /* Individual corners */
    border-radius: 50%;               /* Circle (if square) */
    
    /* Margin (outside the border) */
    margin: 20px;                     /* All sides */
    margin: 20px auto;                /* Vertical Horizontal (auto centers) */
    
    /* Margin collapse: vertical margins collapse to the larger value */
}

/* Box Sizing */
.content-box {
    box-sizing: content-box;  /* Default: width/height = content only */
    width: 300px;             /* Content = 300px */
    padding: 20px;            /* Total width = 300 + 40 + 4 = 344px */
    border: 2px solid black;
}

.border-box {
    box-sizing: border-box;   /* width/height = content + padding + border */
    width: 300px;             /* Total = 300px */
    padding: 20px;            /* Content = 300 - 40 - 4 = 256px */
    border: 2px solid black;
}

/* Always use border-box */
*, *::before, *::after {
    box-sizing: border-box;
}
```

---

## 5. Colors & Backgrounds

### Definition
**Colors** in CSS can be specified using various formats (named, hex, RGB, HSL). **Backgrounds** include colors, images, gradients, and their positioning properties.

### Color System Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                    CSS COLOR FORMATS                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Named Colors          Hexadecimal                              │
│  ├─ red               ├─ #ff0000 (full red)                   │
│  ├─ blue              ├─ #f00 (shorthand)                     │
│  ├─ green             ├─ #ff000080 (with alpha)               │
│  └─ lightgray         └─ #ff0000ff (full opacity)             │
│                                                                 │
│  RGB / RGBA            HSL / HSLA                               │
│  ├─ rgb(255,0,0)      ├─ hsl(0,100%,50%)                    │
│  ├─ rgba(255,0,0,0.5) ├─ hsla(0,100%,50%,0.5)               │
│  └─ rgb(255 0 0 / 50%)└─ hsl(0 100% 50% / 80%)                  │
│                                                                 │
│  Modern (limited support)                                       │
│  ├─ oklch(63% 0.26 29)                                          │
│  └─ color(display-p3 1 0 0)                                     │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

```css
/* COLOR FORMATS */

/* Named colors */
.color1 {
    color: red;
    color: blue;
    color: lightgray;
}

/* Hexadecimal */
.color2 {
    color: #ff0000;       /* Red */
    color: #f00;          /* Shorthand */
    color: #ff000080;     /* With alpha (transparency) */
    color: #ff0000ff;     /* Full opacity */
}

/* RGB / RGBA */
.color3 {
    color: rgb(255, 0, 0);
    color: rgba(255, 0, 0, 0.5);  /* 50% transparent */
    color: rgb(255 0 0 / 50%);    /* Modern syntax */
}

/* HSL / HSLA (Hue, Saturation, Lightness) */
.color4 {
    color: hsl(0, 100%, 50%);      /* Red */
    color: hsla(120, 100%, 50%, 0.5);  /* Green, 50% transparent */
    color: hsl(200 100% 50% / 80%);    /* Modern syntax */
}

/* Modern color functions (limited browser support) */
.color5 {
    color: oklch(63% 0.26 29);     /* Perceptually uniform */
    color: color(display-p3 1 0 0);  /* Wide gamut */
}

/* Current color */
.element {
    color: blue;
    border: 2px solid currentColor;  /* Uses blue */
}

/* BACKGROUNDS */

/* Background color */
.bg1 {
    background-color: #f0f0f0;
    background-color: rgba(0, 0, 0, 0.5);
}

/* Background image */
.bg2 {
    background-image: url('background.jpg');
}

/* Multiple backgrounds */
.bg3 {
    background-image: 
        url('overlay.png'),
        linear-gradient(to right, #333, #666),
        url('pattern.png');
    background-position: center, top, bottom;
    background-repeat: no-repeat, repeat-x, repeat;
}

/* Background size */
.bg4 {
    background-size: cover;       /* Fill entire element, may crop */
    background-size: contain;     /* Fit within element, may letterbox */
    background-size: 100% 100%;   /* Stretch to fill */
    background-size: 500px 300px; /* Fixed size */
}

/* Background position */
.bg5 {
    background-position: center;
    background-position: top right;
    background-position: 50% 25%;
    background-position: 100px 50px;
}

/* Background repeat */
.bg6 {
    background-repeat: no-repeat;
    background-repeat: repeat-x;   /* Horizontal only */
    background-repeat: repeat-y;   /* Vertical only */
    background-repeat: space;      /* Space evenly */
    background-repeat: round;      /* Scale to fit */
}

/* Background attachment */
.bg7 {
    background-attachment: scroll;   /* Default: scrolls with content */
    background-attachment: fixed;    /* Fixed to viewport (parallax) */
    background-attachment: local;    /* Scrolls with element content */
}

/* Background shorthand */
.bg8 {
    background: #f0f0f0 url('image.jpg') no-repeat center/cover;
    /* Order: color image repeat position/size */
}

/* GRADIENTS */

/* Linear gradient */
.gradient1 {
    background: linear-gradient(to right, #ff6b6b, #4ecdc4);
    background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
    background: linear-gradient(to bottom right, red, yellow, green);
}

/* Radial gradient */
.gradient2 {
    background: radial-gradient(circle, #ff6b6b, #4ecdc4);
    background: radial-gradient(ellipse at top, red, blue);
    background: radial-gradient(circle closest-side, red, blue);
}

/* Conic gradient */
.gradient3 {
    background: conic-gradient(from 0deg, red, yellow, green, blue, red);
    background: conic-gradient(at 50% 50%, red 0deg, red 90deg, blue 90deg, blue 180deg);
}

/* Repeating gradients */
.gradient4 {
    background: repeating-linear-gradient(
        45deg,
        #606dbc,
        #606dbc 10px,
        #465298 10px,
        #465298 20px
    );
}
```

---

## 6. Typography

### Definition
**Typography** in CSS refers to the styling and arrangement of text to make it readable, appealing, and appropriate for its purpose.

### Typography System Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                  TYPOGRAPHY HIERARCHY                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Font Family                                                     │
│  ├─ serif (Times, Georgia)                                       │
│  ├─ sans-serif (Arial, Helvetica)                                │
│  ├─ monospace (Courier, monospace)                               │
│  └─ Custom (@font-face)                                          │
│                                                                  │
│  Font Properties                                                 │
│  ├─ font-size: 16px | 1rem | 1.2em                               │
│  ├─ font-weight: 400 (normal) | 700 (bold)                       │
│  ├─ font-style: normal | italic | oblique                        │
│  ├─ line-height: 1.5 | 150% | 24px                               │
│  └─ font-family: 'Custom', fallback                              │
│                                                                  │
│  Text Properties                                                 │
│  ├─ color: #333                                                  │
│  ├─ text-align: left | center | right | justify                  │
│  ├─ text-decoration: none | underline | line-through             │
│  ├─ text-transform: none | uppercase | lowercase | capitalize    │
│  ├─ letter-spacing: 0.5px                                        │
│  ├─ word-spacing: 2px                                            │
│  └─ text-shadow: 2px 2px 4px rgba(0,0,0,0.3)                     │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

```css
/* FONT FAMILY */
.text1 {
    /* Web-safe fonts */
    font-family: Arial, sans-serif;
    font-family: 'Times New Roman', serif;
    font-family: 'Courier New', monospace;
    
    /* System font stack (best performance) */
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 
                 'Helvetica Neue', Arial, sans-serif;
    
    /* Custom fonts (loaded via @font-face) */
    font-family: 'CustomFont', sans-serif;
}

/* Loading custom fonts */
@font-face {
    font-family: 'CustomFont';
    src: url('customfont.woff2') format('woff2'),
         url('customfont.woff') format('woff');
    font-weight: normal;
    font-style: normal;
    font-display: swap;  /* Show fallback font immediately, swap when loaded */
}

/* FONT SIZE */
.text2 {
    font-size: 16px;
    font-size: 1rem;        /* Relative to root font size */
    font-size: 1.2em;       /* Relative to parent font size */
    font-size: 100%;        /* Relative to parent */
    font-size: 2vw;         /* Relative to viewport width */
    font-size: 2vh;         /* Relative to viewport height */
    
    /* Responsive font size */
    font-size: clamp(1rem, 2.5vw, 2rem);
    /* Minimum: 1rem, Preferred: 2.5vw, Maximum: 2rem */
}

/* FONT WEIGHT */
.text3 {
    font-weight: 400;       /* Normal */
    font-weight: normal;
    font-weight: 700;       /* Bold */
    font-weight: bold;
    font-weight: 300;       /* Light */
    font-weight: 100;       /* Thin */
    font-weight: 900;       /* Black */
}

/* FONT STYLE */
.text4 {
    font-style: normal;
    font-style: italic;
    font-style: oblique;
}

/* LINE HEIGHT */
.text5 {
    line-height: 1.5;       /* Unitless (recommended) */
    line-height: 150%;      /* Percentage */
    line-height: 24px;      /* Fixed */
}

/* LETTER & WORD SPACING */
.text6 {
    letter-spacing: 0.5px;  /* Space between letters */
    letter-spacing: 2px;    /* Wider spacing */
    letter-spacing: -0.5px; /* Tighter spacing */
    
    word-spacing: 2px;      /* Space between words */
}

/* TEXT ALIGNMENT */
.text7 {
    text-align: left;       /* Default */
    text-align: right;
    text-align: center;
    text-align: justify;    /* Even spacing */
}

/* TEXT DECORATION */
.text8 {
    text-decoration: none;           /* Remove underline from links */
    text-decoration: underline;
    text-decoration: overline;
    text-decoration: line-through;   /* Strikethrough */
    
    text-decoration-color: red;
    text-decoration-style: dashed;   /* solid, double, dotted, dashed, wavy */
    text-decoration-thickness: 2px;
}

/* TEXT TRANSFORM */
.text9 {
    text-transform: uppercase;
    text-transform: lowercase;
    text-transform: capitalize;      /* First letter of each word */
    text-transform: none;
}

/* TEXT SHADOW */
.text10 {
    text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
    /* Horizontal offset, Vertical offset, Blur radius, Color */
    
    text-shadow: 
        1px 1px 2px red,
        0 0 1em blue,
        0 0 0.2em blue;
    /* Multiple shadows */
}

/* WHITE SPACE & TEXT OVERFLOW */
.text11 {
    white-space: normal;      /* Default: collapse whitespace */
    white-space: nowrap;      /* No wrapping */
    white-space: pre;         /* Preserve whitespace */
    white-space: pre-wrap;    /* Preserve whitespace, wrap lines */
    white-space: pre-line;    /* Collapse whitespace, preserve newlines */
    
    /* Truncation with ellipsis */
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}

/* WORD BREAK & HYPHENS */
.text12 {
    word-break: normal;
    word-break: break-all;        /* Break at any character */
    word-break: keep-all;         /* No breaks for CJK */
    
    overflow-wrap: break-word;    /* Break long words */
    
    hyphens: auto;                /* Automatic hyphenation */
    hyphens: manual;              /* Only at &shy; */
}

/* LIST STYLING */
ul {
    list-style-type: disc;        /* disc, circle, square, none */
    list-style-position: inside;  /* inside or outside */
    list-style-image: url('bullet.png');
    
    /* Shorthand */
    list-style: square inside;
}

ol {
    list-style-type: decimal;     /* decimal, decimal-leading-zero, 
                                     lower-roman, upper-roman, 
                                     lower-alpha, upper-alpha */
}
```

---

## 7. Flexbox Layout

### Definition
**Flexbox (Flexible Box Layout)** is a one-dimensional layout method designed for distributing space between items in an interface and providing powerful alignment capabilities.

### Flexbox Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                  FLEXBOX CONTAINER                               │
│                    display: flex;                                │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Main Axis (default: horizontal row)                            │
│  ←────────────────────────────────────────────→                 │
│                                                                  │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐            │
│  │  Flex   │  │  Flex   │  │  Flex   │  │  Flex   │            │
│  │  Item 1 │  │  Item 2 │  │  Item 3 │  │  Item 4 │            │
│  │ flex: 1 │  │ flex: 2 │  │ flex: 1 │  │ flex: 1 │            │
│  └─────────┘  └─────────┘  └─────────┘  └─────────┘            │
│                                                                  │
│  Cross Axis (default: vertical)                                 │
│  ↑                                                               │
│  │                                                               │
│  │  justify-content: center (main axis alignment)               │
│  │  align-items: center (cross axis alignment)                  │
│  │                                                               │
│  ↓                                                               │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

```css
/* FLEX CONTAINER */
.container {
    display: flex;
    /* or display: inline-flex; */
    
    /* Direction - main axis */
    flex-direction: row;           /* Default: left to right */
    flex-direction: row-reverse;   /* Right to left */
    flex-direction: column;        /* Top to bottom */
    flex-direction: column-reverse;/* Bottom to top */
    
    /* Wrapping */
    flex-wrap: nowrap;             /* Default: single line */
    flex-wrap: wrap;               /* Multiple lines */
    flex-wrap: wrap-reverse;       /* Multiple lines, reversed */
    
    /* Shorthand */
    flex-flow: row wrap;
    
    /* Justify content - alignment on main axis */
    justify-content: flex-start;   /* Default */
    justify-content: flex-end;
    justify-content: center;
    justify-content: space-between; /* Equal space between items */
    justify-content: space-around;  /* Equal space around items */
    justify-content: space-evenly;  /* Truly equal spacing */
    
    /* Align items - alignment on cross axis */
    align-items: stretch;          /* Default: fill container */
    align-items: flex-start;       /* Top */
    align-items: flex-end;         /* Bottom */
    align-items: center;           /* Center */
    align-items: baseline;         /* Text baseline */
    
    /* Align content - for multi-line containers */
    align-content: stretch;        /* Default */
    align-content: flex-start;
    align-content: flex-end;
    align-content: center;
    align-content: space-between;
    align-content: space-around;
    
    /* Gap between items */
    gap: 20px;                     /* Row and column gap */
    gap: 10px 20px;                /* Row gap, Column gap */
    row-gap: 10px;
    column-gap: 20px;
}

/* FLEX ITEMS */
.item {
    /* Grow factor - how much item grows relative to others */
    flex-grow: 0;                  /* Default: don't grow */
    flex-grow: 1;                  /* Grow to fill space */
    
    /* Shrink factor - how much item shrinks */
    flex-shrink: 1;                /* Default: shrink if needed */
    flex-shrink: 0;                /* Don't shrink */
    
    /* Basis size - starting size before grow/shrink */
    flex-basis: auto;              /* Default: content size */
    flex-basis: 200px;             /* Fixed starting size */
    flex-basis: 0;                 /* Start from 0 */
    
    /* Shorthand */
    flex: 1;                       /* Grow: 1, Shrink: 1, Basis: 0% */
    flex: 0 0 200px;               /* Don't grow, don't shrink, 200px basis */
    flex: 2 1 auto;                /* Grow twice as fast, shrink if needed */
    
    /* Align self - override container's align-items */
    align-self: auto;              /* Default: use container */
    align-self: flex-start;
    align-self: flex-end;
    align-self: center;
    align-self: stretch;
    align-self: baseline;
    
    /* Order - visual order (not DOM order) */
    order: 0;                      /* Default */
    order: -1;                     /* Move to beginning */
    order: 1;                      /* Move to end */
}

/* COMMON FLEXBOX PATTERNS */

/* Centering (horizontal and vertical) */
.center-container {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
}

/* Navigation */
.navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 2rem;
}

.nav-links {
    display: flex;
    gap: 2rem;
    list-style: none;
}

/* Card layout */
.card-container {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
}

.card {
    flex: 1 1 300px;  /* Grow, shrink, basis */
}

/* Sidebar layout */
.layout {
    display: flex;
    min-height: 100vh;
}

.sidebar {
    flex: 0 0 250px;  /* Fixed 250px, no grow/shrink */
}

.main-content {
    flex: 1;          /* Takes remaining space */
}

/* Sticky footer */
.page {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
}

.page-content {
    flex: 1;          /* Pushes footer down */
}

/* Equal height columns */
.equal-height {
    display: flex;
    align-items: stretch;  /* Default */
}

.equal-height > * {
    flex: 1;
}

/* Vertical alignment examples */
.vertical-layout {
    display: flex;
    flex-direction: column;
    gap: 1rem;
}

.vertical-layout .top {
    margin-bottom: auto;
}

.vertical-layout .bottom {
    margin-top: auto;
}
```

---

## 8. CSS Grid Layout

### Definition
**CSS Grid Layout** is a two-dimensional layout system for handling both rows and columns simultaneously, making it ideal for complex page layouts.

### Grid Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    CSS GRID CONTAINER                            │
│                     display: grid;                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│                        COLUMNS                                   │
│     1fr          2fr          1fr          1fr                  │
│  ┌──────────┬─────────────┬──────────┬──────────┐               │
│  │          │             │          │          │  ← Row 1      │
│  │  Item 1  │   Item 2    │  Item 3  │  Item 4  │               │
│  │          │             │          │          │               │
│  ├──────────┼─────────────┼──────────┼──────────┤               │
│  │          │             │          │          │  ← Row 2      │
│  │  Item 5  │   Item 6    │  Item 7  │  Item 8  │               │
│  │          │  (spans 2   │          │          │               │
│  │          │   columns)  │          │          │               │
│  └──────────┴─────────────┴──────────┴──────────┘               │
│                                                                  │
│  grid-template-columns: 1fr 2fr 1fr 1fr;                        │
│  grid-template-rows: auto auto;                                 │
│  gap: 20px;                                                     │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

```css
/* GRID CONTAINER */
.grid-container {
    display: grid;
    /* or display: inline-grid; */
    
    /* Define columns */
    grid-template-columns: 200px 200px 200px;  /* 3 fixed columns */
    grid-template-columns: 1fr 2fr 1fr;        /* Fractional units */
    grid-template-columns: repeat(3, 1fr);     /* 3 equal columns */
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); /* Responsive */
    grid-template-columns: 100px 1fr 2fr;      /* Fixed + flexible */
    
    /* Define rows */
    grid-template-rows: 100px auto 100px;      /* Auto adjusts to content */
    grid-template-rows: repeat(3, 1fr);        /* 3 equal rows */
    
    /* Gap */
    gap: 20px;                                 /* Row and column */
    gap: 10px 20px;                            /* Row, Column */
    row-gap: 10px;
    column-gap: 20px;
    
    /* Named areas */
    grid-template-areas:
        "header header header"
        "sidebar main main"
        "footer footer footer";
    
    /* Auto rows/columns for implicit grid */
    grid-auto-rows: 200px;                     /* Size of auto-generated rows */
    grid-auto-columns: 1fr;
    grid-auto-flow: row;                       /* row, column, dense */
    
    /* Justify items (inline axis - horizontal) */
    justify-items: stretch;                    /* Default: fill cell */
    justify-items: start;                      /* Left align */
    justify-items: end;                        /* Right align */
    justify-items: center;                     /* Center */
    
    /* Align items (block axis - vertical) */
    align-items: stretch;                      /* Default */
    align-items: start;                        /* Top align */
    align-items: end;                          /* Bottom align */
    align-items: center;                       /* Center */
    
    /* Shorthand for both */
    place-items: center;                       /* align justify */
    
    /* Justify content (entire grid within container) */
    justify-content: start;
    justify-content: end;
    justify-content: center;
    justify-content: space-between;
    justify-content: space-around;
    justify-content: space-evenly;
    
    /* Align content */
    align-content: start;
    align-content: center;
    align-content: space-between;
}

/* GRID ITEMS */
.grid-item {
    /* Position in grid */
    grid-column: 1 / 3;                        /* Start at 1, end before 3 */
    grid-column: 1 / span 2;                   /* Start at 1, span 2 columns */
    grid-column: span 2;                       /* Span 2 columns */
    grid-column: 1 / -1;                       /* From first to last */
    
    grid-row: 1 / 3;
    grid-row: span 2;
    
    /* Shorthand */
    grid-area: 1 / 1 / 3 / 4;                  /* row-start / col-start / row-end / col-end */
    
    /* Named areas */
    grid-area: header;
    grid-area: sidebar;
    
    /* Self alignment (override container) */
    justify-self: center;
    align-self: center;
    place-self: center center;                 /* Shorthand */
}

/* COMMON GRID PATTERNS */

/* Responsive card grid */
.card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 20px;
}

/* Holy grail layout */
.holy-grail {
    display: grid;
    grid-template-columns: 200px 1fr 200px;
    grid-template-rows: auto 1fr auto;
    grid-template-areas:
        "header header header"
        "nav main aside"
        "footer footer footer";
    min-height: 100vh;
}

.holy-grail header { grid-area: header; }
.holy-grail nav { grid-area: nav; }
.holy-grail main { grid-area: main; }
.holy-grail aside { grid-area: aside; }
.holy-grail footer { grid-area: footer; }

/* Masonry-like layout */
.masonry {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-auto-rows: 10px;                      /* Base row height */
    gap: 20px;
}

.masonry .item {
    grid-row: span 10;                        /* Each item spans 10 rows */
}

.masonry .item.tall {
    grid-row: span 20;                        /* Tall items span 20 rows */
}

/* Complex dashboard layout */
.dashboard {
    display: grid;
    grid-template-columns: 250px repeat(3, 1fr);
    grid-template-rows: 60px 1fr 1fr;
    gap: 20px;
    min-height: 100vh;
}

.dashboard .header {
    grid-column: 1 / -1;
}

.dashboard .sidebar {
    grid-row: 2 / -1;
}

.dashboard .widget {
    grid-column: span 1;
}

.dashboard .widget.large {
    grid-column: span 2;
}

/* Grid with overlapping items */
.overlay-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
}

.overlay-grid .background {
    grid-column: 1 / -1;
    grid-row: 1 / -1;
}

.overlay-grid .content {
    grid-column: 2;
    grid-row: 1;
    z-index: 1;
}
```

---

## 9. Responsive Design

### Definition
**Responsive Design** is an approach to web design that makes web pages render well on a variety of devices and window or screen sizes using flexible layouts, images, and media queries.

### Responsive Design Flow

```
┌─────────────────────────────────────────────────────────────────┐
│                RESPONSIVE DESIGN BREAKPOINTS                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Mobile First Approach (recommended)                             │
│                                                                  │
│  ┌────────────────────────────────────────────────────────┐    │
│  │  BASE STYLES (Mobile)                                  │    │
│  │  ├─ Single column layout                               │    │
│  │  ├─ Touch-friendly sizes                               │    │
│  │  └─ Simplified navigation                              │    │
│  └────────────────────────────────────────────────────────┘    │
│                              │                                   │
│                              ▼                                   │
│  ┌────────────────────────────────────────────────────────┐    │
│  │  @media (min-width: 768px) - Tablets                   │    │
│  │  ├─ Two column layout                                  │    │
│  │  ├─ Larger typography                                  │    │
│  │  └─ Side navigation                                    │    │
│  └────────────────────────────────────────────────────────┘    │
│                              │                                   │
│                              ▼                                   │
│  ┌────────────────────────────────────────────────────────┐    │
│  │  @media (min-width: 1024px) - Desktop                  │    │
│  │  ├─ Multi-column layout                                │    │
│  │  ├─ Full navigation                                    │    │
│  │  └─ Enhanced features                                  │    │
│  └────────────────────────────────────────────────────────┘    │
│                              │                                   │
│                              ▼                                   │
│  ┌────────────────────────────────────────────────────────┐    │
│  │  @media (min-width: 1440px) - Large Desktop            │    │
│  │  ├─ Max-width containers                               │    │
│  │  └─ Expanded layouts                                   │    │
│  └────────────────────────────────────────────────────────┘    │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

```css
/* MEDIA QUERIES */

/* Mobile-first approach (recommended) */
/* Base styles for mobile */
.container {
    padding: 1rem;
    width: 100%;
}

/* Tablet (768px and up) */
@media (min-width: 768px) {
    .container {
        padding: 2rem;
        max-width: 750px;
        margin: 0 auto;
    }
}

/* Desktop (1024px and up) */
@media (min-width: 1024px) {
    .container {
        max-width: 960px;
    }
}

/* Large desktop (1440px and up) */
@media (min-width: 1440px) {
    .container {
        max-width: 1400px;
    }
}

/* Multiple conditions */
@media (min-width: 768px) and (max-width: 1023px) {
    /* Only tablets */
}

@media screen and (orientation: landscape) {
    /* Landscape orientation */
}

@media (min-width: 768px) and (orientation: landscape) {
    /* Tablets in landscape */
}

/* Common breakpoints */
/* 
   320px  - Mobile small
   480px  - Mobile large
   768px  - Tablet
   1024px - Desktop
   1200px - Large desktop
   1440px - Extra large
*/

/* RESPONSIVE UNITS */

### CSS Units Reference

| Unit | Type | Description |
|------|------|-------------|
| `px` | Absolute | Pixels (fixed size) |
| `em` | Relative | Relative to parent element's font-size |
| `rem` | Relative | Relative to root (`html`) element's font-size |
| `vw` / `vh` | Viewport | 1% of viewport width / height |
| `dvh` / `svh` / `lvh` | Viewport | Dynamic, Small, Large viewport height (handles mobile UI) |
| `%` | Relative | Percentage of parent element's size |
| `clamp()` | Function | `clamp(min, preferred, max)` - Smart scaling |

/* Relative units */
.responsive {
    font-size: 1rem;        /* Relative to root (html) font-size */
    font-size: 1em;         /* Relative to parent font-size */
    padding: 1.5rem;
    margin: 2em;
    
    width: 50%;             /* Percentage of parent */
    width: 50vw;            /* Viewport width */
    height: 50vh;           /* Viewport height */
    
    /* New viewport units */
    height: 100dvh;         /* Dynamic viewport height (accounts for mobile browser chrome) */
    height: 100svh;         /* Small viewport height */
    height: 100lvh;         /* Large viewport height */
    
    /* Min/max */
    font-size: clamp(1rem, 2.5vw, 2rem);
    /* clamp(minimum, preferred, maximum) */
}

/* Responsive typography */
html {
    font-size: 16px;
}

@media (min-width: 768px) {
    html {
        font-size: 18px;
    }
}

@media (min-width: 1200px) {
    html {
        font-size: 20px;
    }
}

/* Fluid typography */
h1 {
    font-size: clamp(1.5rem, 5vw, 3rem);
}

/* RESPONSIVE IMAGES */
img {
    max-width: 100%;
    height: auto;
    display: block;  /* Remove extra space below image */
}

/* Object fit for images */
.image-container {
    width: 100%;
    aspect-ratio: 16 / 9;
}

.image-container img {
    width: 100%;
    height: 100%;
    object-fit: cover;       /* Fill container, may crop */
    object-fit: contain;     /* Show full image, may letterbox */
    object-position: center; /* Position within container */
}

/* RESPONSIVE TABLES */
@media (max-width: 768px) {
    .responsive-table {
        display: block;
        overflow-x: auto;
        white-space: nowrap;
    }
}

/* Alternative responsive table */
@media (max-width: 768px) {
    .stacked-table thead {
        display: none;
    }
    
    .stacked-table tr {
        display: block;
        margin-bottom: 1rem;
        border: 1px solid #ddd;
    }
    
    .stacked-table td {
        display: block;
        text-align: right;
        padding: 0.5rem;
    }
    
    .stacked-table td::before {
        content: attr(data-label);
        float: left;
        font-weight: bold;
    }
}

/* CONTAINER QUERIES */

/* Define container */
.card-container {
    container-type: inline-size;
    container-name: card;
}

/* Query based on container size */
@container card (min-width: 400px) {
    .card {
        display: flex;
        flex-direction: row;
    }
    
    .card img {
        width: 40%;
    }
}

@container card (min-width: 600px) {
    .card {
        display: grid;
        grid-template-columns: 1fr 2fr;
    }
}

/* ASPECT RATIO */
.video-container {
    aspect-ratio: 16 / 9;
    background: #000;
}

.square {
    aspect-ratio: 1 / 1;
}

/* PREFERS REDUCED MOTION */
@media (prefers-reduced-motion: reduce) {
    *, *::before, *::after {
        animation-duration: 0.01ms !important;
        animation-iteration-count: 1 !important;
        transition-duration: 0.01ms !important;
    }
}

/* DARK MODE */
@media (prefers-color-scheme: dark) {
    :root {
        --bg-color: #1a1a1a;
        --text-color: #ffffff;
    }
}

/* PRINT STYLES */
@media print {
    .no-print {
        display: none !important;
    }
    
    body {
        font-size: 12pt;
        line-height: 1.5;
    }
    
    a[href]::after {
        content: " (" attr(href) ")";
    }
}
```

---

## 10. Transitions & Animations

### Definition
**Transitions** provide a way to control animation speed when changing CSS properties. **Animations** allow more complex, multi-step animations with keyframes.

### Animation Types Comparison

```
┌─────────────────────────────────────────────────────────────────┐
│          TRANSITIONS vs ANIMATIONS                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  TRANSITIONS                                                     │
│  ├─ Simple A to B changes                                        │
│  ├─ Triggered by state changes (:hover, :focus)                  │
│  ├─ Two states only (start/end)                                  │
│  ├─ Easier to implement                                          │
│  └─ Example: Button hover color change                           │
│                                                                  │
│  ANIMATIONS                                                      │
│  ├─ Complex multi-step animations                                │
│  ├─ Can run automatically (no trigger needed)                    │
│  ├─ Multiple keyframes (@keyframes)                              │
│  ├─ More control (delay, iteration, direction)                   │
│  └─ Example: Loading spinner, complex entrance effects           │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

```css
/* TRANSITIONS */

/* Basic transition */
.button {
    background-color: #007bff;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    
    /* Transition properties */
    transition-property: background-color, transform;
    transition-duration: 0.3s;
    transition-timing-function: ease-in-out;
    transition-delay: 0.1s;
    
    /* Shorthand */
    transition: background-color 0.3s ease, transform 0.2s ease-in-out;
    
    /* All properties */
    transition: all 0.3s ease;
}

.button:hover {
    background-color: #0056b3;
    transform: scale(1.05);
}

/* Timing functions */
.timing-examples {
    transition-timing-function: ease;         /* Default: slow start, fast, slow end */
    transition-timing-function: ease-in;      /* Slow start */
    transition-timing-function: ease-out;     /* Slow end */
    transition-timing-function: ease-in-out;  /* Slow start and end */
    transition-timing-function: linear;       /* Constant speed */
    transition-timing-function: cubic-bezier(0.68, -0.55, 0.265, 1.55); /* Custom bounce */
}

/* Steps for frame-based animation */
.step-animation {
    transition-timing-function: steps(5, end);
}

/* What can be transitioned */
.transitionable {
    transition: 
        color, background-color, border-color, 
        width, height, transform, opacity, 
        margin, padding, font-size;
    /* Cannot transition: display, visibility, position */
}

/* ANIMATIONS */

/* Define keyframes */
@keyframes slideIn {
    from {
        opacity: 0;
        transform: translateX(-100%);
    }
    to {
        opacity: 1;
        transform: translateX(0);
    }
}

@keyframes pulse {
    0%, 100% {
        transform: scale(1);
    }
    50% {
        transform: scale(1.1);
    }
}

@keyframes rotate {
    from {
        transform: rotate(0deg);
    }
    to {
        transform: rotate(360deg);
    }
}

@keyframes bounce {
    0%, 20%, 50%, 80%, 100% {
        transform: translateY(0);
    }
    40% {
        transform: translateY(-30px);
    }
    60% {
        transform: translateY(-15px);
    }
}

@keyframes fadeInUp {
    from {
        opacity: 0;
        transform: translateY(20px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

@keyframes shake {
    0%, 100% { transform: translateX(0); }
    10%, 30%, 50%, 70%, 90% { transform: translateX(-5px); }
    20%, 40%, 60%, 80% { transform: translateX(5px); }
}

/* Apply animation */
.animated-element {
    animation-name: slideIn;
    animation-duration: 1s;
    animation-timing-function: ease-out;
    animation-delay: 0.5s;
    animation-iteration-count: 1;           /* or infinite */
    animation-direction: normal;            /* or reverse, alternate */
    animation-fill-mode: forwards;          /* Keep final state */
    animation-play-state: running;          /* or paused */
    
    /* Shorthand */
    animation: slideIn 1s ease-out 0.5s forwards;
}

/* Multiple animations */
.double-animation {
    animation: 
        fadeInUp 0.5s ease-out,
        pulse 2s ease-in-out 0.5s infinite;
}

/* Infinite animations */
.spinner {
    animation: rotate 2s linear infinite;
}

/* Pause on hover */
.animation-pause:hover {
    animation-play-state: paused;
}

/* TRANSFORMS */

/* Translate (move) */
.transform-translate {
    transform: translateX(50px);     /* Move right 50px */
    transform: translateY(-20px);    /* Move up 20px */
    transform: translate(50px, -20px); /* Move right and up */
    transform: translate3d(50px, -20px, 0); /* Hardware accelerated */
}

/* Scale */
.transform-scale {
    transform: scale(1.5);           /* 1.5x larger */
    transform: scale(0.5);           /* Half size */
    transform: scaleX(2);            /* Wider */
    transform: scaleY(0.5);          /* Shorter */
}

/* Rotate */
.transform-rotate {
    transform: rotate(45deg);        /* 45 degrees clockwise */
    transform: rotate(-90deg);       /* 90 degrees counter-clockwise */
    transform: rotate(1turn);        /* One full rotation */
}

/* Skew */
.transform-skew {
    transform: skewX(10deg);
    transform: skewY(-5deg);
    transform: skew(10deg, -5deg);
}

/* Multiple transforms */
.transform-multiple {
    transform: translateX(50px) rotate(45deg) scale(1.2);
}

/* Transform origin */
.transform-origin {
    transform-origin: top left;      /* Default: center center */
    transform-origin: 50% 50%;       /* Percentages */
    transform-origin: 100px 50px;    /* Pixels */
}

/* 3D Transforms */
.card-3d {
    perspective: 1000px;             /* Depth perspective */
}

.card-3d-inner {
    transform-style: preserve-3d;
    transition: transform 0.6s;
}

.card-3d:hover .card-3d-inner {
    transform: rotateY(180deg);
}

/* Performance optimization */
.gpu-accelerated {
    transform: translateZ(0);        /* Forces GPU acceleration */
    will-change: transform;          /* Hint for browser optimization */
}
```

---

## 11. CSS Variables (Custom Properties)

### Definition
**CSS Variables** (Custom Properties) are entities defined by CSS authors that contain specific values to be reused throughout a document, enabling theming and easier maintenance.

### Variable Scope Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                  CSS VARIABLE SCOPE                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  :root (Global Scope)                                           │
│  ├─ --color-primary: #007bff;                                   │
│  ├─ --font-size-base: 1rem;                                     │
│  └─ --spacing-unit: 1rem;                                       │
│         │                                                        │
│         ▼                                                        │
│  ┌─────────────────────────────────────────────────────────┐    │
│  │  .card (Component Scope)                                │    │
│  │  ├─ --card-padding: 2rem;                               │    │
│  │  ├─ --card-bg: #ffffff;                                 │    │
│  │  │                                                      │    │
│  │  │  Uses: var(--color-primary)                         │    │
│  │  │       var(--card-padding)                           │    │
│  │  │                                                      │    │
│  │  └─ ┌─────────────────────────────────────────────┐    │    │
│  │     │  .card-header (Nested Scope)               │    │    │
│  │     │  ├─ Can access all parent variables         │    │    │
│  │     │  └─ Can define new local variables          │    │    │
│  │     └─────────────────────────────────────────────┘    │    │
│  └─────────────────────────────────────────────────────────┘    │
│                                                                  │
│  Fallback: var(--undefined-var, default-value)                  │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

```css
/* Define in :root for global scope */
:root {
    /* Colors */
    --color-primary: #007bff;
    --color-primary-dark: #0056b3;
    --color-secondary: #6c757d;
    --color-success: #28a745;
    --color-danger: #dc3545;
    --color-warning: #ffc107;
    --color-info: #17a2b8;
    
    /* Neutral colors */
    --color-white: #ffffff;
    --color-gray-100: #f8f9fa;
    --color-gray-200: #e9ecef;
    --color-gray-300: #dee2e6;
    --color-gray-400: #ced4da;
    --color-gray-500: #adb5bd;
    --color-gray-600: #6c757d;
    --color-gray-700: #495057;
    --color-gray-800: #343a40;
    --color-gray-900: #212529;
    --color-black: #000000;
    
    /* Typography */
    --font-family-sans: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    --font-family-serif: Georgia, 'Times New Roman', serif;
    --font-family-mono: 'Courier New', monospace;
    
    --font-size-xs: 0.75rem;
    --font-size-sm: 0.875rem;
    --font-size-base: 1rem;
    --font-size-lg: 1.125rem;
    --font-size-xl: 1.25rem;
    --font-size-2xl: 1.5rem;
    --font-size-3xl: 1.875rem;
    --font-size-4xl: 2.25rem;
    
    --line-height-tight: 1.25;
    --line-height-normal: 1.5;
    --line-height-relaxed: 1.75;
    
    /* Spacing */
    --spacing-0: 0;
    --spacing-1: 0.25rem;   /* 4px */
    --spacing-2: 0.5rem;    /* 8px */
    --spacing-3: 0.75rem;   /* 12px */
    --spacing-4: 1rem;      /* 16px */
    --spacing-5: 1.25rem;   /* 20px */
    --spacing-6: 1.5rem;    /* 24px */
    --spacing-8: 2rem;      /* 32px */
    --spacing-10: 2.5rem;   /* 40px */
    --spacing-12: 3rem;     /* 48px */
    --spacing-16: 4rem;     /* 64px */
    --spacing-20: 5rem;     /* 80px */
    --spacing-24: 6rem;     /* 96px */
    
    /* Border radius */
    --radius-none: 0;
    --radius-sm: 0.125rem;
    --radius-md: 0.375rem;
    --radius-lg: 0.5rem;
    --radius-xl: 0.75rem;
    --radius-2xl: 1rem;
    --radius-full: 9999px;
    
    /* Shadows */
    --shadow-sm: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
    --shadow-md: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
    --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
    --shadow-xl: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
    
    /* Transitions */
    --transition-fast: 150ms ease;
    --transition-base: 300ms ease;
    --transition-slow: 500ms ease;
    
    /* Z-index scale */
    --z-dropdown: 1000;
    --z-sticky: 1020;
    --z-fixed: 1030;
    --z-modal-backdrop: 1040;
    --z-modal: 1050;
    --z-popover: 1060;
    --z-tooltip: 1070;
}

/* Use variables */
body {
    font-family: var(--font-family-sans);
    font-size: var(--font-size-base);
    line-height: var(--line-height-normal);
    color: var(--color-gray-800);
    background-color: var(--color-white);
}

.button {
    padding: var(--spacing-2) var(--spacing-4);
    background-color: var(--color-primary);
    color: var(--color-white);
    border: none;
    border-radius: var(--radius-md);
    font-size: var(--font-size-base);
    box-shadow: var(--shadow-sm);
    transition: all var(--transition-fast);
}

.button:hover {
    background-color: var(--color-primary-dark);
    box-shadow: var(--shadow-md);
}

/* Scoped variables */
.card {
    --card-padding: var(--spacing-6);
    --card-bg: var(--color-white);
    --card-border: 1px solid var(--color-gray-200);
    
    padding: var(--card-padding);
    background: var(--card-bg);
    border: var(--card-border);
    border-radius: var(--radius-lg);
    box-shadow: var(--shadow-md);
}

.card.compact {
    --card-padding: var(--spacing-4);  /* Override for compact variant */
}

/* Fallback values */
.element {
    color: var(--custom-color, blue);  /* Use blue if --custom-color not defined */
}

/* Dynamic variables with JavaScript */
/* JS: element.style.setProperty('--theme-color', '#ff0000'); */
.themed {
    background: var(--theme-color, var(--color-primary));
}

/* Dark mode with variables */
@media (prefers-color-scheme: dark) {
    :root {
        --color-background: var(--color-gray-900);
        --color-text: var(--color-gray-100);
        --color-border: var(--color-gray-700);
    }
}

/* Component theming */
[data-theme="dark"] {
    --color-background: #1a1a1a;
    --color-text: #ffffff;
}
```

---

## 12. CSS Best Practices

### Definition
**CSS Best Practices** are guidelines that promote maintainable, scalable, and performant stylesheets. They cover naming conventions, code organization, specificity management, and performance considerations that help teams write consistent CSS that is easy to understand, extend, and debug over time.

### DO's ✅
- Use semantic class names (`.button-primary` not `.blue-btn`)
- Organize CSS logically (components, utilities, base)
- Use CSS variables for theming
- Mobile-first responsive design
- Comment complex sections
- Use `rem` for font sizes, `em` for component-relative spacing
- Minimize specificity wars
- Test across browsers

### DON'Ts ❌
- Don't use `!important` unless absolutely necessary
- Don't over-qualify selectors (`div.container` vs `.container`)
- Don't use IDs for styling (high specificity)
- Don't nest selectors too deeply (max 3 levels)
- Don't use inline styles
- Don't repeat yourself (DRY principle)

### CSS Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    CSS ARCHITECTURE                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  1. RESET/NORMALIZE                                              │
│     ├─ Remove browser defaults                                   │
│     └─ Consistent baseline                                       │
│                                                                  │
│  2. BASE/GLOBAL                                                  │
│     ├─ Root font sizes                                           │
│     ├─ Body typography                                           │
│     └─ CSS variables                                             │
│                                                                  │
│  3. LAYOUT                                                       │
│     ├─ Container                                                 │
│     ├─ Grid systems                                              │
│     └─ Helper classes                                            │
│                                                                  │
│  4. COMPONENTS                                                   │
│     ├─ Button                                                    │
│     ├─ Card                                                      │
│     ├─ Modal                                                     │
│     └─ Navigation                                                │
│                                                                  │
│  5. UTILITIES                                                    │
│     ├─ Text alignment                                            │
│     ├─ Display utilities                                         │
│     ├─ Spacing                                                   │
│     └─ Visibility                                                │
│                                                                  │
│  6. THEMES/STATES                                                │
│     ├─ Dark mode                                                 │
│     ├─ Print styles                                              │
│     └─ State variations                                          │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

```css
/* 1. CSS Reset / Normalize */
/* Reset browser defaults */

/* 2. Base / Global Styles */
html { font-size: 16px; }
body { line-height: 1.5; }

/* 3. Layout */
.container { max-width: 1200px; }
.grid { display: grid; }

/* 4. Components */
.button { /* button styles */ }
.card { /* card styles */ }
.modal { /* modal styles */ }

/* 5. Utilities */
.text-center { text-align: center; }
.hidden { display: none; }
.mt-4 { margin-top: 1rem; }

/* 6. Themes / Overrides */
[data-theme="dark"] { /* dark theme */ }
```

### Performance Tips
- Minimize repaints and reflows
- Use `transform` and `opacity` for animations
- Avoid `@import` (use `<link>`)
- Minify CSS for production
- Remove unused CSS
- Use `will-change` sparingly

---

**Next:** Learn [JavaScript](./03-javascript.md) to add interactivity!

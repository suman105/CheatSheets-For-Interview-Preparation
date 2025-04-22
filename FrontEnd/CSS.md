# CSS Cheatsheet

## CSS Basics

```html
<!-- External CSS: Preferred for maintainability and caching -->
<link rel="stylesheet" href="styles.css">

<!-- Internal CSS: Useful for small, page-specific styles -->
<style>
  /* Style the main heading */
  h1 {
    color: blue;
    font-size: 2rem;
  }
</style>

<!-- Inline CSS: Use sparingly for quick, one-off styles -->
<h1 style="color: blue; text-align: center;">Hello</h1>
```

- **CSS Overview**: Cascading Style Sheets (CSS) styles HTML content, controlling layout, colors, typography, and animations.
- **Cascading**: Styles are applied based on specificity, source order, and inheritance.
- **Best Practices**:
  - Prefer external CSS for scalability and performance.
  - Avoid inline CSS to maintain separation of concerns.
  - Use `<style>` for prototyping or single-page applications.

**Explanation**:
- External CSS files are cached by browsers, reducing load times.
- Inline CSS increases HTML file size and is harder to maintain.
- The cascade allows styles to be overridden based on selector specificity or `!important`.

---

## CSS Syntax & Selectors

```css
/* Basic syntax: selector targets elements, properties define styles */
selector {
  property: value;
}

/* Examples of common selectors */
/* Universal selector: Targets all elements */
* {
  margin: 0;
}

/* Element selector: Targets specific HTML tags */
p {
  font-size: 1rem;
}

/* Class and ID selectors: Target specific elements */
.class-name {
  color: #333;
}
#unique-id {
  background-color: #f0f0f0;
}

/* Combinators: Define relationships between elements */
div p { /* Descendant: All <p> inside <div> */
  margin-bottom: 1em;
}
div > p { /* Child: Direct <p> children of <div> */
  font-weight: bold;
}
div + p { /* Adjacent sibling: <p> immediately following <div> */
  border-top: 1px solid;
}
div ~ p { /* General sibling: All <p> siblings after <div> */
  color: gray;
}

/* Pseudo-classes: Style based on state or position */
a:hover {
  text-decoration: underline;
}
li:nth-child(odd) {
  background-color: #eee;
}
```

**Common Selectors**:
- **Type**: `h1`, `div`, `span`
- **Class/ID**: `.class`, `#id`
- **Attribute**: `[type="text"]`, `[data-role="admin"]`
- **Pseudo-classes**: `:hover`, `:focus`, `:nth-child(n)`, `:not(.class)`, `:is(h1, h2)`
- **Pseudo-elements**: `::before`, `::after`, `::first-letter`

**Explanation**:
- Selectors determine which elements are styled; specificity determines which rules apply when conflicts arise.
- Combinators (`>`, `+`, `~`) allow precise targeting of element relationships.
- `:is()` and `:where()` reduce repetitive selectors (e.g., `:is(h1, h2, h3)`).
- Avoid overusing universal (`*`) selectors due to performance impact.

---

## CSS Units

```css
/* Relative units: Scale based on context */
.container {
  width: 50%; /* 50% of parent width */
  font-size: 1.5rem; /* 1.5x root font-size (typically 16px) */
  margin: 2em; /* 2x parent font-size */
  height: 50vh; /* 50% of viewport height */
  padding: 2vw; /* 2% of viewport width */
}

/* Absolute units: Fixed measurements */
.box {
  width: 200px; /* Pixels: Device-independent */
  border-width: 2mm; /* Millimeters: Physical unit */
  font-size: 12pt; /* Points: 1pt = 1/72 inch */
}
```

**Units**:
- **Relative**:
  - `%`: Relative to parent’s dimension.
  - `rem`: Relative to root (`<html>`) font-size.
  - `em`: Relative to parent or current font-size.
  - `vw`, `vh`: 1% of viewport width/height.
  - `vmin`, `vmax`: 1% of smaller/larger viewport dimension.
- **Absolute**:
  - `px`: Standard for web (1px ≈ 1/96 inch).
  - `cm`, `mm`, `in`, `pt`, `pc`: Physical units, less common for screens.

**Explanation**:
- Relative units are preferred for responsive design, adapting to user settings or screen sizes.
- `rem` is ideal for consistent typography, avoiding compounding issues with nested `em`.
- Absolute units like `px` are reliable for fixed-size elements but less flexible.

---

## Colors in CSS

```css
/* Various color formats */
.element {
  /* Named color: Simple but limited */
  color: red;
  /* Hex: Common, precise */
  background-color: #ff0000;
  /* RGB: Functional, supports alpha */
  border-color: rgb(255, 0, 0);
  /* RGBA: Adds opacity */
  box-shadow: rgba(255, 0, 0, 0.5);
  /* HSL: Intuitive for hue-based adjustments */
  outline-color: hsl(0, 100%, 50%);
  /* HSLA: HSL with opacity */
  color: hsla(0, 100%, 50%, 0.7);
  /* currentColor: Inherits current text color */
  border: 1px solid currentColor;
}
```

**Color Formats**:
- **Named**: `blue`, `transparent` (limited palette).
- **Hex**: `#RRGGBB` or `#RGB` (shorthand).
- **RGB**: `rgb(255, 0, 0)` or `rgb(100%, 0%, 0%)`.
- **RGBA**: Adds alpha (opacity, 0–1).
- **HSL**: Hue (0–360), Saturation (0–100%), Lightness (0–100%).
- **HSLA**: HSL with alpha.
- **New Formats**: `oklch()`, `lab()` for perceptual uniformity (modern browsers).

**Explanation**:
- HSL is great for creating color schemes by adjusting hue.
- `currentColor` ensures consistency with inherited text color.
- Use `rgba` or `hsla` for semi-transparent effects like shadows or overlays.
- Modern formats like `oklch()` improve color accuracy across devices.

---

## Box Model

```css
/* Box model: Defines element dimensions */
.box {
  /* Margin: External spacing */
  margin: 10px;
  /* Padding: Internal spacing */
  padding: 20px;
  /* Border: Surrounds padding */
  border: 1px solid black;
  /* Content width: Excludes padding/border with box-sizing */
  width: 200px;
  /* Include padding and border in width */
  box-sizing: border-box;
}
```

**Box Model Components**:
- **Content**: The core area (text, images).
- **Padding**: Space inside the border.
- **Border**: Surrounds padding.
- **Margin**: Space outside the border.
- **Box-Sizing**:
  - `content-box`: Width/height excludes padding and border (default).
  - `border-box`: Width/height includes padding and border.

**Explanation**:
- `box-sizing: border-box` simplifies layout calculations, especially in responsive designs.
- Margins can collapse vertically (e.g., adjacent elements share the larger margin).
- Use `outline` instead of `border` for debugging to avoid affecting layout.

---

## Display & Positioning

```css
/* Display: Controls element rendering */
.element {
  /* Block: Takes full width, stacks vertically */
  display: block;
  /* Inline: Flows with text, no width/height */
  display: inline;
  /* Inline-block: Inline flow with block properties */
  display: inline-block;
  /* None: Removes from layout */
  display: none;
  /* Flex: Enables flexbox layout */
  display: flex;
  /* Grid: Enables grid layout */
  display: grid;
}

/* Positioning: Controls element placement */
.positioned {
  /* Relative: Offset from normal position */
  position: relative;
  top: 10px;
  left: 20px;
  /* Absolute: Positioned relative to nearest positioned ancestor */
  position: absolute;
  bottom: 0;
  right: 0;
  /* Fixed: Positioned relative to viewport */
  position: fixed;
  top: 0;
  /* Sticky: Sticks within parent on scroll */
  position: sticky;
  top: 10px;
  /* Z-index: Controls stacking order */
  z-index: 100;
}
```

**Display Types**:
- `block`: `<div>`, `<p>` (full width, new line).
- `inline`: `<span>`, `<a>` (inline flow, no width/height).
- `inline-block`: Combines inline flow with block properties.
- `flex`, `grid`: Modern layout systems.
- `none`: Hides element (removes from flow).

**Positioning**:
- `static`: Default, follows normal flow.
- `relative`: Offset from its normal position.
- `absolute`: Removed from flow, positioned relative to ancestor.
- `fixed`: Stays in place on scroll.
- `sticky`: Hybrid of `relative` and `fixed`.

**Explanation**:
- `z-index` requires a positioned element (`relative`, `absolute`, etc.).
- `sticky` is ideal for headers that stay visible within a container.
- Use `display: none` sparingly; prefer `visibility: hidden` if layout preservation is needed.

---

## Flexbox

```css
/* Flex container: Enables flexible layout */
.container {
  display: flex;
  /* Row: Horizontal layout (default) */
  flex-direction: row;
  /* Column: Vertical layout */
  /* flex-direction: column; */
  /* Justify: Align items along main axis */
  justify-content: center;
  /* Align: Align items along cross axis */
  align-items: center;
  /* Gap: Space between items */
  gap: 1rem;
  /* Wrap: Allow items to wrap to new lines */
  flex-wrap: wrap;
}

/* Flex items: Customize individual behavior */
.item {
  /* Grow: Expand to fill space */
  flex-grow: 1;
  /* Shrink: Allow shrinking */
  flex-shrink: 1;
  /* Basis: Initial size */
  flex-basis: auto;
  /* Shorthand: grow shrink basis */
  flex: 1 1 auto;
  /* Align-self: Override container alignment */
  align-self: flex-start;
}
```

**Key Properties**:
- **Container**:
  - `flex-direction`: `row`, `column`, `row-reverse`, `column-reverse`.
  - `justify-content`: `flex-start`, `center`, `space-between`, `space-around`, `space-evenly`.
  - `align-items`: `flex-start`, `center`, `flex-end`, `stretch`, `baseline`.
  - `flex-wrap`: `nowrap`, `wrap`, `wrap-reverse`.
  - `gap`: Replaces margins for spacing.
- **Items**:
  - `flex`: Shorthand for `flex-grow`, `flex-shrink`, `flex-basis`.
  - `align-self`: Overrides `align-items`.
  - `order`: Controls item order (default: 0).

**Explanation**:
- Flexbox is ideal for one-dimensional layouts (rows or columns).
- `gap` simplifies spacing compared to margins.
- `flex: 1` makes items equally sized, sharing available space.
- Avoid overusing `flex` for complex grids; use CSS Grid instead.

---

## Grid

```css
/* Grid container: Defines a grid layout */
.container {
  display: grid;
  /* Columns: Two equal-width columns */
  grid-template-columns: 1fr 1fr;
  /* Rows: Auto-sized rows */
  grid-template-rows: auto;
  /* Gap: Space between grid cells */
  gap: 1rem;
  /* Auto-flow: Control item placement */
  grid-auto-flow: row;
}

/* Grid items: Customize placement */
.item {
  /* Span specific columns */
  grid-column: 1 / 3;
  /* Span specific rows */
  grid-row: 1 / 2;
}

/* Named areas: Simplify complex layouts */
.grid {
  display: grid;
  grid-template-areas:
    "header header"
    "sidebar main"
    "footer footer";
}
.header {
  grid-area: header;
}
```

**Key Properties**:
- **Container**:
  - `grid-template-columns/rows`: Define column/row sizes (e.g., `1fr`, `100px`, `auto`).
  - `gap`: Spacing between grid cells (`row-gap`, `column-gap`).
  - `grid-auto-flow`: `row`, `column`, `dense`.
  - `grid-template-areas`: Named areas for layout.
  - `justify/align-items`: Align grid items.
  - `justify/align-content`: Align grid tracks.
- **Items**:
  - `grid-column/row`: Specify start/end lines (e.g., `1 / 3`).
  - `grid-area`: Assign to named area or line numbers.

**Explanation**:
- Grid is ideal for two-dimensional layouts with rows and columns.
- `fr` unit distributes free space proportionally.
- Named areas (`grid-template-areas`) simplify complex layouts.
- Use `minmax(100px, 1fr)` for responsive column/row sizes.

---

## Typography

```css
/* Typography: Style text appearance */
body {
  /* Font stack: Fallbacks for unavailable fonts */
  font-family: 'Arial', 'Helvetica', sans-serif;
  /* Font size: Base size for document */
  font-size: 16px;
  /* Font weight: Thickness (100–900) */
  font-weight: 700;
  /* Line height: Spacing between lines */
  line-height: 1.5;
  /* Letter spacing: Space between characters */
  letter-spacing: 0.05em;
  /* Text alignment: Horizontal alignment */
  text-align: center;
  /* Text transform: Case modification */
  text-transform: uppercase;
  /* Text decoration: Underline, strikethrough */
  text-decoration: underline;
  /* Font style: Italic, oblique */
  font-style: italic;
}
```

**Key Properties**:
- `font-family`: Specify fonts with fallbacks.
- `font-size`: Use `rem` or `px` for consistency.
- `font-weight`: `normal` (400), `bold` (700), or numeric values.
- `line-height`: Unitless (e.g., `1.5`) for scalability.
- `text-align`: `left`, `right`, `center`, `justify`.
- `text-transform`: `uppercase`, `lowercase`, `capitalize`.
- `text-decoration`: `underline`, `line-through`, `none`.

**Explanation**:
- Use system fonts (e.g., `-apple-system`) for performance and native look.
- `line-height` improves readability; 1.5–1.8 is typical.
- Avoid `justify` for narrow text blocks to prevent uneven spacing.
- Use `@font-face` for custom fonts, but optimize with `woff2` format.

---

## Backgrounds & Borders

```css
/* Backgrounds and borders: Style element appearance */
.box {
  /* Background color: Solid color */
  background-color: #eee;
  /* Background image: URL with fallback */
  background-image: url('img.jpg');
  /* Background size: Cover entire element */
  background-size: cover;
  /* Background position: Center image */
  background-position: center;
  /* Background repeat: Prevent tiling */
  background-repeat: no-repeat;
  /* Border: Width, style, color */
  border: 2px solid red;
  /* Border radius: Rounded corners */
  border-radius: 10px;
  /* Box shadow: Offset, blur, color */
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}
```

**Key Properties**:
- **Background**:
  - `background-color`: Solid or transparent.
  - `background-image`: Single or multiple images.
  - `background-size`: `auto`, `cover`, `contain`, or specific sizes.
  - `background-position`: Coordinates or keywords (`center`).
  - `background-repeat`: `repeat`, `no-repeat`, `repeat-x/y`.
- **Border**:
  - `border`: Shorthand for width, style, color.
  - `border-radius`: Rounds corners (e.g., `50%` for circles).
- **Box-shadow**: Adds shadows (inset or outset).

**Explanation**:
- Use `background` shorthand for concise code (e.g., `background: #eee url(img.jpg) no-repeat center/cover`).
- `border-radius` can create complex shapes with multiple values.
- Optimize images with modern formats (e.g., WebP) for faster loading.

---

## Pseudo-classes & Pseudo-elements

```css
/* Pseudo-classes: Style based on state or position */
a:hover {
  /* Change color on hover */
  color: red;
}
input:focus {
  /* Highlight focused input */
  outline: 2px solid blue;
}
li:nth-child(2n) {
  /* Style even-numbered items */
  background-color: #f0f0f0;
}

/* Pseudo-elements: Style specific parts of elements */
p::first-letter {
  /* Style first letter */
  font-size: 2em;
}
div::before {
  /* Insert content before element */
  content: '👉 ';
  color: green;
}
::selection {
  /* Style selected text */
  background-color: yellow;
  color: black;
}
```

**Common Pseudo-classes**:
- `:hover`, `:active`, `:focus`, `:focus-within`, `:disabled`.
- `:nth-child(n)`, `:nth-of-type(n)`, `:first-child`, `:last-child`.
- `:not()`, `:is()`, `:where()`, `:has()` (modern browsers).

**Common Pseudo-elements**:
- `::before`, `::after`: Insert content.
- `::first-letter`, `::first-line`: Style text parts.
- `::selection`: Style user-selected text.

**Explanation**:
- `:has()` enables parent-based styling (e.g., `section:has(.error) { border: red; }`).
- `::before` and `::after` require `content` property, even if empty (`content: ""`).
- Use pseudo-elements for decorative content to avoid unnecessary DOM elements.
- Test `:focus` styles for accessibility, ensuring keyboard usability.

---

## Transitions & Animations

```css
/* Transitions: Smooth property changes */
.box {
  /* Transition all properties over 0.3s with easing */
  transition: all 0.3s ease;
  background-color: blue;
}
.box:hover {
  /* Change on hover */
  background-color: red;
  transform: scale(1.1);
}

/* Animations: Keyframe-based movement */
.animated {
  /* Apply animation: name, duration, iteration */
  animation: move 2s infinite ease-in-out;
}

/* Define keyframes for animation */
@keyframes move {
  0% {
    transform: translateX(0);
  }
  50% {
    transform: translateX(100px);
  }
  100% {
    transform: translateX(0);
  }
}
```

**Key Properties**:
- **Transition**:
  - `transition-property`: Properties to animate (e.g., `color`, `transform`).
  - `transition-duration`: Time (e.g., `0.3s`).
  - `transition-timing-function`: `ease`, `linear`, `cubic-bezier()`.
  - `transition-delay`: Delay before starting.
- **Animation**:
  - `animation-name`: Keyframe name.
  - `animation-duration`, `animation-iteration-count`, `animation-direction`.
  - `animation-fill-mode`: `forwards`, `backwards`, `both`.

**Explanation**:
- Transitions are simpler for state changes (e.g., hover effects).
- Animations with `@keyframes` allow complex, multi-step effects.
- Use `will-change` (e.g., `will-change: transform`) for performance optimization.
- Avoid animating properties like `width` or `height` that trigger reflows; prefer `transform`.

---

## Media Queries & Responsive Design

```css
/* Media query: Apply styles based on conditions */
@media (max-width: 600px) {
  /* Mobile styles */
  body {
    background-color: lightblue;
    font-size: 14px;
  }
}

/* Multiple conditions */
@media (min-width: 768px) and (orientation: landscape) {
  .container {
    display: flex;
  }
}
```

**Common Features**:
- `max-width`, `min-width`: Breakpoints for responsive design.
- `orientation`: `portrait`, `landscape`.
- `resolution`: `dpi`, `dppx`.
- `prefers-color-scheme`: `light`, `dark` (for dark mode).
- `prefers-reduced-motion`: `reduce` (for accessibility).

**Explanation**:
- Use mobile-first design with `min-width` for progressive enhancement.
- Common breakpoints: 320px (mobile), 768px (tablet), 1024px (desktop).
- `prefers-reduced-motion` respects user preferences for minimal animations.
- Test media queries thoroughly across devices and browsers.

---

## Variables & Custom Properties

```css
/* Define variables in :root for global scope */
:root {
  /* Custom property for main color */
  --main-color: #3498db;
  /* Spacing unit */
  --spacing: 1rem;
}

/* Use variables */
.box {
  color: var(--main-color);
  margin: var(--spacing);
  /* Fallback value if variable undefined */
  padding: var(--custom-padding, 10px);
}
```

**Explanation**:
- Custom properties (`--name`) are dynamic and can be updated via JavaScript.
- `:root` ensures global availability; scope locally in specific selectors if needed.
- Variables simplify theming and maintenance (e.g., dark mode toggles).
- Fallbacks (`var(--name, fallback)`) ensure robustness.

---

## Advanced Selectors

```css
/* Advanced selectors for precise targeting */
/* :not(): Exclude elements */
button:not(.disabled) {
  cursor: pointer;
}

/* :is(): Group selectors */
:is(h1, h2, h3) {
  font-weight: bold;
}

/* :has(): Style based on children (modern browsers) */
section:has(.error) {
  border: 2px solid red;
}

/* Attribute selectors */
input[type="text"] {
  border: 1px solid gray;
}
[data-role="admin"] {
  background-color: gold;
}

/* Nth selectors */
li:nth-child(3n+1) {
  color: blue;
}
```

**Explanation**:
- `:has()` is powerful but has limited browser support (use with polyfills if needed).
- Attribute selectors are case-sensitive by default; use `i` flag for case-insensitivity (e.g., `[type="text" i]`).
- `:nth-child` supports formulas (e.g., `3n+1` for every third element starting at 1).
- Combine selectors for specificity but avoid overly complex chains for performance.

---

## CSS Functions

```css
/* CSS functions: Dynamic calculations and effects */
.element {
  /* calc(): Perform math */
  width: calc(100% - 50px);
  /* clamp(): Constrain values */
  font-size: clamp(1rem, 2vw, 1.5rem);
  /* var(): Use custom properties */
  color: var(--main-color);
  /* url(): Reference assets */
  background: url('image.jpg');
  /* min/max(): Limit values */
  height: min(50vh, 500px);
  /* transform functions */
  transform: rotate(45deg) scale(1.2);
}
```

**Common Functions**:
- `calc()`: Supports `+`, `-`, `*`, `/`.
- `clamp(min, preferred, max)`: Ideal for responsive typography and spacing.
- `min()`, `max()`: Select smallest/largest value.
- `var()`: Access custom properties.
- `url()`: Load external resources.
- `rgb()`, `hsl()`, `oklch()`: Color definitions.

**Explanation**:
- `calc()` is versatile but requires valid units (e.g., `px`, `%`).
- `clamp()` ensures values stay within practical bounds, enhancing responsiveness.
- Transform functions (`rotate`, `scale`, `translate`) are GPU-accelerated for smooth animations.

---

## Advanced Features

- **Container Queries**:

  ```css
  /* Define container for size queries */
  .container {
    container-type: inline-size;
  }
  /* Style based on container width */
  @container (min-width: 400px) {
    .item {
      font-size: 1.2rem;
    }
  }
  ```

- **Aspect Ratio**:

  ```css
  /* Maintain aspect ratio */
  .video {
    aspect-ratio: 16 / 9;
    width: 100%;
  }
  ```

- **Accent Color**:

  ```css
  /* Customize form element colors */
  input[type="checkbox"] {
    accent-color: #3498db;
  }
  ```

- **Logical Properties**:

  ```css
  /* Use logical properties for internationalization */
  .box {
    margin-inline: 1rem; /* Left/right in LTR */
    padding-block: 1rem; /* Top/bottom */
  }
  ```

- **Subgrid**:

  ```css
  .grid {
    display: grid;
    grid-template-columns: 1fr 2fr;
  }
  .nested {
    display: grid;
    grid-template-columns: subgrid; /* Inherit parent columns */
  }
  ```

**Explanation**:
- Container Queries enable responsive design based on parent size, not viewport.
- `aspect-ratio` simplifies responsive media sizing (e.g., videos, images).
- `accent-color` unifies form control styling with minimal code.
- Logical properties (`margin-inline`) support right-to-left (RTL) languages.
- `subgrid` aligns nested grids with parent grid lines, ideal for complex layouts.

---

## Cheat Codes

```css
/* Debugging: Highlight element boundaries */
* {
  outline: 1px solid red;
}

/* Universal box-sizing: Simplify layout calculations */
*, *::before, *::after {
  box-sizing: border-box;
}

/* Clearfix: Fix float issues */
.clearfix::after {
  content: "";
  display: block;
  clear: both;
}

/* Smooth scrolling: Enhance user experience */
html {
  scroll-behavior: smooth;
}

/* Hide overflow: Prevent unwanted scrolling */
.container {
  overflow: hidden;
}

/* Visually hidden: Hide content for screen readers */
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
}
```

**Explanation**:
- Debugging outlines help identify layout issues without affecting the box model.
- Universal `box-sizing` ensures consistent sizing across elements.
- `.sr-only` hides content visually while keeping it accessible.
- `scroll-behavior: smooth` improves navigation for internal links.

---

## Common Properties List

- **Box Model**: `margin`, `padding`, `border`, `width`, `height`, `box-sizing`.
- **Typography**: `color`, `font-family`, `font-size`, `font-weight`, `line-height`, `text-align`, `text-decoration`.
- **Layout**: `display`, `position`, `top`, `right`, `bottom`, `left`, `z-index`, `flex`, `grid`.
- **Visual**: `background`, `box-shadow`, `opacity`, `filter`, `transform`.
- **Miscellaneous**: `overflow`, `cursor`, `visibility`, `transition`, `animation`.

**Explanation**:
- These properties cover most styling needs; prioritize semantic properties for maintainability.
- Use shorthand properties (e.g., `margin`, `background`) for concise code.
- Avoid deprecated properties like `float` for layout; use Flexbox or Grid.

---

## CSS Shorthands

```css
/* Margin: Top/bottom, left/right */
margin: 10px 20px;

/* Padding: Top, right, bottom, left */
padding: 10px 20px 5px 0;

/* Font: Style, variant, weight, size/line-height, family */
font: italic small-caps bold 16px/1.5 'Arial', sans-serif;

/* Background: Color, image, repeat, position/size */
background: #eee url('img.jpg') no-repeat center/cover;

/* Border: Width, style, color */
border: 1px solid red;

/* Flex: Grow, shrink, basis */
flex: 1 1 auto;
```

**Explanation**:
- Shorthands reduce code verbosity but require understanding of property order.
- Ensure all values are provided or use individual properties for clarity.
- Test shorthands in older browsers for compatibility.

---

## Best Practices

- **Performance**:
  - Minimize reflows by animating `transform` and `opacity` instead of `width` or `top`.
  - Use `will-change` sparingly for GPU acceleration.
  - Optimize selectors (e.g., avoid deep nesting or universal selectors).
- **Accessibility**:
  - Ensure sufficient color contrast (WCAG 2.1 recommends 4.5:1 for text).
  - Use `rem`/`em` for font sizes to respect user preferences.
  - Provide `:focus` styles for keyboard navigation.
- **Maintainability**:
  - Organize CSS with methodologies like BEM or SMACSS.
  - Use CSS variables for theming and consistency.
  - Comment complex rules for clarity.
- **Compatibility**:
  - Test in multiple browsers; use vendor prefixes (`-webkit-`, `-moz-`) via tools like Autoprefixer.
  - Provide fallbacks for modern properties (e.g., `grid` with `flex`).
- **Responsive Design**:
  - Adopt mobile-first approach with `min-width` media queries.
  - Use `clamp()` for fluid typography and spacing.
  - Test on real devices or emulators.

**Explanation**:
- Following best practices ensures performant, accessible, and maintainable CSS.
- Tools like PostCSS or Sass can enhance development with variables, nesting, and more.
- Regular audits with tools like Lighthouse help identify performance and accessibility issues.
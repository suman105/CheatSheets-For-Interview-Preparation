# Advanced HTML Cheatsheet

## HTML Basics

```html
<!-- Declares the document as HTML5, ensuring browsers render it correctly -->
<!DOCTYPE html>
<!-- Root element with language attribute for accessibility -->
<html lang="en">
<head>
  <!-- Specifies UTF-8 encoding for universal character support -->
  <meta charset="UTF-8">
  <!-- Ensures proper scaling on mobile devices -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <!-- Title displayed in browser tab and used by search engines -->
  <title>Document Title</title>
</head>
<!-- Main content area of the webpage -->
<body>
  <!-- Main heading for the page -->
  <h1>Hello, World!</h1>
</body>
</html>
```

- `<!DOCTYPE html>`: Must be the first line to declare HTML5, ensuring compatibility with modern browsers.
- `<html lang="en">`: Specifies the document language, aiding screen readers and search engines.
- `<meta charset="UTF-8">`: Enables support for a wide range of characters, including emojis and non-Latin scripts.
- `<meta name="viewport">`: Critical for responsive design, ensuring proper rendering on mobile devices.

---

## HTML Elements & Attributes

```html
<!-- Generic tag structure with an attribute -->
<tagname attribute="value">Content</tagname>
```

Example:

```html
<!-- Anchor tag with href for navigation and target for new tab -->
<a href="https://example.com" target="_blank" rel="noopener noreferrer">Visit Example</a>
```

**Common Attributes**:

- `id`: Unique identifier for an element (e.g., `<div id="header">`).
- `class`: Assigns one or more classes for CSS/JavaScript (e.g., `<div class="container dark">`).
- `style`: Inline CSS for quick styling (e.g., `<p style="color: blue;">`).
- `title`: Provides tooltip text on hover (e.g., `<abbr title="HyperText">HTML</abbr>`).
- `hidden`: Hides an element (e.g., `<div hidden>`).
- `lang`: Specifies the language of content (e.g., `<p lang="fr">Bonjour</p>`).
- `data-*`: Custom data attributes for JavaScript (e.g., `<div data-user-id="123">`).
- **Accessibility Attributes**:
  - `aria-*`: Enhances accessibility (e.g., `aria-label="Close button"`).
  - `role`: Defines element purpose for screen readers (e.g., `role="navigation"`).

**Explanation**:

- Attributes enhance elements with additional functionality or metadata.
- Use `id` sparingly for unique elements; prefer `class` for reusable styling.
- Custom `data-*` attributes are ideal for storing application-specific data.
- ARIA attributes are crucial for making dynamic content accessible to assistive technologies.

---

## Text Formatting

| Tag | Purpose/Meaning | Example |
| --- | --- | --- |
| `<b>` | Bold (visual styling) | `<b>Bold text</b>` |
| `<strong>` | Strong (semantic importance) | `<strong>Important!</strong>` |
| `<i>` | Italic (visual styling) | `<i>Italic text</i>` |
| `<em>` | Emphasis (semantic italic) | `<em>Emphasized text</em>` |
| `<mark>` | Highlighted text | `<mark>Highlighted</mark>` |
| `<small>` | Smaller text (e.g., fine print) | `<small>Terms apply</small>` |
| `<del>` | Deleted text (strikethrough) | `<del>Old price</del>` |
| `<ins>` | Inserted text (underlined) | `<ins>New price</ins>` |
| `<sub>` | Subscript (e.g., chemical formulas) | `H<sub>2</sub>O` |
| `<sup>` | Superscript (e.g., exponents) | `x<sup>2</sup>` |
| `<code>` | Inline code snippet | `<code>console.log()</code>` |
| `<pre>` | Preformatted text (preserves spacing) | `<pre> Code block </pre>` |
| `<blockquote>` | Block quote with citation | `<blockquote cite="url">Quote</blockquote>` |
| `<q>` | Inline quote | `<q>Short quote</q>` |
| `<abbr>` | Abbreviation with tooltip | `<abbr title="World Wide Web">WWW</abbr>` |

**Explanation**:

- Semantic tags like `<strong>` and `<em>` convey meaning to search engines and assistive technologies, unlike `<b>` and `<i>`, which are purely visual.
- `<mark>` is useful for highlighting search results or key terms.
- `<pre>` is ideal for displaying code or text with specific formatting.
- Use `<cite>` within `<blockquote>` for proper citation attribution.

---

## HTML Lists

### Unordered List

```html
<!-- Unordered list with bullet points -->
<ul>
  <!-- List item -->
  <li>Item 1</li>
  <li>Item 2</li>
</ul>
```

### Ordered List

```html
<!-- Ordered list with customizable numbering -->
<ol type="1|A|a|I|i" start="2">
  <!-- List item -->
  <li>Item A</li>
  <li>Item B</li>
</ol>
```

- `type`: Specifies numbering style (`1`, `A`, `a`, `I`, `i`).
- `start`: Sets the starting number (e.g., `start="2"`).
- `reversed`: Reverses the order (e.g., `<ol reversed>`).

### Description List

```html
<!-- Description list for terms and their definitions -->
<dl>
  <!-- Term -->
  <dt>HTML</dt>
  <!-- Description -->
  <dd>HyperText Markup Language</dd>
  <dt>CSS</dt>
  <dd>Cascading Style Sheets</dd>
</dl>
```

**Explanation**:

- `<ul>` is used for unordered collections (e.g., navigation menus).
- `<ol>` is suitable for sequences or rankings, with `type` and `start` for customization.
- `<dl>` is ideal for glossaries or metadata key-value pairs.
- Nest lists for hierarchical structures (e.g., `<ul><li><ul>...</ul></li></ul>`).

---

## HTML Links

```html
<!-- Anchor tag for external link with security attributes -->
<a href="https://example.com" target="_blank" rel="noopener noreferrer" title="Visit Example">Link</a>
```

- **Attributes**:
  - `href`: URL or anchor (`#section`).
  - `target`: `_self` (default), `_blank` (new tab), `_parent`, `_top`.
  - `rel`: `noopener` (prevents security risks), `noreferrer` (hides referrer), `nofollow` (SEO).
  - `download`: Prompts file download (e.g., `<a href="file.pdf" download>`).
- **Examples**:

  ```html
  <!-- Internal link to a section -->
  <a href="#section1">Jump to Section</a>
  <!-- Email link -->
  <a href="mailto:example@email.com">Email Us</a>
  <!-- Telephone link -->
  <a href="tel:+1234567890">Call Us</a>
  ```

**Explanation**:

- Use `rel="noopener noreferrer"` for external links to enhance security and privacy.
- `title` improves accessibility by providing context on hover.
- Internal links with `#id` enable smooth scrolling with CSS or JavaScript.

---

## HTML Images

```html
<!-- Image with accessibility and lazy loading -->
<img src="image.jpg" alt="Descriptive text" width="300" height="200" loading="lazy">
<!-- Semantic image with caption -->
<figure>
  <img src="photo.jpg" alt="Nature scene">
  <figcaption>Beautiful landscape</figcaption>
</figure>
```

- **Attributes**:
  - `alt`: Describes the image for screen readers and SEO.
  - `width`, `height`: Prevents layout shifts (use CSS for responsive sizing).
  - `loading="lazy"`: Defers off-screen image loading for performance.
  - `srcset`: Provides multiple image resolutions (e.g., `<img srcset="small.jpg 480w, large.jpg 800w">`).
- **Responsive Images**:

  ```html
  <picture>
    <!-- High-resolution image for larger screens -->
    <source srcset="large.jpg" media="(min-width: 800px)">
    <!-- Default image for smaller screens -->
    <img src="small.jpg" alt="Responsive image" loading="lazy">
  </picture>
  ```

**Explanation**:

- `alt` is mandatory for accessibility; empty (`alt=""`) for decorative images.
- `<figure>` and `<figcaption>` provide semantic context for images.
- `loading="lazy"` and `<picture>` optimize performance and responsiveness.
- Use `srcset` and `sizes` for responsive images to serve appropriate resolutions.

---

## HTML Tables

```html
<!-- Accessible table with caption and scope -->
<table>
  <!-- Table title for context -->
  <caption>User Data</caption>
  <thead>
    <tr>
      <!-- Column headers with scope for accessibility -->
      <th scope="col">Name</th>
      <th scope="col">Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <!-- Table data cells -->
      <td>John</td>
      <td>25</td>
    </tr>
  </tbody>
  <tfoot>
    <!-- Footer spanning multiple columns -->
    <tr>
      <td colspan="2">Total: 1 user</td>
    </tr>
  </tfoot>
</table>
```

- **Attributes**:
  - `scope="col"|"row"`: Clarifies header relationships for screen readers.
  - `colspan`, `rowspan`: Merges cells across columns or rows.
- **Best Practices**:
  - Use `<caption>` for table descriptions.
  - Avoid tables for layout; use CSS Grid or Flexbox instead.
  - Ensure tables are responsive with CSS (e.g., `overflow-x: auto`).

**Explanation**:

- Tables are best for tabular data, not page layouts.
- Accessibility is improved with `scope` and `<caption>`.
- `<thead>`, `<tbody>`, and `<tfoot>` enhance semantic structure.

---

## HTML Forms

```html
<!-- Form with POST method and validation -->
<form action="/submit" method="post" novalidate>
  <!-- Label associated with input for accessibility -->
  <label for="name">Name:</label>
  <!-- Text input with validation -->
  <input type="text" id="name" name="name" required pattern="[A-Za-z]+" placeholder="Enter name">
  <!-- Radio buttons for single selection -->
  <fieldset>
    <legend>Gender:</legend>
    <input type="radio" id="male" name="gender" value="male">
    <label for="male">Male</label>
    <input type="radio" id="female" name="gender" value="female">
    <label for="female">Female</label>
  </fieldset>
  <!-- Submit button -->
  <button type="submit">Submit</button>
</form>
```

- **Attributes**:
  - `method="get"|"post"`: `GET` for queries, `POST` for data submission.
  - `novalidate`: Disables HTML5 validation for custom JavaScript validation.
  - `required`, `pattern`: Enforce input validation.
  - `autocomplete="on"|"off"`: Controls browser autofill behavior.
- **Advanced Features**:

  ```html
  <!-- Datalist for input suggestions -->
  <input list="options" id="choice" name="choice">
  <datalist id="options">
    <option value="Option 1">
    <option value="Option 2">
  </datalist>
  ```

**Explanation**:

- Forms are critical for user interaction; always pair `<label>` with `for` to link to `id`.
- Use `<fieldset>` and `<legend>` to group related inputs (e.g., radio buttons).
- `pattern` allows regex-based validation (e.g., `[A-Za-z]+` for letters only).
- `<datalist>` enhances user experience with autocomplete suggestions.

---

## HTML Input Types

```html
<!-- Text-based inputs -->
<input type="text" placeholder="Text">
<input type="email" placeholder="user@example.com">
<input type="password" placeholder="Password">
<input type="url" placeholder="https://example.com">
<input type="tel" placeholder="+1234567890">
<input type="search" placeholder="Search...">

<!-- Date and number inputs -->
<input type="number" min="1" max="100" step="1">
<input type="date" min="2023-01-01">
<input type="time">
<input type="datetime-local">
<input type="month">
<input type="week">

<!-- Selection and file inputs -->
<input type="checkbox" name="option" value="1">
<input type="radio" name="group" value="1">
<input type="file" accept=".pdf,.docx" multiple>
<input type="range" min="0" max="100" step="10">
<input type="color">

<!-- Hidden and button inputs -->
<input type="hidden" name="token" value="abc123">
<input type="submit" value="Submit">
<input type="reset" value="Reset">
<input type="button" value="Click me">
```

**Explanation**:

- Modern input types like `email`, `tel`, and `date` provide built-in validation and mobile-friendly keyboards.
- `accept` restricts file types for `<input type="file">`.
- `range` and `color` offer interactive UI elements.
- Use `hidden` inputs to pass data without user interaction.

---

## HTML5 Semantic Tags

| Tag | Purpose | Example Usage |
| --- | --- | --- |
| `<header>` | Page or section header | Site logo, navigation |
| `<nav>` | Navigation links | Menu bar, breadcrumb |
| `<main>` | Primary content | Main article or app content |
| `<section>` | Logical group of content | Chapter, feature section |
| `<article>` | Self-contained content | Blog post, news article |
| `<aside>` | Supplementary content | Sidebar, ads |
| `<footer>` | Page or section footer | Copyright, contact info |
| `<figure>` | Media with caption | Image with description |
| `<details>` | Expandable content | FAQ accordion |
| `<summary>` | Summary for `<details>` | Accordion toggle text |
| `<dialog>` | Modal or dialog box | Pop-up confirmation |

**Example**:

```html
<!-- Semantic page structure -->
<main>
  <header>
    <h1>Site Title</h1>
    <nav>
      <ul>
        <li><a href="#home">Home</a></li>
      </ul>
    </nav>
  </header>
  <article>
    <h2>Article Title</h2>
    <p>Content...</p>
  </article>
  <aside>
    <h3>Related Links</h3>
  </aside>
  <footer>
    <p>&copy; 2025</p>
  </footer>
</main>
```

**Explanation**:

- Semantic tags improve SEO and accessibility by clearly defining content roles.
- `<dialog>` is useful for modals, activated with `showModal()` in JavaScript.
- Use `<main>` once per page for primary content, excluding headers/footers.

---

## HTML Media Tags

```html
<!-- Video with multiple sources and fallback -->
<video controls autoplay loop muted playsinline poster="thumbnail.jpg">
  <source src="movie.mp4" type="video/mp4">
  <source src="movie.webm" type="video/webm">
  <!-- Fallback for unsupported browsers -->
  <p>Your browser does not support video.</p>
</video>

<!-- Audio with multiple sources -->
<audio controls preload="auto">
  <source src="audio.mp3" type="audio/mpeg">
  <source src="audio.ogg" type="audio/ogg">
  <!-- Fallback -->
  <p>Your browser does not support audio.</p>
</audio>
```

- **Attributes**:
  - `controls`: Displays playback controls.
  - `autoplay`: Starts playback automatically (muted required for most browsers).
  - `loop`: Repeats the media.
  - `muted`: Mutes audio by default.
  - `playsinline`: Allows inline playback on mobile.
  - `preload="auto"|"metadata"|"none"`: Controls preloading behavior.
- **Track for Captions**:

  ```html
  <video controls>
    <source src="movie.mp4" type="video/mp4">
    <track src="subtitles.vtt" kind="subtitles" srclang="en" label="English">
  </video>
  ```

**Explanation**:

- Multiple `<source>` tags ensure compatibility across browsers.
- `<track>` adds subtitles or captions, enhancing accessibility.
- `poster` sets a preview image for videos.
- Use `preload="metadata"` to reduce initial load time.

---

## HTML APIs

- **Geolocation API**: Retrieves user location.

  ```html
  <script>
    // Request user location
    navigator.geolocation.getCurrentPosition(pos => {
      console.log(`Lat: ${pos.coords.latitude}, Lon: ${pos.coords.longitude}`);
    });
  </script>
  ```
- **Drag & Drop API**: Enables draggable elements.

  ```html
  <div draggable="true" ondragstart="event.dataTransfer.setData('text', 'data')">
    Drag me
  </div>
  ```
- **Canvas API**: Draws graphics via JavaScript.

  ```html
  <canvas id="myCanvas" width="200" height="100"></canvas>
  <script>
    const ctx = document.getElementById('myCanvas').getContext('2d');
    ctx.fillRect(10, 10, 50, 50); // Draw a rectangle
  </script>
  ```
- **Web Storage API**: Stores data locally.

  ```html
  <script>
    // Store and retrieve data
    localStorage.setItem('key', 'value');
    console.log(localStorage.getItem('key')); // 'value'
    sessionStorage.setItem('temp', 'data'); // Session-only storage
  </script>
  ```
- **Web Workers API**: Runs scripts in background threads.

  ```html
  <script>
    const worker = new Worker('worker.js');
    worker.postMessage('Start');
    worker.onmessage = e => console.log(e.data);
  </script>
  ```
- **WebSockets API**: Enables real-time communication.

  ```html
  <script>
    const socket = new WebSocket('ws://example.com');
    socket.onmessage = e => console.log(e.data);
  </script>
  ```
- **History API**: Manipulates browser history.

  ```html
  <script>
    history.pushState({ page: 1 }, 'Page 1', '/page1');
  </script>
  ```

**Explanation**:

- APIs extend HTML functionality, enabling dynamic and interactive web applications.
- Use Web Storage for client-side data persistence (`localStorage` for persistent, `sessionStorage` for temporary).
- Web Workers improve performance for heavy computations.
- Ensure proper error handling and user permissions (e.g., for Geolocation).

---

## HTML Entities

| Entity | Character | Use Case |
| --- | --- | --- |
| `&lt;` | &lt; | Less-than in code snippets |
| `&gt;` | &gt; | Greater-than in code |
| `&amp;` | & | Ampersand in text |
| `&quot;` | " | Quotes in attributes |
| `&apos;` | ' | Apostrophes in attributes |
| `&copy;` | © | Copyright symbol |
| `&reg;` | ® | Registered trademark |
| `&euro;` | € | Euro currency |
| `&nbsp;` |  | Non-breaking space |

**Explanation**:

- Entities prevent parsing issues (e.g., `<` in text would break HTML).
- `&nbsp;` ensures spaces are preserved, useful in layouts.
- Use numeric codes (e.g., `&#169;` for ©) for broader compatibility.

---

## HTML Meta Tags for SEO and Performance

```html
<!-- Character encoding -->
<meta charset="UTF-8">
<!-- Responsive viewport -->
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<!-- Page description for SEO -->
<meta name="description" content="Advanced HTML Cheatsheet for developers">
<!-- Keywords for search engines -->
<meta name="keywords" content="HTML, Web Development, Cheatsheet, HTML5">
<!-- Author information -->
<meta name="author" content="Suman Majjari">
<!-- Browser compatibility -->
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<!-- Prevent caching for sensitive pages -->
<meta http-equiv="Cache-Control" content="no-cache">
<!-- Open Graph for social media -->
<meta property="og:title" content="HTML Cheatsheet">
<meta property="og:image" content="thumbnail.jpg">
```

**Explanation**:

- Meta tags improve SEO, social sharing, and browser behavior.
- Open Graph (`og:*`) tags enhance social media previews.
- Use `Cache-Control` for dynamic content to prevent stale data.
- `<meta name="robots" content="index, follow">` controls search engine indexing.

---

## Advanced HTML Features

- **Custom Attributes**:

  ```html
  <!-- Store custom data for JavaScript -->
  <div data-user="suman" data-role="admin">User Info</div>
  <script>
    const user = document.querySelector('div').dataset.user; // 'suman'
  </script>
  ```

- **Responsive Images with** `srcset`:

  ```html
  <picture>
    <!-- Serve high-res image for larger screens -->
    <source srcset="large.jpg 2x" media="(min-width: 800px)">
    <!-- Serve smaller image for mobile -->
    <source srcset="small.jpg 1x" media="(max-width: 799px)">
    <img src="fallback.jpg" alt="Responsive image" loading="lazy">
  </picture>
  ```

- **Template for Dynamic Rendering**:

  ```html
  <!-- Define reusable template -->
  <template id="card">
    <div class="card">
      <h3>Card Title</h3>
      <p>Card Content</p>
    </div>
  </template>
  <script>
    const template = document.getElementById('card').content;
    document.body.appendChild(template.cloneNode(true));
  </script>
  ```

- **Microdata for SEO**:

  ```html
  <!-- Schema.org markup for search engines -->
  <div itemscope itemtype="https://schema.org/Person">
    <span itemprop="name">Suman Majjari</span>
    <span itemprop="jobTitle">Developer</span>
  </div>
  ```

- **Progressive Web App (PWA) Support**:

  ```html
  <!-- Manifest for PWA -->
  <link rel="manifest" href="/manifest.json">
  <!-- Service worker for offline support -->
  <script>
    if ('serviceWorker' in navigator) {
      navigator.serviceWorker.register('/sw.js');
    }
  </script>
  ```

**Explanation**:

- `data-*` attributes are versatile for JavaScript-driven apps.
- `srcset` and `<picture>` optimize image delivery for performance and resolution.
- `<template>` is ideal for reusable UI components in JavaScript frameworks.
- Microdata enhances search engine understanding of content.
- PWA features (manifest, service workers) enable offline functionality and app-like experiences.

---

## Cheat Codes

- **Editable Content**:

  ```html
  <!-- Make any element editable -->
  <div contenteditable="true">Edit me!</div>
  ```
- **Draggable Elements**:

  ```html
  <!-- Enable drag-and-drop -->
  <div draggable="true" ondragstart="event.dataTransfer.setData('text', 'data')">Drag me</div>
  ```
- **Conditional Hiding**:

  ```html
  <!-- Hide element without CSS -->
  <div hidden>Hidden content</div>
  ```
- **Custom Tab Order**:

  ```html
  <!-- Control tab navigation -->
  <button tabindex="2">Second</button>
  <button tabindex="1">First</button>
  ```
- **Auto-Focus Input**:

  ```html
  <!-- Focus input on page load -->
  <input type="text" autofocus>
  ```
- **Spellcheck Control**:

  ```html
  <!-- Enable/disable spellcheck -->
  <textarea spellcheck="true">Check my spelling</textarea>
  ```
- **Translation Control**:

  ```html
  <!-- Prevent machine translation -->
  <p translate="no">Do not translate</p>
  ```
- **Secure Iframe**:

  ```html
  <!-- Restrict iframe permissions -->
  <iframe src="content.html" sandbox="allow-scripts"></iframe>
  ```
- **Inline HTML in Iframe**:

  ```html
  <!-- Embed HTML directly -->
  <iframe srcdoc="<h1>Hello</h1>"></iframe>
  ```
- **Custom Element Extension**:

  ```html
  <!-- Extend built-in element -->
  <button is="custom-button">Custom</button>
  ```

**Explanation**:

- These features enhance interactivity and accessibility with minimal code.
- `contenteditable` is great for rich text editors.
- `sandbox` improves iframe security by limiting permissions.
- `tabindex` ensures logical navigation for keyboard users.

---

## HTML Tags List

A comprehensive list of commonly used HTML tags:

```
<a> <abbr> <address> <area> <article> <aside> <audio>
<b> <base> <bdi> <bdo> <blockquote> <body> <br> <button>
<canvas> <caption> <cite> <code> <col> <colgroup>
<data> <datalist> <dd> <del> <details> <dfn> <dialog> <div> <dl> <dt>
<em> <embed>
<fieldset> <figcaption> <figure> <footer> <form>
<h1> to <h6> <head> <header> <hr> <html>
<i> <iframe> <img> <input> <ins>
<kbd>
<label> <legend> <li> <link>
<main> <map> <mark> <meta> <meter>
<nav> <noscript>
<object> <ol> <optgroup> <option> <output>
<p> <param> <picture> <pre> <progress>
<q>
<rp> <rt> <ruby>
<s> <samp> <script> <section> <select> <slot> <small> <source> <span> <strong> <style> <sub> <summary> <sup> <svg>
<table> <tbody> <td> <template> <textarea> <tfoot> <th> <thead> <time> <title> <tr> <track>
<u> <ul>
<var> <video>
<wbr>
```

**Explanation**:

- Tags like `<dialog>`, `<slot>`, and `<template>` are HTML5-specific and used in modern web components.
- `<bdi>` and `<bdo>` handle bidirectional text for internationalization.
- `<meter>` and `<progress>` visualize data (e.g., task completion).

---

## HTML Attributes List

**Global Attributes**:

- `accesskey`: Keyboard shortcut (e.g., `accesskey="h"`).
- `autocapitalize`: Controls text capitalization (e.g., `autocapitalize="sentences"`).
- `class`: CSS class names.
- `contenteditable`: Makes content editable.
- `contextmenu`: Custom context menu (rarely used).
- `data-*`: Custom data attributes.
- `dir`: Text direction (`ltr`, `rtl`).
- `draggable`: Enables drag-and-drop.
- `hidden`: Hides element.
- `id`: Unique identifier.
- `lang`: Language code.
- `spellcheck`: Enables/disables spell checking.
- `style`: Inline CSS.
- `tabindex`: Tab order.
- `title`: Tooltip text.
- `translate`: Translation control.
- `role`: ARIA role for accessibility.
- `aria-*`: ARIA attributes (e.g., `aria-hidden="true"`).

**Specific Attributes**:

- `loading="lazy"|"eager"`: Image/iframe loading behavior.
- `autofocus`: Auto-focuses element on load.
- `disabled`: Disables interactive elements.
- `form`: Associates element with a form ID.
- `formaction`, `formenctype`, `formmethod`, `formnovalidate`, `formtarget`: Form-specific overrides.
- `required`, `readonly`, `multiple`: Input validation.
- `min`, `max`, `step`: Number/range input constraints.
- `pattern`: Regex for input validation.
- `placeholder`: Input hint.
- `value`, `name`, `type`: Input configuration.

**Explanation**:

- Global attributes apply to all elements, enhancing flexibility.
- ARIA attributes are essential for dynamic or JavaScript-heavy applications.
- Form-specific attributes like `pattern` and `required` reduce JavaScript validation needs.
- `loading="lazy"` is a modern performance optimization.

---

## Best Practices

- **Accessibility**:
  - Always include `alt` for images and `for` for labels.
  - Use semantic tags and ARIA attributes for screen reader compatibility.
  - Ensure keyboard navigability with `tabindex` and focus management.
- **Performance**:
  - Use `loading="lazy"` for images and iframes.
  - Minimize render-blocking resources with async/defer scripts.
  - Optimize images with `srcset` and modern formats (e.g., WebP).
- **SEO**:
  - Include meta tags (`description`, `keywords`, Open Graph).
  - Use semantic structure and microdata.
  - Ensure fast load times with proper resource optimization.
- **Security**:
  - Use `rel="noopener noreferrer"` for external links.
  - Apply `sandbox` to iframes.
  - Validate and sanitize form inputs server-side.
- **Maintainability**:
  - Avoid inline CSS/JavaScript; use external files.
  - Comment code for clarity.
  - Follow consistent naming conventions for `id` and `class`.

**Explanation**:

- Adhering to best practices ensures a robust, accessible, and performant web application.
- Accessibility is a legal and ethical requirement in many regions.
- Performance optimizations like lazy loading can significantly reduce page load times.
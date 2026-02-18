# Introduction to Web Development

**Definition:** Web development is the process of building and maintaining websites and web applications that run in a browser. It encompasses front-end (client-side), back-end (server-side), and full-stack development, combining HTML, CSS, JavaScript, and various frameworks and tools.

---

## 1. How the Web Works

**Definition:** Understanding how the web works means knowing what happens between a user typing a URL and seeing a webpage. It involves the Domain Name System (DNS) resolving domain names to IP addresses, the browser sending an HTTP request to a server, the server processing and returning a response, and the browser rendering the HTML, CSS, and JavaScript into a visible page.

### The Request-Response Cycle

**Definition:** The request-response cycle is the fundamental communication pattern of the web — a client (browser) sends an HTTP request to a server, the server processes it and returns an HTTP response containing the requested resource (HTML, JSON, image, etc.).

```
Browser                         Server
  │                               │
  │── HTTP GET /page ────────────►│
  │                               │ 1. Parse URL
  │                               │ 2. Find resource
  │                               │ 3. Generate response
  │◄─ 200 OK + HTML ─────────────│
  │                               │
  │── HTTP GET /style.css ───────►│
  │◄─ 200 OK + CSS ──────────────│
  │                               │
  │── HTTP GET /script.js ───────►│
  │◄─ 200 OK + JS ───────────────│
```

### Key Protocols

**Definition:** Web protocols are standardized rules that govern how data is transmitted over the internet. HTTP/HTTPS handles web resource transfer, DNS resolves domain names to IP addresses, TCP/IP ensures reliable data delivery, and WebSocket enables real-time bidirectional communication.

| Protocol | Purpose |
|----------|---------|
| **HTTP/HTTPS** | Transfer web resources |
| **DNS** | Translate domain names to IP addresses |
| **TCP/IP** | Reliable data transmission |
| **WebSocket** | Real-time bidirectional communication |

### HTTP Status Codes

**Definition:** HTTP status codes are three-digit numbers returned by a server in response to a client's request, indicating whether the request was successful, redirected, or resulted in an error. They are grouped into five classes: 1xx (informational), 2xx (success), 3xx (redirection), 4xx (client error), 5xx (server error).

| Range | Meaning | Examples |
|-------|---------|---------|
| 2xx | Success | 200 OK, 201 Created |
| 3xx | Redirect | 301 Moved Permanently, 304 Not Modified |
| 4xx | Client Error | 400 Bad Request, 401 Unauthorized, 404 Not Found |
| 5xx | Server Error | 500 Internal Server Error, 503 Service Unavailable |

---

## 2. Front-End vs. Back-End vs. Full-Stack

**Definition:** Web development is divided into three roles: **Front-End** (client-side) developers build what users see and interact with in the browser using HTML, CSS, and JavaScript. **Back-End** (server-side) developers build the logic, databases, and APIs that power the application. **Full-Stack** developers work across both layers, handling everything from UI to server and database.

| | Front-End | Back-End | Full-Stack |
|---|---|---|---|
| **Runs on** | Browser | Server | Both |
| **Languages** | HTML, CSS, JS | PHP, Python, Node.js, etc. | Both |
| **Concerns** | UI, UX, interactivity | Data, logic, APIs | Everything |
| **Tools** | React, Vue, Angular | Laravel, Django, Express | All of the above |

---

## 3. Core Web Vitals

**Definition:** Core Web Vitals are a set of real-world performance metrics defined by Google that measure the user experience of a web page. They focus on loading speed, interactivity, and visual stability. These metrics directly affect Google Search rankings.

### The Three Core Web Vitals

**Definition:** The three Core Web Vitals are LCP (Largest Contentful Paint) measuring loading speed, INP (Interaction to Next Paint) measuring responsiveness, and CLS (Cumulative Layout Shift) measuring visual stability. Together they form Google's primary user experience metrics that directly influence search rankings.

```
┌─────────────────────────────────────────────────────────┐
│                   Core Web Vitals                       │
│                                                         │
│  LCP (Loading)   FID/INP (Interactivity)  CLS (Stability)│
│  ─────────────   ─────────────────────    ──────────────│
│  Largest         Interaction to           Cumulative    │
│  Contentful      Next Paint               Layout        │
│  Paint                                    Shift         │
└─────────────────────────────────────────────────────────┘
```

### 1. LCP — Largest Contentful Paint

**Definition:** Largest Contentful Paint (LCP) measures how long it takes for the largest visible content element (image, video poster, or text block) to render within the viewport. A good LCP score is ≤ 2.5 seconds from when the page starts loading.

Measures **loading performance** — how long it takes for the largest visible element (image, video, or text block) to render.

| Score | LCP Value |
|-------|-----------|
| ✅ Good | ≤ 2.5 seconds |
| ⚠️ Needs Improvement | 2.5 – 4.0 seconds |
| ❌ Poor | > 4.0 seconds |

**Common LCP elements:** Hero images, `<h1>` text, video thumbnails

**How to improve LCP:**
```html
<!-- Preload the LCP image -->
<link rel="preload" as="image" href="/hero.webp" fetchpriority="high">

<!-- Use modern image formats -->
<img src="/hero.webp" alt="Hero" width="1200" height="600"
     fetchpriority="high" loading="eager">

<!-- Avoid lazy loading the LCP element -->
<!-- ❌ Don't do this for above-the-fold images -->
<img src="/hero.jpg" loading="lazy">
```

```css
/* Avoid CSS that blocks LCP rendering */
/* ✅ Inline critical CSS in <head> */
/* ✅ Defer non-critical CSS */
```

### 2. INP — Interaction to Next Paint (replaced FID in 2024)

**Definition:** Interaction to Next Paint (INP) measures the latency of all user interactions (clicks, taps, key presses) throughout the page's lifecycle, reporting the worst-case delay. A good INP score is ≤ 200 ms, meaning the browser paints a visual response within 200ms of the interaction.

Measures **interactivity** — the time from user interaction (click, tap, key press) to when the browser paints the next frame in response.

| Score | INP Value |
|-------|-----------|
| ✅ Good | ≤ 200 ms |
| ⚠️ Needs Improvement | 200 – 500 ms |
| ❌ Poor | > 500 ms |

**How to improve INP:**
```javascript
// ❌ Long task blocking the main thread
button.addEventListener('click', () => {
  const result = heavyComputation(); // blocks for 500ms
  updateUI(result);
});

// ✅ Break up long tasks
button.addEventListener('click', async () => {
  updateUI('Loading...');
  await scheduler.yield(); // yield to browser
  const result = await heavyComputation();
  updateUI(result);
});

// ✅ Move heavy work off the main thread
const worker = new Worker('heavy-task.js');
worker.postMessage(data);
worker.onmessage = (e) => updateUI(e.data);
```

### 3. CLS — Cumulative Layout Shift

**Definition:** Cumulative Layout Shift (CLS) measures the total amount of unexpected layout movement that occurs during the lifespan of a page. It quantifies how often users experience content jumping around — for example, when images load without dimensions and push text down. A good CLS score is ≤ 0.1.

Measures **visual stability** — how much the page layout shifts unexpectedly during loading (e.g., images without dimensions causing content to jump).

| Score | CLS Value |
|-------|-----------|
| ✅ Good | ≤ 0.1 |
| ⚠️ Needs Improvement | 0.1 – 0.25 |
| ❌ Poor | > 0.25 |

**How to improve CLS:**
```html
<!-- ✅ Always specify width and height on images -->
<img src="/photo.jpg" width="800" height="600" alt="Photo">

<!-- ✅ Reserve space for ads/embeds -->
<div style="min-height: 250px;">
  <!-- Ad loads here -->
</div>

<!-- ✅ Use aspect-ratio CSS for responsive images -->
<style>
img {
  width: 100%;
  height: auto;
  aspect-ratio: 16 / 9;
}
</style>
```

```javascript
// ❌ Inserting content above existing content
document.body.prepend(banner); // pushes everything down

// ✅ Reserve space or append below
document.body.append(notification);
```

### Additional Performance Metrics

**Definition:** Beyond Core Web Vitals, additional performance metrics provide a fuller picture of page speed: TTFB (Time to First Byte) measures server responsiveness, FCP (First Contentful Paint) marks when the first content appears, TTI (Time to Interactive) marks when the page is fully usable, and TBT (Total Blocking Time) measures main thread blockage.

| Metric | Measures | Good Threshold |
|--------|---------|----------------|
| **TTFB** (Time to First Byte) | Server response speed | ≤ 800 ms |
| **FCP** (First Contentful Paint) | First visible content | ≤ 1.8 s |
| **TTI** (Time to Interactive) | Fully interactive | ≤ 3.8 s |
| **TBT** (Total Blocking Time) | Main thread blocked | ≤ 200 ms |

### Measuring Core Web Vitals

**Definition:** Core Web Vitals can be measured using both lab tools (simulated, controlled conditions) and field tools (real user data). Lab tools like Lighthouse give instant feedback during development, while field tools like PageSpeed Insights and the Chrome User Experience Report (CrUX) show how real users experience the page.

```bash
# Lighthouse CLI
npm install -g lighthouse
lighthouse https://example.com --view

# PageSpeed Insights API
curl "https://www.googleapis.com/pagespeedonline/v5/runPagespeed?url=https://example.com"
```

```javascript
// Measure in JavaScript with web-vitals library
import { onLCP, onINP, onCLS } from 'web-vitals';

onLCP(metric => console.log('LCP:', metric.value));
onINP(metric => console.log('INP:', metric.value));
onCLS(metric => console.log('CLS:', metric.value));
```

**Tools for measuring:**
- [PageSpeed Insights](https://pagespeed.web.dev/) — Real-world + lab data
- [Chrome DevTools Lighthouse** tab — Lab data
- [Chrome User Experience Report (CrUX)](https://developer.chrome.com/docs/crux/) — Real-world field data
- [web.dev/measure](https://web.dev/measure/) — Online audit

### Performance Optimization Checklist

- [ ] Serve images in WebP/AVIF format
- [ ] Compress images (use `<picture>` for responsive images)
- [ ] Preload LCP image with `fetchpriority="high"`
- [ ] Defer non-critical JavaScript (`defer` or `type="module"`)
- [ ] Inline critical CSS, defer the rest
- [ ] Use a CDN for static assets
- [ ] Enable HTTP/2 or HTTP/3
- [ ] Set proper cache headers
- [ ] Minify HTML, CSS, and JavaScript
- [ ] Remove unused CSS (PurgeCSS, etc.)
- [ ] Use code splitting and lazy loading for routes

---

## 4. Web Accessibility (a11y)

**Definition:** Web accessibility (abbreviated **a11y** — "a" + 11 letters + "y") means designing and building websites that people with disabilities can use. This includes people with visual, auditory, motor, cognitive, and neurological disabilities. Accessibility is both a legal requirement (WCAG, ADA, EAA) and a moral responsibility.

### Why Accessibility Matters

**Definition:** Web accessibility matters because approximately 16% of the world's population lives with some form of disability. Beyond the moral obligation, accessibility is a legal requirement in many countries (WCAG, ADA, EAA), improves SEO through semantic HTML and alt text, and benefits all users — captions help in noisy environments, keyboard navigation helps power users.

- **~16% of the world's population** has some form of disability (WHO)
- **Legal compliance** — WCAG 2.1 AA is required by law in many countries
- **Better UX for everyone** — captions help in noisy environments, keyboard nav helps power users
- **SEO benefits** — semantic HTML and alt text improve search rankings

### WCAG Principles (POUR)

| Principle | Meaning | Example |
|-----------|---------|---------|
| **P**erceivable | Info must be presentable in ways users can perceive | Alt text for images |
| **O**perable | UI must be operable by all users | Keyboard navigation |
| **U**nderstandable | Info and UI must be understandable | Clear error messages |
| **R**obust | Content must be interpreted by assistive technologies | Semantic HTML |

**Conformance Levels:**
- **A** — Minimum (must have)
- **AA** — Standard (legal requirement in most countries)
- **AAA** — Enhanced (aspirational)

### Semantic HTML

**Definition:** Semantic HTML uses elements that carry inherent meaning about their content — `<header>`, `<nav>`, `<main>`, `<article>`, `<footer>` — rather than generic `<div>` and `<span>` elements. Screen readers, search engines, and other assistive technologies rely on semantic HTML to understand page structure and navigate content correctly.

Semantic HTML gives meaning to content, helping screen readers and other assistive technologies understand the page structure.

```html
<!-- ❌ Non-semantic — screen readers can't understand structure -->
<div class="header">
  <div class="nav">
    <div class="nav-item">Home</div>
  </div>
</div>
<div class="main">
  <div class="article">
    <div class="title">My Post</div>
    <div class="content">...</div>
  </div>
</div>
<div class="footer">...</div>

<!-- ✅ Semantic — clear structure for assistive technologies -->
<header>
  <nav aria-label="Main navigation">
    <ul>
      <li><a href="/">Home</a></li>
      <li><a href="/about">About</a></li>
    </ul>
  </nav>
</header>
<main>
  <article>
    <h1>My Post</h1>
    <p>Content here...</p>
  </article>
</main>
<footer>
  <p>&copy; 2025 My Site</p>
</footer>
```

### Heading Hierarchy

**Definition:** Heading hierarchy refers to the logical, sequential use of heading levels (`<h1>` through `<h6>`) to create a document outline. Each page should have exactly one `<h1>` (the page title), with subsequent headings nested in order without skipping levels. Screen readers use headings to navigate pages, making correct hierarchy essential for accessibility.

```html
<!-- ✅ Logical heading order — don't skip levels -->
<h1>Page Title</h1>          <!-- Only ONE h1 per page -->
  <h2>Section</h2>
    <h3>Subsection</h3>
    <h3>Another Subsection</h3>
  <h2>Another Section</h2>

<!-- ❌ Don't use headings for styling — use CSS instead -->
<h3>This looks big</h3>  <!-- Wrong: skipped h2 -->
```

### Images and Alt Text

**Definition:** Alt text (alternative text) is a textual description of an image provided via the `alt` attribute. Screen readers read alt text aloud for visually impaired users. Informative images need descriptive alt text, decorative images use `alt=""` to be skipped by screen readers, and functional images (buttons/links) describe the action they perform.

```html
<!-- ✅ Informative image — describe the content -->
<img src="chart.png" alt="Bar chart showing 40% increase in sales from Q1 to Q2 2024">

<!-- ✅ Decorative image — empty alt so screen readers skip it -->
<img src="divider.png" alt="" role="presentation">

<!-- ✅ Functional image (button/link) — describe the action -->
<a href="/home">
  <img src="logo.png" alt="Go to homepage">
</a>

<!-- ❌ Avoid — unhelpful alt text -->
<img src="photo.jpg" alt="image">
<img src="photo.jpg" alt="photo.jpg">
```

### Keyboard Navigation

**Definition:** Keyboard navigation is the ability to use a website using only a keyboard — Tab to move between interactive elements, Enter/Space to activate them, and arrow keys to navigate within components. All interactive elements must be keyboard-accessible because many users with motor disabilities, power users, and screen reader users rely on keyboard-only navigation.

All interactive elements must be reachable and operable via keyboard (Tab, Enter, Space, Arrow keys).

```html
<!-- ✅ Native elements are keyboard-accessible by default -->
<button>Click me</button>
<a href="/page">Link</a>
<input type="text">
<select>...</select>

<!-- ❌ Custom interactive elements need tabindex and keyboard handlers -->
<div class="button" onclick="doThing()">Click me</div>

<!-- ✅ Fix: use a real button or add ARIA + keyboard support -->
<div
  role="button"
  tabindex="0"
  onclick="doThing()"
  onkeydown="if(event.key==='Enter'||event.key===' ')doThing()"
>
  Click me
</div>
```

```css
/* ✅ Never remove focus indicators without replacing them */
/* ❌ Don't do this */
:focus { outline: none; }

/* ✅ Style focus visibly */
:focus-visible {
  outline: 3px solid #005fcc;
  outline-offset: 2px;
  border-radius: 2px;
}
```

### ARIA (Accessible Rich Internet Applications)

**Definition:** ARIA (Accessible Rich Internet Applications) is a set of HTML attributes (`role`, `aria-label`, `aria-hidden`, `aria-live`, etc.) that add semantic meaning to elements when native HTML semantics are insufficient — particularly for dynamic content and custom UI widgets like modals, tabs, and accordions. The first rule of ARIA: don't use ARIA if native HTML can do the job.

ARIA attributes add semantic meaning to elements when native HTML isn't sufficient.

```html
<!-- aria-label: provides an accessible name -->
<button aria-label="Close dialog">✕</button>
<nav aria-label="Breadcrumb">...</nav>

<!-- aria-labelledby: references another element as the label -->
<h2 id="modal-title">Confirm Delete</h2>
<dialog aria-labelledby="modal-title">...</dialog>

<!-- aria-describedby: references a description -->
<input type="password" aria-describedby="pw-hint">
<p id="pw-hint">Must be at least 8 characters</p>

<!-- aria-hidden: hide decorative elements from screen readers -->
<span aria-hidden="true">★★★★☆</span>
<span class="sr-only">4 out of 5 stars</span>

<!-- aria-live: announce dynamic content changes -->
<div aria-live="polite" aria-atomic="true">
  <!-- Content changes here will be announced -->
  {{ statusMessage }}
</div>

<!-- role: define the purpose of an element -->
<div role="alert">Your session is about to expire.</div>
<div role="dialog" aria-modal="true">...</div>
```

**ARIA Rules:**
1. **Don't use ARIA if native HTML can do it** — `<button>` > `role="button"`
2. **Don't change native semantics** — don't add `role="heading"` to a `<button>`
3. **All interactive ARIA elements must be keyboard operable**
4. **Don't hide visible elements** from assistive technologies without reason

### Color and Contrast

**Definition:** Color contrast refers to the difference in luminance between foreground text and its background. WCAG AA requires a contrast ratio of at least 4.5:1 for normal text and 3:1 for large text. Additionally, information must never be conveyed by color alone — always pair color with text, icons, or patterns for users with color blindness.

```css
/* WCAG AA requires: */
/* Normal text (< 18pt): contrast ratio ≥ 4.5:1 */
/* Large text (≥ 18pt or bold ≥ 14pt): contrast ratio ≥ 3:1 */
/* UI components and graphics: contrast ratio ≥ 3:1 */

/* ❌ Low contrast — fails WCAG */
color: #aaa;
background: #fff; /* ratio: ~2.3:1 */

/* ✅ Sufficient contrast */
color: #595959;
background: #fff; /* ratio: ~7:1 */
```

**Don't rely on color alone to convey information:**
```html
<!-- ❌ Color-only feedback -->
<span style="color: red">Error</span>

<!-- ✅ Color + icon + text -->
<span style="color: #d32f2f">
  <svg aria-hidden="true"><!-- error icon --></svg>
  Error: Field is required
</span>
```

### Forms and Error Handling

**Definition:** Accessible forms associate every input with a visible `<label>` element, group related inputs with `<fieldset>` and `<legend>`, provide clear and specific error messages linked to the relevant field via `aria-describedby`, and announce validation errors to screen readers using `role="alert"` or `aria-live` regions.

```html
<!-- ✅ Associate labels with inputs -->
<label for="email">Email address</label>
<input type="email" id="email" name="email"
       aria-required="true"
       aria-describedby="email-error">

<!-- ✅ Clear, specific error messages -->
<p id="email-error" role="alert">
  Please enter a valid email address (e.g., name@example.com)
</p>

<!-- ✅ Group related inputs -->
<fieldset>
  <legend>Shipping address</legend>
  <label for="street">Street</label>
  <input type="text" id="street" name="street">
  <label for="city">City</label>
  <input type="text" id="city" name="city">
</fieldset>
```

### Skip Navigation

**Definition:** Skip navigation (or "skip to main content") is a visually hidden link placed at the very top of the page that becomes visible on keyboard focus. It allows keyboard and screen reader users to bypass repetitive navigation menus and jump directly to the main content, saving them from tabbing through dozens of links on every page load.

```html
<!-- ✅ Allow keyboard users to skip repetitive navigation -->
<a href="#main-content" class="skip-link">Skip to main content</a>

<nav><!-- long navigation --></nav>

<main id="main-content">
  <!-- Page content starts here -->
</main>

<style>
.skip-link {
  position: absolute;
  top: -40px;
  left: 0;
  background: #000;
  color: #fff;
  padding: 8px;
  z-index: 100;
}
.skip-link:focus {
  top: 0;
}
</style>
```

### Screen Reader-Only Text

**Definition:** Screen reader-only text (`.sr-only`) is content that is visually hidden from sighted users but remains accessible to screen readers. It is used to provide additional context for icon-only buttons, decorative elements, or situations where the visual design conveys meaning that isn't present in the markup — without cluttering the visual interface.

```css
/* Visually hidden but accessible to screen readers */
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}
```

```html
<button>
  <svg aria-hidden="true"><!-- icon --></svg>
  <span class="sr-only">Delete item</span>
</button>
```

### Accessible Media

**Definition:** Accessible media ensures that audio and video content is usable by people with hearing or visual impairments. Videos require synchronized captions (not just subtitles) for deaf users, audio-described versions for blind users, and transcripts for both. Audio content requires transcripts. Captions must be accurate, synchronized, and include speaker identification and sound descriptions.

```html
<!-- ✅ Videos: provide captions and transcripts -->
<video controls>
  <source src="video.mp4" type="video/mp4">
  <track kind="captions" src="captions.vtt" srclang="en" label="English" default>
</video>

<!-- ✅ Audio: provide transcripts -->
<audio controls src="podcast.mp3"></audio>
<a href="transcript.html">Read transcript</a>
```

### Testing Accessibility

**Definition:** Accessibility testing combines automated tools (which catch ~30–40% of issues) with manual testing. Automated tools like axe-core and Lighthouse scan for common violations. Manual testing includes keyboard-only navigation, screen reader testing (NVDA, VoiceOver, TalkBack), zooming to 200%, and disabling CSS to verify logical content order.

**Automated tools (catch ~30-40% of issues):**
```bash
# axe-core CLI
npm install -g @axe-core/cli
axe https://example.com

# Lighthouse accessibility audit
lighthouse https://example.com --only-categories=accessibility
```

**Browser extensions:**
- **axe DevTools** — Most comprehensive automated checker
- **WAVE** — Visual feedback overlay
- **Colour Contrast Analyser** — Check color ratios

**Manual testing:**
1. **Keyboard-only navigation** — Tab through the entire page
2. **Screen reader testing** — NVDA (Windows), VoiceOver (Mac/iOS), TalkBack (Android)
3. **Zoom to 200%** — Ensure layout doesn't break
4. **Disable CSS** — Check if content is still readable and logical

### Accessibility Checklist

- [ ] All images have meaningful alt text (or `alt=""` if decorative)
- [ ] Heading hierarchy is logical (h1 → h2 → h3)
- [ ] All form inputs have associated `<label>` elements
- [ ] Color contrast meets WCAG AA (4.5:1 for normal text)
- [ ] Information is not conveyed by color alone
- [ ] All interactive elements are keyboard accessible
- [ ] Focus indicators are visible
- [ ] Skip navigation link is present
- [ ] Page has a descriptive `<title>`
- [ ] Language is set on `<html lang="en">`
- [ ] Error messages are specific and associated with inputs
- [ ] Videos have captions; audio has transcripts
- [ ] No content flashes more than 3 times per second (seizure risk)

---

## 5. Browser DevTools

**Definition:** Browser DevTools (Developer Tools) are built-in browser utilities that allow developers to inspect, debug, and optimize web pages in real time. They provide panels for examining the DOM and CSS, monitoring network requests, profiling JavaScript performance, auditing accessibility, and testing responsive layouts — all without leaving the browser.

### Key Panels

**Definition:** Browser DevTools panels are specialized views for different aspects of web development: Elements for live DOM/CSS inspection, Console for JavaScript execution and error logging, Network for monitoring HTTP requests and response payloads, Performance for profiling runtime bottlenecks, Lighthouse for automated audits, and Application for inspecting storage and service workers.

| Panel | Use |
|-------|-----|
| **Elements** | Inspect and edit HTML/CSS live |
| **Console** | Run JavaScript, view logs and errors |
| **Network** | Monitor HTTP requests, response times, payloads |
| **Performance** | Record and analyze runtime performance |
| **Lighthouse** | Audit performance, accessibility, SEO |
| **Application** | Inspect cookies, localStorage, Service Workers |

### Useful Shortcuts (Chrome DevTools)

| Shortcut | Action |
|----------|--------|
| `F12` / `Ctrl+Shift+I` | Open DevTools |
| `Ctrl+Shift+C` | Inspect element |
| `Ctrl+Shift+M` | Toggle device toolbar (mobile view) |
| `Ctrl+P` | Open file by name |
| `Ctrl+Shift+P` | Command palette |

---

## 6. Version Control Basics

**Definition:** Version control is a system that records changes to files over time so you can recall specific versions later. **Git** is the most widely used version control system — it tracks every change, enables collaboration through branching and merging, and integrates with platforms like GitHub and GitLab for remote storage and team workflows.

Every web project should use Git from day one.

```bash
git init                    # Initialize a repository
git add .                   # Stage all changes
git commit -m "feat: add homepage"  # Commit with message
git push origin main        # Push to remote
```

See the **Git & GitHub** documentation for a complete guide.

---

## 7. Development Workflow

**Definition:** A development workflow is the structured set of tools, processes, and conventions a developer uses to build, test, and deploy web projects efficiently. It typically includes a code editor, version control (Git), a package manager (npm), browser DevTools for debugging, and a deployment platform — all working together to streamline the development cycle.

### Typical Project Structure

```
my-project/
├── index.html          # Entry point
├── css/
│   └── style.css
├── js/
│   └── main.js
├── images/
├── .gitignore
└── README.md
```

### Tools Every Web Developer Uses

| Category | Tools |
|----------|-------|
| **Code Editor** | VS Code, WebStorm |
| **Version Control** | Git, GitHub/GitLab |
| **Package Manager** | npm, pnpm, Yarn |
| **Browser** | Chrome DevTools, Firefox DevTools |
| **Design** | Figma |
| **API Testing** | Postman, Insomnia |
| **Deployment** | Vercel, Netlify, GitHub Pages |

---

**Resources:**
- [MDN Web Docs](https://developer.mozilla.org/) — Comprehensive web reference
- [web.dev](https://web.dev/) — Google's web best practices
- [a11yproject.com](https://www.a11yproject.com/) — Accessibility resources
- [WCAG 2.1 Guidelines](https://www.w3.org/TR/WCAG21/) — Official accessibility standard
- [PageSpeed Insights](https://pagespeed.web.dev/) — Core Web Vitals measurement

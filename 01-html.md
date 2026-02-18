# 🏗️ HTML - HyperText Markup Language

> The foundation of every web page. HTML provides the structure and semantic meaning to web content.

---

## 📊 HTML Document Structure - UML Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                    DOCUMENT TYPE                            │
│                  <!DOCTYPE html>                            │
└───────────────────────┬─────────────────────────────────────┘
                        │
                        ▼
┌─────────────────────────────────────────────────────────────┐
│  ROOT ELEMENT                                               │
│  <html lang="en">                                           │
│  ├─ Attribute: lang="en" (document language)                │
│  └─ Contains: All page content                              │
└───────────────────────┬─────────────────────────────────────┘
                        │
        ┌───────────────┴───────────────┐
        ▼                               ▼
┌───────────────────────┐   ┌───────────────────────────────┐
│     HEAD SECTION      │   │         BODY SECTION          │
│   <head>...</head>    │   │        <body>...</body>       │
│                       │   │                               │
│ ├─ Meta Information   │   │ ├─ Header (<header>)          │
│ │  ├─ charset         │   │ ├─ Navigation (<nav>)         │
│ │  ├─ viewport        │   │ ├─ Main Content (<main>)      │
│ │  └─ description     │   │ │  ├─ Articles (<article>)    │
│ ├─ Title              │   │ │  ├─ Sections (<section>)    │
│ ├─ Links (CSS)        │   │ │  └─ Asides (<aside>)        │
│ └─ Scripts (async)    │   │ └─ Footer (<footer>)          │
└───────────────────────┘   └───────────────────────────────┘
```

---

## 1. Introduction to HTML

### Definition
**HTML (HyperText Markup Language)** is the standard markup language for documents designed to be displayed in a web browser. It uses a system of **tags** and **attributes** to define the structure and content of web pages.

### The Role of HTML in Web Development

**Definition:** HTML (HyperText Markup Language) is the backbone of every web page — it provides the semantic structure and content that browsers render. HTML defines *what* content exists (headings, paragraphs, images, links), while CSS controls *how* it looks and JavaScript controls *how* it behaves. Without HTML, there is no web page.

```
┌────────────────────────────────────────────────────────────┐
│                  WEB PAGE LAYERS                           │
├────────────────────────────────────────────────────────────┤
│  HTML (Structure)  →  Defines WHAT content exists          │
│       ↓                                                    │
│  CSS (Presentation) →  Defines HOW it looks                │
│       ↓                                                    │
│  JavaScript (Behavior) → Defines HOW it behaves            │
└────────────────────────────────────────────────────────────┘
```

### Basic Document Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Page Title</title>
    <meta name="description" content="Page description for SEO">
</head>
<body>
    <!-- Visible content goes here -->
</body>
</html>
```

**Key Elements:**
- `<!DOCTYPE html>` - Declares HTML5 document type
- `<html>` - Root element of the page
- `<head>` - Contains metadata, title, links to CSS/JS files
- `<body>` - Contains all visible content
- `lang="en"` - Specifies language for accessibility and SEO
- `charset="UTF-8"` - Character encoding for international support

---

## 2. Text Elements

### Definition
**Text Elements** are HTML tags used to structure and format text content semantically. They provide meaning to the content beyond visual presentation.

### Element Hierarchy Diagram

```
TEXT CONTENT HIERARCHY
│
├── Headings (h1-h6)
│   ├── h1: Document Title (ONE per page)
│   ├── h2: Major Sections
│   ├── h3: Subsections
│   ├── h4: Sub-subsections
│   ├── h5: Minor headings
│   └── h6: Smallest headings
│
├── Paragraphs (<p>)
│   └── Block of text content
│
├── Inline Text Semantics
│   ├── <strong> - Strong importance
│   ├── <em> - Emphasis
│   ├── <mark> - Highlighted text
│   ├── <del> - Deleted text
│   ├── <ins> - Inserted text
│   ├── <sub> - Subscript
│   ├── <sup> - Superscript
│   ├── <code> - Code fragment
│   └── <small> - Side comments
│
└── Line Breaks
    ├── <br> - Line break
    └── <hr> - Thematic break
```

### Headings

**Definition:** HTML headings (`<h1>` through `<h6>`) define the hierarchical structure of a page's content. `<h1>` is the most important (used once per page as the main title), and `<h6>` is the least important. Headings are critical for SEO (search engines use them to understand content hierarchy) and accessibility (screen readers use them for navigation).

```html
<!-- Six levels of headings -->
<h1>Main Title (Most Important - One per page)</h1>
<h2>Section Heading</h2>
<h3>Subsection Heading</h3>
<h4>Sub-subsection</h4>
<h5>Smaller Heading</h5>
<h6>Smallest Heading</h6>
```

### Paragraphs and Text Formatting

```html
<!-- Paragraphs -->
<p>This is a paragraph of text. It automatically wraps and maintains spacing.</p>

<!-- Line break -->
<p>This is line one.<br>This is line two.</p>

<!-- Horizontal rule -->
<hr>

<!-- Semantic text elements -->
<p>
    <strong>Important text</strong> (bold + semantic importance)<br>
    <em>Emphasized text</em> (italic + emphasis)<br>
    <mark>Highlighted text</mark><br>
    <del>Deleted text</del> (strikethrough)<br>
    <ins>Inserted text</ins> (underline)<br>
    <sub>Subscript</sub> and <sup>Superscript</sup><br>
    <small>Small text</small> (fine print)<br>
    <code>Inline code</code>
</p>
```

### Block vs Inline Elements

**Definition:**
- **Block Elements**: Elements that start on a new line and take up the full width available
- **Inline Elements**: Elements that do not start on a new line and only take up as much width as necessary

```
┌─────────────────────────────────────────────────────────┐
│  BLOCK ELEMENT FLOW                                     │
│  ┌─────────────────────────────────────────────────┐    │
│  │  <div> - Block container                        │    │
│  └─────────────────────────────────────────────────┘    │
│  ┌─────────────────────────────────────────────────┐    │
│  │  <p> - Paragraph                                │    │
│  └─────────────────────────────────────────────────┘    │
│  ┌─────────────────────────────────────────────────┐    │
│  │  <h1> - Heading                                 │    │
│  └─────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│  INLINE ELEMENT FLOW                                    │
│  Text <span>inline</span> <a>link</a> <strong>bold</strong>│
│  All on same line, only take needed space               │
└─────────────────────────────────────────────────────────┘
```

**Block Elements:** Start on new line, take full width
- `<div>`, `<p>`, `<h1>-<h6>`, `<section>`, `<article>`

**Inline Elements:** Stay in flow, only take needed width
- `<span>`, `<a>`, `<strong>`, `<em>`, `<img>`, `<input>`

---

## 3. Links & Navigation

### Definition
**Links (Anchors)** create hyperlinks between web pages or resources using the `<a>` tag. The `href` attribute specifies the destination URL.

### Link Types Diagram

```
LINK TYPES
│
├── Internal Links
│   ├── Same Page: href="#section-id"
│   ├── Other Page: href="about.html"
│   └── Other Directory: href="/folder/page.html"
│
├── External Links
│   ├── href="https://example.com"
│   └── Attributes: target="_blank", rel="noopener"
│
├── Email Links
│   └── href="mailto:email@example.com"
│
├── Phone Links
│   └── href="tel:+1234567890"
│
└── Download Links
    └── href="file.pdf" download
```

```html
<!-- External link -->
<a href="https://www.example.com">Visit Example</a>

<!-- Open in new tab (with security attributes) -->
<a href="https://example.com" target="_blank" rel="noopener noreferrer">
    Open in New Tab
</a>

<!-- Internal page link -->
<a href="about.html">About Page</a>
<a href="contact.html">Contact Us</a>

<!-- Anchor link (to section on same page) -->
<a href="#section1">Jump to Section 1</a>
<a href="#contact">Go to Contact</a>

<!-- Target sections -->
<section id="section1">
    <h2>Section 1</h2>
    <p>Content here...</p>
</section>

<section id="contact">
    <h2>Contact Us</h2>
</section>

<!-- Email link -->
<a href="mailto:someone@example.com">Send Email</a>
<a href="mailto:help@example.com?subject=Support Request&body=Hello,">
    Email with Subject
</a>

<!-- Phone link -->
<a href="tel:+1234567890">Call Us</a>

<!-- Download link -->
<a href="document.pdf" download>Download PDF</a>
<a href="image.jpg" download="photo.jpg">Download with Custom Name</a>
```

---

## 4. Images & Media

### Definition
**Media Elements** embed visual and audio content into web pages, including images, audio, video, and external content.

### Media Types Diagram

```
MEDIA ELEMENTS
│
├── Images (<img>)
│   ├── Static: src="photo.jpg"
│   ├── Responsive: srcset for different sizes
│   └── Art Direction: <picture> element
│
├── Audio (<audio>)
│   ├── Controls: play, pause, volume
│   └── Multiple sources for compatibility
│
├── Video (<video>)
│   ├── Poster image
│   ├── Subtitles (<track>)
│   └── Multiple formats (mp4, webm)
│
└── Embedded (<iframe>)
    ├── YouTube videos
    ├── Maps
    └── Other websites
```

```html
<!-- Basic image -->
<img src="photo.jpg" alt="Descriptive text for accessibility">

<!-- Complete image with all attributes -->
<img src="images/photo.jpg" 
     alt="Golden retriever playing in park"
     width="800" 
     height="600"
     loading="lazy"
     decoding="async">

<!-- Responsive images with srcset -->
<img srcset="photo-320.jpg 320w,
             photo-768.jpg 768w,
             photo-1200.jpg 1200w"
     sizes="(max-width: 600px) 320px,
            (max-width: 1000px) 768px,
            1200px"
     src="photo-1200.jpg"
     alt="Responsive image example">

<!-- Picture element for art direction -->
<picture>
    <source srcset="large.jpg" media="(min-width: 1024px)">
    <source srcset="medium.jpg" media="(min-width: 768px)">
    <img src="small.jpg" alt="Responsive image">
</picture>

<!-- Figure with caption -->
<figure>
    <img src="chart.png" alt="Annual sales chart">
    <figcaption>Figure 1: Company sales increased by 25% in 2024</figcaption>
</figure>

<!-- Audio -->
<audio controls>
    <source src="music.mp3" type="audio/mpeg">
    <source src="music.ogg" type="audio/ogg">
    <p>Your browser does not support audio. <a href="music.mp3">Download</a></p>
</audio>

<!-- Audio with options -->
<audio controls autoplay muted loop preload="auto">
    <source src="background.mp3" type="audio/mpeg">
</audio>

<!-- Video -->
<video width="640" height="360" controls poster="thumbnail.jpg">
    <source src="movie.mp4" type="video/mp4">
    <source src="movie.webm" type="video/webm">
    <track src="subtitles.vtt" kind="subtitles" srclang="en" label="English">
    <track src="captions.vtt" kind="captions" srclang="en" label="English CC">
    Your browser does not support the video tag.
</video>

<!-- Video with all options -->
<video controls
        width="100%"
        height="auto"
        poster="preview.jpg"
        preload="metadata"
        autoplay
        muted
        loop
        playsinline>
    <source src="video.mp4" type="video/mp4">
</video>

<!-- Iframe for embedding -->
<iframe src="https://www.youtube.com/embed/VIDEO_ID" 
        width="560" 
        height="315"
        title="Video Title"
        frameborder="0"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
        allowfullscreen>
</iframe>
```

---

## 5. Lists

### Definition
**Lists** organize content into ordered (numbered), unordered (bulleted), or descriptive formats to improve readability and structure.

### List Types Diagram

```
LIST TYPES
│
├── Unordered Lists (<ul>)
│   ├── Default: Disc bullets
│   ├── Can be nested
│   └── Used for: Menus, groups of items
│
├── Ordered Lists (<ol>)
│   ├── Default: Numbers
│   ├── Attributes: type, start, reversed
│   └── Used for: Steps, rankings, sequences
│
└── Description Lists (<dl>)
    ├── <dt> - Description Term
    ├── <dd> - Description Details
    └── Used for: Glossaries, key-value pairs
```

```html
<!-- Unordered list (bulleted) -->
<ul>
    <li>Apples</li>
    <li>Bananas</li>
    <li>Oranges</li>
</ul>

<!-- Ordered list (numbered) -->
<ol>
    <li>First step</li>
    <li>Second step</li>
    <li>Third step</li>
</ol>

<!-- Ordered list with attributes -->
<ol type="A" start="5">
    <li>Item E</li>
    <li>Item F</li>
    <li value="10">Item J</li>
</ol>

<ol reversed>
    <li>Third (displayed as 3)</li>
    <li>Second (displayed as 2)</li>
    <li>First (displayed as 1)</li>
</ol>

<!-- Nested lists -->
<ul>
    <li>Fruits
        <ul>
            <li>Apples
                <ul>
                    <li>Red Delicious</li>
                    <li>Granny Smith</li>
                </ul>
            </li>
            <li>Bananas</li>
        </ul>
    </li>
    <li>Vegetables</li>
</ul>

<!-- Description list (key-value pairs) -->
<dl>
    <dt>HTML</dt>
    <dd>HyperText Markup Language - the standard markup language for web pages</dd>
    
    <dt>CSS</dt>
    <dd>Cascading Style Sheets - used for styling HTML elements</dd>
    
    <dt>JavaScript</dt>
    <dd>A programming language that enables interactive web pages</dd>
</dl>
```

---

## 6. Tables

### Definition
**Tables** display tabular data in rows and columns. They consist of table cells organized into rows, with optional header and footer sections for better structure and accessibility.

### Table Structure Diagram

```
┌─────────────────────────────────────────────────────────┐
│                    <table>                              │
├─────────────────────────────────────────────────────────┤
│  <caption>Table Title</caption>                         │
├─────────────────────────────────────────────────────────┤
│  <thead> (Table Head)                                   │
│  ┌─────────────────────────────────────────────────┐    │
│  │  <tr> (Table Row)                               │    │
│  │  ├─ <th scope="col">Column 1</th>              │    │
│  │  ├─ <th scope="col">Column 2</th>              │    │
│  │  └─ <th scope="col">Column 3</th>              │    │
│  └─────────────────────────────────────────────────┘    │
├─────────────────────────────────────────────────────────┤
│  <tbody> (Table Body)                                   │
│  ┌─────────────────────────────────────────────────┐    │
│  │  <tr>                                           │    │
│  │  ├─ <td>Data 1</td>                            │    │
│  │  ├─ <td>Data 2</td>                            │    │
│  │  └─ <td>Data 3</td>                            │    │
│  └─────────────────────────────────────────────────┘    │
│  ┌─────────────────────────────────────────────────┐    │
│  │  <tr>                                           │    │
│  │  ├─ <td>Data 4</td>                            │    │
│  │  ├─ <td>Data 5</td>                            │    │
│  │  └─ <td>Data 6</td>                            │    │
│  └─────────────────────────────────────────────────┘    │
├─────────────────────────────────────────────────────────┤
│  <tfoot> (Table Footer)                                 │
│  ┌─────────────────────────────────────────────────┐    │
│  │  <tr>                                           │    │
│  │  └─ <td colspan="3">Footer content</td>        │    │
│  └─────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────┘
```

```html
<!-- Basic table structure -->
<table>
    <caption>Employee Information</caption>
    <thead>
        <tr>
            <th scope="col">Name</th>
            <th scope="col">Department</th>
            <th scope="col">Salary</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>John Doe</td>
            <td>Engineering</td>
            <td>$80,000</td>
        </tr>
        <tr>
            <td>Jane Smith</td>
            <td>Marketing</td>
            <td>$65,000</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="2">Total Employees</td>
            <td>2</td>
        </tr>
    </tfoot>
</table>

<!-- Complex table with spanning -->
<table>
    <thead>
        <tr>
            <th rowspan="2">Product</th>
            <th colspan="2">Sales</th>
            <th rowspan="2">Total</th>
        </tr>
        <tr>
            <th>Q1</th>
            <th>Q2</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row">Product A</th>
            <td>$10,000</td>
            <td>$15,000</td>
            <td>$25,000</td>
        </tr>
        <tr>
            <th scope="row">Product B</th>
            <td>$8,000</td>
            <td>$12,000</td>
            <td>$20,000</td>
        </tr>
    </tbody>
</table>
```

---

## 7. Forms

### Definition
**Forms** collect user input through various controls (text fields, buttons, checkboxes, etc.) and submit data to a server for processing using the `<form>` element.

### Form Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                     <form>                                  │
│  Attributes: action, method, enctype                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐    ┌──────────────────────────┐           │
│  │ <label>     │    │ <input>                  │           │
│  │ for="name"> │───→│ type="text"              │           │
│  │ Name:       │    │ id="name"                │           │
│  └─────────────┘    │ name="name"              │           │
│                     │ required                 │           │
│                     └──────────────────────────┘           │
│                                                             │
│  ┌─────────────┐    ┌──────────────────────────┐           │
│  │ <label>     │    │ <input>                  │           │
│  │ for="email">│───→│ type="email"             │           │
│  │ Email:      │    │ id="email"               │           │
│  └─────────────┘    │ name="email"             │           │
│                     │ placeholder="...@..."    │           │
│                     └──────────────────────────┘           │
│                                                             │
│  ┌─────────────┐    ┌──────────────────────────┐           │
│  │ <fieldset>  │    │ <input type="radio">     │           │
│  │ <legend>    │    │   name="gender"          │           │
│  │ Gender:     │    │   value="male"           │           │
│  └─────────────┘    │   id="male"              │           │
│                     └──────────────────────────┘           │
│                     ┌──────────────────────────┐           │
│                     │ <label for="male">Male   │           │
│                     └──────────────────────────┘           │
│                                                             │
│  ┌──────────────────────────────────────────────────┐      │
│  │ <button type="submit">Submit</button>            │      │
│  │ <button type="reset">Reset</button>              │      │
│  └──────────────────────────────────────────────────┘      │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Input Types Diagram

```
INPUT TYPES
│
├── Text Input
│   ├── type="text" - Single line text
│   ├── type="email" - Email validation
│   ├── type="password" - Masked input
│   ├── type="search" - Search field
│   ├── type="url" - URL validation
│   └── type="tel" - Telephone
│
├── Numeric Input
│   ├── type="number" - Numeric values
│   └── type="range" - Slider control
│
├── Date/Time Input
│   ├── type="date" - Date picker
│   ├── type="time" - Time picker
│   ├── type="datetime-local" - Both
│   ├── type="month" - Month/Year
│   └── type="week" - Week picker
│
├── Selection Input
│   ├── type="checkbox" - Multiple selection
│   ├── type="radio" - Single selection
│   └── <select> - Dropdown list
│
├── File Input
│   └── type="file" - File upload
│
├── Special Input
│   ├── type="color" - Color picker
│   ├── type="hidden" - Hidden data
│   └── type="submit" - Form submission
│
└── Text Area
    └── <textarea> - Multi-line text
```

```html
<!-- Complete form example -->
<form action="/submit" method="POST" enctype="multipart/form-data" novalidate>
    
    <!-- Text input -->
    <div>
        <label for="username">Username:</label>
        <input type="text" 
               id="username" 
               name="username" 
               required 
               minlength="3" 
               maxlength="20"
               pattern="[a-zA-Z0-9_]+"
               placeholder="Enter username"
               autocomplete="username">
    </div>
    
    <!-- Email input -->
    <div>
        <label for="email">Email:</label>
        <input type="email" 
               id="email" 
               name="email" 
               required
               placeholder="you@example.com"
               autocomplete="email">
    </div>
    
    <!-- Password input -->
    <div>
        <label for="password">Password:</label>
        <input type="password" 
               id="password" 
               name="password" 
               required
               minlength="8"
               pattern="(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{8,}"
               title="Must contain at least one number, one uppercase and lowercase letter, and at least 8 characters"
               autocomplete="new-password">
    </div>
    
    <!-- Number input -->
    <div>
        <label for="age">Age:</label>
        <input type="number" 
               id="age" 
               name="age" 
               min="18" 
               max="120"
               step="1">
    </div>
    
    <!-- Range slider -->
    <div>
        <label for="volume">Volume:</label>
        <input type="range" 
               id="volume" 
               name="volume" 
               min="0" 
               max="100" 
               value="50">
        <span id="volume-value">50</span>
    </div>
    
    <!-- Date input -->
    <div>
        <label for="birthdate">Birth Date:</label>
        <input type="date" 
               id="birthdate" 
               name="birthdate"
               min="1900-01-01"
               max="2024-12-31">
    </div>
    
    <!-- Time input -->
    <div>
        <label for="appointment">Appointment Time:</label>
        <input type="time" 
               id="appointment" 
               name="appointment">
    </div>
    
    <!-- Color picker -->
    <div>
        <label for="favcolor">Favorite Color:</label>
        <input type="color" 
               id="favcolor" 
               name="favcolor" 
               value="#ff0000">
    </div>
    
    <!-- File upload -->
    <div>
        <label for="avatar">Profile Picture:</label>
        <input type="file" 
               id="avatar" 
               name="avatar"
               accept="image/*"
               multiple>
    </div>
    
    <!-- Textarea -->
    <div>
        <label for="bio">Bio:</label>
        <textarea id="bio" 
                  name="bio" 
                  rows="4" 
                  cols="50"
                  maxlength="500"
                  placeholder="Tell us about yourself..."></textarea>
    </div>
    
    <!-- Select dropdown -->
    <div>
        <label for="country">Country:</label>
        <select id="country" name="country" required>
            <option value="">Select a country</option>
            <optgroup label="North America">
                <option value="us">United States</option>
                <option value="ca">Canada</option>
                <option value="mx">Mexico</option>
            </optgroup>
            <optgroup label="Europe">
                <option value="uk">United Kingdom</option>
                <option value="de">Germany</option>
                <option value="fr">France</option>
            </optgroup>
        </select>
    </div>
    
    <!-- Datalist (autocomplete suggestions) -->
    <div>
        <label for="browser">Preferred Browser:</label>
        <input list="browsers" id="browser" name="browser">
        <datalist id="browsers">
            <option value="Chrome">
            <option value="Firefox">
            <option value="Safari">
            <option value="Edge">
            <option value="Opera">
        </datalist>
    </div>
    
    <!-- Radio buttons -->
    <fieldset>
        <legend>Gender:</legend>
        <input type="radio" id="male" name="gender" value="male" required>
        <label for="male">Male</label>
        
        <input type="radio" id="female" name="gender" value="female">
        <label for="female">Female</label>
        
        <input type="radio" id="other" name="gender" value="other">
        <label for="other">Other</label>
        
        <input type="radio" id="prefer-not" name="gender" value="prefer-not">
        <label for="prefer-not">Prefer not to say</label>
    </fieldset>
    
    <!-- Checkboxes -->
    <fieldset>
        <legend>Interests:</legend>
        <input type="checkbox" id="coding" name="interests" value="coding">
        <label for="coding">Coding</label>
        
        <input type="checkbox" id="music" name="interests" value="music">
        <label for="music">Music</label>
        
        <input type="checkbox" id="sports" name="interests" value="sports">
        <label for="sports">Sports</label>
        
        <input type="checkbox" id="reading" name="interests" value="reading">
        <label for="reading">Reading</label>
    </fieldset>
    
    <!-- Hidden field -->
    <input type="hidden" name="form_id" value="registration-001">
    
    <!-- Submit and reset buttons -->
    <div>
        <button type="submit">Register</button>
        <button type="reset">Reset Form</button>
        <button type="button" onclick="saveDraft()">Save Draft</button>
    </div>
    
</form>
```

---

## 8. Semantic HTML5 Elements

### Definition
**Semantic Elements** clearly describe their meaning to both browsers and developers (e.g., `<header>`, `<nav>`, `<main>`, `<article>`), improving accessibility, SEO, and code readability compared to generic `<div>` elements.

### Semantic Page Structure Diagram

```
┌────────────────────────────────────────────────────────────────┐
│                        <body>                                  │
├────────────────────────────────────────────────────────────────┤
│  ┌────────────────────────────────────────────────────────┐   │
│  │                     <header>                           │   │
│  │  ┌──────────────────────────────────────────────────┐  │   │
│  │  │                      <nav>                       │  │   │
│  │  │  Logo │ Home │ About │ Services │ Contact        │  │   │
│  │  └──────────────────────────────────────────────────┘  │   │
│  │                                                         │   │
│  │  ┌──────────────────────────────────────────────────┐  │   │
│  │  │                 Hero Section                      │  │   │
│  │  │  <h1>Main Title</h1>                              │  │   │
│  │  │  <p>Description</p>                               │  │   │
│  │  └──────────────────────────────────────────────────┘  │   │
│  └────────────────────────────────────────────────────────┘   │
│                                                               │
│  ┌────────────────────────────────────────────────────────┐   │
│  │                      <main>                            │   │
│  │                                                         │   │
│  │  ┌──────────────────────────────────────────────────┐  │   │
│  │  │                  <article>                        │  │   │
│  │  │  <header>                                         │  │   │
│  │  │    <h2>Blog Post Title</h2>                       │  │   │
│  │  │    <time>Jan 15, 2024</time>                      │  │   │
│  │  │  </header>                                        │  │   │
│  │  │                                                   │  │   │
│  │  │  <section>                                        │  │   │
│  │  │    <h3>Introduction</h3>                          │  │   │
│  │  │    <p>Content...</p>                              │  │   │
│  │  │  </section>                                       │  │   │
│  │  │                                                   │  │   │
│  │  │  <section>                                        │  │   │
│  │  │    <h3>Conclusion</h3>                            │  │   │
│  │  │    <p>More content...</p>                         │  │   │
│  │  │  </section>                                       │  │   │
│  │  │                                                   │  │   │
│  │  │  <footer>                                         │  │   │
│  │  │    <p>Author: John Doe</p>                        │  │   │
│  │  │    <p>Tags: <mark>HTML</mark></p>                 │  │   │
│  │  │  </footer>                                        │  │   │
│  │  └──────────────────────────────────────────────────┘  │   │
│  │                                                         │   │
│  └────────────────────────────────────────────────────────┘   │
│                                                               │
│  ┌──────────┐  ┌──────────────────────────────────────────┐   │
│  │  <aside> │  │         Related Content                   │   │
│  │ Sidebar  │  │  • Related Articles                       │   │
│  │          │  │  • Categories                             │   │
│  │  • Links │  │  • Tags                                   │   │
│  │  • Ads   │  │                                           │   │
│  └──────────┘  └──────────────────────────────────────────┘   │
│                                                               │
│  ┌────────────────────────────────────────────────────────┐   │
│  │                     <footer>                           │   │
│  │  ┌──────────────────────────────────────────────────┐  │   │
│  │  │  &copy; 2024 Company                             │  │   │
│  │  │  <address>                                       │  │   │
│  │  │    <a href="mailto:info@example.com">Email</a>   │  │   │
│  │  │  </address>                                      │  │   │
│  │  └──────────────────────────────────────────────────┘  │   │
│  └────────────────────────────────────────────────────────┘   │
└────────────────────────────────────────────────────────────────┘
```

### Semantic Elements Reference

```
SEMANTIC HTML5 ELEMENTS
│
├── Document Structure
│   ├── <header> - Introductory content (logo, nav, headings)
│   ├── <nav> - Navigation links
│   ├── <main> - Main content (ONE per page)
│   ├── <footer> - Footer information
│   └── <section> - Thematic grouping
│
├── Content Elements
│   ├── <article> - Self-contained content (blog post, news)
│   ├── <aside> - Tangentially related content (sidebar)
│   ├── <figure> - Self-contained content (image, diagram)
│   └── <figcaption> - Caption for figure
│
├── Text-level Semantics
│   ├── <time> - Date/time with datetime attribute
│   ├── <mark> - Highlighted text
│   ├── <address> - Contact information
│   ├── <details> - Disclosure widget
│   └── <summary> - Summary for details
│
└── Interactive
    ├── <dialog> - Dialog box/modal
    └── <menu> - Toolbar/menu
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Semantic HTML Example</title>
</head>
<body>
    
    <a href="#main-content" class="skip-link">Skip to main content</a>
    
    <header>
        <nav aria-label="Main navigation">
            <ul>
                <li><a href="/">Home</a></li>
                <li><a href="/about">About</a></li>
                <li><a href="/services">Services</a></li>
                <li><a href="/contact">Contact</a></li>
            </ul>
        </nav>
    </header>
    
    <main id="main-content">
        
        <article>
            <header>
                <h2>Blog Post Title</h2>
                <p>Published on <time datetime="2024-01-15">January 15, 2024</time></p>
            </header>
            
            <section>
                <h3>Introduction</h3>
                <p>Article content here...</p>
            </section>
            
            <section>
                <h3>Conclusion</h3>
                <p>More content...</p>
            </section>
            
            <footer>
                <p>Written by Author Name</p>
                <p>Tags: <mark>HTML</mark>, <mark>CSS</mark></p>
            </footer>
        </article>
        
        <aside>
            <h3>Related Articles</h3>
            <ul>
                <li><a href="#">Related Post 1</a></li>
                <li><a href="#">Related Post 2</a></li>
            </ul>
            
            <h3>Author Bio</h3>
            <p>Information about the author...</p>
        </aside>
        
    </main>
    
    <section aria-labelledby="services-heading">
        <h2 id="services-heading">Our Services</h2>
        <p>Description of services...</p>
    </section>
    
    <footer>
        <p>&copy; 2024 My Website. All rights reserved.</p>
        <address>
            Contact: <a href="mailto:info@example.com">info@example.com</a><br>
            Phone: <a href="tel:+1234567890">(123) 456-7890</a>
        </address>
    </footer>
    
    <details>
        <summary>Click to learn more</summary>
        <p>This content is hidden by default and can be expanded.</p>
    </details>
    
    <dialog id="myDialog">
        <h2>Modal Title</h2>
        <p>This is a native HTML dialog element.</p>
        <button onclick="document.getElementById('myDialog').close()">Close</button>
    </dialog>
    
    <button onclick="document.getElementById('myDialog').showModal()">Open Dialog</button>
    
</body>
</html>
```

---

## 9. HTML Best Practices

### Definition
**HTML Best Practices** are a set of guidelines and conventions that ensure your HTML code is clean, accessible, maintainable, and standards-compliant. Following best practices improves SEO, cross-browser compatibility, accessibility for screen readers, and makes code easier to maintain and collaborate on.

### DO's ✅
- Use semantic elements (`<header>`, `<nav>`, `<main>`, `<article>`, `<footer>`)
- Include `alt` text for all images
- Use proper heading hierarchy (don't skip levels)
- Validate your HTML (W3C Validator)
- Include `lang` attribute on `<html>`
- Use `label` elements with form inputs
- Include `meta charset="UTF-8"` and viewport meta tag
- Use lowercase for tags and attributes

### DON'Ts ❌
- Don't use `<br>` for spacing (use CSS)
- Don't use tables for layout (use CSS Grid/Flexbox)
- Don't use inline styles (use CSS classes)
- Don't skip heading levels (h1 → h3)
- Don't forget closing tags (except for void elements)
- Don't use deprecated tags (`<font>`, `<center>`, `<marquee>`)

### Accessibility Tips ♿
- Use `alt` text that describes the image purpose
- Ensure sufficient color contrast
- Use `aria-label` or `aria-labelledby` when needed
- Make interactive elements keyboard accessible
- Use semantic HTML over divs when possible
- Test with screen readers

---

## 10. Complete HTML Template

### Definition
**A Complete HTML Template** is a ready-to-use boilerplate that incorporates all essential HTML5 elements, meta tags, and best practices into a single starting point. It includes proper document structure, character encoding, viewport settings, SEO meta tags, and semantic landmarks that every modern web page should have.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Character Encoding -->
    <meta charset="UTF-8">
    
    <!-- Viewport for Responsive Design -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <!-- SEO Meta Tags -->
    <title>Page Title - Site Name</title>
    <meta name="description" content="Page description for search engines (150-160 characters)">
    <meta name="keywords" content="keyword1, keyword2, keyword3">
    <meta name="author" content="Author Name">
    <meta name="robots" content="index, follow">
    
    <!-- Open Graph for Social Media -->
    <meta property="og:title" content="Page Title">
    <meta property="og:description" content="Page description">
    <meta property="og:image" content="https://example.com/image.jpg">
    <meta property="og:url" content="https://example.com/page">
    <meta property="og:type" content="website">
    
    <!-- Twitter Card -->
    <meta name="twitter:card" content="summary_large_image">
    <meta name="twitter:title" content="Page Title">
    <meta name="twitter:description" content="Page description">
    <meta name="twitter:image" content="https://example.com/image.jpg">
    
    <!-- Favicon -->
    <link rel="icon" type="image/x-icon" href="/favicon.ico">
    <link rel="apple-touch-icon" sizes="180x180" href="/apple-touch-icon.png">
    
    <!-- CSS -->
    <link rel="stylesheet" href="styles.css">
    
    <!-- Preconnect for Performance -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="dns-prefetch" href="https://fonts.googleapis.com">
    
    <!-- Canonical URL -->
    <link rel="canonical" href="https://example.com/page">
</head>
<body>
    
    <a href="#main-content" class="skip-link">Skip to main content</a>
    
    <header>
        <nav aria-label="Main navigation">
            <!-- Navigation -->
        </nav>
    </header>
    
    <main id="main-content">
        <!-- Main content -->
    </main>
    
    <footer>
        <!-- Footer content -->
    </footer>
    
    <!-- JavaScript (deferred for performance) -->
    <script src="script.js" defer></script>
    
</body>
</html>
```

---

## 🔑 Key Takeaways

1. **HTML provides structure**, not presentation (that's CSS's job)
2. **Semantic HTML** improves accessibility, SEO, and maintainability
3. **Always validate** your HTML using the W3C validator
4. **Forms need proper labels** for accessibility
5. **Images need alt text** for screen readers and SEO
6. **Use the right element** for the content (headings for structure, not size)

---

**Next:** Learn [CSS](./02-css.md) to style your HTML content!

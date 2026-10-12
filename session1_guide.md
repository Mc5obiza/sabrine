# Session 1 Teaching Guide: Build the "AI Student Assistant" with HTML and CSS

A live-coding guide for a 4-hour session. You type, you explain, the students follow.

---

## How to use this guide

Every phase has the same parts:

| Part | What it is |
|---|---|
| **What we build** | The goal of the phase, in 1 or 2 sentences. |
| **Concept in plain words** | A short idea from the lesson PDF to say before you type. |
| **Type this** | Code you type live. It is copied from the checkpoint files, so it always works. |
| **Where** | Exactly where the new code goes. New code never replaces old code unless a step says **Change this line**. |
| **Line by line** | One short sentence for every line. |
| **Say it like this** | A sentence you can say out loud. |
| **Students should see** | What appears in the browser after saving. |
| **Demo (do not keep)** | A quick experiment. Undo it (Ctrl+Z) before moving on. It is **not** in the checkpoints. |

Labels you will see:

- **Added by the guide**: something that is not in the PDF. Only three things are added: Live Server, the viewport meta tag, and CSS variables.
- **Correction**: the PDF has a mistake here. The guide shows the right version.

**Checkpoints.** Every phase ends with a working copy of the project in `checkpoints/session1/phase-XX/`. If a student gets lost, they copy that folder and continue from there. `phase-12` is the complete project.

**Fast lane.** If you fall behind, paste these blocks from the checkpoint instead of typing them: the page skeletons and the copied header and footer (Phases 5 and 6), and the repeated table rows and chat bubbles. They teach nothing new.

---

## Before class (10 minutes, the day before)

1. Install **VS Code** and the **Live Server** extension by Ritwick Dey (*added by the guide*).
2. Copy `checkpoints/session1/starter-assets/` and send it to the students. It contains:
   - `images/logo.svg`: the logo (also used as the tab icon).
   - `media/demo.mp4`: a short sample video (free CC0 clip from MDN).
   - `media/chime.wav`: a short "answer ready" sound.
3. Open `checkpoints/session1/phase-12/index.html` with Live Server so you can show the final result at the start.

---

## Session plan

| Phase | Time | Topic | Checkpoint |
|---|---|---|---|
| 1 | 0:00–0:15 | Setup, boilerplate, HTML tree, comments, paired and unpaired tags | `phase-01` |
| 2 | 0:15–0:35 | Head, headings, paragraphs, text formatting, attributes | `phase-02` |
| 3 | 0:35–0:55 | Images, links (external and internal), lists, div | `phase-03` |
| 4 | 0:55–1:05 | Audio, video, iframe, semantic tags | `phase-04` |
| 5 | 1:05–1:22 | Planner page: table and form inputs | `phase-05` |
| 6 | 1:22–1:40 | Assistant page: select, textarea, buttons | `phase-06` |
| 7 | 1:40–1:55 | CSS basics: linking, selectors, variables, text styles | `phase-07` |
| 8 | 1:55–2:10 | Box model: padding, margin, width, border, border-radius | `phase-08` |
| | 2:10–2:20 | **Break** | |
| 9 | 2:20–2:40 | Display values, first flexbox (navbar), form layout | `phase-09` |
| 10 | 2:40–3:05 | Flexbox: feature cards and chat bubbles | `phase-10` |
| 11 | 3:05–3:30 | Responsive design: viewport, media queries | `phase-11` |
| 12 | 3:30–3:45 | Font Awesome icons and one `:hover` | `phase-12` (final) |
| 13 | 3:45–4:00 | Student challenge and preview of Session 2 | (student work) |

**Final folder structure**

```text
ai-student-assistant/
├── index.html        landing page
├── assistant.html    chat page
├── planner.html      weekly planner
├── styles.css        one shared stylesheet
├── images/
│   └── logo.svg
└── media/
    ├── demo.mp4
    └── chime.wav
```

---

## Phase 1: Setup and your first page (0:00–0:15)

**What we build:** The project folder, Live Server, and a first `index.html` with a big title and a short text.

**Concept in plain words:** A computer cannot "see" that some text is a title. HTML (HyperText Markup Language) tells the browser what each piece of content is, using **tags**. The browser reads the file from top to bottom and builds a **tree of tags**. The root of the tree is always `<html>`.

### Step 1.1: Create the folder and open it

1. Create a folder called `ai-student-assistant`.
2. Put the `images` and `media` folders from the starter assets inside it.
3. In VS Code: **File → Open Folder** → choose `ai-student-assistant`.
4. Create a new file called `index.html`. The `.html` ending tells the computer it is a web page.

**Say it like this:** "A website is just a folder of files. The browser opens `index.html` first, like the front door of a house."

### Step 1.2: The HTML boilerplate

**Type this** (in the new file `index.html`):

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>AI Student Assistant</title>
  </head>
  <body>
  </body>
</html>
```

**Line by line**

- `<!DOCTYPE html>`: Tells the browser "this is a modern HTML page". It is always the very first line.
- `<html lang="en">`: Opens the root of the tree. `lang="en"` says the page is in English.
- `<head>`: Opens the head. It holds information *about* the page, and it is not shown inside the page.
- `<meta charset="UTF-8">`: Lets the browser show every letter correctly (accents, Arabic, emoji). It is an unpaired tag, so it has no closing tag.
- `<title>AI Student Assistant</title>`: The text shown on the browser tab.
- `</head>`: Closes the head. A closing tag has a `/`.
- `<body>`: Opens the body. Everything the visitor sees goes here.
- `</body>`: Closes the body.
- `</html>`: Closes the root. Nothing comes after it.

> **Correction:** In the PDF, the first bullet says "must start with a document type declaration: ." and the declaration itself is missing. It is `<!DOCTYPE html>`. The body bullet also lost its closing tag: the visible part is between `<body>` and `</body>`.

**Say it like this:** "The head is the ID card of the page: name, language, settings. The body is the page itself."

### Step 1.3: Live Server (*added by the guide*)

Right-click `index.html` → **Open with Live Server**. The page opens at `http://127.0.0.1:5500/index.html`. From now on, every time you save (Ctrl+S), the browser reloads by itself.

**Students should see:** An empty white page. The tab says **AI Student Assistant**.

### Step 1.4: The first content

**Where:** Inside the body, on the line right after `<body>`.

**Type this:**

```html
    <!-- Main content of the page -->
    <main>
      <!-- Hero: the first thing visitors see -->
      <section class="hero">
        <h1 class="hero-title">Study smarter with AI</h1>
        <p class="hero-text">Ask questions. Get clear answers.<br>Plan your week in minutes.</p>
      </section>
    </main>
```

**Line by line**

- `<!-- Main content of the page -->`: A comment. It is a note for developers, and the browser never shows it.
- `<main>`: A box for the main content of the page. We will meet more boxes like this in Phase 4.
- `<!-- Hero: the first thing visitors see -->`: Another comment. "Hero" is the name designers give to the big welcome area at the top.
- `<section class="hero">`: A section groups related content. `class="hero"` is a label we will use later to style it.
- `<h1 class="hero-title">Study smarter with AI</h1>`: The biggest heading. It is a paired tag: opening tag, content, closing tag.
- `<p class="hero-text">Ask questions. Get clear answers.<br>Plan your week in minutes.</p>`: A paragraph. `<br>` is an unpaired tag that breaks the line.
- `</section>`: Closes the section.
- `</main>`: Closes the main box.

**Say it like this:** "Tags are like boxes inside boxes. Each box must be closed in the same order you opened it, like Russian dolls."

**Students should see:** A big bold title "Study smarter with AI" and two lines of text below it. The comments do not appear.

**HTML tree so far**

```text
html
├── head
│   ├── meta
│   └── title
└── body
    └── main
        └── section
            ├── h1
            └── p (contains br)
```

### Common mistakes

- Forgetting to save (Ctrl+S), so Live Server shows the old version.
- Opening the file by double-clicking it instead of using Live Server. It works for now, but the YouTube video in Phase 4 will not.
- Writing `<br></br>`. `<br>` is unpaired and has no closing tag.
- Closing tags in the wrong order, for example `</main></section>`.
- Typing the file name as `index.html.txt` (Windows can hide extensions).

### Quick check

1. What is the difference between `<head>` and `<body>`? *(The head describes the page, and the body holds what you see.)*
2. Name one paired tag and one unpaired tag. *(Paired: `<h1>`, `<p>`. Unpaired: `<br>`, `<meta>`.)*

**Checkpoint:** `checkpoints/session1/phase-01/`

---

## Phase 2: Head, headings, text and attributes (0:15–0:35)

**What we build:** A tab icon, a "features" section with headings and paragraphs, a price line with text formatting, and a footer.

**Concept in plain words:** The **head** holds settings like the title and the tab icon. **Headings** go from `<h1>` (most important) to `<h6>` (least important). **Attributes** add extra information inside an opening tag, like `class="hero"` or `id="price"`. A `class` can be reused on many elements. An `id` must be unique on the page.

### Step 2.1: The tab icon (head tag)

**Where:** In the head, on the line right after `<title>`.

**Type this:**

```html
    <link rel="icon" href="images/logo.svg" type="image/svg+xml">
```

**Line by line**

- `<link rel="icon" href="images/logo.svg" type="image/svg+xml">`: `link` connects another file to the page. `rel="icon"` says it is the tab icon, `href` is the path to the file, and `type` says it is an SVG image.

**Say it like this:** "`rel`, `href` and `type` are attributes. They are settings that live inside the opening tag."

**Students should see:** The blue speech-bubble logo in the browser tab. Reload with Ctrl+F5 if it does not appear.

### Step 2.2: The features section (headings, paragraphs, attributes)

**Where:** Inside `<main>`, after `</section>` and before `</main>`. Leave one empty line first.

**Type this:**

```html
      <!-- Features: what the assistant can do -->
      <section class="section" id="features">
        <h2 class="section-title">What it can do</h2>
        <div class="feature-list">
          <article class="feature-card">
            <h3 class="feature-title">Explain any topic</h3>
            <p>Get simple explanations of hard lessons, step by step.</p>
          </article>
        </div>
      </section>
```

**Line by line**

- `<!-- Features: what the assistant can do -->`: A comment that names the section.
- `<section class="section" id="features">`: A new section. `class="section"` is shared by all normal sections. `id="features"` is a unique name we will link to in Phase 3.
- `<h2 class="section-title">What it can do</h2>`: A level-2 heading, the title of this section.
- `<div class="feature-list">`: A `div` is a plain box with no meaning. We use it to group the cards.
- `<article class="feature-card">`: An `article` is a self-contained piece of content, like one card or one blog post.
- `<h3 class="feature-title">Explain any topic</h3>`: A level-3 heading inside the card.
- `<p>Get simple explanations of hard lessons, step by step.</p>`: A paragraph. Each paragraph starts on a new line by itself.
- `</article>`: Closes the card.
- `</div>`: Closes the card group.
- `</section>`: Closes the section.

> **Correction:** The PDF's `<section>` and `<article>` examples close the heading with `<h1>` instead of `</h1>`. A closing tag always has a `/`.

> **Note:** The PDF says HTML has "five additional" headings. In total there are six levels, `<h1>` to `<h6>`. Use one `<h1>` per page, and do not skip levels just to get a smaller font (that is CSS's job).

**Say it like this:** "Headings are like a book: `h1` is the book title, `h2` is a chapter, and `h3` is a sub-chapter."

**Students should see:** "What it can do" as a medium heading, then a smaller heading "Explain any topic" and a paragraph.

### Step 2.3: Two more cards

**Where:** Inside `<div class="feature-list">`, right after the first card's `</article>`.

**Type this:**

```html
          <article class="feature-card">
            <h3 class="feature-title">Plan your week</h3>
            <p>Organize your study sessions in a clear weekly table.</p>
          </article>
          <article class="feature-card">
            <h3 class="feature-title">Practice for exams</h3>
            <p>Ask for quiz questions and check your answers.</p>
          </article>
```

**Line by line**

- `<article class="feature-card">` (twice): Opens a new card. Same class, because all cards will look the same.
- `<h3 class="feature-title">Plan your week</h3>`: Title of the second card.
- `<p>Organize your study sessions in a clear weekly table.</p>`: Text of the second card.
- `<h3 class="feature-title">Practice for exams</h3>`: Title of the third card.
- `<p>Ask for quiz questions and check your answers.</p>`: Text of the third card.
- `</article>` (twice): Closes each card.

**Say it like this:** "A class is like a school uniform: many students can wear the same one. An id is like a student number: only one person has it."

**Students should see:** Three card titles, each with its paragraph, one under the other.

### Step 2.4: The price line (text formatting)

**Where:** Inside the hero section, on the line right after the `hero-text` paragraph.

**Type this:**

```html
        <p id="price">Price: <del>$20 per month</del> <b>free</b> for <i>bootcamp students</i></p>
```

**Line by line**

- `<p id="price">Price: <del>$20 per month</del> <b>free</b> for <i>bootcamp students</i></p>`: A paragraph with a unique `id`. Inside it, `<del>` shows deleted text with a line through it, `<b>` makes text bold, and `<i>` makes text italic. All three are paired tags.

**Say it like this:** "Formatting tags work like a highlighter: the effect starts at the opening tag and stops at the closing tag."

**Students should see:** "Price: ~~$20 per month~~ **free** for *bootcamp students*".

### Step 2.5: The footer (`<br>` and `<small>`)

**Where:** After `</main>`, before `</body>`. Leave one empty line first.

**Type this:**

```html
    <!-- Footer: information about the site -->
    <footer class="footer">
      <p>Made by the AI Development Bootcamp students.<br>Built with HTML and CSS.</p>
      <p><small>For learning purposes only.</small></p>
    </footer>
```

**Line by line**

- `<!-- Footer: information about the site -->`: A comment.
- `<footer class="footer">`: The footer is the bottom part of the page: author, contact, copyright.
- `<p>Made by the AI Development Bootcamp students.<br>Built with HTML and CSS.</p>`: A paragraph. `<br>` puts the second sentence on a new line.
- `<p><small>For learning purposes only.</small></p>`: `<small>` shows smaller text, often used for legal notes.
- `</footer>`: Closes the footer.

> **Note:** HTML ignores extra spaces and Enter keys inside text. Ten spaces show as one space. To force a new line inside a paragraph, use `<br>`.

**Students should see:** Two lines of footer text at the bottom, then a line of smaller text.

### Common mistakes

- Using the same `id` twice on one page. Ids must be unique.
- Forgetting the quotes around attribute values: `class=hero` works by luck, but always write `class="hero"`.
- A space inside the tag name, like `< h1 >`. The PDF writes tags this way, but in real code there are no spaces inside the brackets.
- Choosing `<h3>` because it "looks smaller". Choose headings by importance, not size.
- Forgetting to close `<b>` or `<i>`, so the whole rest of the line becomes bold or italic.

### Quick check

1. What is the difference between `class` and `id`? *(Many elements can share a class. An id is unique on the page.)*
2. Which tag would you use for a crossed-out old price? *(`<del>`)*

**Checkpoint:** `checkpoints/session1/phase-02/`

---

## Phase 3: Images, links and lists (0:35–0:55)

**What we build:** A header with the logo and navigation links, two buttons in the hero, footer links, a numbered "how it works" list, and a glossary.

**Concept in plain words:** `<img>` adds an image: `src` is where the file is, and `alt` is the text shown if the image fails (and read aloud to blind users). `<a>` creates a link: `href` is where it goes. A link can go to another site (external), another page of ours, or a spot on the same page (internal, using `#id`). Lists come in three types: unordered `<ul>`, ordered `<ol>`, and description `<dl>`.

### Step 3.1: The header with logo and navigation

**Where:** Right after `<body>`, before the `<!-- Main content of the page -->` comment. Leave one empty line after it.

**Type this:**

```html
    <!-- Header: logo and navigation links -->
    <header class="navbar" id="top">
      <a class="brand" href="index.html" title="Go to the home page">
        <img class="brand-logo" src="images/logo.svg" alt="AI Student Assistant logo" width="40" height="40">
        AI Student Assistant
      </a>
      <nav class="nav-links">
        <a class="nav-link" href="index.html">Home</a>
        <a class="nav-link" href="assistant.html">Assistant</a>
        <a class="nav-link" href="planner.html">Planner</a>
      </nav>
    </header>
```

**Line by line**

- `<!-- Header: logo and navigation links -->`: A comment.
- `<header class="navbar" id="top">`: The header is the top part of the page. `id="top"` lets a link jump back here.
- `<a class="brand" href="index.html" title="Go to the home page">`: A link to the home page. The `title` attribute shows a small tooltip when you hover.
- `<img class="brand-logo" src="images/logo.svg" alt="AI Student Assistant logo" width="40" height="40">`: The logo image. `src` is the path, `alt` is the backup text, and `width`/`height` set the size in pixels. `<img>` is unpaired.
- `AI Student Assistant`: Text inside the link, next to the logo.
- `</a>`: Closes the logo link.
- `<nav class="nav-links">`: `nav` is a semantic tag for a group of navigation links.
- `<a class="nav-link" href="index.html">Home</a>`: A link to our home page.
- `<a class="nav-link" href="assistant.html">Assistant</a>`: A link to the chat page (we create it in Phase 6).
- `<a class="nav-link" href="planner.html">Planner</a>`: A link to the planner page (we create it in Phase 5).
- `</nav>`: Closes the navigation.
- `</header>`: Closes the header.

> **Correction:** In the PDF's `<nav>` example, the `href` values are missing their closing quotes (`href="/html/>`). Every attribute value needs an opening **and** a closing quote: `href="index.html"`.

> **Correction:** The PDF says writing `<img ...> </img>` is wrong. That is right: `<img>` is unpaired and never has a closing tag.

**Say it like this:** "`src` is the address of the photo, and `alt` is the description you would read to a friend on the phone."

**Students should see:** The logo and "AI Student Assistant" at the top, then three blue underlined links. "Assistant" and "Planner" show a "not found" page for now. That is expected.

### Step 3.2: Hero buttons (div, page link and internal link)

**Where:** Inside the hero, on the line right after the `<p id="price">` line.

**Type this:**

```html
        <div class="hero-actions">
          <a class="button" href="assistant.html">Ask a question</a>
          <a class="button button--secondary" href="#features">See features</a>
        </div>
```

**Line by line**

- `<div class="hero-actions">`: A plain box that groups the two buttons.
- `<a class="button" href="assistant.html">Ask a question</a>`: A link to another page of our site. The class `button` will make it look like a button later.
- `<a class="button button--secondary" href="#features">See features</a>`: An **internal link**: `#features` jumps to the element with `id="features"` on this page. It has two classes, separated by a space.
- `</div>`: Closes the box.

> **Correction:** The PDF's internal link uses `<a name="TopOfThePage">`. The `name` attribute on links is outdated. Today we put an `id` on any element and link to it with `href="#that-id"`.

**Say it like this:** "A `#` link is like a bookmark in a book: it jumps to a page you marked earlier."

**Students should see:** Two links under the price. Clicking "See features" scrolls down to "What it can do".

### Step 3.3: Footer links (external and "back to top")

**Where:** In the footer, on the line right after the first paragraph (`Made by the AI Development Bootcamp students...`).

**Type this:**

```html
      <p><a href="https://en.wikipedia.org/wiki/Artificial_intelligence">Learn more about AI</a> | <a href="#top">Back to top</a></p>
```

**Line by line**

- `<p><a href="https://en.wikipedia.org/wiki/Artificial_intelligence">Learn more about AI</a> | <a href="#top">Back to top</a></p>`: A paragraph with two links. The first is **external** (a full address starting with `https://`). The second jumps to `id="top"`, which is our header.

**Students should see:** "Learn more about AI | Back to top" in the footer. "Back to top" scrolls to the header.

### Step 3.4: How it works (ordered list)

**Where:** Inside `<main>`, after the features `</section>`, before `</main>`. Leave one empty line first.

**Type this:**

```html
      <!-- How it works: three simple steps -->
      <section class="section" id="how-it-works">
        <h2 class="section-title">How it works</h2>
        <ol class="steps">
          <li>Choose a subject.</li>
          <li>Type your question and press Send.</li>
          <li>Read the answer and ask a follow-up question.</li>
        </ol>
      </section>
```

**Line by line**

- `<!-- How it works: three simple steps -->`: A comment.
- `<section class="section" id="how-it-works">`: A new section with a unique id.
- `<h2 class="section-title">How it works</h2>`: The section title.
- `<ol class="steps">`: An **ordered** list. The browser numbers the items 1, 2, 3.
- `<li>Choose a subject.</li>` (and the next two `<li>` lines): Each `<li>` is one list item.
- `</ol>`: Closes the list.
- `</section>`: Closes the section.

> **Note:** The PDF shows the `type` attribute (`type="I"`, `type="square"`) to change numbers and bullets. It still works on `<ol>`, but for `<ul>` it is outdated. Later in the course we change list styles with CSS.

**Say it like this:** "Use `<ol>` when order matters, like a recipe. Use `<ul>` when it does not, like a shopping list."

**Students should see:** A numbered list 1, 2, 3 under "How it works".

### Step 3.5: The glossary (description list)

**Where:** After the "How it works" `</section>`, before `</main>`. Leave one empty line first.

**Type this:**

```html
      <!-- Glossary: AI words explained -->
      <section class="section" id="glossary">
        <h2 class="section-title">AI words to know</h2>
        <dl class="glossary">
          <dt>Model</dt>
          <dd>A program that learned patterns from a lot of data.</dd>
          <dt>Prompt</dt>
          <dd>The question or instruction you give to the AI.</dd>
          <dt>Token</dt>
          <dd>A small piece of text the AI reads, like a short word.</dd>
        </dl>
      </section>
```

**Line by line**

- `<!-- Glossary: AI words explained -->`: A comment.
- `<section class="section" id="glossary">`: A new section.
- `<h2 class="section-title">AI words to know</h2>`: The section title.
- `<dl class="glossary">`: A **description list**, used for terms and their meanings.
- `<dt>Model</dt>`, `<dt>Prompt</dt>`, `<dt>Token</dt>`: `dt` is the **term**.
- `<dd>A program that learned patterns from a lot of data.</dd>` (and the other two `<dd>` lines): `dd` is the **description** of the term just above it.
- `</dl>`: Closes the list.
- `</section>`: Closes the section.

**Students should see:** Each word on its own line, with its meaning indented below.

> We will use an unordered list `<ul>` on the assistant page in Phase 6.

### Common mistakes

- Wrong image path: `images/logo.svg` only works if the `images` folder is next to `index.html`. Letter case matters on most servers (`Logo.svg` ≠ `logo.svg`).
- Forgetting `https://` in an external link. `href="wikipedia.org"` is treated as a file in your folder.
- Writing `href="features"` instead of `href="#features"` for an internal link.
- Putting text directly inside `<ul>` or `<ol>` without `<li>`.
- Missing a closing quote in `href`, which breaks the rest of the line (the PDF's nav example has this bug).

### Quick check

1. What does `alt` do, and who needs it? *(It is backup text if the image fails, and screen readers read it to blind users.)*
2. How do you make a link that jumps to the section with `id="glossary"`? *(`<a href="#glossary">`)*

**Checkpoint:** `checkpoints/session1/phase-03/`

---

## Phase 4: Audio, video, iframe and semantic tags (0:55–1:05)

**What we build:** A demo section with a video and a sound, and an embedded YouTube intro video.

**Concept in plain words:** `<audio>` and `<video>` play media files. The `controls` attribute adds the play and volume buttons. `<source>` points to the file, and the text inside is shown only if the browser cannot play it. `<iframe>` shows another web page inside ours. That is how YouTube videos are embedded.

### Step 4.1: The demo section with audio

**Where:** Inside `<main>`, after the glossary `</section>`, before `</main>`. Leave one empty line first.

**Type this:**

```html
      <!-- Demo: video and audio files -->
      <section class="section" id="demo">
        <h2 class="section-title">See and hear it</h2>
        <p>The sound you hear when an answer is ready:</p>
        <audio controls>
          <source src="media/chime.wav" type="audio/wav">
          Your browser cannot play this audio.
        </audio>
      </section>
```

**Line by line**

- `<!-- Demo: video and audio files -->`: A comment.
- `<section class="section" id="demo">`: A new section.
- `<h2 class="section-title">See and hear it</h2>`: The section title.
- `<p>The sound you hear when an answer is ready:</p>`: A label for the audio player.
- `<audio controls>`: An audio player. `controls` shows play, pause and volume. Without it, the player is invisible.
- `<source src="media/chime.wav" type="audio/wav">`: The sound file and its type. The browser uses the first source it understands.
- `Your browser cannot play this audio.`: Backup text, shown only if audio is not supported.
- `</audio>`: Closes the player.
- `</section>`: Closes the section.

**Students should see:** An audio player. Pressing play gives a short "ding-ding".

### Step 4.2: The video inside a figure

**Where:** Inside the demo section, right after the `<h2>` and before the `<p>The sound you hear...` line.

**Type this:**

```html
        <figure class="demo-figure">
          <video class="demo-video" width="320" height="180" controls>
            <source src="media/demo.mp4" type="video/mp4">
            Your browser cannot play this video.
          </video>
          <figcaption class="demo-caption">A sample clip. Later, replace it with a recording of your app.</figcaption>
        </figure>
```

**Line by line**

- `<figure class="demo-figure">`: A `figure` groups media with its caption.
- `<video class="demo-video" width="320" height="180" controls>`: A video player, 320 by 180 pixels, with controls.
- `<source src="media/demo.mp4" type="video/mp4">`: The video file and its type.
- `Your browser cannot play this video.`: Backup text.
- `</video>`: Closes the player.
- `<figcaption class="demo-caption">A sample clip. Later, replace it with a recording of your app.</figcaption>`: The caption that belongs to the figure.
- `</figure>`: Closes the figure.

> **Correction:** The PDF uses `autoplay` to start a video automatically. Modern browsers block autoplay with sound, so `autoplay` only works if you also add `muted`. We use `controls` so the user decides. We use 320×180 instead of the PDF's 320×240 because this video is wide (16:9).

**Students should see:** A video of a flower with play controls, and the caption under it (it becomes grey and italic in Phase 7).

### Step 4.3: The YouTube intro video (iframe)

**Where:** After the demo `</section>`, before `</main>`. Leave one empty line first.

**Type this:**

```html
      <!-- Intro video embedded from YouTube -->
      <section class="section" id="intro">
        <h2 class="section-title">Watch: what is a neural network?</h2>
        <iframe class="intro-video" width="320" height="180" src="https://www.youtube.com/embed/aircAruvnKk" title="But what is a neural network?" allowfullscreen></iframe>
      </section>
```

**Line by line**

- `<!-- Intro video embedded from YouTube -->`: A comment.
- `<section class="section" id="intro">`: A new section.
- `<h2 class="section-title">Watch: what is a neural network?</h2>`: The section title.
- `<iframe class="intro-video" width="320" height="180" src="https://www.youtube.com/embed/aircAruvnKk" title="But what is a neural network?" allowfullscreen></iframe>`: A window that shows YouTube's player. `src` is the embed address (from YouTube → Share → Embed), `title` describes it for screen readers, and `allowfullscreen` lets the user go full screen. The size is small so it fits on phones; Phase 11 makes it bigger on wide screens.
- `</section>`: Closes the section.

> **Important:** YouTube embeds show "Error 153" when the page is opened by double-clicking the file (`file://`). Always use Live Server (`http://127.0.0.1:5500`).

**Students should see:** The YouTube player for "But what is a neural network?" by 3Blue1Brown.

### Step 4.4: Semantic tags recap (no new code)

We already used most semantic tags. Point to them in the code:

| Tag | Meaning | Where we used it |
|---|---|---|
| `<header>` | Top of the page: logo, navigation | Logo and links |
| `<nav>` | A group of navigation links | Home, Assistant, Planner |
| `<main>` | The main content (one per page) | Everything between header and footer |
| `<section>` | A themed part of a page | Hero, features, how it works... |
| `<article>` | A self-contained piece | Each feature card |
| `<aside>` | A sidebar next to the main content | Tips on the assistant page (Phase 6) |
| `<figure>` / `<figcaption>` | Media plus its caption | The demo video |
| `<footer>` | Bottom of the page: author, links | Our footer |

**Say it like this:** "A `div` is a cardboard box with no label. Semantic tags are boxes with a label written on them. The page looks the same, but Google and screen readers understand it better."

Why it matters (from the PDF): better accessibility, more predictable CSS, and better search engine results.

### Common mistakes

- Forgetting `controls`: the audio player becomes invisible.
- Wrong media path (`media/demo.mp4` must match the folder name exactly).
- Pasting the normal YouTube link (`watch?v=`) in `src` instead of the `embed/` link.
- Opening the page without Live Server, which causes YouTube "Error 153".
- Using `<section>` for everything. Ask: "Is this a stand-alone piece (`article`), a sidebar (`aside`), or a themed part (`section`)?"

### Quick check

1. What happens if you remove `controls` from `<audio>`? *(Nothing shows, so the user cannot play it.)*
2. Which tag would you use for a sidebar? *(`<aside>`)*

**Checkpoint:** `checkpoints/session1/phase-04/`

---

## Phase 5: The planner page: tables and form inputs (1:05–1:22)

**What we build:** `planner.html` with a weekly study table and a form to add a study session.

**Concept in plain words:** A table is made of rows `<tr>`. Header cells are `<th>`, and normal cells are `<td>`. A form collects input from the user. `<label>` is the text next to a field, and `<input>` is the field. Its `type` decides what kind of data it takes (text, date, number...). The `name` is like a variable name for the value.

### Step 5.1: Create `planner.html`

**Type this** (in a new file `planner.html`):

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Planner | AI Student Assistant</title>
    <link rel="icon" href="images/logo.svg" type="image/svg+xml">
  </head>
  <body>
  </body>
</html>
```

**Line by line**

- Same as the `index.html` boilerplate (Phase 1, Step 1.2) and the icon line (Phase 2, Step 2.1). Only one line is new:
- `<title>Planner | AI Student Assistant</title>`: A different tab title for this page.

### Step 5.2: The header (copy it)

**Where:** Right after `<body>`. Leave one empty line after it.

**Type this** (copy-paste from `index.html`):

```html
    <!-- Header: logo and navigation links -->
    <header class="navbar" id="top">
      <a class="brand" href="index.html" title="Go to the home page">
        <img class="brand-logo" src="images/logo.svg" alt="AI Student Assistant logo" width="40" height="40">
        AI Student Assistant
      </a>
      <nav class="nav-links">
        <a class="nav-link" href="index.html">Home</a>
        <a class="nav-link" href="assistant.html">Assistant</a>
        <a class="nav-link" href="planner.html">Planner</a>
      </nav>
    </header>
```

**Line by line:** Identical to Phase 3, Step 3.1. Every page shares the same header so the site feels like one site.

**Students should see:** The logo and the three links. "Planner" now opens this page.

### Step 5.3: The main part and the table header row

**Where:** After the header and its empty line, before `</body>`.

**Type this:**

```html
    <!-- Main content of the page -->
    <main>
      <section class="section">
        <h1 class="page-title">My weekly study plan</h1>
        <table class="planner-table">
          <tr>
            <th>Day</th>
            <th>Subject</th>
            <th>Time</th>
            <th>Goal</th>
          </tr>
        </table>
      </section>
    </main>
```

**Line by line**

- `<!-- Main content of the page -->`: A comment.
- `<main>`: Opens the main content.
- `<section class="section">`: One section for the table.
- `<h1 class="page-title">My weekly study plan</h1>`: The page title. Each page has one `h1`.
- `<table class="planner-table">`: Opens the table.
- `<tr>`: Opens a **row** (table row).
- `<th>Day</th>` (and `Subject`, `Time`, `Goal`): **Header cells**, the column names. They are bold and centered by default.
- `</tr>`: Closes the row.
- `</table>`: Closes the table.
- `</section>`: Closes the section.
- `</main>`: Closes the main content.

**Students should see:** The title and one bold row: Day, Subject, Time, Goal.

### Step 5.4: Two data rows

**Where:** Inside the table, right before `</table>`.

**Type this:**

```html
          <tr>
            <td>Monday</td>
            <td>Math</td>
            <td>18:00</td>
            <td>Practice fractions</td>
          </tr>
          <tr>
            <td>Wednesday</td>
            <td>Coding</td>
            <td>17:00</td>
            <td>Build a web page</td>
          </tr>
```

**Line by line**

- `<tr>` (twice): Opens a new row.
- `<td>Monday</td>`, `<td>Math</td>`, `<td>18:00</td>`, `<td>Practice fractions</td>`: Four **data cells**, one per column, in the same order as the headers.
- `<td>Wednesday</td>`, `<td>Coding</td>`, `<td>17:00</td>`, `<td>Build a web page</td>`: The second row's cells.
- `</tr>` (twice): Closes each row.

### Step 5.5: One more row

**Where:** Right before `</table>`.

**Type this:**

```html
          <tr>
            <td>Saturday</td>
            <td>English</td>
            <td>10:00</td>
            <td>Read one article</td>
          </tr>
```

**Line by line**

- `<tr>`: Opens the row.
- `<td>Saturday</td>`, `<td>English</td>`, `<td>10:00</td>`, `<td>Read one article</td>`: Four cells.
- `</tr>`: Closes the row.

**Say it like this:** "A table is like an Excel sheet: `tr` is a line, and each `td` is one box in that line."

**Students should see:** A table with a header row and three study sessions, aligned in columns (no borders yet; CSS comes later).

### Step 5.6: The "add a session" form (inputs)

**Where:** Inside `<main>`, after the table's `</section>`, before `</main>`. Leave one empty line first.

**Type this:**

```html
      <!-- Form to add a study session (it will work with JavaScript later) -->
      <section class="section">
        <h2 class="section-title">Add a study session</h2>
        <form class="planner-form">
          <label class="form-label" for="session-subject">Subject</label>
          <input class="form-field" type="text" id="session-subject" name="subject" placeholder="Example: Math" maxlength="30">
          <label class="form-label" for="session-date">Date</label>
          <input class="form-field" type="date" id="session-date" name="date">
          <label class="form-label" for="session-hours">Hours</label>
          <input class="form-field" type="number" id="session-hours" name="hours" value="1">
          <input class="button" type="submit" value="Add session">
        </form>
      </section>
```

**Line by line**

- `<!-- Form to add a study session (it will work with JavaScript later) -->`: A comment.
- `<section class="section">`: A section for the form.
- `<h2 class="section-title">Add a study session</h2>`: The section title.
- `<form class="planner-form">`: Opens the form, the container for all fields.
- `<label class="form-label" for="session-subject">Subject</label>`: The visible text for a field. `for` must match the field's `id`, so clicking the label puts the cursor in the field.
- `<input class="form-field" type="text" id="session-subject" name="subject" placeholder="Example: Math" maxlength="30">`: A one-line text field. `placeholder` is a grey hint, and `maxlength` limits it to 30 characters. `<input>` is unpaired.
- `<label class="form-label" for="session-date">Date</label>`: The label for the date field.
- `<input class="form-field" type="date" id="session-date" name="date">`: `type="date"` shows a date picker.
- `<label class="form-label" for="session-hours">Hours</label>`: The label for the hours field.
- `<input class="form-field" type="number" id="session-hours" name="hours" value="1">`: `type="number"` accepts only numbers. `value="1"` is the starting value.
- `<input class="button" type="submit" value="Add session">`: A submit button. `value` is the text on the button.
- `</form>`: Closes the form.
- `</section>`: Closes the section.

> **Small addition:** The PDF's labels have no `for`. We add `for` + `id` because it links the label to its field (better for clicks and for screen readers).

**Say it like this:** "`type` decides the keyboard: a date opens a calendar, and a number opens a number pad on phones."

**Students should see:** Labels and fields all on one line, mixed together (we fix the layout with CSS in Phase 9). Clicking "Date" opens a calendar. Clicking "Add session" reloads the page, because nothing handles the data until JavaScript.

### Step 5.7: The footer (copy it)

**Where:** After `</main>`, before `</body>`. Leave one empty line first.

**Type this** (copy-paste from `index.html`):

```html
    <!-- Footer: information about the site -->
    <footer class="footer">
      <p>Made by the AI Development Bootcamp students.<br>Built with HTML and CSS.</p>
      <p><a href="https://en.wikipedia.org/wiki/Artificial_intelligence">Learn more about AI</a> | <a href="#top">Back to top</a></p>
      <p><small>For learning purposes only.</small></p>
    </footer>
```

**Line by line:** Identical to the footer in `index.html` (Phase 2, Step 2.5 and Phase 3, Step 3.3).

### Common mistakes

- Putting `<td>` directly inside `<table>` without a `<tr>`.
- A row with fewer cells than the others, so the columns shift.
- `for` and `id` that do not match exactly (`session-date` ≠ `sessionDate`).
- Forgetting `name`: the value will not be sent with the form.
- Writing `<input></input>`. `input` is unpaired.

### Quick check

1. What is the difference between `<th>` and `<td>`? *(`th` is a header cell, and `td` is a normal data cell.)*
2. Which input type gives a calendar? *(`type="date"`)*

**Checkpoint:** `checkpoints/session1/phase-05/`

---

## Phase 6: The assistant page: select, textarea and buttons (1:22–1:40)

**What we build:** `assistant.html` with example chat bubbles, a question form (subject list, text area, three buttons), and a sidebar with tips.

**Concept in plain words:** `<select>` with `<option>` makes a drop-down list. `<textarea>` is a big text box where Enter makes a new line. `<button>` has three types: `submit` sends the form, `reset` clears it, and `button` does nothing until we add JavaScript.

### Step 6.1: Create `assistant.html`

**Type this** (in a new file `assistant.html`):

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Assistant | AI Student Assistant</title>
    <link rel="icon" href="images/logo.svg" type="image/svg+xml">
  </head>
  <body>
  </body>
</html>
```

**Line by line**

- Same as `planner.html`, Step 5.1. Only one line is new:
- `<title>Assistant | AI Student Assistant</title>`: The tab title for the chat page.

### Step 6.2: The header (copy it)

**Where:** Right after `<body>`. Leave one empty line after it.

**Type this** (copy-paste):

```html
    <!-- Header: logo and navigation links -->
    <header class="navbar" id="top">
      <a class="brand" href="index.html" title="Go to the home page">
        <img class="brand-logo" src="images/logo.svg" alt="AI Student Assistant logo" width="40" height="40">
        AI Student Assistant
      </a>
      <nav class="nav-links">
        <a class="nav-link" href="index.html">Home</a>
        <a class="nav-link" href="assistant.html">Assistant</a>
        <a class="nav-link" href="planner.html">Planner</a>
      </nav>
    </header>
```

**Line by line:** Identical to Phase 3, Step 3.1.

### Step 6.3: The chat area with two bubbles

**Where:** After the header and its empty line, before `</body>`.

**Type this:**

```html
    <!-- Main content: the chat and a sidebar with tips -->
    <main class="chat-page">
      <section class="chat">
        <h1 class="page-title">Ask the assistant</h1>
        <!-- Example conversation (static for now) -->
        <div class="chat-history">
          <div class="chat-row chat-row--user">
            <div class="chat-bubble chat-bubble--user">What is machine learning?</div>
          </div>
          <div class="chat-row chat-row--ai">
            <div class="chat-bubble chat-bubble--ai">It is a way to teach computers with examples instead of writing every rule by hand.</div>
          </div>
        </div>
      </section>
    </main>
```

**Line by line**

- `<!-- Main content: the chat and a sidebar with tips -->`: A comment.
- `<main class="chat-page">`: The main content, with a class so we can lay it out later.
- `<section class="chat">`: The chat column.
- `<h1 class="page-title">Ask the assistant</h1>`: The page title.
- `<!-- Example conversation (static for now) -->`: A comment. Later, AI answers will be added here by code.
- `<div class="chat-history">`: A box for all messages.
- `<div class="chat-row chat-row--user">`: One row of the conversation. `chat-row--user` means "a row for a user message". The `--` is a naming habit for "a variation of".
- `<div class="chat-bubble chat-bubble--user">What is machine learning?</div>`: The user's message bubble.
- `</div>`: Closes the row.
- `<div class="chat-row chat-row--ai">`: A row for an AI message.
- `<div class="chat-bubble chat-bubble--ai">It is a way to teach computers with examples instead of writing every rule by hand.</div>`: The AI's answer bubble.
- `</div>`: Closes the row.
- `</div>`: Closes the chat history.
- `</section>`: Closes the chat column.
- `</main>`: Closes the main content.

**Say it like this:** "Each message sits in a row, like a line in WhatsApp. Later, CSS will push your messages to the right and the AI's to the left."

**Students should see:** The title and two plain lines of text.

### Step 6.4: Two more bubbles

**Where:** Inside `chat-history`, right after the AI row's closing `</div>` (after "...every rule by hand.").

**Type this:**

```html
          <div class="chat-row chat-row--user">
            <div class="chat-bubble chat-bubble--user">Can you give me an example?</div>
          </div>
          <div class="chat-row chat-row--ai">
            <div class="chat-bubble chat-bubble--ai">Sure! A spam filter learns from thousands of emails which ones are spam.</div>
          </div>
```

**Line by line**

- `<div class="chat-row chat-row--user">`: A user row.
- `<div class="chat-bubble chat-bubble--user">Can you give me an example?</div>`: The user's second message.
- `</div>` (twice): Closes each row.
- `<div class="chat-row chat-row--ai">`: An AI row.
- `<div class="chat-bubble chat-bubble--ai">Sure! A spam filter learns from thousands of emails which ones are spam.</div>`: The AI's second answer.

**Students should see:** Four lines of conversation.

### Step 6.5: The form with a drop-down list

**Where:** Inside `<section class="chat">`, right after the `chat-history` closing `</div>` and before `</section>`.

**Type this:**

```html
        <!-- Question form -->
        <form class="chat-form">
          <label class="form-label" for="subject">Subject</label>
          <select class="form-field" id="subject" name="subject">
            <option value="math">Math</option>
            <option value="physics">Physics</option>
            <option value="coding">Coding</option>
            <option value="english">English</option>
          </select>
        </form>
```

**Line by line**

- `<!-- Question form -->`: A comment.
- `<form class="chat-form">`: Opens the form.
- `<label class="form-label" for="subject">Subject</label>`: The label for the drop-down.
- `<select class="form-field" id="subject" name="subject">`: Opens a drop-down list.
- `<option value="math">Math</option>` (and the other three `<option>` lines): Each `option` is one choice. `value` is what the form sends, and the text is what the user sees.
- `</select>`: Closes the list.
- `</form>`: Closes the form.

**Students should see:** "Subject" and a drop-down with Math, Physics, Coding and English.

### Step 6.6: Textarea and the three button types

**Where:** Inside the form, right before `</form>`.

**Type this:**

```html
          <label class="form-label" for="question">Your question</label>
          <textarea class="form-field" id="question" name="question" rows="4" cols="30" placeholder="Type your question here..."></textarea>
          <div class="form-actions">
            <button class="button" type="submit">Send</button>
            <button class="button button--secondary" type="reset">Clear</button>
            <button class="button button--secondary" type="button">New chat</button>
          </div>
```

**Line by line**

- `<label class="form-label" for="question">Your question</label>`: The label for the text area.
- `<textarea class="form-field" id="question" name="question" rows="4" cols="30" placeholder="Type your question here..."></textarea>`: A multi-line text box. `rows` is the visible height in lines, and `cols` is the visible width in characters. It is a paired tag.
- `<div class="form-actions">`: A box for the buttons.
- `<button class="button" type="submit">Send</button>`: Sends the form.
- `<button class="button button--secondary" type="reset">Clear</button>`: Empties every field of the form.
- `<button class="button button--secondary" type="button">New chat</button>`: Does nothing for now. JavaScript will give it a job later.
- `</div>`: Closes the button box.

**Say it like this:** "`submit` is the 'send' button of a letter, `reset` is the eraser, and `type="button"` is a button waiting for instructions."

**Students should see:** A text box and three grey buttons. Type something, then click **Clear**: the text disappears.

### Step 6.7: The sidebar with tips (aside and unordered list)

**Where:** Inside `<main>`, after the chat `</section>`, before `</main>`. Leave one empty line first.

**Type this:**

```html
      <!-- Sidebar: tips for good questions -->
      <aside class="chat-tips">
        <h2 class="tips-title">Tips for good questions</h2>
        <ul class="tips-list">
          <li>Name the topic and your level.</li>
          <li>Ask for an example.</li>
          <li>Ask it to explain "like I am 12 years old".</li>
        </ul>
      </aside>
```

**Line by line**

- `<!-- Sidebar: tips for good questions -->`: A comment.
- `<aside class="chat-tips">`: A sidebar next to the main content.
- `<h2 class="tips-title">Tips for good questions</h2>`: The sidebar title.
- `<ul class="tips-list">`: An **unordered** list (bullets).
- `<li>Name the topic and your level.</li>` (and the next two `<li>` lines): One tip per item.
- `</ul>`: Closes the list.
- `</aside>`: Closes the sidebar.

**Students should see:** A heading and three bullet points under the form (the sidebar moves to the side in Phase 11).

### Step 6.8: The footer (copy it)

**Where:** After `</main>`, before `</body>`. Leave one empty line first.

**Type this** (copy-paste):

```html
    <!-- Footer: information about the site -->
    <footer class="footer">
      <p>Made by the AI Development Bootcamp students.<br>Built with HTML and CSS.</p>
      <p><a href="https://en.wikipedia.org/wiki/Artificial_intelligence">Learn more about AI</a> | <a href="#top">Back to top</a></p>
      <p><small>For learning purposes only.</small></p>
    </footer>
```

**Line by line:** Identical to the footer in `index.html`.

### Common mistakes

- `<option>` written outside `<select>`.
- Writing `<textarea />` as unpaired. It needs `</textarea>`, and any text between the tags becomes the starting value (even spaces).
- Forgetting `type` on `<button>` inside a form. The default is `submit`, so every button sends the form.
- Different header or footer on different pages because one copy was edited by hand.
- Two elements with the same `id` (for example two `id="subject"`).

### Quick check

1. Which button type clears the form? *(`type="reset"`)*
2. When do you use `<textarea>` instead of `<input type="text">`? *(When the user needs several lines.)*

**Checkpoint:** `checkpoints/session1/phase-06/`

---

## Phase 7: CSS basics: linking, selectors, variables, text (1:40–1:55)

**What we build:** `styles.css`, linked to all three pages, with a color theme in variables and text styles.

**Concept in plain words:** HTML is the skeleton, and CSS (Cascading Style Sheets) is the clothes. A CSS **rule** has a **selector** (who to style) and a **declaration block** in `{ }` with `property: value;` pairs (how to style it). There are three ways to add CSS. We try the first two, then use the third for the rest of the course.

### Step 7.1: Inline and internal CSS (Demo, do not keep)

**Demo 1, inline CSS.** In `index.html`, temporarily change the `<h1>` line to:

```html
        <h1 class="hero-title" style="color: crimson;">Study smarter with AI</h1>
```

The title turns red. Explain: "This works, but imagine doing it on 100 elements." **Undo it (Ctrl+Z).**

**Demo 2, internal CSS.** Temporarily add this inside `<head>`, before `</head>`:

```html
    <style>
      h1 {
        color: darkblue;
        font-family: sans-serif;
      }
    </style>
```

All `h1` elements on **this page** change. Explain: "Better, but the other pages cannot use it." **Undo it (Ctrl+Z).**

> **Correction:** The PDF's internal CSS example writes `font: sans-serif;` and `font: small;`. These are invalid, so the browser ignores them. Use `font-family: sans-serif;` and `font-size: small;`.

### Step 7.2: External CSS: link the stylesheet

**Where:** In the `<head>` of **all three pages** (`index.html`, `planner.html`, `assistant.html`), on the line right after the `<link rel="icon" ...>` line.

**Type this:**

```html
    <link rel="stylesheet" href="styles.css">
```

**Line by line**

- `<link rel="stylesheet" href="styles.css">`: Connects the file `styles.css` to the page. `rel="stylesheet"` says "this file is CSS".

**Say it like this:** "One CSS file is like one wardrobe for the whole house. Change one shirt, and every room sees it."

### Step 7.3: Create `styles.css` with theme variables

CSS variables are *added by the guide*. They are not in the PDF, but they make restyling easy.

**Type this** (in a new file `styles.css`, next to `index.html`):

```css
/* ---------- Theme: change these values to restyle the whole site ---------- */
html {
  --color-primary: #2563eb;
  --color-on-primary: #ffffff;
  --color-text: #1f2937;
  --color-muted: #6b7280;
  --color-background: #ffffff;
  --color-surface: #f3f4f6;
  --color-border: #d1d5db;
  --font-main: Arial, Helvetica, sans-serif;
  font-size: 16px;
}
```

**Line by line**

- `/* ---------- Theme: change these values to restyle the whole site ---------- */`: A CSS comment. CSS comments use `/* */`, not `<!-- -->`.
- `html {`: A **type selector**: it selects the `<html>` element, the root that contains everything.
- `--color-primary: #2563eb;`: A **CSS variable** (a name that starts with `--`) holding our main blue. `#2563eb` is a hex color code.
- `--color-on-primary: #ffffff;`: The color of text that sits on the blue (white).
- `--color-text: #1f2937;`: Normal text color (almost black).
- `--color-muted: #6b7280;`: Grey for less important text.
- `--color-background: #ffffff;`: Page background (white).
- `--color-surface: #f3f4f6;`: Light grey for cards and boxes.
- `--color-border: #d1d5db;`: Grey for borders.
- `--font-main: Arial, Helvetica, sans-serif;`: Our font. If Arial is missing, the browser tries Helvetica, then any sans-serif font.
- `font-size: 16px;`: The base text size of the page, in pixels. It is the reference for `rem` (see below).
- `}`: Ends the rule.

> **Note:** Many tutorials write `:root { }` for variables. `:root` is a pseudo-class (Session 2). `html { }` selects the same element, so it works the same way.

**Say it like this:** "A variable is a named paint pot. We paint with the name, so changing the pot repaints the whole site."

**Students should see:** Nothing changes yet. Variables only store values.

### Step 7.4: Base styles (type selectors)

**Where:** At the end of `styles.css`, after an empty line.

**Type this:**

```css
/* ---------- Base: whole elements ---------- */
body {
  margin: 0;
  font-family: var(--font-main);
  color: var(--color-text);
  background-color: var(--color-background);
  line-height: 1.5;
}

a {
  color: var(--color-primary);
}
```

**Line by line**

- `/* ---------- Base: whole elements ---------- */`: A comment.
- `body {`: Selects the `<body>` element.
- `margin: 0;`: Removes the small white gap the browser adds around the page (more on margin in Phase 8).
- `font-family: var(--font-main);`: Uses our font. `var(--name)` reads a variable.
- `color: var(--color-text);`: Sets the text color. Children inherit it.
- `background-color: var(--color-background);`: Sets the page background.
- `line-height: 1.5;`: Space between lines: 1.5 times the text size. A number without a unit is the recommended way.
- `}`: Ends the rule.
- `a {`: Selects every link.
- `color: var(--color-primary);`: Links use our blue.
- `}`: Ends the rule.

**Students should see:** A cleaner font on all pages, slightly more space between lines, and links in our blue.

### Step 7.5: Multiple selectors (comma)

**Where:** At the end of `styles.css`, after an empty line.

**Type this:**

```css
.brand, .nav-link, .button {
  font-weight: bold;
  text-decoration: none;
}
```

**Line by line**

- `.brand, .nav-link, .button {`: Three **class selectors** separated by commas: the rule applies to all three. A class selector starts with a dot.
- `font-weight: bold;`: Makes the text bold.
- `text-decoration: none;`: Removes the underline from these links.
- `}`: Ends the rule.

**Say it like this:** "The comma means 'and also'. Write once, apply to many. That is the DRY rule: Don't Repeat Yourself."

**Students should see:** The logo text, the nav links and the hero buttons are bold and no longer underlined.

### Step 7.6: Class selectors for the hero (text-align, sizes)

**Where:** At the end of `styles.css`, after an empty line.

**Type this:**

```css
/* ---------- Hero ---------- */
.hero {
  text-align: center;
}

.hero-title {
  font-size: 2.5rem;
}

.hero-text {
  font-size: 1.25rem;
  color: var(--color-muted);
}
```

**Line by line**

- `/* ---------- Hero ---------- */`: A comment.
- `.hero {`: Selects every element with `class="hero"`.
- `text-align: center;`: Centers the text inside it. Other values: `left`, `right`, `justify`.
- `}`: Ends the rule.
- `.hero-title {`: Selects the hero heading.
- `font-size: 2.5rem;`: 2.5 times the root size (16px × 2.5 = 40px). `rem` = "root em".
- `}`: Ends the rule.
- `.hero-text {`: Selects the hero paragraph.
- `font-size: 1.25rem;`: 20px.
- `color: var(--color-muted);`: Grey text.
- `}`: Ends the rule.

### Step 7.7: An ID selector (and `em`)

**Where:** At the end of `styles.css`, after an empty line.

**Type this:**

```css
#price {
  font-size: 0.9em;
}
```

**Line by line**

- `#price {`: An **ID selector** starts with `#` and selects the one element with `id="price"`.
- `font-size: 0.9em;`: `em` is relative to the **parent's** text size: 0.9em is 90% of it.
- `}`: Ends the rule.

**Units in one sentence each:** `px` is a fixed size. `em` is relative to the parent's font size. `rem` is relative to the root (`html`) font size.

**Students should see:** A centered hero with a big title, grey text, and a slightly smaller price line.

### Step 7.8: Section titles and the caption (letter-spacing, font-style)

**Where:** At the end of `styles.css`, after an empty line.

**Type this:**

```css
/* ---------- Sections and feature cards ---------- */
.section-title {
  font-size: 1.75rem;
  letter-spacing: 1px;
}

/* ---------- Video and audio ---------- */
.demo-caption {
  font-style: italic;
  color: var(--color-muted);
}
```

**Line by line**

- `/* ---------- Sections and feature cards ---------- */`: A comment.
- `.section-title {`: Selects all section headings.
- `font-size: 1.75rem;`: 28px.
- `letter-spacing: 1px;`: Adds 1px of space between letters.
- `}`: Ends the rule.
- `/* ---------- Video and audio ---------- */`: A comment.
- `.demo-caption {`: Selects the video caption.
- `font-style: italic;`: Italic text. Values: `normal`, `italic`, `oblique`.
- `color: var(--color-muted);`: Grey text.
- `}`: Ends the rule.

> **Correction:** The PDF writes `font-style: bold;`. That is invalid. Bold is `font-weight: bold;`, and `font-style` is only for italic.

### Step 7.9: The footer text

**Where:** At the end of `styles.css`, after an empty line.

**Type this:**

```css
/* ---------- Footer ---------- */
.footer {
  text-align: center;
  color: var(--color-muted);
}
```

**Line by line**

- `/* ---------- Footer ---------- */`: A comment.
- `.footer {`: Selects the footer.
- `text-align: center;`: Centers the footer text.
- `color: var(--color-muted);`: Grey text.
- `}`: Ends the rule.

**Students should see:** A centered grey footer, spaced-out section titles, and an italic grey caption under the video.

### Common mistakes

- Forgetting the dot (`hero { }` instead of `.hero { }`), so the rule looks for a `<hero>` tag that does not exist.
- Forgetting `;` at the end of a line, which breaks the next line.
- `href="style.css"` but the file is named `styles.css`.
- Writing `var(--color-primary` without the closing `)`.
- Using HTML comments `<!-- -->` inside the CSS file.

### Quick check

1. How do you select an element with `class="footer"`? With `id="price"`? *(`.footer`, `#price`)*
2. What does `.brand, .nav-link { }` mean? *(The same rule applies to both classes.)*

**Checkpoint:** `checkpoints/session1/phase-07/`

---

## Phase 8: The box model (1:55–2:10)

**What we build:** Spacing, borders and rounded corners: a real navbar line, a grey hero, button shapes, cards, and a colored table header.

**Concept in plain words:** Every element is a rectangle, even if it looks round. From the inside out it has four layers: **content** (text, image), **padding** (space inside the border), **border** (the line), and **margin** (space outside the border). Padding is inside, and margin is outside.

```text
┌──────────── margin ────────────┐
│  ┌───────── border ─────────┐  │
│  │  ┌────── padding ─────┐  │  │
│  │  │      content       │  │  │
│  │  └────────────────────┘  │  │
│  └──────────────────────────┘  │
└────────────────────────────────┘
```

> **Correction:** The PDF says total width = width + padding + margin. The border is missing. The space an element takes is: width + left and right padding + left and right **border** + left and right margin.

### Step 8.1: Spacing variables

**Where:** Inside the `html { }` rule, on the line right after `--font-main: ...;`.

**Type this:**

```css
  --space-s: 8px;
  --space-m: 16px;
  --space-l: 32px;
  --radius: 8px;
```

**Line by line**

- `--space-s: 8px;`: Small space.
- `--space-m: 16px;`: Medium space.
- `--space-l: 32px;`: Large space.
- `--radius: 8px;`: How round our corners are.

**Say it like this:** "Three sizes of space, like S, M, L in clothes. Everything uses them, so the design stays even."

### Step 8.2: Navbar spacing (padding, border, margin)

**Where:** In `styles.css`, right **before** the `/* ---------- Hero ---------- */` comment. Leave one empty line after it.

**Type this:**

```css
/* ---------- Navbar ---------- */
.navbar {
  padding: var(--space-m);
  border-bottom: 1px solid var(--color-border);
}

.brand-logo {
  margin-right: var(--space-s);
}

.nav-link {
  padding: var(--space-s) var(--space-m);
}
```

**Line by line**

- `/* ---------- Navbar ---------- */`: A comment.
- `.navbar {`: Selects the header.
- `padding: var(--space-m);`: 16px of space inside, on all four sides.
- `border-bottom: 1px solid var(--color-border);`: A line only at the bottom: 1px thick, solid, grey. `border-bottom` works like `border`, but for one side (like `padding-top`).
- `}`: Ends the rule.
- `.brand-logo {`: Selects the logo image.
- `margin-right: var(--space-s);`: 8px of space outside, on the right only, so the text does not touch the logo.
- `}`: Ends the rule.
- `.nav-link {`: Selects each navigation link.
- `padding: var(--space-s) var(--space-m);`: Two values: 8px top and bottom, 16px left and right.
- `}`: Ends the rule.

**Padding and margin shortcut:** 1 value means all sides. 2 values mean top/bottom and left/right. 4 values mean top, right, bottom, left (clockwise, starting at 12 o'clock).

### Step 8.3: The hero box

**Where:** Inside the `.hero { }` rule, on the line right after `.hero {`.

**Type this:**

```css
  padding: var(--space-l) var(--space-m);
  background-color: var(--color-surface);
```

**Line by line**

- `padding: var(--space-l) var(--space-m);`: 32px top and bottom, 16px left and right.
- `background-color: var(--color-surface);`: A light grey background for the whole hero box.

**Students should see:** A grey hero band with space around the title.

### Step 8.4: Buttons (border, border-radius)

**Where:** Right **before** the `/* ---------- Sections and feature cards ---------- */` comment. Leave one empty line after it.

**Type this:**

```css
/* ---------- Buttons ---------- */
.button {
  margin: var(--space-s);
  padding: var(--space-s) var(--space-m);
  border: 2px solid var(--color-primary);
  border-radius: var(--radius);
  background-color: var(--color-primary);
  color: var(--color-on-primary);
  font-family: var(--font-main);
  font-size: 1rem;
}
```

**Line by line**

- `/* ---------- Buttons ---------- */`: A comment.
- `.button {`: Selects all buttons.
- `margin: var(--space-s);`: 8px outside, so buttons do not touch each other.
- `padding: var(--space-s) var(--space-m);`: Space inside: 8px top and bottom, 16px on the sides.
- `border: 2px solid var(--color-primary);`: The shorthand: width, style, color. Other styles: `dashed`, `dotted`, `double`, `none`...
- `border-radius: var(--radius);`: Rounds the corners by 8px.
- `background-color: var(--color-primary);`: Blue background.
- `color: var(--color-on-primary);`: White text.
- `font-family: var(--font-main);`: Real `<button>` and `<input>` elements do not take the page font by default, so we set it.
- `font-size: 1rem;`: Same reason: the same size as normal text (16px).
- `}`: Ends the rule.

> **Correction:** The PDF's border-radius slide has a confusing sentence about "color change". Simply put: rounded corners are only **visible** when the element has a background color or a border. On a transparent box with no border, there is nothing to see.

### Step 8.5: The secondary button

**Where:** Right **before** the `/* ---------- Sections and feature cards ---------- */` comment again (so it lands after `.button`). Leave one empty line after it.

**Type this:**

```css
.button--secondary {
  background-color: var(--color-background);
  color: var(--color-primary);
}
```

**Line by line**

- `.button--secondary {`: Selects buttons that also have the `button--secondary` class.
- `background-color: var(--color-background);`: A white background instead of blue.
- `color: var(--color-primary);`: Blue text. The blue border comes from `.button`.
- `}`: Ends the rule.

**Students should see:** A blue "Ask a question" button and a white "See features" button with a blue border. Both are rounded.

### Step 8.6: Section spacing

**Where:** Right **after** the `/* ---------- Sections and feature cards ---------- */` comment. Leave one empty line after it.

**Type this:**

```css
.section {
  padding: var(--space-l) var(--space-m);
}
```

**Line by line**

- `.section {`: Selects every normal section.
- `padding: var(--space-l) var(--space-m);`: Breathing room: 32px top and bottom, 16px on the sides.
- `}`: Ends the rule.

### Step 8.7: Feature cards (width)

**Where:** Right **before** the `/* ---------- Video and audio ---------- */` comment. Leave one empty line after it.

**Type this:**

```css
.feature-card {
  width: 250px;
  margin: var(--space-s);
  padding: var(--space-m);
  border: 1px solid var(--color-border);
  border-radius: var(--radius);
  background-color: var(--color-surface);
}
```

**Line by line**

- `.feature-card {`: Selects each card.
- `width: 250px;`: The card is 250px wide (content only, padding and border are added on top).
- `margin: var(--space-s);`: 8px of space around each card.
- `padding: var(--space-m);`: 16px of space inside.
- `border: 1px solid var(--color-border);`: A thin grey line.
- `border-radius: var(--radius);`: Rounded corners.
- `background-color: var(--color-surface);`: Light grey background.
- `}`: Ends the rule.

> **Height:** we usually let the content decide the height. We will set a fixed `height` on the YouTube video in Phase 11.

**Say it like this:** "Padding is the bubble wrap inside the box. Margin is the empty space you leave between boxes on the shelf."

**Students should see:** Three grey rounded cards, stacked one under the other on the left (they go side by side in Phase 10).

### Step 8.8: Remove the figure's default margin

**Where:** Right **after** the `/* ---------- Video and audio ---------- */` comment. Leave one empty line after it.

**Type this:**

```css
.demo-figure {
  margin: 0;
}
```

**Line by line**

- `.demo-figure {`: Selects the figure around the video.
- `margin: 0;`: Browsers give `<figure>` a 40px margin on the left and right. We remove it so the video lines up with the text and fits on small phones.
- `}`: Ends the rule.

### Step 8.9: Footer spacing

**Where:** Inside the `.footer { }` rule, on the line right after `.footer {`.

**Type this:**

```css
  padding: var(--space-l) var(--space-m);
  border-top: 1px solid var(--color-border);
```

**Line by line**

- `padding: var(--space-l) var(--space-m);`: Space inside the footer.
- `border-top: 1px solid var(--color-border);`: A separator line on top of the footer.

### Step 8.10: The planner table

**Where:** At the end of `styles.css`, after an empty line.

**Type this:**

```css
/* ---------- Planner table ---------- */
.planner-table {
  width: 100%;
}

th, td {
  padding: var(--space-s);
  text-align: left;
}
```

**Line by line**

- `/* ---------- Planner table ---------- */`: A comment.
- `.planner-table {`: Selects our table.
- `width: 100%;`: The table fills the full width of its section. `%` is relative to the parent.
- `}`: Ends the rule.
- `th, td {`: Two type selectors with a comma: all header and data cells.
- `padding: var(--space-s);`: 8px of space inside every cell.
- `text-align: left;`: Left-align the text (headers are centered by default).
- `}`: Ends the rule.

### Step 8.11: Table colors

**Where:** At the end of `styles.css`, after an empty line.

**Type this:**

```css
th {
  background-color: var(--color-primary);
  color: var(--color-on-primary);
}

td {
  background-color: var(--color-surface);
}
```

**Line by line**

- `th {`: Selects the header cells.
- `background-color: var(--color-primary);`: Blue background.
- `color: var(--color-on-primary);`: White text.
- `}`: Ends the rule.
- `td {`: Selects the data cells.
- `background-color: var(--color-surface);`: Light grey. The small white gaps between cells act as grid lines.
- `}`: Ends the rule.

**Students should see** (open `planner.html`): A full-width table with a blue header row and grey cells.

### Common mistakes

- Mixing up padding and margin. Ask: "Do I want space **inside** the line or **outside** it?"
- Writing `border: 1px var(--color-border);` without a style. With no `solid`, the style is `none`, so there is no border.
- Forgetting the unit: `padding: 16;` does nothing. Write `16px` (only `0` can skip the unit).
- Adding rules in the wrong place in the file. Order matters only when two rules set the same property on the same element, but a tidy file is easier to restyle.
- Expecting `border-radius` to show on an element with no background and no border.

### Quick check

1. Name the four layers of the box model, from inside to outside. *(Content, padding, border, margin.)*
2. What does `padding: 8px 16px;` mean? *(8px top and bottom, 16px left and right.)*

**Checkpoint:** `checkpoints/session1/phase-08/`

---

## Break (2:10–2:20)

---

## Phase 9: Display values and the first flexbox (2:20–2:40)

**What we build:** Buttons that behave like boxes, a clean form layout (one field per line), and a navbar built with flexbox.

**Concept in plain words:** The `display` property decides how a box behaves.

- **block**: starts on a new line and takes the full width. You can set width and height. Examples: `<p>`, `<div>`, `<h1>`.
- **inline**: stays in the line of text and takes only the space it needs. Width and height are ignored. Examples: `<a>`, `<b>`, `<label>`, `<input>`.
- **inline-block**: stays in the line, **and** accepts width, height and vertical padding.
- **none**: the element disappears completely.

### Step 9.1: Display demo on the feature cards (Demo, do not keep)

Inside `.feature-card { }`, temporarily add one line at the top and change its value step by step. Save each time:

```css
  display: inline;
```

1. `display: inline;`: The cards lose their width and look broken. Width is ignored on inline boxes.
2. `display: inline-block;`: The cards sit side by side **and** keep their width.
3. `display: none;`: The cards disappear, and the space they used is gone too.
4. Replace it with `visibility: hidden;`: The cards are invisible, **but their empty space stays**.

**Delete the demo line** before moving on.

> **Correction:** The PDF says there is "a difference" between `display: none` and `visibility: hidden` but does not say what it is. `display: none` removes the element **and its space**. `visibility: hidden` hides the element but **keeps its space**, like an invisible person still sitting on a chair.

### Step 9.2: Buttons as inline-block

**Where:** Inside the `.button { }` rule, on the line right after `.button {`.

**Type this:**

```css
  display: inline-block;
```

**Line by line**

- `display: inline-block;`: Our buttons are `<a>` links, which are inline. `inline-block` keeps them side by side, but their vertical padding and margin now push other content away correctly.

**Students should see:** The hero buttons get proper space above and below them.

### Step 9.3: Form layout with display: block

**Where:** Right **before** the `/* ---------- Planner table ---------- */` comment. Leave one empty line after it.

**Type this:**

```css
/* ---------- Forms ---------- */
.form-label {
  display: block;
  margin-top: var(--space-m);
  font-weight: bold;
}

.form-field {
  display: block;
  padding: var(--space-s);
  border: 1px solid var(--color-border);
  border-radius: var(--radius);
  font-family: var(--font-main);
  font-size: 1rem;
}
```

**Line by line**

- `/* ---------- Forms ---------- */`: A comment.
- `.form-label {`: Selects all labels.
- `display: block;`: A label is inline by default. Block puts it on its own line.
- `margin-top: var(--space-m);`: Space above each label. Vertical margin only works now that the label is a block.
- `font-weight: bold;`: Bold labels.
- `}`: Ends the rule.
- `.form-field {`: Selects inputs, the select and the textarea.
- `display: block;`: Each field gets its own line, under its label.
- `padding: var(--space-s);`: 8px inside the field, so the text does not touch the edge.
- `border: 1px solid var(--color-border);`: A thin grey border.
- `border-radius: var(--radius);`: Rounded corners.
- `font-family: var(--font-main);`: Fields do not take the page font by default. The textarea would use a typewriter font.
- `font-size: 1rem;`: Normal text size in fields.
- `}`: Ends the rule.

> **Note:** The PDF's display: block example sets `display: block` on a `div`, which is already block, so nothing changes. Labels and inputs are a better example because they really are inline.

**Students should see** (`assistant.html` and `planner.html`): Each label on its own line in bold, with its field under it.

### Step 9.4: Flexbox concept

**Concept in plain words:** Flexbox is a layout tool. You put `display: flex` on a **parent**, and its **direct children** (flex items) line up. Flexbox has two axes:

- The **main axis** follows `flex-direction`: `row` (default, left to right) or `column` (top to bottom).
- The **cross axis** is the other direction.
- `justify-content` places the items along the **main** axis: `flex-start`, `center`, `flex-end`, `space-between`, `space-around`.
- `align-items` places the items along the **cross** axis: `stretch` (default), `flex-start`, `center`, `flex-end`.

```text
flex-direction: row                    flex-direction: column
main axis ───────────────►             main axis  │
┌──────────────────────────┐                      ▼
│ [A] [B] [C]              │ ▲ cross   ┌───────┐
└──────────────────────────┘ │ axis    │  [A]  │ ◄── cross axis ──►
                                       │  [B]  │
                                       │  [C]  │
                                       └───────┘
```

**Say it like this:** "The parent is a shelf. `justify-content` slides books along the shelf, and `align-items` decides if they stand at the top, middle or bottom of the shelf."

### Step 9.5: The navbar as a flex column

On phones the logo goes on top and the links below. Phase 11 puts them side by side on wide screens.

**Where:** Inside the `.navbar { }` rule, on the line right after `.navbar {`.

**Type this:**

```css
  display: flex;
  flex-direction: column;
  align-items: center;
```

**Line by line**

- `display: flex;`: The header becomes a flex container. Its children (the logo link and the nav) become flex items.
- `flex-direction: column;`: Items stack from top to bottom. The main axis is now vertical.
- `align-items: center;`: Centers the items on the cross axis, which is horizontal here.

**Students should see:** The logo centered on top, the links centered under it.

### Step 9.6: Logo and text side by side

**Where:** Right **before** the `.brand-logo {` rule. Leave one empty line after it.

**Type this:**

```css
.brand {
  display: flex;
  align-items: center;
}
```

**Line by line**

- `.brand {`: Selects the logo link.
- `display: flex;`: Its children (the image and the text) line up in a row (row is the default direction).
- `align-items: center;`: The text is vertically centered next to the logo.
- `}`: Ends the rule.

### Step 9.7: The nav links

**Where:** Right **before** the `.nav-link {` rule. Leave one empty line after it.

**Type this:**

```css
.nav-links {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
```

**Line by line**

- `.nav-links {`: Selects the `<nav>`.
- `display: flex;`: The three links line up in a row.
- `flex-wrap: wrap;`: If the screen is too narrow, links move to a new line instead of being squeezed.
- `justify-content: center;`: The links are centered along the row.
- `}`: Ends the rule.

**Demo (do not keep):** Change `justify-content: center;` to `flex-start`, `flex-end`, `space-between` and `space-around`. Save each time, then put back `center`.

**Students should see:** A centered navbar on every page: logo plus name on one line, links on the next line.

### Common mistakes

- Putting `display: flex` on the **children** instead of the **parent**.
- Expecting `width` to work on an inline element.
- Confusing `justify-content` (main axis) and `align-items` (cross axis), especially after changing to `flex-direction: column`, which swaps the axes.
- Using `visibility: hidden` and wondering why there is an empty gap.
- Forgetting to delete the demo line in `.feature-card`.

### Quick check

1. What is the difference between `display: none` and `visibility: hidden`? *(`none` removes the space, and `hidden` keeps it.)*
2. With `flex-direction: column`, which property centers items left to right? *(`align-items`, because the cross axis is now horizontal.)*

**Checkpoint:** `checkpoints/session1/phase-09/`

---

## Phase 10: Flexbox for feature cards and chat bubbles (2:40–3:05)

**What we build:** Feature cards side by side that wrap on small screens, and a real chat layout: your messages on the right, the AI's on the left.

**Concept in plain words:** By default, flex items all try to fit on one line and shrink if needed. `flex-wrap: wrap` lets them move to the next line instead. `align-content` places those **lines** inside a tall container. It only works when wrapping is on.

### Step 10.1: Feature cards in a wrapping row

**Where:** Right **before** the `.feature-card {` rule. Leave one empty line after it.

**Type this:**

```css
.feature-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
```

**Line by line**

- `.feature-list {`: Selects the div that holds the cards.
- `display: flex;`: The cards line up in a row.
- `flex-wrap: wrap;`: When there is not enough room, cards move to the next line.
- `justify-content: center;`: The cards are centered on each line.
- `}`: Ends the rule.

**Students should see:** Three cards side by side. Make the window narrow: the cards wrap to two lines, then one card per line.

**Demo (do not keep): align-content.** Inside `.feature-list`, temporarily add:

```css
  height: 700px;
  align-content: space-between;
```

Make the window narrow so the cards make two lines. Try `flex-start`, `center` and `space-between`: the **lines** move inside the 700px box. Then delete both lines.

> **Correction:** The PDF says `align-content` "has no effect when there is only one line". More precisely, it has no effect when `flex-wrap` is `nowrap` (the default). With `flex-wrap: wrap`, it works even with one line.

### Step 10.2: Chat page and chat rows

**Where:** At the end of `styles.css`, after an empty line.

**Type this:**

```css
/* ---------- Chat page ---------- */
.chat-page {
  display: flex;
  flex-direction: column;
  padding: var(--space-m);
}

.chat-row {
  display: flex;
  align-items: flex-end;
  margin-bottom: var(--space-m);
}
```

**Line by line**

- `/* ---------- Chat page ---------- */`: A comment.
- `.chat-page {`: Selects the `<main>` of the assistant page.
- `display: flex;`: Its children (the chat section and the tips aside) become flex items.
- `flex-direction: column;`: On phones they stack: chat first, tips below.
- `padding: var(--space-m);`: Space around the whole chat page.
- `}`: Ends the rule.
- `.chat-row {`: Selects each message row.
- `display: flex;`: The bubble (and later an avatar icon) line up in the row.
- `align-items: flex-end;`: Items sit at the bottom of the row. You will see why when we add avatars in Phase 12.
- `margin-bottom: var(--space-m);`: Space between messages.
- `}`: Ends the rule.

### Step 10.3: Left and right messages (justify-content)

**Where:** At the end of `styles.css`, after an empty line.

**Type this:**

```css
.chat-row--user {
  justify-content: flex-end;
}

.chat-row--ai {
  justify-content: flex-start;
}
```

**Line by line**

- `.chat-row--user {`: Selects rows with the user's messages.
- `justify-content: flex-end;`: Pushes the bubble to the **end** of the row, on the right.
- `}`: Ends the rule.
- `.chat-row--ai {`: Selects rows with the AI's messages.
- `justify-content: flex-start;`: Keeps the bubble at the **start**, on the left. This is the default, but writing it makes the intention clear.
- `}`: Ends the rule.

**Say it like this:** "Same row, same bubble. One word, `flex-end` or `flex-start`, decides if it is your message or the AI's."

### Step 10.4: The bubbles

**Where:** At the end of `styles.css`, after an empty line.

**Type this:**

```css
.chat-bubble {
  padding: var(--space-s) var(--space-m);
  border-radius: var(--radius);
}

.chat-bubble--user {
  margin-left: var(--space-l);
  background-color: var(--color-primary);
  color: var(--color-on-primary);
}

.chat-bubble--ai {
  margin-right: var(--space-l);
  background-color: var(--color-surface);
}
```

**Line by line**

- `.chat-bubble {`: Selects every bubble.
- `padding: var(--space-s) var(--space-m);`: Space inside the bubble.
- `border-radius: var(--radius);`: Rounded corners. They are visible because the bubbles have a background color.
- `}`: Ends the rule.
- `.chat-bubble--user {`: Selects the user's bubbles.
- `margin-left: var(--space-l);`: Keeps long messages from touching the left edge.
- `background-color: var(--color-primary);`: Blue bubble.
- `color: var(--color-on-primary);`: White text.
- `}`: Ends the rule.
- `.chat-bubble--ai {`: Selects the AI's bubbles.
- `margin-right: var(--space-l);`: Keeps long answers from touching the right edge.
- `background-color: var(--color-surface);`: Grey bubble.
- `}`: Ends the rule.

### Step 10.5: The tips box

**Where:** At the end of `styles.css`, after an empty line.

**Type this:**

```css
.chat-tips {
  margin-top: var(--space-l);
  padding: var(--space-m);
  border-radius: var(--radius);
  background-color: var(--color-surface);
}
```

**Line by line**

- `.chat-tips {`: Selects the sidebar.
- `margin-top: var(--space-l);`: Space between the chat and the tips on phones.
- `padding: var(--space-m);`: Space inside.
- `border-radius: var(--radius);`: Rounded corners.
- `background-color: var(--color-surface);`: Light grey box.
- `}`: Ends the rule.

**Students should see** (`assistant.html`): Blue bubbles on the right, grey bubbles on the left, the form below, then a grey tips box.

### Common mistakes

- Putting `justify-content: flex-end` on the bubble instead of the row (the parent).
- Forgetting `flex-wrap: wrap`, so the cards shrink and squash instead of moving to a new line.
- Expecting `align-content` to do something without wrapping or without extra height.
- Writing `justify-content: right`. In flexbox, use `flex-end`.
- Spelling the class differently in HTML and CSS (`chat-row--user` vs `chat-row-user`).

### Quick check

1. Why does the user's bubble go to the right? *(Its row has `justify-content: flex-end`.)*
2. What does `flex-wrap: wrap` change? *(Items move to a new line instead of shrinking to fit one line.)*

**Checkpoint:** `checkpoints/session1/phase-10/`

---

## Phase 11: Responsive design (3:05–3:30)

**What we build:** A site that looks right on phones **and** laptops: the navbar becomes one row on wide screens, the tips move next to the chat, and the YouTube video gets bigger.

**Concept in plain words:** A responsive page adapts to the screen size. We write the phone version first (**mobile-first**), then add rules for wider screens with a **media query**: "if the screen is at least X pixels wide, also apply these rules". We already got some responsiveness for free with `flex-wrap`.

### Step 11.1: The viewport meta tag (*added by the guide*)

**Where:** In the `<head>` of **all three pages**, on the line right after `<meta charset="UTF-8">`.

**Type this:**

```html
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**Line by line**

- `<meta name="viewport" content="width=device-width, initial-scale=1.0">`: Tells phones "use your real screen width and do not zoom out". Without it, phones pretend to be about 980px wide and show a tiny desktop page, and media queries do not work as expected.

**Say it like this:** "Without this line, the phone shows a photo of the desktop site. With it, the phone shows its own version."

### Step 11.2: How to test

Open the DevTools (F12), then click the phone-and-tablet icon (**Ctrl+Shift+M**). Choose a phone such as "iPhone SE" (375px). Or just make the browser window narrow.

### Step 11.3: The first media query: navbar

**Where:** At the end of `styles.css`, after an empty line. Media queries go at the **end**, so they win over the earlier rules.

**Type this:**

```css
/* ---------- Wider screens: tablets and up ---------- */
@media screen and (min-width: 768px) {
  .navbar {
    flex-direction: row;
    justify-content: space-between;
  }
}
```

**Line by line**

- `/* ---------- Wider screens: tablets and up ---------- */`: A comment.
- `@media screen and (min-width: 768px) {`: "On screens that are **at least** 768px wide, apply what is inside."
- `.navbar {`: The same navbar, only on wide screens.
- `flex-direction: row;`: Logo and links side by side.
- `justify-content: space-between;`: The logo goes to the far left, the links to the far right.
- `}`: Ends the `.navbar` rule.
- `}`: Ends the media query. **Two closing braces**: one for the rule, one for the media query.

**Students should see:** On a laptop, a one-line navbar. Below 768px, the stacked version from Phase 9.

### Step 11.4: The chat page on wide screens

**Where:** Inside the media query, after the `.navbar { }` rule's closing `}` and before the last `}`. Leave one empty line first.

**Type this:**

```css
  .chat-page {
    flex-direction: row;
    align-items: flex-start;
  }

  .chat {
    width: 70%;
  }

  .chat-tips {
    width: 30%;
    margin-top: 0;
    margin-left: var(--space-l);
  }
```

**Line by line**

- `.chat-page {`: The chat page's main box.
- `flex-direction: row;`: The chat and the tips go side by side.
- `align-items: flex-start;`: Each one is only as tall as its content (instead of stretching to the same height).
- `}`: Ends the rule.
- `.chat {`: The chat column.
- `width: 70%;`: Takes 70% of the width.
- `}`: Ends the rule.
- `.chat-tips {`: The tips sidebar.
- `width: 30%;`: Takes 30% of the width.
- `margin-top: 0;`: Cancels the top margin we only need on phones.
- `margin-left: var(--space-l);`: Space between the chat and the tips. If it does not fit exactly, flexbox shrinks both items a little.
- `}`: Ends the rule.

### Step 11.5: A bigger video on wide screens

**Where:** Inside the media query, after the `.chat-tips { }` rule's `}` and before the last `}`. Leave one empty line first.

**Type this:**

```css
  .intro-video {
    width: 560px;
    height: 315px;
  }
```

**Line by line**

- `.intro-video {`: The YouTube iframe.
- `width: 560px;`: YouTube's standard width.
- `height: 315px;`: YouTube's standard height (the same 16:9 shape as 320×180).
- `}`: Ends the rule.

**Students should see:** On a laptop, the tips sit to the right of the chat and the video is larger. At phone width, everything stacks and nothing scrolls sideways.

> **Correction:** The PDF's breakpoint list overlaps: `(min-width: 576px) and (max-width: 768px)` and `(min-width: 768px) and (max-width: 992px)` both match at exactly 768px (and the same at 576px and 992px). Mobile-first avoids this: write the phone styles with no media query, then add `min-width` queries only, going up (for example 768px, then 992px if needed). Each width falls clearly into one group.

### Common mistakes

- Forgetting the viewport meta tag, so the phone shows a tiny page.
- Forgetting the media query's closing `}`, which breaks every rule after it.
- Putting the media query at the **top** of the file. The normal rules below then override it.
- Writing `max-width` and `min-width` queries that overlap at the same pixel.
- Testing only on a laptop. Always check the phone view in DevTools.

### Quick check

1. In mobile-first CSS, which styles come without a media query? *(The phone styles.)*
2. What does `@media screen and (min-width: 768px)` mean? *(Apply these rules only when the screen is at least 768px wide.)*

**Checkpoint:** `checkpoints/session1/phase-11/`

---

## Phase 12: Font Awesome icons and polish (3:30–3:45)

**What we build:** Icons on the feature cards, the buttons and the chat avatars, and a hover effect on buttons.

**Concept in plain words:** Font Awesome is a free library of icons that behave like text: you can change their size and color with CSS. We load it from the internet with one `<link>`, then write an `<i>` tag with the icon's class. It reuses the `<i>` tag, but here `<i>` does **not** mean italic.

### Step 12.1: Load Font Awesome

**Where:** In the `<head>` of **all three pages**, on the line right after `<link rel="icon" ...>` (before the `styles.css` link).

**Type this:**

```html
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
```

**Line by line**

- `<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">`: Loads Font Awesome 4.7 (the version in the PDF) from a CDN, a fast public file server. We put it **before** our `styles.css` so our styles can override it.

### Step 12.2: Icons on the feature cards

**Where:** In `index.html`, inside each card, on the line right **before** each `<h3 class="feature-title">`.

**Type this** (before `Explain any topic`):

```html
            <i class="fa fa-lightbulb-o feature-icon"></i>
```

**Type this** (before `Plan your week`):

```html
            <i class="fa fa-calendar feature-icon"></i>
```

**Type this** (before `Practice for exams`):

```html
            <i class="fa fa-check-square-o feature-icon"></i>
```

**Line by line**

- `<i class="fa fa-lightbulb-o feature-icon"></i>`: `fa` turns on Font Awesome, `fa-lightbulb-o` picks the light bulb icon, and `feature-icon` is our own class for styling. The tag is empty on purpose.
- `<i class="fa fa-calendar feature-icon"></i>`: A calendar icon.
- `<i class="fa fa-check-square-o feature-icon"></i>`: A check-box icon.

Find other icons at <https://fontawesome.com/v4/icons/> (use the 4.7 names).

### Step 12.3: Icons on two buttons (Change this line)

**Change this line** in `index.html`:

```html
          <a class="button" href="assistant.html">Ask a question</a>
```

**to:**

```html
          <a class="button" href="assistant.html"><i class="fa fa-comments"></i> Ask a question</a>
```

**Change this line** in `assistant.html`:

```html
            <button class="button" type="submit">Send</button>
```

**to:**

```html
            <button class="button" type="submit"><i class="fa fa-paper-plane"></i> Send</button>
```

**Line by line**

- `<a class="button" href="assistant.html"><i class="fa fa-comments"></i> Ask a question</a>`: The same link with a speech-bubble icon before the text. The space after `</i>` separates the icon from the words.
- `<button class="button" type="submit"><i class="fa fa-paper-plane"></i> Send</button>`: The same button with a paper-plane icon.

### Step 12.4: Chat avatars

**Where:** In `assistant.html`, inside the chat rows. The user's icon goes **after** the user bubble, and the AI's icon goes **before** the AI bubble.

**Type this** (after the bubble `What is machine learning?`):

```html
            <i class="fa fa-user chat-avatar"></i>
```

**Type this** (before the bubble `It is a way to teach computers...`):

```html
            <i class="fa fa-graduation-cap chat-avatar"></i>
```

**Type this** (after the bubble `Can you give me an example?`):

```html
            <i class="fa fa-user chat-avatar"></i>
```

**Type this** (before the bubble `Sure! A spam filter...`):

```html
            <i class="fa fa-graduation-cap chat-avatar"></i>
```

**Line by line**

- `<i class="fa fa-user chat-avatar"></i>` (twice): A person icon for the student.
- `<i class="fa fa-graduation-cap chat-avatar"></i>` (twice): A graduation-cap icon for the AI tutor.

### Step 12.5: Style the icons

**Type this** in `styles.css`, right **before** the `/* ---------- Video and audio ---------- */` comment, followed by one empty line:

```css
.feature-icon {
  font-size: 2rem;
  color: var(--color-primary);
}
```

**Type this** right **before** the `.chat-tips {` rule, followed by one empty line:

```css
.chat-avatar {
  margin: 0 var(--space-s);
  font-size: 1.5rem;
  color: var(--color-muted);
}
```

**Line by line**

- `.feature-icon {`: Selects the card icons.
- `font-size: 2rem;` (in `.feature-icon`): Icons are text, so `font-size` changes their size (32px).
- `color: var(--color-primary);`: Blue icons.
- `}`: Ends the rule.
- `.chat-avatar {`: Selects the chat icons.
- `margin: 0 var(--space-s);`: No space top and bottom, 8px left and right, so the icon does not touch the bubble.
- `font-size: 1.5rem;` (in `.chat-avatar`): 24px icons.
- `color: var(--color-muted);`: Grey icons.
- `}`: Ends the rule.

**Say it like this:** "Remember `align-items: flex-end` on `.chat-row`? Now you see it: the avatar sits at the bottom of a tall bubble, like in a messaging app."

### Step 12.6: A hover effect (the only pseudo-class today)

**Type this** inside `html { }`, on the line right after `--color-primary: #2563eb;`:

```css
  --color-primary-dark: #1e40af;
```

**Type this** right **before** the `/* ---------- Sections and feature cards ---------- */` comment, followed by one empty line:

```css
.button:hover {
  background-color: var(--color-primary-dark);
  color: var(--color-on-primary);
}
```

**Line by line**

- `--color-primary-dark: #1e40af;`: A darker blue, used for hover.
- `.button:hover {`: `:hover` is a **pseudo-class**. The rule applies only while the mouse is over a button.
- `background-color: var(--color-primary-dark);`: The background gets darker.
- `color: var(--color-on-primary);`: Text becomes white (useful for the white secondary buttons).
- `}`: Ends the rule.

> Other pseudo-classes (`:link`, `:visited`, `:active`, ...) are in Session 2.

**Students should see:** Icons on the cards, the buttons and in the chat. Buttons turn dark blue under the mouse. This is the complete project, identical to `checkpoints/session1/phase-12/`.

### Common mistakes

- Forgetting the Font Awesome `<link>` on one page, so that page shows empty squares or nothing.
- Writing only `fa-user` without `fa`. Both classes are needed.
- Using Font Awesome 5 or 6 icon names (`fa-solid fa-user`) with version 4.7.
- Putting the Font Awesome link **after** `styles.css`, so it can override our styles.
- Spelling `:hover` with a space (`.button :hover`), which means something completely different.

### Quick check

1. How do you make a Font Awesome icon bigger? *(Change its `font-size`, because icons are text.)*
2. When does a `:hover` rule apply? *(Only while the mouse pointer is over the element.)*

**Checkpoint:** `checkpoints/session1/phase-12/` (final project)

---

## Phase 13: Student challenge and next session (3:45–4:00)

### Challenge (10 minutes): make it yours

Students change **only** the values inside `html { }` at the top of `styles.css` and watch the whole site change. Ideas:

1. Pick a new main color (try a site like coolors.co) and a matching dark version for hover.
2. Make corners rounder (`--radius: 16px;`) or square (`--radius: 0;`).
3. Make the site more spacious (`--space-l: 48px;`).
4. Bonus: a dark theme.

**Example dark theme** (a possible answer, not part of the checkpoints):

```css
html {
  --color-primary: #60a5fa;
  --color-primary-dark: #3b82f6;
  --color-on-primary: #0f172a;
  --color-text: #e5e7eb;
  --color-muted: #9ca3af;
  --color-background: #0f172a;
  --color-surface: #1e293b;
  --color-border: #334155;
}
```

(Students edit the existing lines. They keep `--font-main`, the spacing variables and `font-size`.)

**Say it like this:** "This is exactly what AI design tools will do for us later: they change the theme values and the class styles, without touching the HTML."

### Preview of Session 2 (5 minutes)

- **Combinators**: select "a `p` inside an `article`" without adding a class to every element.
- **Pseudo-classes**: `:link`, `:visited`, `:active`, and more.
- **Position**: `relative`, `absolute`, `fixed`, `sticky` (for example, a navbar that stays on top while you scroll).
- **CSS Grid**: two-dimensional layouts.
- **SASS**, **@font-face** and **Bootstrap**.
- Homework after Session 2: Flexbox Froggy, Grid Garden, CSS Diner.

Later, JavaScript will make the form send questions to an AI model and show real answers in the chat bubbles we built today.

---

## Appendix A: Corrections to the PDF

| PDF says | Correct version | Where in this guide |
|---|---|---|
| "must start with a document type declaration: ." (missing) | `<!DOCTYPE html>`; the body ends with `</body>` | Phase 1 |
| "five additional heading elements" | Six levels, `<h1>` to `<h6>` | Phase 2 |
| `<section>` / `<article>` examples close `<h1>` with `<h1>` | Close with `</h1>` | Phase 2 |
| Nav example: `href="/html/>` (unclosed quotes) | `href="index.html"` with both quotes | Phase 3 |
| Internal link with `<a name="TopOfThePage">` | Put `id="top"` on an element, link with `href="#top"` | Phase 3 |
| `type` attribute on `<ul>` for bullets | Outdated for `<ul>`; style lists with CSS later | Phase 3 |
| `autoplay` to start a video | Blocked by browsers unless `muted` is added; we use `controls` | Phase 4 |
| Internal CSS: `font: sans-serif;` and `font: small;` | `font-family: sans-serif;` and `font-size: small;` | Phase 7 |
| `font-style: bold;` | `font-weight: bold;` (`font-style` is for italic) | Phase 7 |
| Total width = width + padding + margin | Add the left and right **border** too | Phase 8 |
| Border-radius "color change" sentence | Rounded corners are only visible with a background color or a border | Phase 8 |
| Border style "idge" | `ridge` | (not used) |
| "difference" between `display: none` and `visibility: hidden` (not explained) | `none` removes the element and its space; `hidden` keeps the space | Phase 9 |
| `display: block` example on a `div` | A `div` is already block. We use labels and inputs, which are inline | Phase 9 |
| `align-content` "no effect with only one line" | No effect when `flex-wrap` is `nowrap`; with `wrap` it works even with one line | Phase 10 |
| Breakpoints overlap at 576, 768 and 992px | Mobile-first: base styles + `min-width` queries only | Phase 11 |
| Tags written with spaces, like `< h1 >` | No spaces inside the brackets: `<h1>` | Phase 2 |

## Appendix B: What the guide adds that is not in the PDF

Main additions (as agreed):

- **Live Server** (Phase 1)
- **Viewport meta tag** (Phase 11)
- **CSS variables** (Phases 7, 8, 12)

Small details you should know about, also not shown in the PDF:

- `for` on `<label>` to connect it to the field's `id` (Phase 5).
- One-side shorthands `border-bottom`, `border-top`, `margin-top`, `margin-left`, `margin-right`, `margin-bottom`. They work like the PDF's `padding-top`.
- The `html { }` selector to hold variables (instead of `:root`, which is a Session 2 pseudo-class).
- `title` and `allowfullscreen` on the iframe. Both come with YouTube's embed code.
- `type="audio/wav"` instead of `audio/mpeg`, because our sound file is a `.wav`.

## Appendix C: What was trimmed to fit 4 hours

- **Password input** (`type="password"`) from the PDF's form example is not typed. Mention it in one sentence in Phase 5.
- **All ten border styles** are not typed. Phase 8 uses `solid` and mentions `dashed`, `dotted`, `double` and `none`.
- **`display: inline`, `display: none`, `visibility: hidden` and `align-content`** are live demos only (not kept), because the final layout does not need them.
- **One breakpoint** (768px) instead of two. A second one (for example 992px) is easy to add in the challenge if time allows.
- **The table has three rows**, and the forms have no working logic (JavaScript comes later).
- **Phases 7 and 8 are the tightest** (about 19 short CSS blocks in 30 minutes). If you run late, paste Steps 8.10 and 8.11 (table styles) from `phase-08` instead of typing them.

## Appendix D: How this guide was checked

- Every "Type this" block is generated from the same step list that builds the checkpoints. Applying all steps in order reproduces `phase-12` exactly, byte for byte.
- No step deletes or rewrites earlier code, except the two explicit "Change this line" steps in Phase 12.
- No code block is longer than 15 lines.
- All 12 checkpoints were checked for: balanced tags, unique ids, working internal links, valid CSS, defined variables, and none of the Session 2 features (combinators, pseudo-classes other than `:hover`, `position`, grid, SASS, `@font-face`, Bootstrap, JavaScript).
- Every page of every checkpoint was rendered in Microsoft Edge at 375px (phone) with no horizontal scrolling. The final pages were also checked at 1280px.

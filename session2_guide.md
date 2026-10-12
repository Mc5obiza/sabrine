# Session 2 Teaching Guide: Level Up the "AI Student Assistant"

A live-coding guide for a session of about 2.5 hours. We upgrade the **same** project from Session 1. Nothing is started from scratch, except one page that we rebuild with Bootstrap on purpose.

---

## How to use this guide

Every phase has the same parts as in Session 1:

| Part | What it is |
|---|---|
| **What we build** | The goal of the phase, in 1 or 2 sentences. |
| **Concept in plain words** | A short idea from the lesson PDF to say before you type. |
| **Type this** | Code you type live. It is copied from the checkpoint files, so it always works. |
| **Where** | Exactly where the new code goes. |
| **Change this line** | Old code that must change. The guide shows the old version, then the new version. |
| **Line by line** | One short sentence for every line. |
| **Say it like this** | A sentence you can say out loud. |
| **Students should see** | What appears in the browser after saving. |
| **Demo (do not keep)** | A quick experiment. Undo it (Ctrl+Z) before moving on. It is **not** in the checkpoints. |

Labels:

- **Added by the guide**: something that is not in the PDF.
- **Correction**: the PDF has a mistake here. The guide shows the right version.
- **(Session 1)**: a one-line reminder of something already taught. Do not re-teach it.

**Checkpoints.** Every phase ends with a working copy in `checkpoints/session2/phase-XX/`. `phase-09` is the complete upgraded project. If a student is lost, they copy the folder of the last phase and continue.

---

## Before class

1. **Starting point:** every student opens their own Session 1 project. If someone does not have it, give them `checkpoints/session1/phase-12/`.
2. **Install the Live Sass Compiler extension** in VS Code. Search for "Live Sass Compiler" and pick the one by **Glenn Marks**. The older one by Ritwick Dey is no longer updated and does not understand `@use` (Phase 6).
3. **Send the font:** `checkpoints/session2/starter-assets/fonts/` contains `poppins-bold.woff2` (Poppins Bold, free under the SIL Open Font License, included as `OFL.txt`). Students need it in Phase 7.
4. **Internet:** Bootstrap and Font Awesome load from CDNs.

---

## Session plan

| Phase | Time | Topic | Checkpoint |
|---|---|---|---|
| 1 | 0:00–0:12 | Combinators: descendant, child, adjacent sibling, general sibling | `phase-01` |
| 2 | 0:12–0:20 | Pseudo-classes: `:link`, `:visited`, `:hover`, `:active` | `phase-02` |
| 3 | 0:20–0:45 | CSS position: static, relative, absolute, fixed, sticky | `phase-03` |
| 4 | 0:45–1:10 | CSS grid: rebuild the features section | `phase-04` |
| 5 | 1:10–1:25 | SASS part 1: setup, compiling, variables | `phase-05` |
| 6 | 1:25–1:40 | SASS part 2: partials, nesting, mixins | `phase-06` |
| 7 | 1:40–1:50 | `@font-face`: a custom font from a `.woff2` file | `phase-07` |
| 8 | 1:50–2:10 | Bootstrap part 1: link, navbar, container, rows, columns | `phase-08` |
| 9 | 2:10–2:30 | Bootstrap part 2: alerts, buttons, form, progress bar | `phase-09` (final) |
| 10 | 2:30–2:40 | Wrap-up, homework, preview of JavaScript | — |

> **Order:** the PDF teaches SASS before position and grid. We do position and grid first, in plain CSS, so the SASS phases convert the **whole** stylesheet once, at the end.

**Folder structure at the end**

```text
ai-student-assistant/
├── index.html         our own CSS (compiled from Sass)
├── planner.html       our own CSS (compiled from Sass)
├── assistant.html     rebuilt with Bootstrap
├── styles.scss        main Sass file (we edit this)
├── styles.css         made by Live Sass Compiler (never edit by hand)
├── scss/
│   ├── _variables.scss
│   ├── _mixins.scss
│   └── _navbar.scss
├── fonts/
│   ├── poppins-bold.woff2
│   └── OFL.txt
├── images/
└── media/
```

---

## Phase 1: Combinators (0:00–0:12)

**What we build:** Small refinements to chat avatars, the tips list, the navbar logo text and the forms, without adding a single new class to the HTML.

**Concept in plain words:** A combinator joins two selectors to say how the elements are related in the HTML tree. A **space** means "inside, at any depth" (descendant). `>` means "a direct child". `+` means "the very next sibling". `~` means "any sibling after it". Siblings are elements with the same parent.

### Step 1.1: Descendant combinator (space): blue avatars for the user

**Where:** In `styles.css`, right **before** the `.chat-tips {` rule. Leave one empty line after it.

**Type this:**

```css
.chat-row--user .chat-avatar {
  color: var(--color-primary);
}
```

**Line by line**

- `.chat-row--user .chat-avatar {`: Selects every `.chat-avatar` that is **somewhere inside** a `.chat-row--user`. The space is the descendant combinator.
- `color: var(--color-primary);`: Makes the user's icon blue (the AI icon stays grey).
- `}`: Ends the rule.

**Say it like this:** "Read the selector from right to left: 'an avatar… that lives inside a user row'."

**Students should see** (`assistant.html`): The person icons are blue. The graduation-cap icons stay grey.

### Step 1.2: Descendant again: space between tips

**Where:** Right **before** the `/* ---------- Wider screens: tablets and up ---------- */` comment. Leave one empty line after it.

**Type this:**

```css
.chat-tips li {
  margin-bottom: var(--space-s);
}
```

**Line by line**

- `.chat-tips li {`: Every `<li>` inside the tips box. We did not need to add a class to each `<li>`.
- `margin-bottom: var(--space-s);`: 8px under each tip.
- `}`: Ends the rule.

**Students should see:** The three tips are a little more spaced out.

### Step 1.3: Child combinator (`>`): the logo text

**Where:** Right **before** the `.brand-logo {` rule. Leave one empty line after it.

**Type this:**

```css
.navbar > .brand {
  color: var(--color-text);
}
```

**Line by line**

- `.navbar > .brand {`: Selects a `.brand` that is a **direct child** of `.navbar` (not a grandchild).
- `color: var(--color-text);`: The site name becomes dark instead of link blue.
- `}`: Ends the rule.

**Say it like this:** "A space means 'my descendants', like all my grandchildren. `>` means 'only my children'."

**Students should see:** "AI Student Assistant" in the navbar is dark grey. The nav links stay blue.

### Step 1.4: Adjacent sibling combinator (`+`): label and field

**Where:** Right **before** the `/* ---------- Planner table ---------- */` comment. Leave one empty line after it.

**Type this:**

```css
.form-label + .form-field {
  margin-top: var(--space-s);
}
```

**Line by line**

- `.form-label + .form-field {`: Selects a `.form-field` that comes **immediately after** a `.form-label`, with the same parent.
- `margin-top: var(--space-s);`: Adds 8px between each label and its field.
- `}`: Ends the rule.

### Step 1.5: General sibling combinator (`~`): the planner's submit button

**Where:** Right **before** the `/* ---------- Planner table ---------- */` comment again. Leave one empty line after it.

**Type this:**

```css
.form-field ~ .button {
  margin: var(--space-m) 0;
}
```

**Line by line**

- `.form-field ~ .button {`: Selects a `.button` that comes **anywhere after** a `.form-field`, with the same parent. In the planner form, the submit button comes after the fields.
- `margin: var(--space-m) 0;`: 16px above and below, 0 left and right, so the button lines up with the fields.
- `}`: Ends the rule.

> On the assistant page, the buttons are inside `<div class="form-actions">`, so they are **not** siblings of the fields and this rule does not touch them.

**Say it like this:** "`+` is 'the person sitting right next to me'. `~` is 'everyone sitting after me in the same row'."

**Students should see** (`planner.html`): A small gap between each label and its field, and the "Add session" button aligned to the left edge of the fields.

### Common mistakes

- Adding spaces in the wrong place: `.chat-row--user.chat-avatar` (no space) means "one element with both classes", not "inside".
- Using `>` when the element is a grandchild, so nothing matches.
- Expecting `+` or `~` to select an element that comes **before**. Siblings are only selected after.
- Expecting `+` to work across different parents.

### Quick check

1. What is the difference between `.navbar .brand` and `.navbar > .brand`? *(The first matches at any depth, the second only direct children.)*
2. In `h1 + p`, which element gets the style? *(The `p` right after an `h1`.)*

**Checkpoint:** `checkpoints/session2/phase-01/`

---

## Phase 2: Pseudo-classes (0:12–0:20)

**What we build:** Footer links that change color when visited, hovered and clicked, and nav links with a hover background.

**Concept in plain words:** A pseudo-class selects an element in a **state**: `:link` (never visited), `:visited` (already visited), `:hover` (mouse over it), `:active` (while you click it). You write the selector, a colon, then the state. We used `:hover` once in Session 1.

### Step 2.1: A color for visited links

**Where:** Inside `html { }`, on the line right after `--color-primary-dark: #1e40af;`.

**Type this:**

```css
  --color-visited: #7c3aed;
```

**Line by line**

- `--color-visited: #7c3aed;`: A purple, used only for visited links.

### Step 2.2: The four link states in the footer

**Where:** Right **before** the `/* ---------- Forms ---------- */` comment. Leave one empty line after it.

**Type this:**

```css
.footer a:link {
  color: var(--color-primary);
}

.footer a:visited {
  color: var(--color-visited);
}

.footer a:hover {
  color: var(--color-primary-dark);
}

.footer a:active {
  color: var(--color-text);
}
```

**Line by line**

- `.footer a:link {`: Footer links the user has **not** visited yet.
- `color: var(--color-primary);` (in `:link`): Blue.
- `.footer a:visited {`: Footer links the user **has** visited.
- `color: var(--color-visited);`: Purple, so you can see the difference.
- `.footer a:hover {`: While the mouse is over the link.
- `color: var(--color-primary-dark);`: Dark blue.
- `.footer a:active {`: During the click (mouse button pressed).
- `color: var(--color-text);`: Almost black for that short moment.
- `}` (four times): Ends each rule.

> **Correction:** The PDF gives `a:link` and `a:visited` the **same** color (tomato), so you cannot see any difference. Use two different colors. The PDF's comment also calls `:active` "selected link". It actually means "while it is being clicked".

> **Order matters:** write them in the order **L**ink, **V**isited, **H**over, **A**ctive (remember "**LoVe HAte**"). If `:hover` comes before `:visited`, a visited link never shows its hover color, because the later rule wins.

**Students should see:** Click "Learn more about AI", come back: the link is now purple. Hover it: dark blue. Hold the mouse button down on it: almost black.

### Step 2.3: Hover and active on the nav links

**Where:** Right **before** the `/* ---------- Hero ---------- */` comment. Leave one empty line after it.

**Type this:**

```css
.nav-link:hover {
  border-radius: var(--radius);
  background-color: var(--color-surface);
}

.nav-link:active {
  color: var(--color-primary-dark);
}
```

**Line by line**

- `.nav-link:hover {`: A nav link under the mouse.
- `border-radius: var(--radius);`: Rounded corners for the hover background.
- `background-color: var(--color-surface);`: A light grey "pill" behind the link.
- `}`: Ends the rule.
- `.nav-link:active {`: A nav link while it is being clicked.
- `color: var(--color-primary-dark);`: Darker blue during the click.
- `}`: Ends the rule.

**Say it like this:** "A pseudo-class is a mood. The same link is calm (`:link`), remembers you (`:visited`), gets excited when you come close (`:hover`), and reacts when you press it (`:active`)."

**Students should see:** A grey rounded background appears behind each nav link under the mouse.

### Common mistakes

- A space before the colon: `.nav-link :hover` means "a hovered element **inside** `.nav-link`".
- Wrong order (hover before visited), so the hover never shows on visited links.
- Expecting `:visited` to change anything other than colors. Browsers only allow color changes on visited links, for privacy.
- Testing `:visited` on a link you never clicked.

### Quick check

1. In which order should you write the four link states? *(`:link`, `:visited`, `:hover`, `:active`.)*
2. When does `:active` apply? *(Only while the mouse button is held down on the element.)*

**Checkpoint:** `checkpoints/session2/phase-02/`

---

## Phase 3: CSS position (0:20–0:45)

**What we build:** A navbar that stays on top while scrolling (sticky), a "New" badge in the corner of a feature card (relative parent, absolute child), and a floating "Ask AI" button (fixed).

**Concept in plain words:** By default every element is `position: static`: it simply follows the normal flow of the page. The other values let you move an element with `top`, `right`, `bottom` and `left`:

| Value | Moves relative to… | Keeps its space in the page? |
|---|---|---|
| `static` (default) | Does not move (`top`/`left` are ignored) | Yes |
| `relative` | Its own normal place | Yes |
| `absolute` | The nearest ancestor that is **not** static | No, it floats above the page |
| `fixed` | The browser window (the viewport) | No, it stays when you scroll |
| `sticky` | Normal, until you scroll to it, then it sticks | Yes |

### Step 3.1: Relative (Demo, do not keep)

Inside `.hero-title { }`, temporarily add:

```css
  position: relative;
  top: 20px;
  left: 20px;
```

The title moves 20px down and 20px right **from where it was**, and the space it used stays empty. **Undo it.**

### Step 3.2: Sticky navbar

**Where:** Inside the `.navbar { }` rule, on the line right after `.navbar {`.

**Type this:**

```css
  position: sticky;
  top: 0;
  z-index: 1;
  background-color: var(--color-background);
```

**Line by line**

- `position: sticky;`: The navbar scrolls normally until it reaches the edge given by `top`, then it sticks there.
- `top: 0;`: "Stick when you are 0px from the top of the window." Without a `top` value, sticky does nothing.
- `z-index: 1;`: *(Added by the guide.)* Puts the navbar on a layer **above** the other positioned elements (like the badge below), so they slide under it instead of over it. A bigger number means closer to you.
- `background-color: var(--color-background);`: A white background, so the page does not show through the navbar while scrolling.

**Say it like this:** "Sticky is like a sticky note on the inside of a box: it moves with the page until it hits the top, then it stays there."

**Students should see:** Scroll down `index.html`: the navbar stays at the top of the window.

### Step 3.3: The badge (relative parent, absolute child): HTML

**Where:** In `index.html`, inside the **second** card ("Plan your week"), on the line right **before** `<i class="fa fa-calendar feature-icon"></i>`.

**Type this:**

```html
            <small class="feature-badge">New</small>
```

**Line by line**

- `<small class="feature-badge">New</small>`: A small "New" label (Session 1: `<small>`). CSS will place it in the corner.

### Step 3.4: Make the card the reference

**Where:** Inside the `.feature-card { }` rule, on the line right after `.feature-card {`.

**Type this:**

```css
  position: relative;
```

**Line by line**

- `position: relative;`: The card does not move, but it becomes the **reference box** for any absolute child inside it.

### Step 3.5: Place the badge with absolute

**Where:** Right **before** the `/* ---------- Video and audio ---------- */` comment. Leave one empty line after it.

**Type this:**

```css
.feature-badge {
  position: absolute;
  top: var(--space-s);
  right: var(--space-s);
  padding: 2px var(--space-s);
  border-radius: var(--radius);
  background-color: var(--color-primary);
  color: var(--color-on-primary);
  font-weight: bold;
}
```

**Line by line**

- `.feature-badge {`: Selects the badge.
- `position: absolute;`: The badge leaves the normal flow and is placed relative to the nearest non-static ancestor: the card.
- `top: var(--space-s);`: 8px from the card's top edge.
- `right: var(--space-s);`: 8px from the card's right edge.
- `padding: 2px var(--space-s);`: A small space inside the badge.
- `border-radius: var(--radius);`: Rounded corners.
- `background-color: var(--color-primary);`: Blue background.
- `color: var(--color-on-primary);`: White text.
- `font-weight: bold;`: Bold text.
- `}`: Ends the rule.

> **Correction:** The PDF's position slides mix things up (one says the parent is `static`, another says `relative`). The rule is simple: an **absolute** element is placed against its **nearest ancestor that is not `static`**. So we give the parent `position: relative`. If no ancestor is positioned, the element is placed against the whole page.

**Demo (do not keep):** Remove `position: relative;` from `.feature-card` and save. The badge jumps to the top-right corner of the **page**, because no ancestor is positioned anymore. Put the line back.

**Say it like this:** "The card is a picture frame and the badge is a sticker. `relative` on the frame says 'measure from me'. `absolute` on the sticker says 'I can go anywhere inside that frame'."

**Students should see:** A blue "New" badge in the top-right corner of the "Plan your week" card.

### Step 3.6: The floating button: HTML

**Where:** In **`index.html` and `planner.html`**, right after `</footer>` and before `</body>`. Leave one empty line first.

**Type this:**

```html
    <!-- Floating button: fixed in the corner of the screen -->
    <a class="button floating-chat" href="assistant.html"><i class="fa fa-comments"></i> Ask AI</a>
```

**Line by line**

- `<!-- Floating button: fixed in the corner of the screen -->`: A comment.
- `<a class="button floating-chat" href="assistant.html"><i class="fa fa-comments"></i> Ask AI</a>`: A link styled as our button (Session 1), with a second class `floating-chat` for its position.

### Step 3.7: Fix it to the corner

**Where:** In `styles.css`, right **before** the `/* ---------- Sections and feature cards ---------- */` comment. Leave one empty line after it.

**Type this:**

```css
.floating-chat {
  position: fixed;
  right: var(--space-m);
  bottom: var(--space-m);
  border-radius: 50px;
}
```

**Line by line**

- `.floating-chat {`: Selects the floating button.
- `position: fixed;`: Placed relative to the **browser window**. It does not move when you scroll.
- `right: var(--space-m);`: 16px from the right edge of the window.
- `bottom: var(--space-m);`: 16px from the bottom edge of the window.
- `border-radius: 50px;`: Very round ends, a "pill" shape.
- `}`: Ends the rule.

> **Note:** The PDF says a fixed element is "locked to the size of the browser's window". More precisely, it is positioned relative to the **window (viewport)** and ignores scrolling.

**Students should see:** An "Ask AI" pill in the bottom-right corner of `index.html` and `planner.html`. It stays there while scrolling.

### Common mistakes

- `position: absolute` without a positioned parent: the element flies to the page corner.
- Forgetting `top: 0` on a sticky element, so it never sticks.
- A sticky navbar with no background: text shows through it while scrolling.
- Using `fixed` for things that should scroll with the page.
- Forgetting the floating button on one of the two pages.

### Quick check

1. The badge is `absolute`. Why does the card need `position: relative`? *(An absolute element is placed against its nearest non-static ancestor.)*
2. What is the difference between `fixed` and `sticky`? *(Fixed always stays in the window. Sticky scrolls normally until it reaches its `top`, then sticks.)*

**Checkpoint:** `checkpoints/session2/phase-03/`

---

## Phase 4: CSS grid (0:45–1:10)

**What we build:** The features section rebuilt with CSS grid. On phones it is one centered column. On wider screens it is two columns, with a big first card that spans two rows.

**Concept in plain words:** A grid is made of horizontal and vertical **lines** that create rows and columns, like a spreadsheet. You put `display: grid` on the **parent** (the grid container), and you describe the columns and rows. Each child (grid item) goes into a cell, or can span several cells by saying which **lines** it starts and ends on.

**Grid lines** are numbered from 1. Two columns have **three** vertical lines:

```text
     line 1      line 2      line 3
       │           │           │
row    ├───────────┼───────────┤  line 1
 1     │  card 1   │  card 2   │
       │  (spans   ├───────────┤  line 2
row    │  rows 1   │  card 3   │
 2     │  and 2)   │           │
       ├───────────┴───────────┤  line 3
```

Card 1 starts at column line 1 and ends at column line 2. It starts at row line 1 and ends at row line 3, so it spans two rows.

### Step 4.1: From flexbox to grid (Change these lines)

**Change these lines** in `styles.css` (the `.feature-list` rule):

```css
.feature-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
```

**to:**

```css
.feature-list {
  display: grid;
  grid-template-columns: 1fr;
}
```

**Line by line**

- `.feature-list {`: The parent of the cards.
- `display: grid;`: The parent becomes a grid container, and the cards become grid items.
- `grid-template-columns: 1fr;`: One column. *(Added by the guide: `fr` means "fraction of the free space". `1fr` = all of it.)*
- `}`: Ends the rule.

**Demo (do not keep):** Change it to `grid-template-columns: 100px 200px 300px;` (the PDF's example). You get three columns of exactly those widths. Then put back `1fr`.

### Step 4.2: Center each card in its cell (justify-self)

**Where:** Inside the `.feature-card { }` rule, on the line right after `.feature-card {`.

**Type this:**

```css
  justify-self: center;
```

**Line by line**

- `justify-self: center;`: Our cards are 250px wide, narrower than the cell. `justify-self` places **one grid item** inside its cell, left to right. Values: `start`, `end`, `center`, `stretch`.

**Say it like this:** "The grid draws the boxes on the floor. `justify-self` decides where you stand inside your box: on the left, on the right, in the middle, or spread across it."

**Students should see:** The same as before on a phone: cards one under the other, centered.

### Step 4.3: Two columns on wider screens

**Where:** Inside the media query, after the `.intro-video { }` rule's closing `}` and before the last `}`. Leave one empty line first.

**Type this:**

```css
  .feature-list {
    grid-template-columns: 1fr 1fr;
    grid-template-rows: auto auto;
  }

  .feature-card {
    width: auto;
    justify-self: stretch;
  }
```

**Line by line**

- `.feature-list {`: The grid container, on screens 768px and wider (Session 1: media queries).
- `grid-template-columns: 1fr 1fr;`: Two columns of equal width.
- `grid-template-rows: auto auto;`: Two rows. `auto` means "as tall as the content".
- `}`: Ends the rule.
- `.feature-card {`: The cards, on wide screens.
- `width: auto;`: Forget the fixed 250px.
- `justify-self: stretch;`: Fill the whole width of the cell.
- `}`: Ends the rule.

**Students should see** (window wider than 768px): Cards in two columns: card 1 and card 2 on the first row, card 3 on the second row.

### Step 4.4: Mark the main card (Change this line)

**Change these lines** in `index.html` (only the **first** card's opening tag changes; the icon line is shown so you find the right card):

```html
          <article class="feature-card">
            <i class="fa fa-lightbulb-o feature-icon"></i>
```

**to:**

```html
          <article class="feature-card feature-card--main">
            <i class="fa fa-lightbulb-o feature-icon"></i>
```

**Line by line**

- `<article class="feature-card feature-card--main">`: The first card gets a second class, so we can place it alone.
- `<i class="fa fa-lightbulb-o feature-icon"></i>`: Unchanged.

### Step 4.5: Place the main card with line numbers

**Where:** Inside the media query, after the `.feature-card { }` rule you just added (after its `}`). Leave one empty line first.

**Type this:**

```css
  .feature-card--main {
    grid-column-start: 1;
    grid-column-end: 2;
    grid-row-start: 1;
    grid-row-end: 3;
  }
```

**Line by line**

- `.feature-card--main {`: The big card.
- `grid-column-start: 1;`: It starts at vertical line 1 (the left edge).
- `grid-column-end: 2;`: It ends at vertical line 2, so it takes one column.
- `grid-row-start: 1;`: It starts at horizontal line 1 (the top).
- `grid-row-end: 3;`: It ends at horizontal line 3, so it spans **two rows**.
- `}`: Ends the rule.

> **Note on the PDF's grid slides:** their diagrams do not come through as text. To be precise: `grid-template-columns` and `grid-template-rows` **create** the tracks (they do not place items). `grid-column-start/end` and `grid-row-start/end` use **line numbers** (starting at 1), not cell numbers. Items you do not place fill the free cells automatically, in order. That is why cards 2 and 3 go into the right column.

**Say it like this:** "Like booking seats in a theater: 'from seat line 1 to line 2, from row line 1 to line 3'. You book two rows for the big card, and the others take the free seats."

**Students should see:** On a wide screen, the light-bulb card fills the left column at full height. "Plan your week" and "Practice for exams" are stacked in the right column. On a phone nothing changed.

### Common mistakes

- Putting `display: grid` on the cards instead of their parent.
- Counting cells instead of lines: to span 2 rows from the top, end at line **3**, not 2.
- Forgetting that `justify-self` goes on the **item**, not on the container.
- Leaving `width: 250px` on wide screens, so cards do not fill their cells.
- Changing every `<article class="feature-card">`. Only the first one gets `feature-card--main`.

### Quick check

1. With `grid-template-columns: 1fr 1fr`, how many vertical lines are there? *(Three.)*
2. Which property centers one grid item inside its cell, left to right? *(`justify-self: center`.)*

**Checkpoint:** `checkpoints/session2/phase-04/`

---

## Phase 5: SASS part 1: setup and variables (1:10–1:25)

**What we build:** The stylesheet becomes a Sass file that compiles into `styles.css`. Our theme moves from CSS variables to Sass variables.

**Concept in plain words:** SASS (Syntactically Awesome Style Sheets) is a **CSS preprocessor**: a language with extra features (variables, nesting, partial files, mixins) that is **compiled** into normal CSS. We write `.scss` files, and a tool turns them into `.css` files. The HTML still loads the `.css` file.

> **Correction:** The PDF says "the browser only reads CSS code and cannot read CSS code". It means: the browser **cannot read SASS code**. That is why we need a compiler. The PDF also titles the section "SAAS". The name is **SASS**.

### Step 5.1: Turn the CSS file into a Sass file

1. In VS Code, right-click `styles.css` → **Rename** → `styles.scss`.
2. At the bottom of VS Code, click **Watch Sass** (from the Live Sass Compiler extension).
3. A new `styles.css` appears next to it (and maybe a `styles.css.map`, which helps DevTools show the `.scss` line. Leave it).

**Say it like this:** "Every CSS file is already valid SCSS. So renaming changes nothing yet, but now a robot rewrites `styles.css` for us every time we save."

**Students should see:** The pages look exactly the same.

> **Rule from now on:** edit **only** `.scss` files. `styles.css` is overwritten on every save.

### Step 5.2: Sass variables

**Where:** In `styles.scss`, at the **very top** of the file, before the `/* ---------- Theme ...` comment. Leave one empty line after it.

**Type this:**

```scss
// Theme: change these values to restyle the whole site
$color-primary: #2563eb;
$color-primary-dark: #1e40af;
$color-visited: #7c3aed;
$color-on-primary: #ffffff;
$color-text: #1f2937;
$color-muted: #6b7280;
$color-background: #ffffff;
$color-surface: #f3f4f6;
$color-border: #d1d5db;
$font-main: Arial, Helvetica, sans-serif;
$space-s: 8px;
$space-m: 16px;
$space-l: 32px;
$radius: 8px;
```

**Line by line**

- `// Theme: change these values to restyle the whole site`: A Sass comment. `//` comments are removed from the compiled CSS.
- `$color-primary: #2563eb;`: A Sass variable starts with `$`. Same value as our old CSS variable.
- `$color-primary-dark`, `$color-visited`, `$color-on-primary`, `$color-text`, `$color-muted`, `$color-background`, `$color-surface`, `$color-border`: The rest of our colors, same names and values as before.
- `$font-main: Arial, Helvetica, sans-serif;`: The font list.
- `$space-s: 8px;`, `$space-m: 16px;`, `$space-l: 32px;`: The spacing sizes.
- `$radius: 8px;`: The corner radius.

### Step 5.3: Use the Sass variables everywhere (find and replace)

Every `var(--name)` must become `$name`. There are 85 of them, so we let VS Code do it:

| Find | Replace |
|---|---|
| `var\(--([a-z-]+)\)` | `$$$1` |

1. Press **Ctrl+H** in `styles.scss`.
2. Click the **`.*`** button (regular expressions) or press **Alt+R**.
3. Type the "Find" and "Replace" values above, then click **Replace All**.

*(Added by the guide: this VS Code trick is not in the PDF.)* In the "Find" box, `([a-z-]+)` remembers the name. In the "Replace" box, `$$` writes a real `$` and `$1` puts the remembered name back.

**No regex?** Use normal Replace All once per name: `var(--color-primary)` → `$color-primary`, `var(--space-m)` → `$space-m`, and so on for the 14 names.

**Example of one line before and after:**

```text
  padding: var(--space-s) var(--space-m);   →   padding: $space-s $space-m;
```

### Step 5.4: Remove the old CSS variables

Nothing uses `var(--...)` anymore, so the old CSS variables can go. (We replaced first and deleted second, so the page never loses its colors in between.)

**Where:** In `styles.scss`, select from the line `/* ---------- Theme: change these values to restyle the whole site ---------- */` down to the next `--radius: 8px;` line (both included), and replace the whole selection with:

```scss
html {
```

You keep `html {`, `font-size: 16px;` and `}`. Only the old comment and the `--` lines disappear.

**Line by line**

- `html {`: The same rule as before, now only holding the base font size.

**Say it like this:** "A Sass variable is a nickname for a value. The compiler replaces every nickname with the real value before the browser sees it."

**Students should see:** The page looks exactly the same. Open `styles.css`: the `$` names are gone, replaced by real values like `#2563eb` and `16px`.

### Common mistakes

- Editing `styles.css` after the switch: the next save overwrites the changes.
- Forgetting to click **Watch Sass**, so `styles.css` is never updated.
- Using a variable before (above) the line that defines it: "Undefined variable".
- Installing the old Live Sass Compiler (Ritwick Dey). Use the one by Glenn Marks.
- Missing `;` at the end of a variable line, which breaks the compile. Read the error in VS Code's **Output** panel.

### Quick check

1. Why does the HTML still link `styles.css` and not `styles.scss`? *(Browsers cannot read Sass. They read the compiled CSS.)*
2. Where do Sass `//` comments go after compiling? *(They are removed. Only `/* */` comments are kept.)*

**Checkpoint:** `checkpoints/session2/phase-05/`

---

## Phase 6: SASS part 2: partials, nesting and mixins (1:25–1:40)

**What we build:** The variables move to their own file, the navbar styles become nested Sass in their own file, and two mixins remove repeated code.

**Concept in plain words:** A **partial** is a small Sass file whose name starts with `_`. It is not compiled on its own; another file loads it. **Nesting** writes child rules inside their parent rule, like HTML. A **mixin** is a reusable group of declarations, like a function for CSS. It can take **arguments**.

### Step 6.1: The variables partial

**Where:** Create a folder `scss`, and inside it a new file `_variables.scss`. **Copy** the variable lines from the top of `styles.scss` and paste them here.

**Type this** (paste):

```scss
// Theme: change these values to restyle the whole site
$color-primary: #2563eb;
$color-primary-dark: #1e40af;
$color-visited: #7c3aed;
$color-on-primary: #ffffff;
$color-text: #1f2937;
$color-muted: #6b7280;
$color-background: #ffffff;
$color-surface: #f3f4f6;
$color-border: #d1d5db;
$font-main: Arial, Helvetica, sans-serif;
$space-s: 8px;
$space-m: 16px;
$space-l: 32px;
$radius: 8px;
```

**Line by line:** The same 15 lines as Step 5.2. They now live in their own file.

### Step 6.2: Load the partial with `@use` (Change these lines)

**Change these lines** at the top of `styles.scss` (the variables now live in the partial, so they leave this file):

```scss
// Theme: change these values to restyle the whole site
$color-primary: #2563eb;
$color-primary-dark: #1e40af;
$color-visited: #7c3aed;
$color-on-primary: #ffffff;
$color-text: #1f2937;
$color-muted: #6b7280;
$color-background: #ffffff;
$color-surface: #f3f4f6;
$color-border: #d1d5db;
$font-main: Arial, Helvetica, sans-serif;
$space-s: 8px;
$space-m: 16px;
$space-l: 32px;
$radius: 8px;
```

**to:**

```scss
@use 'scss/variables' as *;
```

**Line by line**

- `@use 'scss/variables' as *;`: Loads `scss/_variables.scss`. You do not write the `_` or the `.scss`. `as *` lets us write `$color-primary` directly, without a prefix.

> **Added by the guide / Correction:** The PDF uses `@import 'variables';`. `@import` is **deprecated** in current Sass and will be removed. Use `@use`. You will still see `@import` in older tutorials. Each file must `@use` the partials **it** needs, and `@use` lines go at the very top of the file.

**Students should see:** No change. Everything still compiles.

### Step 6.3: Nesting: the navbar partial

**Where:** Create `scss/_navbar.scss`.

**Type this:**

```scss
@use 'variables' as *;

// Navbar: one parent block, with its children nested inside
.navbar {
  position: sticky;
  top: 0;
  z-index: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: $space-m;
  border-bottom: 1px solid $color-border;
  background-color: $color-background;
}
```

**Line by line**

- `@use 'variables' as *;`: This partial needs the variables too. The path is relative to this file, which is already in `scss/`.
- `// Navbar: one parent block, with its children nested inside`: A comment.
- `.navbar {`: The parent rule.
- `position: sticky;`, `top: 0;`, `z-index: 1;`: The sticky navbar from Phase 3.
- `display: flex;`, `flex-direction: column;`, `align-items: center;`: The flex layout (Session 1).
- `padding: $space-m;`, `border-bottom: 1px solid $color-border;`, `background-color: $color-background;`: Spacing, line and background, now with Sass variables.
- `}`: Ends the parent rule (the children go **inside** it next).

### Step 6.4: Nest the logo rules

**Where:** In `_navbar.scss`, inside `.navbar { }`, after the `background-color` line and before the last `}`. Leave one empty line first.

**Type this:**

```scss
  > .brand {
    display: flex;
    align-items: center;
    color: $color-text;
  }

  .brand-logo {
    margin-right: $space-s;
  }
```

**Line by line**

- `> .brand {`: Nested inside `.navbar`, this compiles to `.navbar > .brand`, our child combinator from Phase 1.
- `display: flex;`, `align-items: center;`: Logo and text side by side (from Session 1's `.brand` rule).
- `color: $color-text;`: The dark text from Phase 1.
- `}`: Ends `> .brand`.
- `.brand-logo {`: Compiles to `.navbar .brand-logo` (a descendant combinator).
- `margin-right: $space-s;`: Space next to the logo.
- `}`: Ends `.brand-logo`.

### Step 6.5: Nest the links, with `&:hover`

**Where:** In `_navbar.scss`, after the `.brand-logo { }` block's `}`, still inside `.navbar`. Leave one empty line first.

**Type this:**

```scss
  .nav-links {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }

  .nav-link {
    padding: $space-s $space-m;

    &:hover {
      border-radius: $radius;
      background-color: $color-surface;
    }
  }
```

**Line by line**

- `.nav-links {`: Compiles to `.navbar .nav-links`.
- `display: flex;`, `flex-wrap: wrap;`, `justify-content: center;`: The flex row of links (Session 1).
- `}`: Ends `.nav-links`.
- `.nav-link {`: Compiles to `.navbar .nav-link`.
- `padding: $space-s $space-m;`: Space inside each link.
- `&:hover {`: `&` means "the parent selector itself". This compiles to `.navbar .nav-link:hover`, with no space before the colon.
- `border-radius: $radius;`, `background-color: $color-surface;`: The hover pill from Phase 2.
- `}` (twice): Ends `&:hover`, then ends `.nav-link`.

### Step 6.6: Add `&:active`

**Where:** Inside `.nav-link { }`, after the `&:hover { }` block's `}`. Leave one empty line first.

**Type this:**

```scss
    &:active {
      color: $color-primary-dark;
    }
```

**Line by line**

- `&:active {`: Compiles to `.navbar .nav-link:active`.
- `color: $color-primary-dark;`: Dark blue while clicking.
- `}`: Ends the block.

### Step 6.7: Replace the old navbar rules with the partial

**Where:** In `styles.scss`, delete everything from the line `/* ---------- Navbar ---------- */` down to the line just before `/* ---------- Hero ---------- */`. Then, on the line right after `@use 'scss/variables' as *;`, add:

```scss
@use 'scss/navbar';
```

**Line by line**

- `@use 'scss/navbar';`: Loads `_navbar.scss` and puts its CSS here. No `as *` is needed because we do not use anything **from** this file, we only want its CSS output.

**Say it like this:** "Nesting writes CSS the way HTML is written: children inside parents. Partials are chapters of a book. `styles.scss` is the table of contents."

**Students should see:** The navbar looks and behaves exactly as before. Open `styles.css`: the nested code became `.navbar .nav-link:hover { ... }`.

> **Note:** The PDF imports the header partial **before** the variables partial (`@import 'header'; @import 'variables';`), which fails because the header uses variables that are not loaded yet. With `@use`, each partial loads what it needs, so the order problem disappears.

### Step 6.8: Mixins: a mixin without arguments

**Where:** Create `scss/_mixins.scss`.

**Type this:**

```scss
@use 'variables' as *;

// Mixin without arguments: center the children with flexbox
@mixin flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

**Line by line**

- `@use 'variables' as *;`: The second mixin (next step) uses our variables.
- `// Mixin without arguments: center the children with flexbox`: A comment.
- `@mixin flex-center {`: Creates a mixin called `flex-center`.
- `display: flex;`, `justify-content: center;`, `align-items: center;`: The three lines we write again and again to center things.
- `}`: Ends the mixin.

### Step 6.9: A mixin with an argument

**Where:** At the end of `_mixins.scss`, after an empty line.

**Type this:**

```scss
// Mixin with an argument: a rounded box with a border and a background
@mixin box($background) {
  padding: $space-m;
  border: 1px solid $color-border;
  border-radius: $radius;
  background-color: $background;
}
```

**Line by line**

- `// Mixin with an argument: a rounded box with a border and a background`: A comment.
- `@mixin box($background) {`: A mixin that takes one **argument**, `$background`: the box color.
- `padding: $space-m;`: Space inside.
- `border: 1px solid $color-border;`: A thin border.
- `border-radius: $radius;`: Rounded corners.
- `background-color: $background;`: Uses whatever color we pass in.
- `}`: Ends the mixin.

### Step 6.10: Use the `box` mixin

**Where:** In `styles.scss`, on the line right after `@use 'scss/variables' as *;`:

```scss
@use 'scss/mixins' as *;
```

**Change these lines** inside `.feature-card { }`:

```scss
  padding: $space-m;
  border: 1px solid $color-border;
  border-radius: $radius;
  background-color: $color-surface;
```

**to:**

```scss
  @include box($color-surface);
```

**Change these lines** inside `.chat-tips { }`:

```scss
  padding: $space-m;
  border-radius: $radius;
  background-color: $color-surface;
```

**to:**

```scss
  @include box($color-surface);
```

**Line by line**

- `@use 'scss/mixins' as *;`: Loads our mixins.
- `@include box($color-surface);` (twice): Pastes the four lines of the mixin here, with `$background` set to `$color-surface`.

### Step 6.11: Use `flex-center` in the navbar

**Where:** In `_navbar.scss`, on the line right after `@use 'variables' as *;`:

```scss
@use 'mixins' as *;
```

**Change these lines** inside `.nav-links { }`:

```scss
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
```

**to:**

```scss
    @include flex-center;
    flex-wrap: wrap;
```

**Line by line**

- `@use 'mixins' as *;`: This partial now needs the mixins.
- `@include flex-center;`: Brings in `display: flex`, `justify-content: center` and `align-items: center`.
- `flex-wrap: wrap;`: Kept, because the mixin does not include it.

**Say it like this:** "A mixin is a recipe. `@include` is 'cook that recipe here'. An argument is the ingredient you choose each time: same recipe, different color."

**Students should see:** Everything as before. The tips box on `assistant.html` now also has a thin border (the `box` mixin includes one).

### Common mistakes

- Naming a partial without `_`: Live Sass Compiler then makes an extra `.css` file for it.
- Forgetting `@use 'variables' as *;` at the top of a partial that uses variables: "Undefined variable".
- Writing `& :hover` (with a space) or `:hover` without `&` inside a nested block. That compiles to a descendant selector.
- `@include box;` without the argument: "Missing argument $background".
- Putting `@use` below other rules. It must be at the top of the file.

### Quick check

1. What does `&:hover` compile to inside `.nav-link { }`? *(`.nav-link:hover`, prefixed by its parents.)*
2. What is the difference between a mixin with and without arguments? *(With arguments you can change some values each time you include it.)*

**Checkpoint:** `checkpoints/session2/phase-06/`

---

## Phase 7: `@font-face`: a custom font (1:40–1:50)

**What we build:** All headings use Poppins Bold, loaded from our own `.woff2` file.

**Concept in plain words:** `@font-face` teaches the browser a new font: you give it a name and the path to the font file. After that, you use that name in `font-family` like any other font.

### Step 7.1: Add the font file

Copy the `fonts` folder from the starter assets into the project (next to `index.html`). It contains `poppins-bold.woff2` and `OFL.txt` (the free license).

### Step 7.2: Declare the font

**Where:** In `styles.scss`, after the `@use` lines (right after `@use 'scss/navbar';`). Leave one empty line first.

**Type this:**

```scss
// Custom font: load Poppins Bold from our own file
@font-face {
  font-family: "Poppins";
  src: url("fonts/poppins-bold.woff2") format("woff2");
  font-weight: bold;
  font-style: normal;
}
```

**Line by line**

- `// Custom font: load Poppins Bold from our own file`: A comment.
- `@font-face {`: Starts a font declaration.
- `font-family: "Poppins";`: The name we choose for this font.
- `src: url("fonts/poppins-bold.woff2") format("woff2");`: Where the file is, and its format. The path is relative to the **compiled `styles.css`** (in the project root), not to the `.scss` file.
- `font-weight: bold;`: This file is the **bold** version. Headings are bold, so they will use it.
- `font-style: normal;`: Not italic.
- `}`: Ends the declaration.

> **Correction:** The PDF's example loads a `.eot` file. EOT is an old format that only Internet Explorer used. Today, use **`.woff2`**: small, compressed, and supported by every modern browser.

### Step 7.3: A variable for the heading font

**Where:** In `scss/_variables.scss`, on the line right after `$font-main: ...;`.

**Type this:**

```scss
$font-heading: "Poppins", Arial, sans-serif;
```

**Line by line**

- `$font-heading: "Poppins", Arial, sans-serif;`: Our font first. If it cannot load, the browser uses Arial, then any sans-serif font.

### Step 7.4: Use it for headings

**Where:** In `styles.scss`, in the Base section, right **before** the `a {` rule. Leave one empty line after it.

**Type this:**

```scss
h1, h2, h3 {
  font-family: $font-heading;
}
```

**Line by line**

- `h1, h2, h3 {`: All three heading levels (Session 1: multiple selectors).
- `font-family: $font-heading;`: Use Poppins.
- `}`: Ends the rule.

**Say it like this:** "`@font-face` is introducing a new friend to the browser: 'this is Poppins, and here is where she lives'. After that, you can call her by name."

**Students should see:** All headings ("Study smarter with AI", "What it can do"...) switch to Poppins, a rounder geometric font. In DevTools → Network, `poppins-bold.woff2` loads with status 200.

### Common mistakes

- A wrong path: `url("../fonts/...")` copied from a tutorial. Our `styles.css` is in the root, so it is `fonts/...`.
- Different names in `@font-face` and `font-family` (`"Poppins"` vs `"poppins bold"`).
- Forgetting to copy the `fonts` folder: the browser silently falls back to Arial.
- Opening the page without Live Server. Some browsers block local font files on `file://`.

### Quick check

1. Which font format should you use today? *(`.woff2`.)*
2. The `@font-face` is in `styles.scss`. Why is the path `fonts/...` and not `../fonts/...`? *(The browser reads the compiled `styles.css`, which is in the project root.)*

**Checkpoint:** `checkpoints/session2/phase-07/`

---

## Phase 8: Bootstrap part 1: link, navbar, container, rows, columns (1:50–2:10)

**What we build:** We rebuild **one** page, `assistant.html`, with Bootstrap, to see the shortcut. Bootstrap's navbar replaces ours, and the page uses Bootstrap's container and 12-column grid. `index.html` and `planner.html` stay on our own CSS.

**Concept in plain words:** Bootstrap is a big library of ready-made CSS (and some JavaScript). You add one `<link>`, then you use its **class names** in your HTML. Copying ready-made code from the Bootstrap docs and adapting it is called **snippeting**. Its **grid** cuts each row into 12 equal columns: `col-md-8` + `col-md-4` = 12.

> **Why only one page?** Bootstrap also has a class called `navbar` (and others). If we loaded Bootstrap **and** our `styles.css` on the same page, the two `.navbar` rules would fight. So this page uses Bootstrap only. That is also the honest comparison: compare the two pages' code at the end.

### Step 8.1: Swap our stylesheet for Bootstrap (Change this line)

**Change this line** in the `<head>` of `assistant.html`:

```html
    <link rel="stylesheet" href="styles.css">
```

**to:**

```html
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css">
```

**Line by line**

- `<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css">`: Loads Bootstrap 5.3.8's CSS from a CDN.

> **Correction:** The PDF links **Bootstrap 3.4.1** (`maxcdn.bootstrapcdn.com/bootstrap/3.4.1`), but its examples use newer class names like `col-8` and `btn-secondary` that do not exist in version 3. We use **Bootstrap 5** with a current link. *(Added by the guide.)* Also, the PDF says to put the link "inside the section of your HTML page". The missing word is **head**: the `<link>` goes inside `<head>`.

**Students should see:** The page loses our styles and gets Bootstrap's base look: a different font, plain bubbles, the old header unstyled.

### Step 8.2: Bootstrap's navbar (snippet)

**Where:** In `assistant.html`, select from the line `<!-- Header: logo and navigation links -->` down to the next `</header>` line (both included), and replace it with:

```html
    <!-- Header: Bootstrap navbar (snippet adapted from the Bootstrap docs) -->
    <header class="navbar navbar-expand-md bg-body-tertiary" id="top">
      <div class="container">
        <a class="navbar-brand brand" href="index.html" title="Go to the home page">
          <img class="brand-logo" src="images/logo.svg" alt="AI Student Assistant logo" width="40" height="40">
          AI Student Assistant
        </a>
        <nav class="navbar-nav nav-links">
          <a class="nav-link" href="index.html">Home</a>
          <a class="nav-link active" href="assistant.html">Assistant</a>
          <a class="nav-link" href="planner.html">Planner</a>
        </nav>
      </div>
    </header>
```

**Line by line**

- `<!-- Header: Bootstrap navbar (snippet adapted from the Bootstrap docs) -->`: A comment saying where it comes from.
- `<header class="navbar navbar-expand-md bg-body-tertiary" id="top">`: `navbar` is Bootstrap's navigation bar. `navbar-expand-md` shows the links in a row from medium screens (768px) up. `bg-body-tertiary` is a light grey background. We keep `id="top"` for "Back to top".
- `<div class="container">`: Keeps the navbar content aligned with the page content below.
- `<a class="navbar-brand brand" href="index.html" title="Go to the home page">`: `navbar-brand` styles the logo link. We keep our `brand` class too, as a label for future restyling.
- `<img class="brand-logo" src="images/logo.svg" alt="AI Student Assistant logo" width="40" height="40">`: Our logo (unchanged).
- `AI Student Assistant`: The site name.
- `</a>`: Closes the brand link.
- `<nav class="navbar-nav nav-links">`: `navbar-nav` styles the group of links.
- `<a class="nav-link" href="index.html">Home</a>`: `nav-link` is Bootstrap's link class. It has the same name as ours, so this line did not even change.
- `<a class="nav-link active" href="assistant.html">Assistant</a>`: `active` highlights the current page.
- `<a class="nav-link" href="planner.html">Planner</a>`: Third link.
- `</nav>`, `</div>`, `</header>`: Close the links, the container and the header.

> Bootstrap's docs show a "hamburger" button that opens the menu on phones. That button needs Bootstrap's JavaScript, which comes in a later session, so we leave it out. On phones the links simply stack.

**Students should see:** A light grey navbar: logo and name on the left, three links on the right; "Assistant" is darker (active).

### Step 8.3: Container, row and columns

**Where:** In `assistant.html`, right **before** the line `<!-- Main content: the chat and a sidebar with tips -->`. Leave one empty line after it. (For a few minutes, the page has the new layout **and** the old one below it.)

**Type this:**

```html
    <!-- Main content: a Bootstrap container with one row and two columns -->
    <main class="chat-page container my-4">
      <div class="row g-4">
        <section class="chat col-md-8">
          <h1 class="page-title">Ask the assistant</h1>
        </section>

        <!-- Sidebar: tips, a warning alert and a progress bar -->
        <aside class="chat-tips col-md-4">
          <h2 class="tips-title">Tips for good questions</h2>
        </aside>
      </div>
    </main>
```

**Line by line**

- `<!-- Main content: a Bootstrap container with one row and two columns -->`: A comment.
- `<main class="chat-page container my-4">`: `container` centers the content with a maximum width and side padding. `my-4` adds space above and below *(Added by the guide: a Bootstrap spacing class, m = margin, y = top and bottom, 4 = size)*. We keep our `chat-page` class as a label.
- `<div class="row g-4">`: A **row**, a horizontal line of columns. `g-4` is the gutter, the space between columns *(added by the guide)*.
- `<section class="chat col-md-8">`: From medium screens up, this column takes **8 of the 12** parts. On phones it takes the full width.
- `<h1 class="page-title">Ask the assistant</h1>`: The page title.
- `</section>`: Closes the chat column.
- `<!-- Sidebar: tips, a warning alert and a progress bar -->`: A comment.
- `<aside class="chat-tips col-md-4">`: The other **4 of 12** parts: 8 + 4 = 12, one full row.
- `<h2 class="tips-title">Tips for good questions</h2>`: The sidebar title.
- `</aside>`, `</div>`, `</main>`: Close the column, the row and the main box.

> **Correction:** The PDF lists Bootstrap's screen sizes as **xs, sm, md, lg**. Those are Bootstrap **3** names. Bootstrap **5** uses **sm** (576px), **md** (768px), **lg** (992px), **xl** (1200px) and **xxl** (1400px). Plain `col-8` (no size) applies on every screen. `col-md-8` applies from 768px up, and below that the column takes the full width.

> **Correction:** The PDF says the container is "as essential as the body tag". To be precise, the `container` goes **inside** `<body>` and holds the rows. Rows hold columns. Your content goes **inside the columns**.

**Demo (do not keep):** Change `container` to `container-fluid` and save. The content now spans the full window width. Change it back.

**Say it like this:** "Bootstrap's grid is a chocolate bar with 12 squares. Every row is one bar. You decide how many squares each column gets, and they must add up to 12."

### Step 8.4: The tips list (copy it from the old page)

**Where:** Inside the new `<aside>`, on the line right after `<h2 class="tips-title">Tips for good questions</h2>`.

**Type this** (copy the `<ul>` from the old `<main>` below and add two spaces of indentation):

```html
          <ul class="tips-list">
            <li>Name the topic and your level.</li>
            <li>Ask for an example.</li>
            <li>Ask it to explain "like I am 12 years old".</li>
          </ul>
```

**Line by line:** The same list as Session 1 (`ul` and `li`), inside the new column.

### Step 8.5: Delete the old main content

**Where:** In `assistant.html`, delete everything from the line `<!-- Main content: the chat and a sidebar with tips -->` down to the next `</main>` line (both included), and the empty line after it. (The chat bubbles and the form come back in Phase 9, built with Bootstrap.)

### Step 8.6: The footer in a container (Change this line)

**Change this line:**

```html
    <footer class="footer">
```

**to:**

```html
    <footer class="footer container">
```

**Line by line**

- `<footer class="footer container">`: The footer text gets the same width and side padding as the content.

**Students should see:** On a laptop, two columns: "Ask the assistant" on the left (wide), the tips on the right (narrow). Make the window narrow (below 768px): the tips go under the title. Nothing scrolls sideways.

### Common mistakes

- Using Bootstrap 3 class names from old tutorials (`col-xs-6`, `navbar-default`). Check the docs version (5.3).
- Putting columns directly in a container without a `row`, so the gutters and alignment break.
- Columns that add up to more than 12: the last ones wrap to a new line.
- Loading our `styles.css` **and** Bootstrap on the same page, so the two `.navbar` rules fight.
- Putting the Bootstrap `<link>` in `<body>` instead of `<head>`.

### Quick check

1. What do `col-md-8` and `col-md-4` do on a phone? *(Each takes the full width, so they stack.)*
2. What is the difference between `container` and `container-fluid`? *(`container` has a maximum width and is centered; `container-fluid` always takes the full width.)*

**Checkpoint:** `checkpoints/session2/phase-08/`

---

## Phase 9: Bootstrap part 2: alerts, form, buttons, progress bar (2:10–2:30)

**What we build:** The chat bubbles as Bootstrap alerts, the question form with Bootstrap buttons, and a warning alert and a progress bar in the sidebar. With these, the page is complete.

**Concept in plain words:** Bootstrap components are ready-made designs: you write the right classes and Bootstrap draws the rest. Colors come from **contextual names** that repeat everywhere: `primary`, `secondary`, `success`, `danger`, `warning`, `info`, `light`, `dark`.

### Step 9.1: Alerts as chat bubbles

**Where:** Inside the chat column, on the line right after `<h1 class="page-title">Ask the assistant</h1>`.

**Type this:**

```html
          <!-- Example conversation: Bootstrap alerts used as chat bubbles -->
          <div class="chat-history">
            <div class="chat-bubble chat-bubble--user alert alert-primary"><i class="fa fa-user"></i> What is machine learning?</div>
            <div class="chat-bubble chat-bubble--ai alert alert-secondary"><i class="fa fa-graduation-cap"></i> It is a way to teach computers with examples instead of writing every rule by hand.</div>
            <div class="chat-bubble chat-bubble--user alert alert-primary"><i class="fa fa-user"></i> Can you give me an example?</div>
            <div class="chat-bubble chat-bubble--ai alert alert-secondary"><i class="fa fa-graduation-cap"></i> Sure! A spam filter learns from thousands of emails which ones are spam.</div>
          </div>
```

**Line by line**

- `<!-- Example conversation: Bootstrap alerts used as chat bubbles -->`: A comment.
- `<div class="chat-history">`: Our box for messages (our class kept as a label).
- `<div class="chat-bubble chat-bubble--user alert alert-primary"><i class="fa fa-user"></i> What is machine learning?</div>`: `alert` makes a box with padding, a border and rounded corners. `alert-primary` makes it blue. Our classes stay for future restyling, and the Font Awesome icon (Session 1) goes before the text.
- `<div class="chat-bubble chat-bubble--ai alert alert-secondary"><i class="fa fa-graduation-cap"></i> It is a way to teach computers...</div>`: `alert-secondary` is grey, for the AI.
- The next two lines: the second question (`alert-primary`) and the second answer (`alert-secondary`).
- `</div>`: Closes the chat history.

**Students should see:** Four colored boxes: blue for the student, grey for the AI.

### Step 9.2: The form with a row inside (select)

**Where:** Inside the chat column, right **before** `</section>`.

**Type this:**

```html
          <!-- Question form: a Bootstrap row inside the form -->
          <form class="chat-form">
            <div class="row">
              <div class="col-md-4 mb-3">
                <label class="form-label" for="subject">Subject</label>
                <select class="form-select" id="subject" name="subject">
                  <option value="math">Math</option>
                  <option value="physics">Physics</option>
                  <option value="coding">Coding</option>
                  <option value="english">English</option>
                </select>
              </div>
            </div>
          </form>
```

**Line by line**

- `<!-- Question form: a Bootstrap row inside the form -->`: A comment.
- `<form class="chat-form">`: Our form (Session 1).
- `<div class="row">`: A row **inside** the form: the grid works anywhere, not only for the page layout.
- `<div class="col-md-4 mb-3">`: 4 of 12 columns for the subject. `mb-3` adds space below *(added by the guide)*.
- `<label class="form-label" for="subject">Subject</label>`: `form-label` is Bootstrap's label style *(added by the guide: form classes snippeted from the docs)*.
- `<select class="form-select" id="subject" name="subject">`: `form-select` gives the drop-down Bootstrap's look and full width.
- `<option value="math">Math</option>` (and the other three): Same options as Session 1.
- `</select>`, `</div>`, `</div>`, `</form>`: Close the drop-down, the column, the row and the form.

### Step 9.3: The textarea column

**Where:** Inside the form's row, after the subject column's `</div>` and before the row's `</div>`.

**Type this:**

```html
              <div class="col-md-8 mb-3">
                <label class="form-label" for="question">Your question</label>
                <textarea class="form-control" id="question" name="question" rows="4" placeholder="Type your question here..."></textarea>
              </div>
```

**Line by line**

- `<div class="col-md-8 mb-3">`: The other 8 columns: 4 + 8 = 12.
- `<label class="form-label" for="question">Your question</label>`: The label.
- `<textarea class="form-control" id="question" name="question" rows="4" placeholder="Type your question here..."></textarea>`: `form-control` gives the text box full width, padding and a border. We no longer need `cols`.
- `</div>`: Closes the column.

### Step 9.4: Bootstrap buttons

**Where:** Inside the form, after the row's `</div>`, right **before** `</form>`.

**Type this:**

```html
            <button class="btn btn-primary" type="submit"><i class="fa fa-paper-plane"></i> Send</button>
            <button class="btn btn-secondary" type="reset">Clear</button>
            <button class="btn btn-link" type="button">New chat</button>
```

**Line by line**

- `<button class="btn btn-primary" type="submit"><i class="fa fa-paper-plane"></i> Send</button>`: `btn` is the base button style. `btn-primary` makes it blue.
- `<button class="btn btn-secondary" type="reset">Clear</button>`: A grey button.
- `<button class="btn btn-link" type="button">New chat</button>`: A button that looks like a link.

**Demo (do not keep):** Change `btn-secondary` to `btn-success`, `btn-danger`, `btn-warning`, `btn-info`, `btn-light` and `btn-dark` (the PDF's list). Then change it back.

**Say it like this:** "In Session 1 we wrote 12 lines of CSS for one button. Here it is two words: `btn btn-primary`. That is the shortcut, and the price is that every Bootstrap site looks a bit the same."

### Step 9.5: A warning alert and a progress bar

**Where:** In the sidebar, on the line right after the tips list's `</ul>`.

**Type this:**

```html
          <div class="alert alert-warning" role="alert">AI can make mistakes. Check important answers with your teacher.</div>
          <p>Questions used today: 3 of 10</p>
          <div class="progress" role="progressbar" aria-label="Questions used today" aria-valuenow="30" aria-valuemin="0" aria-valuemax="100">
            <div class="progress-bar" style="width: 30%">30%</div>
          </div>
```

**Line by line**

- `<div class="alert alert-warning" role="alert">AI can make mistakes. Check important answers with your teacher.</div>`: A yellow warning box. `role="alert"` tells screen readers this is an important message.
- `<p>Questions used today: 3 of 10</p>`: A label for the bar.
- `<div class="progress" role="progressbar" aria-label="Questions used today" aria-valuenow="30" aria-valuemin="0" aria-valuemax="100">`: The grey track of the bar. `role` and the `aria-` attributes describe the bar (30 out of 100) for screen readers.
- `<div class="progress-bar" style="width: 30%">30%</div>`: The blue filled part. Its width (inline CSS, Session 1) sets how full it is, and the text shows the value.
- `</div>`: Closes the track.

> **Note:** In the PDF's example, `role="progressbar"` and the `aria-` attributes are on the inner `.progress-bar` (Bootstrap 4 style). In Bootstrap 5.3 they go on the outer `.progress` div, as above.

**Students should see** (the final page): A Bootstrap navbar; blue and grey message boxes; a form with the subject and the question side by side on a laptop (stacked on a phone); three buttons; and in the sidebar the tips, a yellow warning and a progress bar at 30%.

### Common mistakes

- Writing only `btn-primary` without `btn` (or `alert-primary` without `alert`): the shape is missing.
- Changing the progress text to 50% but forgetting the `width` (or the reverse).
- Using `form-control` on a `<select>`: in Bootstrap 5, a select uses `form-select`.
- Expecting buttons to do something: they still need JavaScript (next session).
- Adding Bootstrap's JavaScript components (dropdowns, collapse) without its JS file.

### Quick check

1. Which two classes make a blue Bootstrap button? *(`btn btn-primary`)*
2. Name two things Bootstrap gave us that took many lines of our own CSS in Session 1. *(For example the navbar, buttons, the two-column layout, or the form field styles.)*

**Checkpoint:** `checkpoints/session2/phase-09/` (final project)

---

## Phase 10: Wrap-up, homework and next session (2:30–2:40)

### Recap (3 minutes)

Open `index.html` (our own CSS, compiled from Sass) next to `assistant.html` (Bootstrap). Ask: "Which one was faster to build? Which one is easier to make unique?" There is no wrong answer. Professionals use both.

### Homework: learn CSS by playing games

| Game | Link | What it practices |
|---|---|---|
| Flexbox Froggy | <https://flexboxfroggy.com/> | Flexbox: `justify-content`, `align-items`, `flex-direction`, `flex-wrap`, `order`... (24 levels; the last one is hard) |
| Grid Garden | <https://cssgridgarden.com/> | CSS grid: lines, `grid-column`, `grid-row`, templates (28 levels) |
| CSS Diner | <https://flukeout.github.io/> | Selectors: types, classes, combinators, pseudo-classes such as `:first-child` and `:not()` (32 levels) |

> **Note:** The PDF says CSS Diner has 26 levels. The current version has 32.

### Next session: JavaScript

JavaScript will finally make the page **do** things:

- The **Send** button will read the question from the form.
- New chat bubbles will appear in the conversation.
- Later, the question will go to a real AI model and the answer will come back into a bubble.
- The **New chat** button and Bootstrap's phone menu will work.

---

## Appendix A: Corrections to the PDF

| PDF says | Correct version | Where |
|---|---|---|
| `a:link` and `a:visited` use the same color | Use two colors, so you can see the difference; order: link, visited, hover, active | Phase 2 |
| `:active` = "selected link" | `:active` = while being clicked | Phase 2 |
| Absolute child: parent is `static` (one slide) vs `relative` (another) | An absolute element is placed against its nearest **non-static** ancestor, so the parent needs `position: relative` | Phase 3 |
| Fixed is "locked to the size of the browser's window" | Fixed is positioned relative to the viewport and ignores scrolling | Phase 3 |
| Sticky (no `top` mentioned) | Sticky needs `top` (or another side) to work | Phase 3 |
| Grid slides (diagrams missing as text) | Template properties create tracks; start/end use **line numbers** from 1; unplaced items fill free cells | Phase 4 |
| "SAAS" | SASS | Phase 5 |
| The browser "cannot read CSS code" | The browser cannot read **SASS** code | Phase 5 |
| `@import 'header'; @import 'variables';` | `@import` is deprecated: use `@use`. Also, the header was imported before the variables it needs | Phase 6 |
| `@font-face` with a `.eot` file | Use `.woff2` | Phase 7 |
| Bootstrap 3.4.1 link with `col-8`, `btn-secondary` (v4/v5 classes) | Bootstrap 5.3.8 link and Bootstrap 5 classes | Phase 8 |
| Screen sizes xs, sm, md, lg | Bootstrap 3 names; Bootstrap 5 uses sm, md, lg, xl, xxl | Phase 8 |
| Link "inside the section of your HTML page" | Inside the `<head>` section | Phase 8 |
| "Container is as essential as the body tag" | The container goes **inside** `<body>`; rows inside the container; columns inside rows | Phase 8 |
| Progress bar with `role` on the inner bar | Bootstrap 5.3 puts `role` and `aria-` attributes on the outer `.progress` | Phase 9 |
| CSS Diner has 26 levels | It has 32 | Phase 10 |

## Appendix B: Added by the guide

The two expected additions:

- **Bootstrap 5** (5.3.8 CDN link and Bootstrap 5 classes) instead of the PDF's Bootstrap 3 link.
- **`@use`** instead of `@import` for Sass partials, with `as *` to use variables and mixins without a prefix.

Other small additions, each marked in the phase:

- `z-index: 1` on the sticky navbar, so the positioned badge slides under it (Phase 3).
- The `fr` unit and `auto` row height in grid (Phase 4).
- VS Code's regular-expression find and replace to convert `var(--x)` to `$x` (Phase 5).
- Choosing the Live Sass Compiler by Glenn Marks (the PDF names the extension but not the publisher).
- From the Bootstrap docs (snippeting, as the PDF suggests): `navbar-expand-md`, `navbar-brand`, `navbar-nav`, `active`, `bg-body-tertiary`, `form-label`, `form-select`, `form-control`, and the spacing classes `my-4`, `mb-3`, `g-4`.

## Appendix C: Time check and what was trimmed

- **Teaching time:** 2 h 30 for the six topics (combinators and pseudo-classes 20 min, position 25, grid 25, SASS 30, `@font-face` 10, Bootstrap 40), plus a 10-minute wrap-up: **about 2 h 40 in total**. If you need to finish at exactly 2 h 30, shorten the wrap-up to the homework table only.
- **Trimmed:** grid is used on the features section only (not on the planner). `display: inline-grid` is only mentioned. Mixins are used in three places instead of everywhere. Only one Bootstrap page. Bootstrap's JavaScript components (dropdown, the collapsing phone menu) are left for after JavaScript.
- **Fast lane:** in Phase 8, students copy the tips list from the old page. In Phase 9, the four alert lines can be pasted from `phase-09`.

## Appendix D: How this guide was checked

- The guide starts from `checkpoints/session1/phase-12/`. Every "Type this" and "Change this line" block is generated from the same step list that builds the checkpoints. Applying all steps reproduces `phase-09` exactly, including `styles.css`.
- After **every** step that touches a `.scss` file, the project was compiled with Dart Sass 1.105.1 (the same compiler Live Sass Compiler uses), with zero errors and zero warnings.
- The Sass conversion was checked with screenshots: `index.html`, `planner.html` and `assistant.html` are **pixel-identical** before (Phase 4, plain CSS) and after (Phase 5, compiled Sass). Phase 6 changes only `assistant.html`, on purpose (the tips box gains a border from the `box` mixin).
- All 9 checkpoints were checked for balanced tags, unique ids, one `<main>` per page, working internal links, existing local files (including the font in the compiled CSS), valid CSS, and no JavaScript.
- Every page of every checkpoint was rendered in Microsoft Edge at 375px (phone) with no horizontal scrolling. The final pages were also checked at 1280px.
- Session 1 topics are only used, never re-taught. They appear as one-line "(Session 1)" reminders.

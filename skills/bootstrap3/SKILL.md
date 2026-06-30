---
name: bootstrap3
license: MIT
description: Use when working with Bootstrap 3 (v3.3.6) — grid, components, JS plugins, forms, responsive utilities
---

# Bootstrap 3 Skill

Bootstrap 3.3.6 — mobile-first responsive HTML/CSS/JS framework. Source: official BootstrapDocs v3.3.6 documentation (11 pages).

## When to Use This Skill

Use when:

- Building responsive layouts with Bootstrap's 12-column grid
- Adding UI components: navbars, modals, dropdowns, alerts, panels, tabs
- Using JS plugins: tooltips, popovers, collapse, carousel, modal
- Styling forms, tables, buttons with Bootstrap classes
- Debugging glyphicons, accessibility attributes, or responsive breakpoints
- Working in ServiceNow Service Portal (uses Bootstrap 3 internally)

## Key Concepts

### Grid System

12-column fluid grid. Four breakpoints:

| Class prefix | Viewport | Device        |
| ------------ | -------- | ------------- |
| `.col-xs-*`  | < 768px  | Phone         |
| `.col-sm-*`  | ≥ 768px  | Tablet        |
| `.col-md-*`  | ≥ 992px  | Desktop       |
| `.col-lg-*`  | ≥ 1200px | Large desktop |

Columns must sum to 12 per row. Rows go inside `.container` or `.container-fluid`.

### JavaScript Plugin Pattern

All JS plugins initialize via data attributes OR jQuery:

```html
<!-- data-attribute (no JS needed) -->
<button
  data-toggle="modal"
  data-target="#myModal">
  Open
</button>

<!-- jQuery -->
$('#myModal').modal('show')
```

### Contextual Color Classes

Used across alerts, buttons, labels, panels, tables:

- `default` / `primary` / `success` / `info` / `warning` / `danger`

---

## Quick Reference

### Grid Layout

```html
<div class="container">
  <div class="row">
    <div class="col-md-8">Main content</div>
    <div class="col-md-4">Sidebar</div>
  </div>
</div>
```

Offset columns: `col-md-offset-4` — pushes right by 4 columns.  
Push/pull: `col-md-push-4` / `col-md-pull-4` — reorder visually.

### Buttons

```html
<button
  type="button"
  class="btn btn-default">
  Default
</button>
<button
  type="button"
  class="btn btn-primary">
  Primary
</button>
<button
  type="button"
  class="btn btn-success btn-lg">
  Large Success
</button>
<button
  type="button"
  class="btn btn-danger btn-sm">
  Small Danger
</button>

<!-- Icon button with aria-label for accessibility -->
<button
  type="button"
  class="btn btn-default"
  aria-label="Search">
  <span
    class="glyphicon glyphicon-search"
    aria-hidden="true"></span>
</button>
```

Sizes: `btn-lg` / `btn-sm` / `btn-xs` / `btn-block` (full width).

### Alerts

```html
<div
  class="alert alert-success"
  role="alert">
  Success message
</div>
<div
  class="alert alert-info"
  role="alert">
  Info message
</div>
<div
  class="alert alert-warning"
  role="alert">
  Warning message
</div>
<div
  class="alert alert-danger"
  role="alert">
  Danger message
</div>

<!-- Dismissible alert (requires alerts JS plugin) -->
<div
  class="alert alert-warning alert-dismissible"
  role="alert">
  <button
    type="button"
    class="close"
    data-dismiss="alert"
    aria-label="Close">
    <span aria-hidden="true">&times;</span>
  </button>
  Warning! Check your input.
</div>
```

### Dropdown

```html
<div class="dropdown">
  <button
    class="btn btn-default dropdown-toggle"
    type="button"
    id="dropdownMenu1"
    data-toggle="dropdown"
    aria-haspopup="true"
    aria-expanded="true">
    Dropdown
    <span class="caret"></span>
  </button>
  <ul
    class="dropdown-menu"
    aria-labelledby="dropdownMenu1">
    <li><a href="#">Action</a></li>
    <li><a href="#">Another action</a></li>
    <li
      role="separator"
      class="divider"></li>
    <li><a href="#">Separated link</a></li>
  </ul>
</div>
```

Right-align: add `dropdown-menu-right` to `.dropdown-menu`.  
Open upward: add `dropup` to parent instead of `dropdown`.

### Navbar

```html
<nav class="navbar navbar-default">
  <div class="container-fluid">
    <div class="navbar-header">
      <button
        type="button"
        class="navbar-toggle collapsed"
        data-toggle="collapse"
        data-target="#navbar1"
        aria-expanded="false">
        <span class="sr-only">Toggle navigation</span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <a
        class="navbar-brand"
        href="#">
        Brand
      </a>
    </div>
    <div
      class="collapse navbar-collapse"
      id="navbar1">
      <ul class="nav navbar-nav">
        <li class="active"><a href="#">Home</a></li>
        <li><a href="#">About</a></li>
      </ul>
    </div>
  </div>
</nav>
```

Variants: `navbar-default` / `navbar-inverse`.  
Position: `navbar-fixed-top` / `navbar-fixed-bottom` / `navbar-static-top`.  
Fixed navbars require `padding-top: 70px` on `<body>`.

### Forms

```html
<!-- Vertical (default) -->
<form>
  <div class="form-group">
    <label for="email">Email</label>
    <input
      type="email"
      class="form-control"
      id="email"
      placeholder="Email" />
    <span class="help-block">Example block-level help text.</span>
  </div>
  <div class="form-group has-error">
    <label
      class="control-label"
      for="inputError">
      Input with error
    </label>
    <input
      type="text"
      class="form-control"
      id="inputError" />
  </div>
  <button
    type="submit"
    class="btn btn-primary">
    Submit
  </button>
</form>

<!-- Horizontal form -->
<form class="form-horizontal">
  <div class="form-group">
    <label
      class="col-sm-2 control-label"
      for="inputEmail">
      Email
    </label>
    <div class="col-sm-10">
      <input
        type="email"
        class="form-control"
        id="inputEmail" />
    </div>
  </div>
</form>
```

Validation states: `has-success` / `has-warning` / `has-error` on `.form-group`.

### Input Group

```html
<!-- Prepend addon -->
<div class="input-group">
  <span class="input-group-addon">@</span>
  <input
    type="text"
    class="form-control"
    placeholder="Username" />
</div>

<!-- Append button -->
<div class="input-group">
  <input
    type="text"
    class="form-control" />
  <span class="input-group-btn">
    <button
      class="btn btn-default"
      type="button">
      Go!
    </button>
  </span>
</div>
```

### Modal

```html
<!-- Trigger -->
<button
  type="button"
  class="btn btn-primary"
  data-toggle="modal"
  data-target="#myModal">
  Launch modal
</button>

<!-- Modal -->
<div
  class="modal fade"
  id="myModal"
  tabindex="-1"
  role="dialog"
  aria-labelledby="myModalLabel">
  <div
    class="modal-dialog"
    role="document">
    <div class="modal-content">
      <div class="modal-header">
        <button
          type="button"
          class="close"
          data-dismiss="modal"
          aria-label="Close">
          <span aria-hidden="true">&times;</span>
        </button>
        <h4
          class="modal-title"
          id="myModalLabel">
          Modal title
        </h4>
      </div>
      <div class="modal-body">Content here</div>
      <div class="modal-footer">
        <button
          type="button"
          class="btn btn-default"
          data-dismiss="modal">
          Close
        </button>
        <button
          type="button"
          class="btn btn-primary">
          Save
        </button>
      </div>
    </div>
  </div>
</div>
```

jQuery API: `$('#myModal').modal('show')` / `'hide'` / `'toggle'`.

### Tabs / Pills (Nav)

```html
<!-- Tabs -->
<ul class="nav nav-tabs">
  <li
    role="presentation"
    class="active">
    <a
      href="#home"
      data-toggle="tab">
      Home
    </a>
  </li>
  <li role="presentation">
    <a
      href="#profile"
      data-toggle="tab">
      Profile
    </a>
  </li>
</ul>
<div class="tab-content">
  <div
    role="tabpanel"
    class="tab-pane active"
    id="home">
    Home content
  </div>
  <div
    role="tabpanel"
    class="tab-pane"
    id="profile">
    Profile content
  </div>
</div>

<!-- Pills (swap nav-tabs → nav-pills) -->
<ul class="nav nav-pills nav-stacked">
  ...
</ul>
```

### Panels

```html
<div class="panel panel-default">
  <div class="panel-heading">
    <h3 class="panel-title">Panel Title</h3>
  </div>
  <div class="panel-body">Content</div>
  <div class="panel-footer">Footer</div>
</div>

<!-- Contextual: panel-primary, panel-success, panel-info, panel-warning, panel-danger -->
<div class="panel panel-danger">...</div>
```

### Tooltip & Popover (JS)

```javascript
// Tooltips must be initialized via JS — not auto-activated
$(function () {
  $('[data-toggle="tooltip"]').tooltip();
});

// Popovers same
$(function () {
  $('[data-toggle="popover"]').popover();
});

// Programmatic control
$('#element').tooltip('show'); // show | hide | toggle | destroy
$('#element').popover('show');
```

```html
<button
  type="button"
  class="btn btn-default"
  data-toggle="tooltip"
  data-placement="top"
  title="Tooltip text">
  Hover me
</button>
```

**Important:** When tooltip/popover inside `.btn-group` or `.input-group`, use `container: 'body'` to prevent layout issues:

```javascript
$('[data-toggle="tooltip"]').tooltip({ container: 'body' });
```

### Progress Bar

```html
<div class="progress">
  <div
    class="progress-bar"
    role="progressbar"
    aria-valuenow="60"
    aria-valuemin="0"
    aria-valuemax="100"
    style="width: 60%;">
    60%
  </div>
</div>

<!-- Striped + animated -->
<div class="progress">
  <div
    class="progress-bar progress-bar-striped active"
    style="width: 45%"></div>
</div>
```

### Responsive Utilities

```html
<!-- Show/hide per breakpoint -->
<div class="visible-xs-block">Only on phones</div>
<div class="hidden-sm hidden-md">Hidden on tablet/desktop</div>
<span class="sr-only">Screen-reader only text</span>
```

---

## Accessibility Patterns

| Situation                  | Solution                                            |
| -------------------------- | --------------------------------------------------- |
| Icon only (decorative)     | `aria-hidden="true"` on `<span>`                    |
| Icon conveying meaning     | `<span class="sr-only">Description</span>` adjacent |
| Icon-only button           | `aria-label="Action"` on `<button>`                 |
| Form without visible label | `aria-label` or `.sr-only` label                    |
| Dropdown button            | `aria-haspopup="true"` + `aria-expanded`            |
| Modal                      | `role="dialog"` + `aria-labelledby`                 |

---

## Common Gotchas

- **Tooltips/popovers not showing**: Must call `.tooltip()` / `.popover()` in JS — not auto-initialized.
- **Justified button groups on IE8**: Wrap each `<button>` in its own `.btn-group`.
- **Dropdown in overflow container**: Dropdowns clip — parent must not have `overflow: hidden`.
- **`.pull-right` on dropdown deprecated**: Use `.dropdown-menu-right` instead (since v3.1.0).
- **`.pull-left` / `.pull-right` on media deprecated**: Use `.media-left` / `.media-right` (since v3.3.0).
- **Input groups with `<select>` or `<textarea>`**: Avoid — cannot be fully styled cross-browser.

---

## Reference Files

| File | Contents | Confidence |
| --- | --- | --- |
| `references/v3.3.6.md` | Full 11-page official docs: CSS, components, JS plugins, grid, forms, navbar | medium |
| `references/index.md` | Documentation index / category map | medium |

Source: BootstrapDocs v3.3.6 (bootstrapdocs.com). Single authoritative source — no conflicts.

---

## Working with This Skill

**Starting out**: Read the Grid and Buttons sections above. Bootstrap's naming is consistent — once you know `btn-primary`, `alert-primary`, `panel-primary` all follow the same pattern.

**Building a layout**: Grid → Navbar → Forms. All in `references/v3.3.6.md` under CSS and Components sections.

**JS plugins** (modal, tooltip, collapse, carousel): Always check initialization — most require a jQuery call. Data-attribute API works for simple cases.

**Accessibility**: Bootstrap 3 has partial a11y support. Follow the table above and add `role` + `aria-*` attributes as shown in examples.

**Detailed docs**: Open `references/v3.3.6.md` and search for the component name. The file covers all 11 official doc pages in order.

---
name: fontawesome4
license: MIT
metadata:
  doc_version: "4.7.0"
description: Font Awesome v4.7 icon library — use when adding icons, looking up icon names, or implementing FA4 features (stacking, spinning, fixed-width, lists, accessibility)
---

# Font Awesome v4.7

Font Awesome 4 is a CSS/font-based icon library with 675+ icons. Version 4.7.0 is the final release of the v4 series. Icons render as a font glyph, styled entirely with CSS.

**Homepage:** https://fontawesome-v4.github.io  
**CDN:** https://fontawesome-v4.github.io/assets/font-awesome/css/font-awesome.min.css  
**Icon count:** 675 icons  
**License:** SIL OFL 1.1 (fonts), MIT (CSS/docs)

---

## When to Use This Skill

- Adding an icon to HTML/template with `<i class="fa fa-...">` syntax
- Looking up the correct icon name (e.g. is it `fa-trash` or `fa-trash-o`?)
- Using FA4 modifiers: size, spin, pulse, rotate, flip, fixed-width, list, stack
- Troubleshooting icon not rendering (missing CSS, wrong class prefix)
- Implementing accessible icons (aria-hidden, sr-only)
- Working with ServiceNow Service Portal or legacy projects that depend on FA4

---

## Quick Reference

### Basic Usage

```html
<!-- Syntax: fa (base class) + fa-{icon-name} -->
<i class="fa fa-home"></i>
<i class="fa fa-user"></i>
<i class="fa fa-cog"></i>
```

### Installation

```html
<!-- CDN (recommended for quick start) -->
<link
  rel="stylesheet"
  href="https://fontawesome-v4.github.io/assets/font-awesome/css/font-awesome.min.css" />

<!-- Or self-hosted: download font-awesome-4.7.0.zip from the site -->
<!-- Requires: css/font-awesome.min.css + fonts/ directory -->
```

### Sizes

```html
<i class="fa fa-home fa-lg"></i>
<!-- 1.33x -->
<i class="fa fa-home fa-2x"></i>
<!-- 2x -->
<i class="fa fa-home fa-3x"></i>
<!-- 3x -->
<i class="fa fa-home fa-4x"></i>
<!-- 4x -->
<i class="fa fa-home fa-5x"></i>
<!-- 5x -->
```

### Fixed Width (for aligned lists/menus)

```html
<i class="fa fa-home fa-fw"></i>
Home
<i class="fa fa-cog fa-fw"></i>
Settings
<i class="fa fa-user fa-fw"></i>
Profile
```

### Animated Icons

```html
<i class="fa fa-spinner fa-spin"></i>
<!-- continuous rotation -->
<i class="fa fa-circle-o-notch fa-spin"></i>
<i class="fa fa-refresh fa-spin"></i>
<i class="fa fa-cog fa-spin"></i>

<i class="fa fa-spinner fa-pulse"></i>
<!-- 8-step rotation -->
```

### Rotate & Flip

```html
<i class="fa fa-shield fa-rotate-90"></i>
<i class="fa fa-shield fa-rotate-180"></i>
<i class="fa fa-shield fa-rotate-270"></i>
<i class="fa fa-shield fa-flip-horizontal"></i>
<i class="fa fa-shield fa-flip-vertical"></i>
```

### Stacked Icons

```html
<!-- Stack: outer 2x + inner 1x -->
<span class="fa-stack fa-lg">
  <i class="fa fa-circle fa-stack-2x"></i>
  <i class="fa fa-flag fa-stack-1x fa-inverse"></i>
</span>

<!-- Banned icon example -->
<span class="fa-stack fa-lg">
  <i class="fa fa-camera fa-stack-1x"></i>
  <i class="fa fa-ban fa-stack-2x text-danger"></i>
</span>
```

### List Icons (replacing bullets)

```html
<ul class="fa-ul">
  <li>
    <i class="fa-li fa fa-check-square"></i>
    Item done
  </li>
  <li>
    <i class="fa-li fa fa-spinner fa-spin"></i>
    In progress
  </li>
  <li>
    <i class="fa-li fa fa-square-o"></i>
    Pending
  </li>
</ul>
```

### Accessibility

```html
<!-- Decorative icon: hide from screen readers -->
<i
  class="fa fa-home"
  aria-hidden="true"></i>

<!-- Meaningful icon: provide label -->
<a href="/home">
  <i
    class="fa fa-home"
    aria-hidden="true"></i>
  <span class="sr-only">Home</span>
</a>

<!-- Icon as sole content of button -->
<button aria-label="Delete">
  <i
    class="fa fa-trash"
    aria-hidden="true"></i>
</button>
```

### CSS Customization

```css
/* Custom size */
.fa-huge {
  font-size: 5em;
}

/* Custom color */
.fa-success {
  color: #5cb85c;
}
.fa-danger {
  color: #d9534f;
}

/* Icon in ::before pseudo-element */
.my-element::before {
  font-family: FontAwesome;
  content: '\f015'; /* fa-home unicode */
  margin-right: 6px;
}
```

---

## Key Concepts

### Icon Name Format

| Pattern            | Meaning         | Example                   |
| ------------------ | --------------- | ------------------------- |
| `fa-{name}`        | solid/filled    | `fa-star`, `fa-heart`     |
| `fa-{name}-o`      | outline variant | `fa-star-o`, `fa-heart-o` |
| `fa-{name}-square` | square variant  | `fa-github-square`        |
| `fa-{name}-circle` | circle variant  | `fa-question-circle`      |

### Common Icons by Category

**Navigation** `fa-home` `fa-arrow-left` `fa-arrow-right` `fa-chevron-down` `fa-chevron-up` `fa-bars` `fa-times` `fa-search`

**Actions** `fa-plus` `fa-minus` `fa-edit` `fa-pencil` `fa-trash` `fa-trash-o` `fa-save` `fa-floppy-o` `fa-download` `fa-upload`

**Status / Feedback** `fa-check` `fa-times` `fa-check-circle` `fa-times-circle` `fa-exclamation-triangle` `fa-info-circle` `fa-question-circle`

**Users / Social** `fa-user` `fa-users` `fa-user-plus` `fa-user-times` `fa-envelope` `fa-envelope-o` `fa-phone`

**Files / Media** `fa-file` `fa-file-o` `fa-file-text` `fa-file-pdf-o` `fa-file-excel-o` `fa-folder` `fa-folder-open`

**Loading / Progress** `fa-spinner` `fa-circle-o-notch` `fa-refresh` `fa-cog` (all use `fa-spin`)

**Brand Icons** `fa-github` `fa-twitter` `fa-facebook` `fa-google` `fa-linkedin` `fa-youtube`

### Unicode Reference (for CSS content)

| Icon   | Class       | Unicode |
| ------ | ----------- | ------- |
| Home   | `fa-home`   | `\f015` |
| User   | `fa-user`   | `\f007` |
| Cog    | `fa-cog`    | `\f013` |
| Star   | `fa-star`   | `\f005` |
| Heart  | `fa-heart`  | `\f004` |
| Check  | `fa-check`  | `\f00c` |
| Times  | `fa-times`  | `\f00d` |
| Search | `fa-search` | `\f002` |
| Plus   | `fa-plus`   | `\f067` |
| Minus  | `fa-minus`  | `\f068` |

Full unicode list: https://fontawesome-v4.github.io/cheatsheet/

---

## Troubleshooting

**Icon shows as box/tofu**

- CSS not loaded — check network tab for 404 on `font-awesome.min.css`
- Font files missing — `fonts/` dir must be at same level as `css/`
- Wrong class prefix — must have both `fa` and `fa-{name}`

**Icon not found**

- Check cheatsheet at https://fontawesome-v4.github.io/icons/
- Some icons only exist in FA5+ (e.g. `fa-times-circle-o` → `fa-times-circle` in v5)
- Outline variants end in `-o`: `fa-circle-o`, `fa-square-o`

**Alignment issues in lists/menus**

- Use `fa-fw` (fixed width) to make all icons same width

**Icon too small inside button/badge**

- Use `fa-lg` or `fa-2x` modifier

---

## Available References

- `references/README.md` — Minimal README (confidence: medium; source: GitHub repo)
- `references/file_structure.md` — Full repo file tree with 738 items including all 675 icon HTML pages (confidence: medium; source: GitHub repo)

> Note: Reference files are sparse. Icon details best looked up at https://fontawesome-v4.github.io/icons/

---

## FA4 vs FA5+ Migration Notes

FA5 changed the prefix system (`fas`/`far`/`fab` instead of `fa`) and renamed many icons. If maintaining a legacy FA4 project, do NOT upgrade CSS without auditing icon names. Key renames:

| FA4                    | FA5                   |
| ---------------------- | --------------------- |
| `fa fa-institution`    | `fas fa-university`   |
| `fa fa-send`           | `fas fa-paper-plane`  |
| `fa fa-photo`          | `fas fa-image`        |
| `fa fa-times-circle-o` | `far fa-times-circle` |

---

**Source:** fontawesome-v4.github.io | Version 4.7.0

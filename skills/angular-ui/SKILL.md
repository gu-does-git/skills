---
name: angular-ui
license: MIT
description: Use when working with angular-ui Bootstrap directives (ui.bootstrap) — accordions, modals, datepickers, dropdowns, carousels, and more
---

# Angular-UI Bootstrap Skill

Native AngularJS directives for Bootstrap components. No jQuery or Bootstrap JS required — only AngularJS + Bootstrap CSS.

**Source:** Official docs at `angular-ui.github.io/bootstrap` (v1.1.2). Single source, medium confidence.

---

## When to Use This Skill

Use when:

- Adding Bootstrap UI components (modal, datepicker, dropdown, accordion, tabs) to AngularJS apps
- Looking up directive attributes/options for any `uib-*` component
- Migrating from pre-0.14.0 (unprefixed) to prefixed `uib-` directives
- Parsing/formatting dates with `uibDateParser`
- Debugging cursor/styling issues with Bootstrap + AngularJS routing

---

## Key Concepts

**Prefix:** All components use `uib-` prefix (since v0.14.0). Pre-0.14.0 used unprefixed names.

**Attribute badges in docs:**

- `$` — Angular expression (not literal string)
- `B` — Boolean flag, no value needed
- `$watch` — has Angular watch listener
- `readonly` — read-only binding

---

## Quick Reference

```css
/* Fix cursor for Bootstrap components that use empty href */
.nav,
.pagination,
.carousel,
.panel-title a {
  cursor: pointer;
}
```

### 2. Accordion

```html
<uib-accordion close-others="true">
  <uib-accordion-group
    heading="Section 1"
    is-open="ctrl.isOpen">
    Content here
  </uib-accordion-group>
  <uib-accordion-group
    heading="Section 2"
    is-disabled="ctrl.disabled"
    panel-class="panel-primary">
    More content
  </uib-accordion-group>
</uib-accordion>
```

Key attrs: `close-others` ($C), `heading`, `is-open` ($), `is-disabled` ($), `panel-class`, `template-url`

### 3. Alert

```html
<uib-alert
  type="danger"
  close="ctrl.closeAlert()"
  dismiss-on-timeout="5000">
  Something went wrong!
</uib-alert>
```

Key attrs: `type` (default: `warning`), `close()` ($), `dismiss-on-timeout`

### 4. Buttons (checkbox / radio)

```html
<!-- Checkbox group -->
<button
  type="button"
  uib-btn-checkbox
  ng-model="ctrl.checked"
  btn-checkbox-true="1"
  btn-checkbox-false="0">
  Toggle
</button>

<!-- Radio group -->
<button
  type="button"
  uib-btn-radio="'left'"
  ng-model="ctrl.radioVal"
  uncheckable>
  Left
</button>
<button
  type="button"
  uib-btn-radio="'right'"
  ng-model="ctrl.radioVal">
  Right
</button>
```

Global config: `uibButtonConfig.activeClass` (default: `active`), `toggleEvent` (default: `click`)

### 5. Carousel

```html
<uib-carousel
  interval="3000"
  no-wrap="false"
  no-pause="false">
  <uib-slide
    ng-repeat="slide in slides"
    index="$index"
    active="slide.active">
    <img ng-src="{{slide.image}}" />
    <div class="carousel-caption">{{slide.text}}</div>
  </uib-slide>
</uib-carousel>
```

Key attrs: `interval` ($), `no-wrap` ($), `no-pause` ($), `no-transition` ($)

### 6. Collapse

```html
<button ng-click="ctrl.isOpen = !ctrl.isOpen">Toggle</button>
<div
  uib-collapse="!ctrl.isOpen"
  expanding="ctrl.onExpanding()"
  expanded="ctrl.onExpanded()"
  collapsing="ctrl.onCollapsing()"
  collapsed="ctrl.onCollapsed()">
  Collapsible content
</div>
```

Callbacks accept promises — animation waits until resolved; rejection cancels animation.

### 8. Datepicker

```html
<!-- Inline -->
<uib-datepicker
  ng-model="ctrl.date"
  min-date="ctrl.minDate"
  max-date="ctrl.maxDate"
  date-disabled="ctrl.disabled(date, mode)"
  show-weeks="true"
  starting-day="0"></uib-datepicker>

<!-- Popup (requires uib-datepicker-popup) -->
<input
  type="text"
  uib-datepicker-popup="MM/dd/yyyy"
  ng-model="ctrl.date"
  is-open="ctrl.popupOpen"
  datepicker-options="ctrl.options" />
<button ng-click="ctrl.popupOpen = true">Open</button>
```

### 9. Dropdown

```html
<div uib-dropdown>
  <button
    uib-dropdown-toggle
    type="button">
    Toggle
    <span class="caret"></span>
  </button>
  <ul uib-dropdown-menu>
    <li><a href="#">Action 1</a></li>
    <li><a href="#">Action 2</a></li>
  </ul>
</div>

<!-- Auto-close options -->
<div
  uib-dropdown
  auto-close="outsideClick">
  <!-- values: always (default), outsideClick, disabled -->
</div>
```

### 10. Modal

```javascript
// Controller
var modal = $uibModal.open({
  templateUrl: 'myModal.html',
  size: 'lg', // sm, lg, or custom
  resolve: {
    items: function () {
      return ['a', 'b', 'c'];
    },
  },
});

modal.result.then(
  function (result) {
    /* closed */
  },
  function () {
    /* dismissed */
  },
);

// Modal controller
this.items = items;
this.ok = function () {
  $uibModalInstance.close('ok');
};
this.cancel = function () {
  $uibModalInstance.dismiss('cancel');
};
```

### 11. Pagination / Pager

```html
<uib-pagination
  total-items="ctrl.totalItems"
  ng-model="ctrl.currentPage"
  max-size="5"
  items-per-page="10"
  boundary-links="true"
  rotate="true"
  ng-change="ctrl.pageChanged()"></uib-pagination>

<uib-pager
  total-items="ctrl.totalItems"
  ng-model="ctrl.currentPage"
  previous-text="&lsaquo; Prev"
  next-text="Next &rsaquo;"></uib-pager>
```

### 12. Tabs

```html
<uib-tabset
  active="ctrl.activeTab"
  justified="true"
  type="pills">
  <uib-tab
    index="0"
    heading="Tab 1"
    select="ctrl.onSelect()"
    deselect="ctrl.onDeselect()">
    Tab 1 content
  </uib-tab>
  <uib-tab
    index="1"
    disable="ctrl.tabDisabled">
    <uib-tab-heading>
      <i class="glyphicon glyphicon-home"></i>
      Tab 2
    </uib-tab-heading>
    Tab 2 content
  </uib-tab>
</uib-tabset>
```

### 13. Tooltip / Popover

```html
<!-- Tooltip -->
<button
  uib-tooltip="Hello!"
  tooltip-placement="right"
  tooltip-trigger="'mouseenter'">
  Hover me
</button>

<!-- Popover -->
<button
  uib-popover="Content here"
  popover-title="Title"
  popover-placement="bottom"
  popover-is-open="ctrl.isOpen">
  Click me
</button>
```

Placement options: `top`, `bottom`, `left`, `right`, `top-left`, `top-right`, etc.

### 14. Progressbar

```html
<uib-progressbar
  value="ctrl.progress"
  max="100"
  type="success"
  animate="true">
  {{ctrl.progress}}%
</uib-progressbar>

<!-- Stacked -->
<uib-progress>
  <uib-bar
    value="30"
    type="success"></uib-bar>
  <uib-bar
    value="20"
    type="warning"></uib-bar>
  <uib-bar
    value="10"
    type="danger"></uib-bar>
</uib-progress>
```

### 15. Rating

```html
<uib-rating
  ng-model="ctrl.rate"
  max="10"
  readonly="ctrl.isReadonly"
  on-hover="ctrl.hoverRating(value)"
  on-leave="ctrl.resetRating()"></uib-rating>
```

---

## Reference Files

| File | Contents | Source | Confidence |
| --- | --- | --- | --- |
| `references/other.md` | Full directive docs: all components, all attributes, examples | Official docs (v1.1.2) | Medium |

`references/index.md` — index only, 93 chars, no standalone value.

---

## Working with This Skill

**New to ui.bootstrap:** Start with setup (add CSS fix). Pick a component from Quick Reference above.

**Looking up attrs:** Each component section lists key attributes. For full attr list with defaults, read `references/other.md` and search for the component name.

**Migrating from 0.13.x:** All directives need `uib-` prefix. E.g. `accordion` → `uib-accordion`, `accordion-group` → `uib-accordion-group`.

**Global config:** Inject `uibXxxConfig` in `.config()` block to set defaults app-wide.

**Templates:** All components have `template-url` attr to override default template. Default paths: `uib/template/<component>/<component>.html`.

**Touch/swipe:** Carousel swipe needs `ngTouch` module loaded.

---

## Known Limitations

- Docs sourced from v1.1.2 — latest version may differ
- No codebase analysis available — examples are from official docs only
- `references/other.md` content was truncated in source extraction; full docs at `https://angular-ui.github.io/bootstrap/versioned-docs/1.1.2/`

---

## Updating

Re-run scraper with same config to rebuild with latest docs.

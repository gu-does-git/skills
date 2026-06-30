---
name: select2
license: MIT
description: Select2 v3 searchable select/tag component — init, sync with AngularJS, cascading dropdowns, modals, events, remote data, templating
---

# Select2 v3.5 — ServiceNow & AngularJS

Select2 replaces `<select>` elements (single or multiple) with a searchable, tag/pill UI. Version 3 is available in ServiceNow instances at `/styles/thirdparty/select2/`.

**API level:** v3 `.select2()` style. Not compatible with v4 API.

---

## When to Use

- Replacing a native `<select>` with a searchable dropdown
- Multi-select pills/tags for selecting systems, profiles, roles
- Cascading/dependent selects (options of B depend on A's selection)
- Inside ServiceNow widget modals

---

## Key Concepts

- **Angular + Select2 don't sync.** Select2 replaces the DOM; Angular's `ng-model` changes don't reach Select2's visual. You must manually fire **`change.select2`** (namespaced event) on the underlying `<select>` after every programmatic model change. `ng-change` on the `<select>` will NOT fire from Select2's DOM changes — wire it inside the `change.select2` handler instead.
- **Multi-select:** `<select multiple>` → `ng-model` is an array of scalars.
- **Single-select:** bare `<select>` → `ng-model` is a scalar.
- **Init timing:** always from `ng-init` + nested `$timeout`s. Never `$(document).ready`.
- **`allowClear`:** adds an "×" to clear all selections.

---

## Quick Reference

### Init

```js
// Constant at top of controller
var SELECT2_CHANGE_EVENT = 'change.select2';

c.initSelect2 = function (id) {
    $timeout(function () {
        angular.element('#' + id).select2({ allowClear: true });
        $timeout(function () {
            angular.element('#' + id).trigger(SELECT2_CHANGE_EVENT);
        }, 50);
    }, 1);
};
```

Called from template via `ng-init`:

```html
<select ng-init="c.initSelect2('mySelect')"
        ng-model="c.myModel"
        ng-change="c.onSelectionChange()"
        id="mySelect"
        multiple>
    <option value="{{ opt.value }}" ng-repeat="opt in c.options">
        {{ opt.label }}
    </option>
</select>
```

### Sync after programmatic model change

```js
c.myModel = newValue;
$timeout(function () {
    angular.element('#mySelect').trigger('change.select2');
}, 1);
```

Fire this after:
- `initSelect2` — sync initial model → UI
- Resetting / clearing values
- Filtering available options (cascading)
- Opening a modal that contains Select2
- Restoring saved values

### Change handler

```js
c.onMyChange = function () {
    // Build displayValue from selected option labels (multi-select)
    model.displayValue = _(c.allOptions)
        .filter(function (opt) { return _.includes(model.value, opt.value); })
        .map('display')
        .value();
};
```

### Cascading dropdowns

```js
c.setDependentOptions = function (parentValues) {
    var filtered = _.isEmpty(parentValues) ? [] : _(allOptions)
        .filter(function (opt) { return _.includes(parentValues, opt.parent); })
        .map(function (opt) { return { value: opt.name, display: opt.description }; })
        .value();

    // Prune selections that no longer exist
    model.value = _.filter(model.value, function (v) {
        return _.some(filtered, { value: v });
    });

    c.filteredOptions = filtered;

    $timeout(function () {
        angular.element('#dependentSelect').trigger('change.select2');
    }, 1);
};
```

Optionally disable when parent is empty:

```html
<span ng-class="{'disabled': c.filteredOptions.length === 0}">
    <span ng-if="c.filteredOptions.length === 0" class="text-muted">
        Select a system to enable this field
    </span>
    <select id="dependentSelect" ...>
```

### Inside modals

Re-trigger `change.select2` when the modal opens — Bootstrap modals detach/reattach DOM elements, which can lose Select2's rendered state:

```js
c.onModalOpen = function () {
    _.forEach(['select1', 'select2'], function (id) {
        $timeout(function () {
            angular.element('#' + id).trigger('change.select2');
        }, 1);
    });
};
```

Also override `enforceFocus` in `link.js` to prevent Select2's offscreen input from trapping focus:

```js
$(document).ready(function () {
    $.fn.modal.Constructor.prototype.enforceFocus = function () {};
});
```

### Placeholder

Placeholder text shown when nothing is selected.

```js
// Simple string
$('select').select2({ placeholder: 'Placeholder' });

// Object — required when using allowClear
$('select').select2({
    placeholder: { id: '', text: 'Placeholder' },
    allowClear: true
});
```

**Rules:**

| Situation | Format | Reason |
|----------|---------|-------|
| No `allowClear` | `string` or `{ id: '', text }` | Both work |
| With `allowClear` | **`{ id: '', text }` required** | Select2 uses empty `id` to distinguish placeholder from real item |
| Empty `<option value="">` in HTML | Can conflict with placeholder | Remove the `<option>` or use `allowClear` with object |
| Multi-select | Placeholder disappears on first selection | Default behavior — reappears when cleared |

**Gotchas:**

- Placeholder with `allowClear` but no object → clear "×" may not appear or clears incorrectly
- ServiceNow: if select is populated via `options` in server script, ensure the first option doesn't have `value=""`
- Placeholder not showing on empty select with no `<option>`? Add a manual `<option value=""></option>`

---

## i18n / Translations

Set locale strings per-instance to override defaults:

```js
$('select').select2({
    formatNoMatches: function() { return 'Nenhum resultado encontrado'; },
    formatSearching: function() { return 'Buscando…'; }
});
```

---

## Pitfalls

| Problem | Cause | Fix |
|---------|-------|-----|
| Select2 not attaching | DOM not ready when `select2()` called | `ng-init` + nested `$timeout`s |
| Pills/selection not visible after model change | Angular model changed but Select2 not notified | Fire `change.select2` |
| Modal reopens with empty Select2 | DOM detach cleared Select2 state | Re-trigger `change.select2` on modal open |
| Select2 input steals focus in modal | Bootstrap's `enforceFocus` fights Select2 | Override in `link.js` |
| Close icon missing | Sprite path not found in ServiceNow instance | Add CSS override |

---

## CSS

```scss
// Fix missing close-icon sprite (ServiceNow instances)
.select2-container-multi .select2-search-choice-close {
    background: url('/styles/thirdparty/select2/select2.png') right top no-repeat !important;
}

// Match Bootstrap 3 border colors
#myForm {
    .select2-default,
    .select2-choice,
    .select2-choices {
        border-color: #ced4d5;
    }
}
```

---

## Reference Files

| File | Contents |
|------|----------|
| `references/select2-3.5.md` | Full Select2 v3.5 API docs |

---

## Limitations

- Select2 v3 only — v4 uses different event names and init API
- No `ng-model-options` support on Select2-replaced elements
- Programmatic `$watch` on the model won't update the UI without manually firing `change.select2`
- Select2 replaces the `<select>` entirely — standard CSS pseudo-selectors like `:checked` won't work on the visible UI

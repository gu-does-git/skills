# Select2 v3.5.x API Reference

Source: [select2.github.io/select2](https://web.archive.org/web/20191230140524/http://select2.github.io/select2/) (archived)

## Constructor Options

### Core

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `width` | string | `resolve` | `off` — no width set. `element` — js-calculated from source. `copy` — copies width style from source. `resolve` — try copy, fallback element. Other values used verbatim. |
| `minimumInputLength` | int | `0` | Min chars before search kicks in |
| `maximumInputLength` | int | — | Max chars allowed for input |
| `minimumResultsForSearch` | int | `10` | Min results to keep search field visible. Negative value = permanently hide search. Single-value only. |
| `maximumSelectionSize` | int/fn | — | Max selectable items (multi only). `<1` = unlimited. |
| `placeholder` | string | — | Text when nothing selected. Also via `data-placeholder` attr. For single-select, requires an empty `<option></option>` as first option. |
| `placeholderOption` | string/fn | `first` | Resolves which `<option>` is the placeholder. `"first"` = first option. Or a function receiving the select element. |
| `separator` | string | `","` | Delimiter for ids in `value` attribute of multi-selects. |
| `allowClear` | boolean | `false` | Show clear button when selection exists. Requires `placeholder`. Single-select only. Requires empty `<option>` when attached to `<select>`. |
| `multiple` | boolean | — | Allow multi-select. Ignored when attached to `<select>` (uses `multiple` attribute). |
| `closeOnSelect` | boolean | `true` | `false` keeps dropdown open for rapid multi-selection. Multi-select only. |
| `openOnEnter` | boolean | `true` | Opens dropdown when Enter pressed and Select2 is closed. |
| `id` | function | — | Extracts id from choice object: `id(object)` returns string. Default expects `object.id`. |
| `matcher` | function | — | `matcher(term, text, option)` returns boolean. Default: case-insensitive substring match. |
| `sortResults` | function | — | `sortResults(results, container, query)` returns sorted results array. |
| `selectOnBlur` | boolean | `false` | Select highlighted option when Select2 loses focus. |
| `loadMorePadding` | integer | `0` | Pixels below fold before loading next page. |
| `nextSearchTerm` | function | — | `nextSearchTerm(data, searchVal)` determines next search term after selection. |
| `containerCss` | object/fn | — | Inline CSS for container. |
| `containerCssClass` | string/fn | — | CSS class for container. |
| `dropdownCss` | object/fn | — | Inline CSS for dropdown. |
| `dropdownCssClass` | string/fn | — | CSS class for dropdown. |
| `dropdownAutoWidth` | boolean | `false` | Auto-size dropdown width based on content. |
| `adaptContainerCssClass` | function | — | `adaptContainerCssClass(clazz)` filters container CSS classes from source. |
| `adaptDropdownCssClass` | function | — | `adaptDropdownCssClass(clazz)` filters dropdown CSS classes. Default: returns `null` (filters all). |
| `escapeMarkup` | function | — | `escapeMarkup(markup)` post-processes formatter output. Default escapes HTML. |
| `createSearchChoicePosition` | string/fn | `top` | Position of created choice: `"top"`, `"bottom"`, or custom function. |

### Display / Formatting

| Option | Type | Description |
|--------|------|-------------|
| `formatSelection` | function | `formatSelection(object, container, escapeMarkup)` renders current selection. Returns html/dom. Access original option via `object.element`. |
| `formatResult` | function | `formatResult(object, container, query, escapeMarkup)` renders a result item. |
| `formatResultCssClass` | function | `formatResultCssClass(object)` returns CSS classes for result. |
| `formatNoMatches` | string/fn | `formatNoMatches(term)` — "No matches" message. |
| `formatSearching` | string/fn | `formatSearching()` — "Searching..." message. Return `null` to disable. |
| `formatAjaxError` | string/fn | `formatAjaxError(jqXHR, textStatus, errorThrown)` — error message. |
| `formatInputTooShort` | string/fn | `formatInputTooShort(term, minLength)` — input too short message. |
| `formatInputTooLong` | string/fn | `formatInputTooLong(term, maxLength)` — input too long message. |
| `formatSelectionTooBig` | string/fn | `formatSelectionTooBig(maxSize)` — max selection reached message. |
| `formatLoadMore` | string/fn | `formatLoadMore(pageNumber)` — loading more results message. |

### Data Sources

| Option | Type | Description |
|--------|------|-------------|
| `query` | function | `query(options)` — custom query function. `options = { element, term, page, context, callback }`. Callback receives `{ results: [...], more: bool, context }`. Attach to `input[type=hidden]`. |
| `data` | array/object | Inline data array `[{id, text}, ...]`. Or object `{ results: [...], text: "key" }`. |
| `ajax` | object | AJAX shortcut. See AJAX section below. |
| `tags` | array/fn | Tagging mode. Array of objects/strings, or function returning array. |
| `initSelection` | function | `initSelection(element, callback)` maps id → object. Used for initial selection. |
| `createSearchChoice` | function | `createSearchChoice(term)` creates choice from search term. Returns object with `id`. |
| `tokenizer` | function | `tokenizer(input, selection, selectCallback, opts)` extracts tokens from input. |
| `tokenSeparators` | array | Token separators e.g. `[',', ' ']`. Requires `createSearchChoice`. |

### AJAX Options

| Option | Type | Description |
|--------|------|-------------|
| `transport` | function | Custom transport function. Default: `$.ajax`. |
| `url` | string/fn | AJAX endpoint URL. |
| `dataType` | string | `"json"`, `"jsonp"`, etc. |
| `quietMillis` | int | Debounce delay in ms before request. |
| `cache` | boolean | `false` to prevent browser caching. Default `false`. |
| `jsonpCallback` | string/fn | Custom JSONP callback name. |
| `data` | function | `data(term, page, context)` returns URL params object. |
| `results` | function | `results(data, page, query)` extracts results from response. Returns `{ results, more }`. |
| `params` | object/fn | Extra parameters for transport (e.g. `{contentType: "application/json"}`). |

## Methods

```js
// Get/set value (id-based)
$('select').select2('val');                  // get — returns id or array of ids
$('select').select2('val', 'CA');            // set single
$('select').select2('val', ['CA', 'NY']);    // set multi
$('select').select2('val', 'CA', true);      // set + trigger change event

// Get/set value (object-based)
$('select').select2('data');                 // get — returns object or array
$('select').select2('data', { id, text });   // set

// Lifecycle
$('select').select2('destroy');              // teardown, preserves DOM

// Open / close
$('select').select2('open');
$('select').select2('close');

// State
$('select').select2('enable', true);         // enable
$('select').select2('enable', false);        // disable
$('select').select2('readonly', true);       // readonly mode

// Container access
$('select').select2('container');            // get container element

// Drag & drop sorting
$('select').select2('onSortStart');
$('select').select2('onSortEnd');

// Programmatic search
$('select').select2('search', 'California');
```

**Note:** `val()` with `initSelection`: to use `val(id)` on `input[type=hidden]`, `initSelection` must be defined so Select2 can map id → full object.

## Events

All events are triggered on the original `<select>` or `<input>` element.

| Event | Description | Preventable | Properties |
|-------|-------------|-------------|------------|
| `change` | Selection changed | no | `val`, `added`, `removed` |
| `select2-opening` | Before dropdown opens | yes (`preventDefault()`) | — |
| `select2-open` | After dropdown opened | no | — |
| `select2-close` | After dropdown closed | no | — |
| `select2-highlight` | Choice highlighted in dropdown | no | `val`, `choice` |
| `select2-selecting` | Before selection is made | yes (`preventDefault()`) | `val`, `choice` |
| `select2-clearing` | Before clear button action | yes (`preventDefault()`) | — |
| `select2-removing` | Before a choice is removed | yes (`preventDefault()`) | `val`, `choice` |
| `select2-removed` | After a choice removed/cleared | no | `val`, `choice` |
| `select2-loaded` | Query done, results list updated | no | `items` |
| `select2-focus` | Control focused | no | — |
| `select2-blur` | Control blurred | no | — |

```js
// Change handler
$('select').on('change', function(e) {
    // e.val — current value(s)
    // e.added — newly added { id, text } (or null)
    // e.removed — removed { id, text } (or null)
});

// Prevent dropdown from opening
$('select').on('select2-opening', function(e) {
    if (!canOpen) e.preventDefault();
});
```

**Important:** Select2 v3 uses **namespaced events**. When using with AngularJS or programmatic model changes, always fire `change.select2` (not just `change`):

```js
$('select').trigger('change.select2');
```

## Configuring Defaults

```js
$.fn.select2.defaults.set('width', 'copy');
$.fn.select2.defaults.set('allowClear', true);
```

Properties changed via `$.fn.select2.defaults` apply to all future instances.

## Data Format

### Flat results

```js
{
    more: false,
    results: [
        { id: "CA", text: "California" },
        { id: "AL", text: "Alabama" }
    ]
}
```

### Hierarchical (optgroup-style)

```js
{
    more: false,
    results: [
        {
            text: "Western",
            children: [
                { id: "CA", text: "California" },
                { id: "AZ", text: "Arizona" }
            ]
        }
    ]
}
```

### Option extras

Each result object may include:
- `disabled: true` — prevent selection
- `locked: true` — prevent removal (multi)
- `children: [...]` — hierarchical data

## CSS Classes

| Class | Element |
|-------|---------|
| `.select2-container` | Outer wrapper |
| `.select2-container-multi` | Multi-select variant |
| `.select2-choice` | Single-select display |
| `.select2-choices` | Multi-select tags area |
| `.select2-search-choice` | Individual pill/tag (multi) |
| `.select2-search-choice-close` | Close icon on a pill |
| `.select2-search-field` | Search input wrapper |
| `.select2-drop` | Dropdown container |
| `.select2-results` | Results list |
| `.select2-highlighted` | Hovered result |
| `.select2-offscreen` | Hidden assistive `<select>` |

## Browser Support

- IE 8+
- Chrome 8+
- Firefox 10+
- Safari 3+
- Opera 10.6+

## License

Apache Software Foundation License Version 2.0 and GPL Version 2.0. Coded by Igor Vaynberg.

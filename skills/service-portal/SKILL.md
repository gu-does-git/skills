---
name: service-portal
license: MIT
description: Use when building, debugging, or configuring ServiceNow Service Portal widgets, pages, portals, and themes
---

# Service Portal Skill

Unofficial community documentation for ServiceNow Service Portal. Source: serviceportal.io (based on original ServiceNow dev team docs, now community-maintained).

## When to Use This Skill

Trigger on:

- Building or editing SP widgets (server script, client script, HTML template, CSS)
- Accessing widget options/instance config
- Real-time record watching in widgets
- Widget internationalization (i18n)
- Page layout with Bootstrap containers/rows/columns
- Widget dependencies (JS/CSS libraries)
- Portal and page configuration
- `$sp`, `spUtil`, `c.server`, `c.data`, `c.options` usage

## OOTB Libraries

### Frontend

| Library | Version | Global | Use Case |
| --- | --- | --- | --- |
| **AngularJS** | 1.x | `angular` | Widget framework — all widgets are Angular directives |
| **Bootstrap** | 3.3.6 | `$.fn.bootstrap` | Grid, responsive layout, UI components |
| **jQuery** | 3.4.1 | `$` | DOM manipulation (use cautiously with Angular) |
| **jQuery Lite** | — | `angular.element` | Lightweight jQuery built into Angular |
| **Lodash** | 4.17.15 | `_` | Data manipulation, utilities |
| **Moment.js** | — | `moment` | Date/time parsing and formatting |
| **Font Awesome** | 4 | — | Icons via CSS classes (`fa fa-*`) |
| **Angular-UI** | 1.1.2 | `angular.ui` | UI components: `ui-bootstrap`, `ui-router` |
| **Select2** | — | `$.fn.select2` | Enhanced dropdowns |

> DataTables is **NOT** OOTB — add via Dependency Package if needed.

### Backend (Server Script)

| API                   | Use Case                           |
| --------------------- | ---------------------------------- |
| `GlideRecord`         | Database queries and updates       |
| `GlideAggregate`      | COUNT, SUM, GROUP BY queries       |
| `GlideDateTime`       | Date/time manipulation server-side |
| `GlideSystem (gs)`    | Logging, user info, messages       |
| `sn_ws.RESTMessageV2` | External REST API calls            |
| `$sp`                 | Service Portal server API          |

### Client-Side APIs

```javascript
// spUtil
spUtil.recordWatch($scope, table, filter, callback); // real-time updates
spUtil.addInfoMessage('message');
spUtil.addErrorMessage('message');
spUtil.update(); // refresh widget
spUtil.getPreference(name); // get widget preference

// GlideForm (Form widget and SC Catalog widget only)
g_form.setValue(field, value);
g_form.getValue(field);
g_form.setDisplay(field, visible);
g_form.setMandatory(field, mandatory);
g_form.addInfoMessage(message);
g_form.addErrorMessage(message);

// Angular services (inject in client script)
($scope, $rootScope); // scope and broadcast
$http; // HTTP requests
$timeout; // use instead of setTimeout (triggers digest cycle)
$window; // window object
$sce; // sanitization: $sce.trustAsHtml(rawHtml)
```

## Key Concepts

| Concept | Description |
| --- | --- |
| Widget | Self-contained UI unit: server script + client script + HTML template + CSS + option schema |
| `data` | Server→client bridge. Set on server, read on client as `c.data.*` |
| `input` | Client→server bridge. Set on client via `c.server.get({...})`, read on server as `input.*` |
| `options` | Instance-level config. Set via Option Schema UI. Accessed as `c.options.*` (client) or `options.*` (server) |
| `$sp` | Server-side Service Portal API |
| `spUtil` | Client-side utility service (Angular) |
| Widget Instance | One placement of a widget on a page — has its own option values |
| Page | Bootstrap layout of containers → rows → columns → widgets |
| Portal | Top-level config: theme, header/footer widgets, homepage |

## Quick Reference

### Server Script — basic data fetch

```javascript
// Server script
(function () {
  if (input) {
    var r = new RESTMessage('Yahoo Finance', 'get');
    r.setStringParameter('symbol', input.symbol);
    var response = r.execute();
    data.price = response.getBody();
  }
})();
```

### Client Script — call server and update UI

```javascript
function() {
    var c = this;
    c.update = function() {
        c.data.price = false;
        c.server.get({ symbol: c.data.symbol }).then(function(r) {
            c.data.price = r.data.price;
        });
    };
}
```

### Client Script — read widget option

```javascript
function() {
    var c = this;
    console.log(c.options.text_color); // value from instance option schema
}
```

### Server Script — read option + set default

```javascript
(function () {
  // Default before instance value is set
  options.text_color = options.text_color || '#000000';
  $sp.log(options.text_color);
})();
```

### Record Watch — real-time table listener

```javascript
function(spUtil, $scope) {
    var c = this;
    spUtil.recordWatch($scope, 'incident', 'active=true', function(name, data) {
        console.log(name); // event type
        console.log(data); // inserted/updated record data
    });
}
```

### Internationalization — HTML template

```html
<div>
  <p>${This message will be internationalized.}</p>
  <p>However, this will NOT be.</p>
</div>
```

### Internationalization — Client Script

```javascript
function() {
    var c = this;
    c.message = '${This message will be internationalized}';
}
```

### Internationalization — Server Script (safe, avoids quote escaping)

```javascript
// Fetch in server, bind to data — avoids JS parse errors from translated quotes
data.translatedMsg = gs.getMessage('Some message key');
```

## Reference Files

Located in `references/`:

| File               | Contents                                | Confidence |
| ------------------ | --------------------------------------- | ---------- |
| `documentation.md` | 24 pages covering all major SP concepts | medium     |

### What's in `documentation.md`

Covers:

- `widget_server_script.md` — server-side properties, Glide API usage, `input`/`data` pattern
- `widget_client_script.md` — Angular controller, `c.server.get()`, `c.data` binding
- `widget_options.md` — defining option schema, accessing `options.*`, setting defaults
- `widget_record_watch.md` — `spUtil.recordWatch()` for real-time updates
- `widget_internationalization.md` — `${}` syntax, `gs.getMessage()`, safe translation patterns
- `widget_link.md` — Angular link function for direct DOM manipulation (advanced/rare)
- `widget_dependencies.md` — linking JS/CSS libraries to widgets asynchronously
- `page_layout.md` — Bootstrap containers/rows/columns, custom flexbox layout
- `page.md` — page config, page IDs, multi-portal reuse
- `portal.md` — portal settings, `$scope.portal`, theme config
- `widget_server_script.md` — server context execution model

## Conventions & Preferences

### JavaScript — ES5 only

Server script runs on Rhino (ES5). Client script runs in browser but keep ES5 for consistency.

```javascript
// correct
var items = [];
var fn = function () {};

// wrong — do not use
let x = 1;
const y = 2;
() => {};
```

### Client Script structure

Organize in this order — no section comments, just grouping:

```javascript
function($q, $scope) {
    var c = this;

    // 1. variables / state
    var PAGE_SIZE = 20;
    c.data.loading = false;
    c.data.items = [];

    // 2. generic / reusable functions
    c.formatRecord = function(gr) { /* ... */ };
    c.handleError  = function(err) { /* ... */ };

    // 3. grouped by feature/responsibility
    c.loadItems = function() { /* ... */ };
    c.selectItem = function(item) { /* ... */ };

    c.saveForm   = function() { /* ... */ };
    c.resetForm  = function() { /* ... */ };

    // last line — init after everything is defined
    c.init();
}
```

### Record shape — always use this structure

When fetching a record to display or track, map it to:

```javascript
// Server script
data.record = {
  displayValue: gr.getDisplayValue('field'),
  value: gr.getValue('field'),
  sys_id: gr.sys_id.toString(),
};

// Makes the record easy to display (displayValue), submit (value), and reference (sys_id)
```

### $q — async / promises

`$q` is available OOTB. Use when coordinating multiple async calls:

```javascript
function($q) {
    var c = this;

    c.loadAll = function() {
        var promises = [
            c.server.get({ action: 'fetchUsers' }),
            c.server.get({ action: 'fetchRoles' })
        ];
        $q.all(promises).then(function(results) {
            c.data.users = results[0].data.users;
            c.data.roles = results[1].data.roles;
        });
    };

    // deferred — use when wrapping non-promise callbacks
    c.waitForSomething = function() {
        var deferred = $q.defer();
        doAsyncThing(function(result) {
            deferred.resolve(result);
        });
        return deferred.promise;
    };
}
```

### Template — OOTB first, customize on top

Always prefer OOTB components before writing custom HTML:

```html
<!-- Tabs: use UI Bootstrap uib-tabset (OOTB) -->
<uib-tabset>
  <uib-tab heading="Details">...</uib-tab>
  <uib-tab heading="History">...</uib-tab>
</uib-tabset>

<!-- Panels: Bootstrap panel (OOTB) -->
<div class="panel panel-default">
  <div class="panel-heading">Title</div>
  <div class="panel-body">Content</div>
</div>

<!-- Grid: Bootstrap columns (OOTB) -->
<div class="row">
  <div class="col-md-8">Main</div>
  <div class="col-md-4">Sidebar</div>
</div>
```

Customize by adding CSS classes on top — don't replace OOTB structure with custom divs.

### ServiceNow SDK gotchas

- `client_script.js` must begin with `function (...) {}` or `api.controller = function (...) {}` so the SDK build validator accepts the file.
- Do not place JSDoc before the top-level controller in `client_script.js`; document helper functions inside the controller body instead when you need lint coverage.
- The ServiceNow SCSS compiler is older; plain nesting with `&` is fine, but avoid BEM suffix/prefix patterns like `&--` and `&__`.
- When writing SCSS, prefer nesting under the component root when it improves readability, but keep the selector structure compatible with the older compiler.
- Prefer central ESLint globals for Service Portal server-side globals such as `data` when available, instead of repeating `/* global ... */` in each file.

## Working with This Skill

### New to Service Portal

1. Understand the `data`/`input` bridge between server and client scripts first
2. Widget = server script + client script + HTML template; these share `data` but run in different contexts
3. Page layout: always Portal → Theme → Page → Container → Row → Column → Widget

### Building a Widget

1. Server script: fetch data, set `data.*` properties
2. Client script: bind to `c.data.*`, call `c.server.get(input)` for dynamic fetches
3. HTML template: use `c.data.*` bindings in Angular expressions `{{ c.data.price }}`
4. Options: define schema in Widget Editor → hamburger → Edit Option Schema; access as `c.options.*`

### Real-Time Updates

Use `spUtil.recordWatch($scope, table, filter, callback)` in client script. Unregisters automatically on `$scope.$destroy`.

### i18n

- HTML: `${message}` shorthand
- Client script: `'${message}'` string literal
- Server script: `gs.getMessage('key')` → assign to `data.*` (safest — avoids translated-quote JS parse errors)

### Performance

```javascript
// $timeout instead of setTimeout — triggers Angular digest
$timeout(function() { /* ... */ }, 100);

// debounce via ng-model-options in HTML (preferred)
<input ng-model="c.searchTerm" ng-model-options="{ debounce: 300 }" ng-change="c.loadData()" />

// or via Lodash in client script
c.search = _.debounce(function(term) { c.loadData(term); }, 300);

// ng-if removes from DOM (better than ng-show for heavy content)
<div ng-if="c.showDetails">...</div>

// one-time binding for static data
<div>{{::c.staticLabel}}</div>
```

### Security

```javascript
// Server: validate required inputs
if (!input || !input.recordId) {
  return;
}

// Server: check ACLs when needed
if (!gr.canRead()) {
  return;
}

// Server: sanitize user input before output
data.safe = gs.getEscapeMessage(userInput);

// Client: render trusted HTML with ng-bind-html
// template: <div ng-bind-html="c.data.safeHtml"></div>
$scope.data.safeHtml = $sce.trustAsHtml(rawHtml);
```

### input.action — dispatch multiple actions in one widget

```javascript
// Client
c.server.get({ action: 'fetchData', term: c.searchTerm });
c.server.get({ action: 'save', record: c.record });

// Server — switch when 2+ actions
if (input) {
  switch (input.action) {
    case 'fetchData':
      /* ... */ break;
    case 'save':
      /* ... */ break;
  }
}
```

### Lodash — use to simplify, not complicate

Lodash is OOTB (`_`). Use it when it makes intent clearer than vanilla JS.

```javascript
// iteration — _.forEach reads like English
_.forEach(data.records, function (record) {
  record.label = record.number + ' - ' + record.short_description;
});

// unique DOM IDs
c.widgetId = _.uniqueId('widget_');

// transform arrays
var titles = _.map(data.records, 'short_description');
var active = _.filter(data.records, { active: true });
var found = _.find(data.records, { sys_id: targetId });
var sorted = _.sortBy(data.records, 'sys_created_on');

// group by field value
data.byCategory = _.groupBy(data.records, 'category');

// pick/omit fields before sending to server
c.server.get({ record: _.pick(c.data.form, ['sys_id', 'short_description', 'state']) });
```

**Chain** — use when doing 2+ sequential transforms on same collection:

```javascript
// without chain: nested calls, hard to read
var result = _.sortBy(_.filter(_.map(records, formatFn), { active: true }), 'date');

// with chain: left-to-right, each step clear
var result = _(records).map(formatFn).filter({ active: true }).sortBy('date').value(); // always end chain with .value()
```

> Rule: if Lodash makes a line longer or harder to read than vanilla JS, use vanilla JS instead.

### GlideAggregate

```javascript
var ga = new GlideAggregate('incident');
ga.addAggregate('COUNT');
ga.groupBy('category');
ga.query();
while (ga.next()) {
  data.count = ga.getAggregate('COUNT');
}
```

### Option Defaults

Always set defaults in server script:

```javascript
options.my_option = options.my_option || 'default_value';
```

Unset options return `undefined`; missing defaults cause silent failures.

### Custom Layout (non-Bootstrap)

Mark "Bootstrap alternative" on the container → removes `.container` class → add custom CSS class for flexbox/grid.

### Widget Dependencies

Add JS/CSS libs via dependency packages (Widget Editor → Related Lists → Dependencies). Loaded async at widget render time.

## Linting Rules (widgets)

Angular rules enforced by `eslint-plugin-angular` on `sp_widget/**/*.js`:

### `angular/angularelement` — use `angular.element` not `$` for DOM

```javascript
// wrong — jQuery $ for DOM in Angular context
$('#my-element').addClass('active');

// correct
angular.element('#my-element').addClass('active');
```

### `angular/interval-service` — use `$interval` not `setInterval`

```javascript
// wrong — bypasses Angular digest
setInterval(function () {
  c.tick();
}, 1000);

// correct — triggers digest automatically
$interval(function () {
  c.tick();
}, 1000);
```

### `angular/window-service` — use `$window` not `window`

```javascript
// wrong
window.location.href = '/sp';
window.open(url);

// correct — testable and Angular-aware
$window.location.href = '/sp';
$window.open(url);
```

### HTML template rules (`@html-eslint`)

```html
<!-- id-naming-convention: kebab-case only -->
<!-- wrong -->
<div id="myWidget"></div>
<div id="my_widget"></div>

<!-- correct -->
<div id="my-widget"></div>

<!-- quotes: double quotes on all attributes -->
<!-- wrong -->
<div class="panel">
  <input ng-model="c.data.name" />

  <!-- correct -->
  <div class="panel">
    <input ng-model="c.data.name" />
  </div>
</div>
```

---

## Source Notes

- Source: serviceportal.io — unofficial community docs, originally from ServiceNow dev team
- No codebase analysis available — examples are from official documentation only
- No known discrepancies between sources (single source)
- Cross-verify with ServiceNow official docs for version-specific API changes

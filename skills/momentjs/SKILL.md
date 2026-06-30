---
name: momentjs
license: MIT
metadata:
  doc_version: "2.x"
description: Use when working with Moment.js — parsing, formatting, manipulating, querying, displaying dates/times, durations, timezones, locales, and plugins
---

# Moment.js Skill

Covers the **Moment.js** library (moment/moment) and its documentation site (moment/momentjs.com). Use for date/time parsing, manipulation, formatting, i18n, durations, timezone support (moment-timezone), and plugin integration.

> **Note:** Moment.js is in maintenance mode. For new projects, consider Luxon, Day.js, or date-fns. For existing code using Moment.js, this skill applies fully.

**Repository:** [moment/momentjs.com](https://github.com/moment/momentjs.com) **Language:** JavaScript (71%), SCSS (15.8%), Handlebars (12.3%) **License:** MIT

---

## When to Use This Skill

Trigger this skill when the user:

- Parses date strings: `moment("2023-01-20")`, `moment("Jan 20 2023", "MMM DD YYYY")`
- Formats dates for display: `.format("YYYY-MM-DD")`, `.fromNow()`, `.calendar()`
- Manipulates dates: `.add()`, `.subtract()`, `.startOf()`, `.endOf()`
- Queries dates: `.isBefore()`, `.isAfter()`, `.isBetween()`, `.isSame()`
- Works with durations: `moment.duration(2, 'hours')`
- Handles timezones via moment-timezone: `moment.tz("2023-01-20", "America/New_York")`
- Sets up locales / i18n: `moment.locale("pt-br")`
- Asks about Moment.js plugins (twix, range, recur, duration-format, etc.)
- Debugs Moment.js warnings (deprecation, invalid date, ambiguous input)
- Migrates away from Moment.js to Luxon/Day.js

---

## ⚡ Quick Reference

### Parsing

```javascript
// Current time
moment();

// ISO string
moment('2023-01-20');

// Custom format
moment('20/01/2023', 'DD/MM/YYYY');

// Multiple formats (tries each)
moment('20/01/2023', ['DD/MM/YYYY', 'MM/DD/YYYY']);

// Unix timestamp (seconds)
moment.unix(1674172800);

// Unix timestamp (milliseconds)
moment(1674172800000);

// From object
moment({ year: 2023, month: 0, day: 20 }); // month is 0-indexed

// UTC mode
moment.utc('2023-01-20T12:00:00Z');

// Strict mode (prevents forgiving parse)
moment('2023-01-20', 'YYYY-MM-DD', true);
```

### Validation

```javascript
moment('2023-13-01', 'YYYY-MM-DD').isValid(); // false — month 13 invalid
moment('2023-01-20', 'YYYY-MM-DD', true).isValid(); // strict parse
```

### Formatting

```javascript
moment().format(); // ISO 8601: "2023-01-20T15:30:00+03:00"
moment().format('YYYY-MM-DD'); // "2023-01-20"
moment().format('DD/MM/YYYY HH:mm'); // "20/01/2023 15:30"
moment().format('dddd, MMMM Do YYYY'); // "Friday, January 20th 2023"
moment().toISOString(); // "2023-01-20T12:30:00.000Z"
moment().valueOf(); // milliseconds since epoch
moment().unix(); // seconds since epoch
```

### Relative Time

```javascript
moment('2020-01-01').fromNow(); // "3 years ago"
moment('2020-01-01').from('2021-01-01'); // "a year ago"
moment().toNow(); // "in a few seconds"
moment().calendar(); // "Today at 3:30 PM"
```

### Manipulation

```javascript
moment().add(7, 'days');
moment().add({ hours: 2, minutes: 30 });
moment().subtract(1, 'month');
moment().startOf('day'); // 00:00:00
moment().endOf('month'); // last ms of month
moment().utc(); // switch to UTC mode
moment().local(); // switch to local mode
moment().utcOffset('+05:30'); // set offset
```

### Get / Set

```javascript
moment().year(); // get year
moment().year(2025); // set year
moment().month(); // 0-11
moment().date(); // day of month
moment().hour();
moment().minute();
moment().second();
moment().millisecond();
moment().dayOfYear();
moment().week();
moment().isoWeek();
moment().quarter();
moment().get('year'); // generic getter
moment().set('year', 2025);
```

### Querying

```javascript
moment('2023-01-15').isBefore('2023-06-01'); // true
moment('2023-01-15').isAfter('2023-01-01'); // true
moment('2023-01-15').isSame('2023-01-15', 'day'); // true
moment('2023-01-15').isBetween('2023-01-01', '2023-02-01'); // true
moment('2023-01-15').isSameOrBefore('2023-01-15'); // true
moment().isDST();
moment().isLeapYear();
moment.isMoment(x);
moment.isDate(x);
```

### Difference

```javascript
const a = moment('2023-01-01');
const b = moment('2023-06-30');
b.diff(a, 'days'); // 180
b.diff(a, 'months'); // 5
b.diff(a, 'years', true); // 0.49... (float)
```

### Durations

```javascript
moment.duration(2, 'hours');
moment.duration({ hours: 1, minutes: 30 });
moment.duration('P1Y2M3DT4H5M6S'); // ISO 8601 duration

const d = moment.duration(90, 'minutes');
d.hours(); // 1
d.minutes(); // 30
d.as('hours'); // 1.5
d.humanize(); // "2 hours"
d.toISOString(); // "PT1H30M"
```

### i18n / Locale

```javascript
// Global locale
moment.locale('pt-br');

// Instance locale
moment().locale('fr').format('LLLL');

// Check current locale
moment.locale(); // "pt-br"

// List months/weekdays in current locale
moment.months();
moment.weekdays();

// Load locale in Node.js
require('moment/locale/pt-br');
```

### Timezone (moment-timezone)

```javascript
const moment = require('moment-timezone');

// Parse in timezone
moment.tz('2023-01-20 12:00', 'America/New_York');

// Convert existing moment to timezone
moment().tz('Europe/London');

// Format with timezone
moment().tz('Asia/Tokyo').format('YYYY-MM-DD HH:mm z');

// Default timezone
moment.tz.setDefault('America/New_York');

// Guess user timezone
moment.tz.guess(); // "America/Sao_Paulo"

// Get all zone names
moment.tz.names();

// Get zones for a country
moment.tz.zonesForCountry('BR');
```

### Clone

```javascript
const a = moment();
const b = a.clone(); // independent copy — mutations don't affect a
```

---

## Key Concepts

### Mutability

Moment objects are **mutable**. `.add()`, `.subtract()`, `.startOf()` modify in-place. Use `.clone()` before chaining when you need the original.

```javascript
const start = moment();
const end = start.clone().add(7, 'days'); // safe — start unchanged
```

### Month Indexing

Months are **0-indexed** (January = 0, December = 11). Day of month is 1-indexed.

### Strict Parsing

Without strict mode, Moment is forgiving and may silently parse wrong dates. Use `true` as third arg:

```javascript
moment('01-20-2023', 'YYYY-MM-DD', true).isValid(); // false — format mismatch
```

### UTC vs Local

`.utc()` switches mode; `.local()` switches back. `.utcOffset()` sets a fixed offset without DST adjustments.

### Format Tokens

| Token  | Output                                |
| ------ | ------------------------------------- |
| `YYYY` | 4-digit year                          |
| `MM`   | 2-digit month (01–12)                 |
| `DD`   | 2-digit day                           |
| `HH`   | 24h hour                              |
| `hh`   | 12h hour                              |
| `mm`   | minutes                               |
| `ss`   | seconds                               |
| `A`    | AM/PM                                 |
| `a`    | am/pm                                 |
| `ddd`  | Mon–Sun                               |
| `dddd` | Monday–Sunday                         |
| `MMM`  | Jan–Dec                               |
| `MMMM` | January–December                      |
| `Do`   | 1st, 2nd, 3rd…                        |
| `X`    | Unix timestamp (s)                    |
| `x`    | Unix timestamp (ms)                   |
| `Z`    | UTC offset (+05:30)                   |
| `z`    | Timezone abbr (needs moment-timezone) |

---

## Docs Structure (momentjs.com repo)

The documentation is organized under `docs/` with numbered sections:

| Section | Content |
| --- | --- |
| `01-parsing/` | String, format, formats, special, object, unix, date, array, clone, UTC, parseZone, isValid, defaults |
| `02-get-set/` | millisecond–year, weekday, isoWeekday, dayOfYear, week, isoWeek, quarter, get/set, max/min |
| `03-manipulating/` | add, subtract, startOf, endOf, local, utc, utcOffset |
| `04-displaying/` | format, fromNow, from, toNow, to, calendar, diff, unix, daysInMonth, toDate, toArray, toJSON, toISOString, toObject, toString, inspect |
| `05-query/` | isBefore, isSame, isAfter, isSameOrBefore, isSameOrAfter, isBetween, isDST, isLeapYear, isMoment, isDate |
| `06-i18n/` | locale, instance-locale, loading, adding, getting, listing months/weekdays, locale-data, pseudo |
| `07-customization/` | month names/abbr, weekday names/abbr, long-date-formats, relative-time, AM/PM, calendar, ordinal, thresholds, rounding, now, dow-doy, eras, invalidDate |
| `08-durations/` | creating, clone, humanize, as, get, add/subtract, diffing, ISO string |
| `09-utilities/` | normalize-units, invalid |
| `10-plugins/` | strftime, msdate, jdateformatparser, range, twix, preciserange, recur, hijri, duration-format, etc. |

moment-timezone docs under `docs/moment-timezone/`: | Section | Content | |---------|---------| | `00-use-it/` | Node.js, browser, require.js, webpack | | `01-using-timezones/` | parsing-in-zone, ambiguous-inputs, converting, formatting, default-timezone, guessing, zone-names, country-zones | | `02-zone-object/` | name, abbr, offset, parse | | `03-data-formats/` | unpacked, packed, link | | `04-data-loading/` | adding zone, adding link, loading bundle, checking existence | | `05-data-utilities/` | pack, unpack, pack-base-60, filter-years, create-links |

---

## Available References

| File | Content | Confidence |
| --- | --- | --- |
| `references/file_structure.md` | Full repo tree (384 items) — navigate docs sections | medium |
| `references/issues.md` | 9 GitHub issues (2 open, 7 closed) — real-world bugs | medium |
| `references/README.md` | Main README | — |
| `references/CHANGELOG.md` | Version history | — |
| `references/releases.md` | Release notes | — |

---

## Working with This Skill

**Beginner:** Start with parsing + format. Use `moment().format("YYYY-MM-DD")` pattern. Remember months are 0-indexed.

**Intermediate:** Use strict parsing (`true` third arg). Clone before mutating. Understand UTC vs local mode.

**Advanced:** moment-timezone for DST-correct timezone work. Custom locales with `moment.defineLocale`. Duration diffing with `.as()`.

**Migrating away from Moment:** See `docs/moment-timezone/05-data-utilities/` for data patterns. Luxon is the official successor — API differs significantly (immutable, different format tokens).

---

**Sources:** GitHub repo file structure (medium confidence) + GitHub issues (medium confidence) **Generated by Skill Seeker** | Enhanced synthesis

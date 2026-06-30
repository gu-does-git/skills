---
name: lodash
license: MIT
metadata:
  doc_version: "4.18.1"
description: Use when working with lodash utility library. Triggers on: _.map, _.filter, _.groupBy, _.chunk, _.flatten, _.cloneDeep, _.isEqual, _.merge, _.get, _.set, _.pick, _.omit, _.camelCase, _.kebabCase, _.debounce, _.throttle, _.memoize, _.flow, _.curry, _.partial, _.uniq, _.orderBy, _.flatMap, _.flattenDeep, _.sumBy, _.template. Also triggers on: deep clone, deep equal, debounce, throttle, memoize, chain, iteratee shorthand, collection transform, object path, clone, sort, unique.
---

# lodash

JavaScript utility library delivering modularity, performance, & extras. Most depended-on npm package. Now in Feature-Complete maturity stage under OpenJS Foundation governance.

**Repository:** [lodash/lodash](https://github.com/lodash/lodash) **Version:** 4.18.1 (2026-04-01) **Docs:** https://lodash.com/docs **License:** MIT **Stars:** 61,304

## When to Use This Skill

**Use this skill when:**

- Writing array/collection transforms (`_.map`, `_.filter`, `_.groupBy`, `_.chunk`, `_.flatten`)
- Deep cloning or comparing objects (`_.cloneDeep`, `_.isEqual`, `_.merge`)
- Working with object paths (`_.get`, `_.set`, `_.pick`, `_.omit`)
- String utilities (`_.camelCase`, `_.kebabCase`, `_.deburr`, `_.template`)
- Functional programming patterns (`_.flow`, `_.curry`, `_.partial`, `lodash/fp`)
- Debugging known lodash bugs (see Known Issues)
- Checking security advisories before upgrading

**Do NOT use this skill for:** Underscore.js (different API), RxJS operators, or native ES2022+ equivalents.

---

## ⚡ Quick Reference

### Object utilities

```js
// Safe deep get with default
_.get(obj, 'a.b.c', 'default');

// Deep clone (avoids reference sharing)
const copy = _.cloneDeep(original);

// Merge (mutates first arg) vs assign (shallow)
_.merge({ a: { x: 1 } }, { a: { y: 2 } });
// => { a: { x: 1, y: 2 } }

// Pick/omit keys
_.pick(user, ['id', 'name']);
_.omit(user, ['password', 'token']);

// Deep equality
_.isEqual({ a: [1, 2] }, { a: [1, 2] }); // => true
```

### Array utilities

```js
// Group by property
_.groupBy([{ type: 'a' }, { type: 'b' }, { type: 'a' }], 'type');
// => { a: [...], b: [...] }

// Chunk array into pages
_.chunk([1, 2, 3, 4, 5], 2);
// => [[1, 2], [3, 4], [5]]

// Flatten nested arrays
_.flatMap([[1, 2], [3]], (x) => x); // => [1, 2, 3]
_.flattenDeep([1, [2, [3, [4]]]]); // => [1, 2, 3, 4]

// Unique values
_.uniqBy(items, 'id');

// Sort by multiple fields
_.orderBy(users, ['age', 'name'], ['asc', 'desc']);
```

### String utilities

```js
// Case transforms
_.camelCase('foo-bar'); // => 'fooBar'
_.kebabCase('fooBar'); // => 'foo-bar'
_.snakeCase('fooBar'); // => 'foo_bar'

// Remove diacritics (slugify helper)
_.deburr('déjà vu'); // => 'deja vu'

// Trim custom chars
_.trim('-_-abc-_-', '_-'); // => 'abc'

// Chain casing roundtrip
_.camelCase(_.snakeCase(_.kebabCase('fooBar'))); // => 'fooBar'
```

### Function utilities

```js
// Debounce / throttle
const search = _.debounce(fetchResults, 300);
const scroll = _.throttle(onScroll, 100);

// Memoize expensive computation
const memoized = _.memoize(expensiveCalc);

// Partial application
const double = _.partial(_.multiply, 2);
double(5); // => 10

// Fix parseInt radix issue with map
_.map(['6', '8', '10'], parseInt); // => [6, NaN, 2]  ← WRONG
_.map(['6', '8', '10'], _.partial(parseInt, _, 0)); // => [6, 8, 10] ← correct
```

---

## 📖 Reference Files

| File | Contents | Use When |
| --- | --- | --- |
| `references/README.md` | Full README with install, module formats, why lodash | New to lodash or setting up |
| `references/CHANGELOG.md` | Version history | Checking API changes between versions |
| `references/releases.md` | Release notes with security details | Evaluating upgrade impact |
| `references/issues.md` | 21 recent GitHub issues (10 open) | Debugging unexpected behavior |
| `references/file_structure.md` | Repo structure (187 items) | Contributing or understanding internals |

---

## 🗺️ Working with This Skill

### Beginner

1. Start with: `_.get`, `_.cloneDeep`, `_.map`, `_.filter`, `_.groupBy`
2. Docs: https://lodash.com/docs

### Intermediate

- Use `_.flow` to compose transforms without intermediate variables
- Prefer `_.mergeWith` when custom merge logic needed
- Use `_.memoize` for expensive pure functions

### Avoiding pitfalls

- `_.cloneDeep` does NOT handle sparse arrays correctly (issue #6191) — keep dense arrays or use spread
- `_.template` is a security boundary — never pass untrusted strings as import keys (CVE-2026-4800)
- `_.sumBy` on boolean arrays returns boolean — cast values first
- `_.invert` corrupts `__proto__` keys — sanitize input if keys come from user data

---

## 🔑 Key Concepts

### Chaining

```js
// Implicit chain — unwrap with .value()
_(items).filter('active').map('name').sort().value();

// Lazy evaluation kicks in automatically for large collections
```

### Iteratee shorthands

```js
// All equivalent
_.map(users, (user) => user.name);
_.map(users, 'name'); // property shorthand
_.map(users, ['name', 'Ana']); // matches shorthand
_.filter(users, { active: true }); // object match shorthand
```

---

**Source:** GitHub repository scraper | lodash/lodash | Last updated: 2026-04-21

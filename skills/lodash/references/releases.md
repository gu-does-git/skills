# Releases

Version history for this repository (4 releases).

## 4.18.1: 4.18.1

**Published:** 2026-04-01

## Bugs

Fixes a `ReferenceError` issue in `lodash` `lodash-es` `lodash-amd` and `lodash.template` when using the `template` and `fromPairs` functions from the modular builds. See https://github.com/lodash/lodash/issues/6167#issuecomment-4165269769

These defects were related to how lodash distributions are built from the main branch using https://github.com/lodash-archive/lodash-cli. When internal dependencies change inside lodash functions, equivalent updates need to be made to a mapping in the lodash-cli. (hey, it was ahead of its time once upon a time!). We know this, but we missed it in the last release. It's the kind of thing that passes in CI, but fails bc the build is not the same thing you tested.

There is no diff on main for this, but you can see the diffs for each of the npm packages on their respective branches:

- `lodash`: https://github.com/lodash/lodash/compare/4.18.0-npm...4.18.1-npm
- `lodash-es`: https://github.com/lodash/lodash/compare/4.18.0-es...4.18.1-es
- `lodash-amd`: https://github.com/lodash/lodash/compare/4.18.0-amd...4.18.1-amd
- `lodash.template`https://github.com/lodash/lodash/compare/4.18.0-npm-packages...4.18.1-npm-packages

[View on GitHub](https://github.com/lodash/lodash/releases/tag/4.18.1)

---

## 4.18.0: 4.18.0

**Published:** 2026-03-31

## v4.18.0

**Full Changelog**: https://github.com/lodash/lodash/compare/4.17.23...4.18.0

### Security

**`_.unset` / `_.omit`**: Fixed prototype pollution via `constructor`/`prototype` path traversal ([GHSA-f23m-r3pf-42rh](https://github.com/lodash/lodash/security/advisories/GHSA-f23m-r3pf-42rh), [fe8d32e](https://github.com/lodash/lodash/commit/fe8d32eda854377349a4f922ab7655c8e5df9a0b)). Previously, array-wrapped path segments and primitive roots could bypass the existing guards, allowing deletion of properties from built-in prototypes. Now `constructor` and `prototype` are blocked unconditionally as non-terminal path keys, matching `baseSet`. Calls that previously returned `true` and deleted the property now return `false` and leave the target untouched.

**`_.template`**: Fixed code injection via `imports` keys ([GHSA-r5fr-rjxr-66jc](https://github.com/lodash/lodash/security/advisories/GHSA-r5fr-rjxr-66jc), CVE-2026-4800, [879aaa9](https://github.com/lodash/lodash/commit/879aaa93132d78c2f8d20c60279da9f8b21576d6)). Fixes an incomplete patch for CVE-2021-23337. The `variable` option was validated against `reForbiddenIdentifierChars` but `importsKeys` was left unguarded, allowing code injection via the same `Function()` constructor sink. `imports` keys containing forbidden identifier characters now throw `"Invalid imports option passed into _.template"`.

### Docs

- Add security notice for `_.template` in threat model and API docs ([#6099](https://github.com/lodash/lodash/pull/6099))
- Document `lower > upper` behavior in `_.random` ([#6115](https://github.com/lodash/lodash/pull/6115))
- Fix quotes in `_.compact` jsdoc ([#6090](https://github.com/lodash/lodash/pull/6090))

### `lodash.*` modular packages

[Diff](https://github.com/lodash/lodash/pull/6157)

We have also regenerated and published a select number of the `lodash.*` modular packages.

These modular packages had fallen out of sync significantly from the minor/patch updates to lodash. Specifically, we have brought the following packages up to parity w/ the latest lodash release because they have had CVEs on them in the past:

- [lodash.orderby](https://www.npmjs.com/package/lodash.orderby)
- [lodash.tonumber](https://www.npmjs.com/package/lodash.tonumber)
- [lodash.trim](https://www.npmjs.com/package/lodash.trim)
- [lodash.trimend](https://www.npmjs.com/package/lodash.trimend)
- [lodash.sortedindexby](https://www.npmjs.com/package/lodash.sortedindexby)
- [lodash.zipobjectdeep](https://www.npmjs.com/package/lodash.zipobjectdeep)
- [lodash.unset](https://www.npmjs.com/package/lodash.unset)
- [lodash.omit](https://www.npmjs.com/package/lodash.omit)
- [lodash.template](https://www.npmjs.com/package/lodash.template)

[View on GitHub](https://github.com/lodash/lodash/releases/tag/4.18.0)

---

## 4.0.0: 4.0.0

**Published:** 2016-01-12

# [lodash v4.0.0](https://github.com/lodash/lodash/wiki/Changelog#v400)

2015 was big year! [Lodash](https://lodash.com/) became the [most depended on](https://gist.github.com/anvaka/8e8fa57c7ee1350e3491#file-01-most-dependent-upon-md) npm package, passed [1 billion](http://npm-stat.com/charts.html?package=&author=jdalton) downloads, & its v3 release saw massive adoption!

The year was also one of collaboration, as discussions began on [merging Lodash & Underscore](https://github.com/underdash/underdash/issues/14). Much of Lodash v4 is proofing out the ideas from those discussions. Lodash v4 **would not be possible** without the collaboration & contributions of the Underscore core team. In the spirit of merging our teams have blended with [several members](https://github.com/orgs/lodash/people) contributing to both libraries.

For 2016 & [lodash v4.0.0](https://github.com/lodash/lodash/wiki/Changelog#v400) we wanted to cut loose, push forward, & take things up a notch!

## Modern only

With v4 we’re breaking free from [old projects](https://github.com/lodash-archive), old environments, & dropping [old IE < 9 support](https://www.microsoft.com/en-us/WindowsForBusiness/End-of-IE-support)!

## 4 kB Core

Lodash’s kitchen-sink size will continue to grow as new methods & functionality are added. However, we now offer a 4 kB (gzipped) [core build](https://github.com/lodash/lodash/tree/4.0.0/dist) that’s compatible with [Backbone v1.2.4](https://github.com/jashkenas/backbone/issues/3839) for folks who want Lodash without lugging around the kitchen sink.

## More ES6

We’ve continued to embrace ES6 with methods like [\_.isSymbol](https://lodash.com/docs#isSymbol), added support for cloning & comparing array buffers, maps, sets, & symbols, converting iterators to arrays, & iterable `_(…)`.

In addition, we’ve published an [es-build](https://github.com/lodash/lodash/tree/4.0.0-es/) & pulled [babel-plugin-lodash](https://github.com/lodash/babel-plugin-lodash) into core to make tree-shaking a breeze.

## More Modular

Pop quiz! 📣

What category path does the `bindAll` method belong to? Is it

A) `require('lodash/function/bindAll')` B) `require('lodash/utility/bindAll')` C) `require('lodash/util/bindAll')`

Don’t know? Well, with v4 it doesn’t matter because now module paths are as simple as

```js
var bindAll = require('lodash/bindAll');
```

We’ve also reduced module complexity making it easier to create smaller bundles. This has helped Lodash adoption with libraries like [Async](https://github.com/caolan/async/pull/996) & [Redux](https://github.com/rackt/redux/pull/611)!

## 1st Class FP

With v3 we introduced [lodash-fp](https://github.com/lodash-archive/lodash-fp). We learned a lot & with v4 we decided to [pull it into core](https://github.com/lodash/lodash/wiki/FP-Guide).

Now you can get immutable, auto-curried, iteratee-first, data-last methods as simply as

```js
var _ = require('lodash/fp');
var object = { a: 1 };
var source = { b: 2 };
var newObject = _.assign(source)(object);

console.log(newObject);
// => { 'a': 1, 'b': 2 }

console.log(object);
// => { 'a': 1 }

var convert = require('lodash/fp/convert');
var assign = convert('assign', require('lodash.assign'));
// works too!
```

## Chakra Optimized

Well actually, while we’re [excited about Chakra](https://blogs.windows.com/msedgedev/2016/01/13/chakracore-now-open/), Lodash is optimized for great performance across **all engines**. Unlike many libraries, we don’t favor a single engine so we can deliver solid performance & support regardless of engine.

With v4 we’ve continued our commitment to performance; expanding support for lazy evaluation & improving the performance of core functionality like circular reference detection.

## Emojis

Taking things up a notch Lodash v4 has added support for emojis! Includes things like [astral symbols](https://twitter.com/jdalton/status/643438391498010624), [unicode modifiers](https://twitter.com/jdalton/status/647236920448172032), [variation selector characters](https://twitter.com/jdalton/status/645144377229078528), [zero-width joiners](https://twitter.com/jdalton/status/644783287508926464), & [regional indicator symbols](https://twitter.com/jdalton/status/644781038221201408).

<img src="https://cloud.githubusercontent.com/assets/4303/12280603/077c73ba-b944-11e5-900c-8463f8680612.png">

## Breaking changes

We’ve introduced more breaking changes in this release than any other so be sure to check out the [changelog](https://github.com/lodash/lodash/wiki/Changelog#compatibility-warnings) for a full rundown of changes & give [lodash-migrate](https://www.npmjs.com/package/lodash-migrate) a spin to help migrate older Lodash code to the latest release.

If you dig Lodash don’t forget to [star the repo](https://github.com/lodash/lodash/stargazers) or `npm star lodash`!

[View on GitHub](https://github.com/lodash/lodash/releases/tag/4.0.0)

---

## 3.0.0: 3.0.0

**Published:** 2015-01-26

# lodash v3.0.0

After a little over a year & more than [2,000](https://github.com/lodash/lodash/graphs/contributors?from=2013-12-01&type=c) [commits](https://github.com/lodash/lodash-cli/graphs/contributors?from=2013-12-01&type=c) we’re excited to release [lodash v3.0.0](https://github.com/lodash/lodash/tree/3.0.0). lodash follows [semantic versioning](http://semver.org/) so with this major release we’ve taken the opportunity to clean house & make [some back-compat breaking changes](https://github.com/lodash/lodash/wiki/Changelog#compatibility-warnings). We’ll get into that in a bit, but first lets talk about all the cool things this release has to offer.

## String methods

By popular demand we surveyed the utility landscape for a cross-section of string APIs to add to lodash. We settled on 17 string methods: [\_.camelCase](https://lodash.com/docs#camelCase), [\_.capitalize](https://lodash.com/docs#capitalize), [\_.deburr](https://lodash.com/docs#deburr), [\_.endsWith](https://lodash.com/docs#endsWith), [\_.escapeRegExp](https://lodash.com/docs#escapeRegExp), [\_.kebabCase](https://lodash.com/docs#kebabCase), [\_.pad](https://lodash.com/docs#pad), [\_.padLeft](https://lodash.com/docs#padLeft), [\_.padRight](https://lodash.com/docs#padRight), [\_.repeat](https://lodash.com/docs#repeat), [\_.snakeCase](https://lodash.com/docs#snakeCase), [\_.startsWith](https://lodash.com/docs#startsWith), [\_.trim](https://lodash.com/docs#trim), [\_.trimLeft](https://lodash.com/docs#trimLeft), [\_.trimRight](https://lodash.com/docs#trimRight), [\_.trunc](https://lodash.com/docs#trunc), & [\_.words](https://lodash.com/docs#words)

There’s familiar methods from ES5, like `_.trim`, & ES6, like `_.endsWith`, `_.repeat`, & `_.startsWith`, as well as some lesser known methods like `_.deburr` & `_.kebabCase`.

```js
// trims whitespace like `String#trim` but
// also allows specifying characters to trim
_.trim('  abc  ');
// → 'abc'
_.trim('-_-abc-_-', '_-');
// → 'abc'

// works great with `_.map` too
_.map(['  foo  ', '  bar  '], _.trim);
// → ['foo', 'bar']

// deburr diacritical marks (http://en.wikipedia.org/wiki/Diacritic)
_.deburr('déjà vu');
// → 'deja vu'

// similar to a `dasherize` or `slugify` method
_.kebabCase('foo bar');
// → 'foo-bar'
```

Following casing rules with methods like `_.camelCase`, `_.kebabCase`, & `_.snakeCase` allows for strings to be transformed from say camel case, to kebab case, to snake case, & back again.

```js
_.camelCase(_.snakeCase(_.kebabCase('fooBar')));
// → 'fooBar'
```

## ES is our jam

Previous versions of lodash added `_.assign`, `_.find`, `_.findIndex`, & ES template delimiter support. In this release we’re taking our ES adoption up a notch by aligning `_.includes`, `_.isFinite`, & `_.keys`, supporting typed arrays in `_.clone` & `_.isEqual`, using `Set` & `WeakMap` for [performance](http://jsperf.com/array-object-unique/2#chart=bar)-[gains](http://jsperf.com/weakmap-wrap#chart=bar), allowing `Map` & `WeakMap` to be used as [\_.memoize.Cache](https://lodash.com/docs/#memoize), & supporting [ES modularized builds](https://github.com/lodash/lodash/tree/3.0.0-es) with [lodash-cli](https://www.npmjs.com/package/lodash-cli).

## Functional goodies

There’s lots of functional goodies in v3 like `_.ary`, `_.curryRight`, `_.flow`, `_.rearg`, & support for customizable argument placeholders in `_.bind`, `_.bindKey`, `_.curry`, `_.curryRight`, `_.partial`, & `_.partialRight`.

```js
// infomercial fail
_.map(['6', '8', '10'], parseInt);
// → [6, NaN, 2]

// using a placeholder to pass over the
// `string` parameter & specify a `radix` of `0`
_.map(['6', '8', '10'], _.partial(parseInt, _, 0));
// → [6, 8, 10]

// is equivalent to
_.map(['6', '8', '10'], function (value) {
  return parseInt(value, 0);
});

// customize `_.partial.placeholder`
_.partial.placeholder = '_';
_.map(['6', '8', '10'], _.partial(parseInt, '_', 0));
// → [6, 8, 10]
```

Also several methods now [work out-of-the-box](https://github.com/lodash/lodash/wiki/Changelog#notable-changes) as iteratees for methods like `_.map` & `_.reduce`

```js
_.map(['6', '8', '10'], _.parseInt);
// → [6, 8, 10]

_.map(['a', 'a'], ['b', 'b'], _.uniq);
// → [['a'], ['b']]

_.reduce([{ b: 2 }, { c: 3 }], _.assign, { a: 1 });
// → { 'a': 1, 'b': 2, 'c': 3}
```

We’ve heard from some functional programming fans that lodash wasn’t _functional enough_, often citing our method signatures as an issue. To ease composition & currying they’d prefer methods like `_.filter` be `predicate` first & `collection` second instead of `collection` first & `predicate` second.

![Butter-side up](http://cdn.static.ovimg.com/episode/3092831.jpg)

It’d be a shame for those fans to lose out on lodash over something as little as method signatures so with v3 we’ve added `_.ary` & `_.rearg`. The `_.ary` method sets the argument cap of a function & `_.rearg` rearranges the arguments provided to a function.

```js
// cap the number arguments provided to `parseInt` at one
_.map(['6', '8', '10'], _.ary(parseInt, 1));
// → [6, 8, 10]

// create a `filter` that’s predicate-first
var filter = _.rearg(_.filter, 1, 0);
filter('a', [{ a: 0 }, { a: 1 }]);
// → [{ 'a': 1 }]

// create an `includes` that’s auto-curried & needle-first
var includes = _(_.includes).ary(2).rearg(1, 0).curry(2).value();
includes(2)([1, 2, 3]);
// → true
```

You can also use individual packages like [lodash.ary](https://www.npmjs.com/package/lodash.ary), [lodash.curry](https://www.npmjs.com/package/lodash.curry), & [lodash.rearg](https://www.npmjs.com/package/lodash.rearg) to convert functions.

```js
var ary = require('lodash.ary'),
  curry = require('lodash.curry'),
  rearg = require('lodash.rearg');

var getobject = require('getobject'),
  get = curry(rearg(ary(getobject, 2), [1, 0]), 2);

get('a.b.c')({ a: { b: { c: 'foo' } } });
// → 'foo'
```

Combined with [\_.runInContext](https://lodash.com/docs#runInContext) you could easily create a version of lodash with auto-curried iteratee-first methods. In fact, that’s what [we’ve done](https://github.com/lodash/lodash-fp/blob/0.1.0/index.js)! Introducing [lodash-fp](https://www.npmjs.com/package/lodash-fp).

```js
var items = [{ value: _.constant(['a', 'b']) }, { value: _.constant(['b', 'c']) }];

var getValues = _.flow(_.map(_.result('value')), _.flatten, _.uniq);

getValues(items);
// => ['a', 'b', 'c']

_.map(parseInt)(['6', '08', '10']);
// → [6, 8, 10]
```

lodash reduces the cost of method wrapping produced by `_.ary`, `_.curry`, & `_.rearg` by using a `WeakMap` to store function metadata. In this way a function is only wrapped once even though it may have `_.ary`, `_.curry`, & `_.rearg` applied.

## Modules, modules, modules

In lodash v2 we introduced [npm packages](https://www.npmjs.com/browse/keyword/lodash-modularized) per-method as well as bundles of modules for AMD & Node.js. With v3 we’ve improved [lodash-cli’s](https://www.npmjs.com/package/lodash-cli) ability to inline dependencies allowing us to easily customize inlining per method, enabling a better balance between deep dependency graphs & code duplication.

<table><tbody>
<tr><td valign="top">
<img src="http://f.cl.ly/items/2P1g0x0d0u2q3N0d022J/v2-dep-graph.png" alt="v2 dep graph">
</td><td valign="top">
<img src="http://f.cl.ly/items/1i3D3E0k0W1L1M1Z1k2w/v3-dep-graph.png" alt="v3 dep graph">
</td></tr>
</tbody></table>

In addition all modularized dependencies now use the `^` version range, instead of the `~`, so they’ll update as needed without you having to worry about it. Moving forward all per-method packages will be independently updated, instead of in bulk, because `lodash-cli` will soon be able to detect changes in packages & automatically bump patch/minor version numbers.

The [lodash](https://www.npmjs.com/package/lodash) & [lodash-compat](https://www.npmjs.com/package/lodash-compat) npm packages now come with modules baked in too. Perfect for [browserify](http://browserify.org/) and [webpack](http://webpack.github.io/)!

```js
// load the modern build
var _ = require('lodash');
// or a method category
var array = require('lodash/array');
// or a method
var chunk = require('lodash/array/chunk');
```

The method modules are organized by category so they’re [easy to find](https://lodash.com/docs).

lodash is available in a variety of other builds & module formats.

- npm packages for [modern](https://www.npmjs.com/package/lodash), [compatibility](https://www.npmjs.com/package/lodash-compat), & [per method](https://www.npmjs.com/browse/keyword/lodash-modularized) builds
- AMD modules for [modern](https://github.com/lodash/lodash/tree/3.0.0-amd) & [compatibility](https://github.com/lodash/lodash-compat/tree/3.0.0-amd) builds
- ES modules for the [modern](https://github.com/lodash/lodash/tree/3.0.0-es) build

## Performance

We’ve improved performance 20-40% overall in v3 by better utilizing the JIT in JavaScript engines, using internal helper functions that avoid optimization disqualifications & increase the likelihood of function inlining.

![performance comparison v3 vs v2](http://f.cl.ly/items/421w03451o322E1i1Y0S/perf-compare.png)

In v3 we’ve also introduced [lazily evaluated](http://filimanjaro.com/blog/2014/introducing-lazy-evaluation/) chaining for [massive performance wins](http://jsperf.com/lazy-demo#chart=bar) in certain scenarios.

As mentioned above we’re using `Set` & `WeakMap` for [performance](http://jsperf.com/array-object-unique/2#chart=bar)-[gains](http://jsperf.com/weakmap-wrap#chart=bar) which all modern browsers, Node.js, & io.js can benefit from.

## Breaking changes

lodash v3 is a major bump & we’ve introduced several back-compat breaking changes. One such change is that while we still [test against](https://saucelabs.com/u/lodash) Underscore/Backbone unit tests we’re no longer supporting an Underscore/Backbone build. Over the last year we’ve seen Underscore align more & more with lodash’s API so the need for a separate Underscore build has diminished. If you still need compatibility around some of the edges we recommend leveraging modules in lodash v3 to supplement your Underscore use.

Be sure to check out the [changelog](https://github.com/lodash/lodash/wiki/Changelog#compatibility-warnings-1) for a full rundown of changes & give [lodash-migrate](https://www.npmjs.com/package/lodash-migrate) a spin to help migrate older lodash code to the latest release.

## New Core Member

In closing I want to welcome [Benjamin Tan](https://twitter.com/bnjmnt4n) ([bnjmnt4n](https://github.com/bnjmnt4n)) as an official core member. Without the efforts of [contributors](https://github.com/lodash/lodash/graphs/contributors), like Benjamin, lodash v3 would not have happened.

If you dig lodash v3 don't forget to star the repo or `npm star lodash`!

[View on GitHub](https://github.com/lodash/lodash/releases/tag/3.0.0)

---

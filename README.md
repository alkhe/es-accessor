# Summary

Accessors reduce code redundancy and streamline various aspects of functional programming.

# Abstract

An accessor is syntactic sugar for retrieving object properties, taking the form of `.a.b.c`.

Many functional programming libraries (e.g. RxJS, Lodash, Ramda, fnjs, bilby) include a `pluck('key')` function on their primitives' prototypes as an alternative for `map(x => x.key)`. With accessors, `pluck` would be unnecessary. Many data-oriented libraries, like Redux, rely heavily on *selectors*, functions that often take the shape of `x => x.child`. With an accessor, this could be reduced to simply `.child`.

Consider `x => x.property`: the intent is to create a function that retrieves the value `property` on arbitrary data. The expression therefore contains extraneous code (`x => x`) and thus introduces more cognitive load.

Other functional programming languages, like Clojure, have this feature.

```clj
(def person { :name "John" :age 32 }) ; #'ns/person
(:name person) ; "John"
(:age person) ; 32
```

Accessors also simplify for many other plural or temporal design patterns, like Promises.

```js
somePromise().then(x => x.body)
```

```js
somePromise().then(.body)
```

# Desugaring

## Single

Accessor
```js
const fn = .x;
```

Naive (ES6)
```js
const fn = a => a.x;
```

Naive (ES5)
```js
var fn = function(a) {
  return a.x;
};
```

Strict
```js
const fn = function() {
  return arguments[0].x;
}
```

## Plural

Accessor
```js
const fn = .x['123'].y;
```

Naive (ES6)
```js
const fn = a => a.x['123'].y;
```

Naive (ES5)
```js
var fn = function(a) {
  return a.x['123'].y;
};
```

Strict
```js
const fn = function() {
  return arguments[0].x['123'].y;
}
```

# Syntax

*WIP*

# Notes

The format for this document was taken from [wycats/javascript-decorators](https://github.com/wycats/javascript-decorators).

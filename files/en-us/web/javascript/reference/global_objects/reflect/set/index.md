---
title: Reflect.set()
slug: Web/JavaScript/Reference/Global_Objects/Reflect/set
page-type: javascript-static-method
tags:
  - ECMAScript 2015
  - JavaScript
  - Method
  - Reference
  - Reflect
  - Polyfill
browser-compat: javascript.builtins.Reflect.set
---

{{JSRef}}

The static **`Reflect.set()`** method works like setting a
property on an object.

{{EmbedInteractiveExample("pages/js/reflect-set.html")}}

## Syntax

```js-nolint
Reflect.set(target, propertyKey, value)
Reflect.set(target, propertyKey, value, receiver)
```

### Parameters

- `target`
  - : The target object on which to set the property.
- `propertyKey`
  - : The name of the property to set.
- `value`
  - : The value to set.
- `receiver` {{optional_inline}}
  - : The value of `this` provided for the call to the setter for `propertyKey` on `target`. If provided and `target` does not have a setter for `propertyKey`, the property will be set on `receiver` instead.

### Return value

A {{jsxref("Boolean")}} indicating whether or not setting the property was successful.

### Exceptions

A {{jsxref("TypeError")}}, if `target` is not an
{{jsxref("Object")}}.

## Description

The `Reflect.set` method allows you to set a property on an object. It does
property assignment and is like the
[property accessor](/en-US/docs/Web/JavaScript/Reference/Operators/Property_Accessors) syntax as a function.

## Examples

### Using Reflect.set()

```js
// Object
let obj = {};
Reflect.set(obj, "prop", "value"); // true
obj.prop; // "value"

// Array
let arr = ["duck", "duck", "duck"];
Reflect.set(arr, 2, "goose"); // true
arr[2]; // "goose"

// It can truncate an array.
Reflect.set(arr, "length", 1); // true
arr; // ["duck"]

// With just one argument, propertyKey and value are "undefined".
let obj = {};
Reflect.set(obj); // true
Reflect.getOwnPropertyDescriptor(obj, "undefined");
// { value: undefined, writable: true, enumerable: true, configurable: true }
```

### Different target and receiver

When the `target` and `receiver` are different, `Reflect.set` will use the property descriptor of `target` (to find the setter or determine if the property is writable), but set the property on `receiver`.

```js
const target = {};
const receiver = {};
Reflect.set(target, "a", 2, receiver); // true
// target is {}; receiver is { a: 2 }

const target = { a: 1 };
const receiver = {};
Reflect.set(target, "a", 2, receiver); // true
// target is { a: 1 }; receiver is { a: 2 }

const target = {
  set a(v) {
    this.b = v;
  },
};
const receiver = {};
Reflect.set(target, "a", 2, receiver); // true
// target is { a: [Setter] }; receiver is { b: 2 }
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [Polyfill of `Reflect.set` in `core-js`](https://github.com/zloirock/core-js#ecmascript-reflect)
- {{jsxref("Reflect")}}
- [Property accessors](/en-US/docs/Web/JavaScript/Reference/Operators/Property_Accessors)

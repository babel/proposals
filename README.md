# Babel progress on [ECMAScript](https://github.com/tc39/ecma262) proposals

## [Official TC39 Proposals Repo](https://github.com/tc39/proposals)

## Proposals

For the official list, check the [TC39 repo](https://github.com/tc39/proposals). This list only contains all proposals higher than Stage 0 that are compilable by Babel. (If Stage 4, it will be in [preset-env](https://github.com/babel/babel-preset-env))

| Proposal Repo                                                                                               | Stage |
|-------------------------------------------------------------------------------------------------------------|-------|
| [Rest/Spread Properties](#restspread-properties)                               | 3     |
| [Asynchronous Iteration](#asynchronous-iteration)                                  | 3     |
| [Dynamic Import](#dynamic-import)                                               | 3     |
| [RegExp Unicode Property Escapes](https://github.com/tc39/proposal-regexp-unicode-property-escapes)         | 3     |
| [RegExp named capture groups](https://github.com/tc39/proposal-regexp-named-groups)                         | 3     |
| [`s` (`dotAll`) flag for regular expressions](https://github.com/mathiasbynens/es-regexp-dotall-flag)       | 3     |
| [`function.sent` metaproperty](https://github.com/allenwb/ESideas/blob/master/Generator%20metaproperty.md)  | 2     |
| [Class Fields](https://github.com/tc39/proposal-class-fields)                                               | 2     |
| [Class and Property Decorators](http://tc39.github.io/proposal-decorators/)                                 | 2     |
| [Arbitrary-precision Integers](https://github.com/tc39/proposal-integer)                                    | 2     |
| [`import.meta`](https://github.com/tc39/proposal-import-meta)                                               | 2     |
| [`export * as ns from "mod";` statements](https://github.com/leebyron/ecmascript-export-ns-from)            | 1     |
| [`export v from "mod";` statements](https://github.com/leebyron/ecmascript-export-default-from)             | 1     |
| Generator arrow functions (`=>*`)                                                                           | 1     |
| [Null Propagation](https://docs.google.com/presentation/d/11O_wIBBbZgE1bMVRJI8kGnmC6dWCBOwutbN9SWOK0fU/view)| 1     |
| [`do` expressions](https://gist.github.com/dherman/1c97dfb25179fa34a41b5fff040f9879)                        | 1     |
| [Numeric separators](https://github.com/samuelgoto/proposal-numeric-separator)                              | 1     |
| [Function bind syntax](https://github.com/zenparsing/es-function-bind)                                      | 0     |

## Implemented

### [Rest/Spread Properties](https://github.com/tc39/proposal-object-rest-spread)

**TC39 Champion**: Sebastian Markbage  
**Preset**: [babel-preset-stage-3](https://www.npmjs.com/package/babel-preset-stage-3)  
**Plugin**: [babel-plugin-transform-object-rest-spread](https://www.npmjs.com/package/babel-plugin-transform-object-rest-spread)  

<details>
<summary>Code Example</summary>

```js
// Rest properties 
let { x, y, ...z } = { x: 1, y: 2, a: 3, b: 4 };
console.log(x); // 1 
console.log(y); // 2 
console.log(z); // { a: 3, b: 4 } 
 
// Spread properties 
let n = { x, y, ...z };
console.log(n); // { x: 1, y: 2, a: 3, b: 4 } 
```
</details>

### [Asynchronous Iteration](https://github.com/tc39/proposal-async-iteration) 

**TC39 Champion**: Domenic Denicola  
**Preset**: [babel-preset-stage-3](https://www.npmjs.com/package/babel-preset-stage-3)  
**Plugin**: [babel-plugin-transform-async-generator-functions](https://www.npmjs.com/package/babel-plugin-transform-async-generator-functions)  

<details>
<summary>Code Example</summary>

```js
async function* agf() {
  await 1;
  yield 2;
}

async function f() {
  for await (let x of y) {
    g(x);
  }
}
```
</details>

### [Dynamic Import](https://github.com/tc39/proposal-dynamic-import) 

**TC39 Champion**: Domenic Denicola  
**Preset**: [babel-preset-stage-3](https://www.npmjs.com/package/babel-preset-stage-3)  
**Plugins**: [babel-plugin-syntax-dynamic-import](https://www.npmjs.com/package/babel-plugin-syntax-dynamic-import)  


Webpack 1: https://github.com/airbnb/babel-plugin-dynamic-import-webpack  
Webpack 2: supports this by default (just needs Babel to parse)  
Node: https://www.npmjs.com/package/babel-plugin-dynamic-import-node  

<details>
<summary>Code Example</summary>

```js
import('test-module').then(() => (
  import('test-module-2');
));
```
</details>

## Parser Only

## Not Implemented

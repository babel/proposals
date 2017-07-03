# Babel progress on [ECMAScript](https://github.com/tc39/ecma262) proposals

## [Official TC39 Proposals Repo](https://github.com/tc39/proposals)

## Proposals

For the official list, check the [TC39 repo](https://github.com/tc39/proposals). This list only contains all proposals higher than Stage 0 that are compilable by Babel. (If Stage 4, it will be in [preset-env](https://github.com/babel/babel-preset-env))

| Proposal Link                                                       | Current Stage | Status   |
|---------------------------------------------------------------------|---------------|----------|
| [Rest/Spread Properties](#restspread-properties)                    | 3             | 3        |
| [Asynchronous Iteration](#asynchronous-iteration)                   | 3             | 3        |
| [Dynamic Import](#dynamic-import)                                   | 3             | 3        |
| [RegExp Unicode Property Escapes](#regexp-unicode-property-escapes) | 3             | 3        |
| [RegExp Named Capture Groups](#regexp-named-capture-groups)         | 3             | 3        |
| [RegExp DotAll Flag](#regexp-dotall-flag)                           | 3             | 3        |
| [`function.sent`](#functionsent)                                    | 2             | Parseble |
| [Class Fields](#class-fields)                                       | 2             | 2        |
| [Class and Property Decorators](#class-and-property-decorators)     | 2             | 1        |
| [BigInt](#bigint)                                                   | 2             | Parseble |
| [`import.meta`](#importmeta)                                        | 2             | Parseble |
| [`export * as ns from "mod";`](#export-extensions)                  | 1             | 1        |
| [`export v from "mod";`](#export-extensions)                        | 1             | 1        |
| [Generator Arrow Functions](#generator-arrow-functions)             | 1             | N/A      |
| [Optional Chaining](#optional-chaining)                             | 1             | 1        |
| [`do` Expressions](#do-expressions)                                 | 1             | 1        |
| [Numeric Separator](#numeric-separator)                             | 1             | 1        |
| [Function Bind](#function-bind)                                     | 0             | 0        |
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

### [RegExp Unicode Property Escapes](https://github.com/tc39/proposal-regexp-unicode-property-escapes)

**TC39 Champion**: Brian Terlson, Daniel Ehrenberg, Mathias Bynens  
**Preset**: [babel-preset-stage-3](https://www.npmjs.com/package/babel-preset-stage-3)  
**Plugins**: [babel-plugin-transform-unicode-property-regex](https://www.npmjs.com/package/babel-plugin-transform-unicode-property-regex)  
<details>
<summary>Code Example</summary>

```js
const a = /^\p{Decimal_Number}+$/u;
const b = /\p{Script_Extensions=Greek}/u;
```
</details>

### [RegExp Named Capture Groups](https://github.com/tc39/proposal-regexp-named-groups)

**TC39 Champion**: Daniel Ehrenberg, Brian Terlson  
**Preset**: N/A
**Plugins**: [babel-plugin-transform-modern-regexp with `namedCapturingGroups` flag](https://www.npmjs.com/package/babel-plugin-transform-modern-regexp)  
<details>
<summary>Code Example</summary>

```js
let re = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/u;

let result = re.exec('2015-01-02');
// result.groups.year === '2015';
// result.groups.month === '01';
// result.groups.day === '02';

// result[0] === '2015-01-02';
// result[1] === '2015';
// result[2] === '01';
// result[3] === '02';
```
</details>

### [Regexp DotAll Flag](https://github.com/tc39/proposal-regexp-dotall-flag)

**TC39 Champion**: Daniel Ehrenberg, Jeff Morrison 
**Preset**: N/A
**Plugins**: [babel-plugin-transform-dotall-regex](https://github.com/mathiasbynens/babel-plugin-transform-dotall-regex), [babel-plugin-transform-modern-regexp with `dotAll` flag](https://www.npmjs.com/package/babel-plugin-transform-modern-regexp)     
<details>
<summary>Code Example</summary>

```js
/./s; // /[\0-\uFFFF]/;
```
</details>

### [Class Fields](https://github.com/tc39/proposal-class-fields)

**TC39 Champion**: Daniel Ehrenberg, Jeff Morrison 

> Stage 2

**Preset**: WIP
**Plugins**: WIP

> Stage 1

**Preset**: [babel-preset-stage-1](https://www.npmjs.com/package/babel-preset-stage-1)   
**Plugins**: [babel-plugin-transform-class-properties](babel-plugin-transform-class-properties)   
<details>
<summary>Code Example</summary>

```js
class Bork {
  instanceProperty = "bork";
  boundFunction = () => {
    return this.instanceProperty;
  }

  static staticProperty = "babelIsCool";
  static staticFunction = function() {
    return Bork.staticProperty;
  }
}
```
</details>

### [Class and Property Decorators](https://github.com/tc39/proposal-decorators)

**TC39 Champion**: Yehuda Katz and Brian Terlson 

> Stage 2

**Preset**: WIP
**Plugins**: WIP

> Stage 1

**Preset**: [babel-preset-stage-1](https://www.npmjs.com/package/babel-preset-stage-1)   
**Plugins**: [babel-plugin-transform-decorators](babel-plugin-transform-decorators), [babel-plugin-transform-decorators-legacy](https://github.com/loganfsmyth/babel-plugin-transform-decorators-legacy)   
<details>
<summary>Code Example</summary>

```js
@frozen class Foo {
  @configurable(false) @enumerable(true) method() {}
}
```
</details>

### Export Extensions

> This proposal was split into 2:  
> https://github.com/tc39/proposal-export-ns-from  
> https://github.com/tc39/ecmascript-export-default-from  

**TC39 Champion**: Lee Byron  
**Preset**: [babel-preset-stage-1](https://www.npmjs.com/package/babel-preset-stage-1)  
**Plugins**: [babel-plugin-transform-export-extensions](https://www.npmjs.com/package/babel-plugin-transform-export-extensions)  
<details>
<summary>Code Example</summary>

```js
export * as ns from 'mod'; // export-ns-from
export v from 'mod'; // export default from
```
</details>

### [Optional Chaining](https://github.com/tc39/proposal-optional-chaining)

**TC39 Champion**: Gabriel Isenberg  
**Preset**: [babel-preset-stage-1](https://www.npmjs.com/package/babel-preset-stage-1)  
**Plugins**: [babel-plugin-transform-optional-chaining](https://www.npmjs.com/package/babel-plugin-transform-optional-chaining)  
<details>
<summary>Code Example</summary>

```js
obj?.prop       // optional property access
obj?.[expr]     // optional property access
func?.(...args) // optional function or method call

a?.b = 42; // a == null ? undefined : a.b = 42;
```
</details>

### [`do` Expressions](https://gist.github.com/dherman/1c97dfb25179fa34a41b5fff040f9879)

**TC39 Champion**: Dave Herman  
**Preset**: [babel-preset-stage-1](https://www.npmjs.com/package/babel-preset-stage-1)  
**Plugins**: [babel-plugin-transform-do-expressions](https://www.npmjs.com/package/babel-plugin-transform-do-expressions)  
<details>
<summary>Code Example</summary>

```js
let a = do {
  if (x > 10) {
    'big';
  } else {
    'small';
  }
};

// let a = x > 10 ? 'big' : 'small';
```
</details>

### [Numeric Separator](https://github.com/tc39/proposal-numeric-separator)

**TC39 Champion**: Sam Goto  
**Preset**: [babel-preset-stage-1](https://www.npmjs.com/package/babel-preset-stage-1)  
**Plugins**: [babel-plugin-transform-numeric-separator](https://www.npmjs.com/package/babel-plugin-transform-numeric-separator)  
<details>
<summary>Code Example</summary>

```js
// Decimal Literals
let budget = 1_000_000_000_000;
// Binary Literals
let nibbles = 0b1010_0001_1000_0101;
// Hex Literal
let message = 0xA0_B0_C0;
```
</details>

### [Function Bind](https://github.com/tc39/proposal-regexp-named-groups)

**TC39 Champion**: Brian Terlson & Matthew Podwysocki  
**Preset**: [babel-preset-stage-0](https://www.npmjs.com/package/babel-preset-stage-0)  
**Plugins**: [babel-plugin-transform-function-bind](https://www.npmjs.com/package/babel-plugin-transform-function-bind)  
<details>
<summary>Code Example</summary>

```js
obj::func
// is equivalent to:
func.bind(obj)

obj::func(val)
// is equivalent to:
func.call(obj, val)

::obj.func(val)
// is equivalent to:
func.call(obj, val)
```
</details>

## Parser Only

### `function.sent`

**Info**: https://github.com/allenwb/ESideas/blob/master/Generator%20metaproperty.md
**TC39 Champion**: Allen Wirfs-Brock   
**Preset**: WIP  
**Plugins**: WIP  

### [BigInt](https://github.com/tc39/proposal-bigint)

**TC39 Champion**: Daniel Ehrenberg   
**Preset**: WIP  
**Plugins**: WIP  
**First Pull Request**: [babel/babylon#588](https://github.com/babel/babylon/pull/588) by [@wdhorton](https://github.com/wdhorton)  
**Babylon Label**: [Spec: BigInt](https://github.com/babel/babylon/issues?utf8=%E2%9C%93&q=label%3A%22Spec%3A%20BigInt%22%20)  
<details>
<summary>Code Example</summary>

```js
1n; // integer
0b101n // binary
0xFF123n // hex
0o16432n // octal
9223372036854775807n // larger than floating
```
</details>

<details>
<summary>Invalid Example</summary>

```js
// Invalid
1.0n // no decimals
2e9n // no exponential notation
016n // no old octal
```
</details>

### [`import.meta`](https://github.com/tc39/proposal-import-meta)

**TC39 Champion**: Domenic Denicola  
**Preset**: [babel-preset-stage-2](https://www.npmjs.com/package/babel-preset-stage-2)  
**Plugins**: [babel-plugin-syntax-import-meta](https://www.npmjs.com/package/babel-plugin-syntax-import-meta)  
<details>
<summary>Code Example</summary>

```js
import.meta.url;
mport.meta.scriptElement.dataset.size;
```
</details>

## Not Implemented

### Generator Arrow Functions

**TC39 Champion**: Brendan Eich, Domenic Denicola  
**Preset**: N/A  
**Plugins**: N/A  
<details>
<summary>Code Example</summary>

```js
()=>*{}
```
</details>

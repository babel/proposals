# Babel progress on [ECMAScript](https://github.com/tc39/ecma262) proposals
## [Official TC39 Proposals Repo](https://github.com/tc39/proposals)
#### [TC39 Proposals Process Document](https://tc39.github.io/process-document/)

## Proposals

For the official list, check the [TC39 repo](https://github.com/tc39/proposals). This list only contains all proposals higher than Stage 0 that are compilable by Babel. (If Stage 4, it will be in [preset-env](https://github.com/babel/babel/tree/master/packages/babel-preset-env))

| Proposal Link                                                       | Current Stage | Status   |
|---------------------------------------------------------------------|---------------|----------|
| [Dynamic Import](#dynamic-import)                                   | 4             | 3        |
| [RegExp Unicode Property Escapes](#regexp-unicode-property-escapes) | 4             | 3        |
| [RegExp Named Capture Groups](#regexp-named-capture-groups)         | 4             | 3        |
| [RegExp DotAll Flag](#regexp-dotall-flag)                           | 4             | 3        |
| [Class Fields](#class-fields)                                       | 3             | 2        |
| [`function.sent`](#functionsent)                                    | 2             | 2        |
| [Class and Property Decorators](#class-and-property-decorators)     | 2             | 1        |
| [BigInt](#bigint)                                                   | 4             | Parsable |
| [`import.meta`](#importmeta)                                        | 3             | Parsable |
| [`export * as ns from "mod";`](#export-extensions)                  | 4             | 1        |
| [`export v from "mod";`](#export-extensions)                        | 1             | 1        |
| [Generator Arrow Functions](#generator-arrow-functions)             | 1             | N/A      |
| [Optional Chaining](#optional-chaining)                             | 4             | 1        |
| [`do` Expressions](#do-expressions)                                 | 1             | 1        |
| [Numeric Separator](#numeric-separator)                             | 3             | 1        |
| [Function Bind](#function-bind)                                     | 0             | 0        |
| [Pattern matching](#pattern-matching)                               | 1             | 0        |

## Implemented

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
**Plugins**: [babel-plugin-transform-modern-regexp](https://www.npmjs.com/package/babel-plugin-transform-modern-regexp) (with `namedCapturingGroups` flag)  
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
**Plugins**: [babel-plugin-transform-dotall-regex](https://github.com/mathiasbynens/babel-plugin-transform-dotall-regex), [babel-plugin-transform-modern-regexp](https://www.npmjs.com/package/babel-plugin-transform-modern-regexp) (with `dotAll` flag)   
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
**First Pull Request**: [babel/babylon#608](https://github.com/babel/babylon/issues/608) by [@diervo](https://github.com/diervo)  
**Babylon Label**: [Spec: Class Fields](https://github.com/babel/babylon/issues?q=is%3Aopen+is%3Aissue+label%3A%22Spec%3A+Class+Fields%22)  

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
**First Pull Request**: [babel/babylon#587](https://github.com/babel/babylon/pull/587) by [@peey](https://github.com/peey)  
**Babylon Label**: [Spec: Decorators](https://github.com/babel/babylon/issues?q=is%3Aopen+is%3Aissue+label%3A%22Spec%3A+Decorators%22)  
<details>
<summary>Code Example</summary>

```
@frozen class Foo {
  @configurable(false) @enumerable(true) method() {}
}
function frozen(constructor, parent, elements) {
  return {
    constructor,
    elements,
    finisher(constructor) {
      Object.freeze(constructor.prototype)
      Object.freeze(constructor)
    }
  }
}
function configurable(configurable) {
  return decorator;
  function decorator(previousDescriptor) {
    return {
      ...previousDescriptor,
      descriptor: {
        ...previousDescriptor.descriptor,
        configurable
      }
    }
  }
}
function enumerable(enumerable) {
  return decorator;
  function decorator(previousDescriptor) {
    return {
      ...previousDescriptor,
      descriptor: {
        ...previousDescriptor.descriptor,
        enumerable
      }
    }
  }
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
**First Pull Request**: [babel/babylon#541](https://github.com/babel/babylon/pull/541) by [@rwaldron](https://github.com/rwaldron)  
**Babylon Label**: [Spec: Numeric Separator](https://github.com/babel/babylon/issues?q=is%3Aopen+is%3Aissue+label%3A%22Spec%3A+Numeric+Separator%22)  
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

### [Function Bind](https://github.com/tc39/proposal-bind-operator)

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

### [`function.sent`](https://github.com/allenwb/ESideas/blob/master/Generator%20metaproperty.md)

**TC39 Champion**: Allen Wirfs-Brock  
**Preset**: [babel-preset-stage-2](https://www.npmjs.com/package/babel-preset-stage-2)  
**Plugins**: [babel-plugin-transform-function-sent](https://www.npmjs.com/package/babel-plugin-transform-function-sent)    
<details> 
<summary>Code Example</summary>

```js
function* generator() {
  console.log("Sent", function.sent);
  console.log("Yield", yield);
}

const iterator = generator();
iterator.next(1); // Logs "Sent 1"
iterator.next(2); // Logs "Yield 2"
```
</details>

## Parser Only

### [BigInt](https://github.com/tc39/proposal-bigint)

**TC39 Champion**: Daniel Ehrenberg   
**Preset**: WIP  
**Plugins**: WIP  
**First Pull Request**: [babel/babylon#588](https://github.com/babel/babylon/pull/588) by [@wdhorton](https://github.com/wdhorton)  
**Babylon Label**: [Spec: BigInt](https://github.com/babel/babylon/issues?utf8=%E2%9C%93&q=label%3A%22Spec%3A%20BigInt%22%20)  
<details>
<summary>Code Example</summary>

```js
1n // integer
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
**First Pull Request**: [babel/babylon#544](https://github.com/babel/babylon/pull/544) by [@jkrems](https://github.com/jkrems)  
**Babylon Label**: [Spec: import.meta](https://github.com/babel/babylon/issues?q=import.meta+is%3Aclosed+label%3A%22Spec%3A+import.meta%22)  
<details>
<summary>Code Example</summary>

```js
import.meta.url;
import.meta.scriptElement.dataset.size;
```
</details>

## Not Implemented

### [Pattern Matching](https://github.com/tc39/proposal-pattern-matching)

**TC39 Champion**: Brian Terlson (Microsoft, @bterlson), Sebastian Markbåge (Facebook, @sebmarkbage)  
**Preset**: WIP    
**Plugins**: WIP    
**Babylon Label**: [Spec: pattern matching](https://github.com/babel/babylon/labels/Spec%3A%20Pattern%20matching)    
**First Pull Request**: [babel/babylon#635](https://github.com/babel/babylon/pull/635) by [@krzkaczor](https://github.com/krzkaczor)
<details>
<summary>Code Example</summary>

```js
const length = vector => {
  case (vector) {
    when { x, y, z } -> return Math.sqrt(x ** 2 + y ** 2 + z ** 2)
    when { x, y } ->   return Math.sqrt(x ** 2 + y ** 2)
    when [...etc] ->     return vector.length
  }
}
```

```js
const isVerbose = config => {
   case (config) {
    when {output: { verbose: true }} -> return true
    when config -> return false
    }
}

```

```js
const res = await fetch(jsonService)
case (res) {
  when {status: 200, headers: {'Content-Length': s}} ->
    console.log(`size is ${s}`)
  when {status: 404} ->
    console.log('JSON not found')
  when {status} if (status >= 400) -> {
    throw new RequestError(res)
  }
}
```
</details>

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

## FAQ

### When does Babel implement new features?

Babel will accept any PR for a proposal that is intended to go through the TC39 Proposal Process. This just means that we could implement and release a proposal starting at Stage 0. However this doesn't mean that we will implement it ourselves, but that we will work with both TC39 Champions and the community to get an implementation in. (And sometimes we have to wait for Summer of Code for that to happen).

It's our intention (and one of our main goals) as a project to help TC39 get feedback from the community through using the new syntax in their codebases. There is however a balance between supporting new proposals and informing users that any proposal is still just a proposal and subject to change. In order to move the community forward, we will continuously make changes to adhere to the spec as patches. If bigger changes require a major version, we will deprecate older versions of plugins, document those changes, and see if we can automate the upgrade via a codemod. This way everyone is moving towards Stage 4 and closer to what will be in the spec if the proposal makes it to the end.

This means we will also include proposals in this repo that haven't been presented to the committee yet if they are concrete enough and someone on TC39 is planning on presenting it (and marked appropriately).

<div align="center">
  <img src="shots/logo.png" alt="kleur" height="120" />
</div>

<div align="center">
  <a href="https://npmjs.org/package/kleur">
    <img src="https://img.shields.io/npm/v/kleur.svg" alt="version" />
  </a>
  <a href="https://travis-ci.org/lukeed/kleur">
    <img src="https://img.shields.io/travis/lukeed/kleur.svg" alt="travis" />
  </a>
  <a href="https://npmjs.org/package/kleur">
    <img src="https://img.shields.io/npm/dm/kleur.svg" alt="downloads" />
  </a>
</div>

<div align="center">The fastest Node.js library for formatting terminal text with ANSI colors~!</div>

## Features

* No dependencies
* Super [lightweight](##load-time) & [performant](#performance)
* Supports [nested](#nested-methods) & [chained](#chained-methods) colors
* No `String.prototype` modifications
* Conditional [color support](#conditional-support)
* Familiar [API](#api)

_Originally inspired by [`ansi-colors`](https://github.com/doowb/ansi-colors). See [Credits](#credits) for more info!_


## Install

```
$ npm install --save kleur
```


## Usage

```js
const kleur = require('kleur');

// basic usage
kleur.red('red text');

// chained methods
kleur.blue.bold.underline('howdy partner');

// nested methods
kleur.bold(`${ kleur.bgRed.white('[ERROR]') } ${ kleur.red.italic('Something happened')}`);
```

### Chained Methods

```js
console.log(kleur.bold.red('this is a bold red message'));
console.log(kleur.bold.italic('this is a bold italicized message'));
console.log(kleur.bold.yellow.bgRed.italic('this is a bold yellow italicized message'));
console.log(kleur.green.bold.underline('this is a bold green underlined message'));
```

<img src="shots/1.png" width="300" />

### Nested Methods

```js
const { yellow, red, cyan } = require('kleur');

console.log(yellow(`foo ${red.bold('red')} bar ${cyan('cyan')} baz`));
console.log(yellow('foo ' + red.bold('red') + ' bar ' + cyan('cyan') + ' baz'));
```

<img src="shots/2.png" width="300" />


### Conditional Support

Toggle color support as needed; `kleur` assumes it's always enabled.

```js
const kleur = require('kleur');

// manually disable
kleur.enabled = false;

// or use a library to detect support
kleur.enabled = require('color-support').level;

console.log(kleur.red('I will only be colored red if the terminal supports colors'));
```


## API

Any `kleur` method returns a `String` (when invoked, not chained). It's up to the developer to pass the output to destinations like `console.log`, `process.stdout.write`, etc.

The methods below are grouped by type for legbility purposes only. They each can be [chained](#chained-methods) or [nested](#nested-methods) with one another.

***Colors:***
> black &mdash; red &mdash; green &mdash; yellow &mdash; blue &mdash; magenta &mdash; cyan &mdash; white &mdash; gray

***Backgrounds:***
> bgBlack &mdash; bgRed &mdash; bgGreen &mdash; bgYellow &mdash; bgBlue &mdash; bgMagenta &mdash; bgCyan &mdash; bgWhite

***Modifiers:***
> reset &mdash; bold &mdash; dim &mdash; italic* &mdash; underline &mdash; inverse &mdash; hidden &mdash; strikethrough*

<sup>* <em>Not widely supported</em></sup>


## Benchmarks

> Using Node v8.9.0

### Load time

```
chalk: 9.372ms
turbocolor: 0.526ms
ansi-colors: 0.851ms
kleur: 0.862ms
```

### Performance

```
# All Colors
  ansi-colors x 60,762 ops/sec ±0.36% (96 runs sampled)
  chalk x 7,144 ops/sec ±3.99% (71 runs sampled)
  turbocolor x 98,181 ops/sec ±0.30% (95 runs sampled)
  kleur x 146,739 ops/sec ±0.55% (93 runs sampled)

# Stacked colors
  ansi-colors x 13,600 ops/sec ±0.15% (95 runs sampled)
  chalk x 1,690 ops/sec ±4.75% (70 runs sampled)
  turbocolor x 28,830 ops/sec ±0.21% (94 runs sampled)
  kleur x 30,573 ops/sec ±0.15% (96 runs sampled)

# Nested colors
  ansi-colors x 28,747 ops/sec ±0.50% (90 runs sampled)
  chalk x 3,424 ops/sec ±4.04% (71 runs sampled)
  turbocolor x 41,181 ops/sec ±2.99% (91 runs sampled)
  kleur x 61,155 ops/sec ±0.19% (96 runs sampled)
```


## Credits

This project was originally inspired by [Brian Woodward](https://github.com/doowb)'s awesome [`ansi-colors`](https://github.com/doowb/ansi-colors) project.

Unlike v1, the latest version(s) of `kleur` no longer supports:

* printf-formatting
* variadic function arguments
* multiline text via `\n` or `\r`
* `kleur.clear()` method

In addition, `kleur` continues to be ship without symbols and bright color variants.

If you need _any_ of these features, please use `ansi-colors` instead~!


## License

MIT © [Luke Edwards](https://lukeed.com)

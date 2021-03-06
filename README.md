# makeup-navigation-emitter

<p>
    <a href="https://travis-ci.org/makeup-js/makeup-navigation-emitter"><img src="https://api.travis-ci.org/makeup-js/makeup-navigation-emitter.svg?branch=master" alt="Build Status" /></a>
    <a href='https://coveralls.io/github/makeup-js/makeup-navigation-emitter?branch=master'><img src='https://coveralls.io/repos/makeup-js/makeup-navigation-emitter/badge.svg?branch=master&service=github' alt='Coverage Status' /></a>
    <a href="https://david-dm.org/makeup-js/makeup-navigation-emitter"><img src="https://david-dm.org/makeup-js/makeup-navigation-emitter.svg" alt="Dependency status" /></a>
    <a href="https://david-dm.org/makeup-js/makeup-navigation-emitter#info=devDependencies"><img src="https://david-dm.org/makeup-js/makeup-navigation-emitter/dev-status.svg" alt="devDependency status" /></a>
</p>

A vanilla JavaScript port of <a href="https://github.com/ianmcburnie/jquery-linear-navigation">jquery-linear-navigation</a>.

Emits custom events based on keyboard navigation of one or two dimensional model.

## Experimental

This module is still in an experimental state, until it reaches v1.0.0 you must consider all minor releases as breaking
changes. Patch releases may introduce new features, but will be backwards compatible.

## Install

```js
// via npm
npm install makeup-navigation-emitter

// via yarn
yarn add makeup-navigation-emitter
```

## Example 1

Example support for a roving tabindex model of keyboard navigation.

Note that this module will not change focus, that is the job of an observer such as makeup-roving-tabindex.

```html
<div class="widget">
    <ul>
        <li tabindex="0">Item 0</li>
        <li>Item 1</li>
        <li>Item 2</li>
    </ul>
</div>
```

```js
const NavigationEmitter = require('makeup-navigation-emitter');

const widgetEl = document.querySelector('.widget');

var emitter = NavigationEmitter.createLinear(widgetEl, 'li'));

widgetEl.addEventListener('navigationModelChange', function(e) {
    console.log(e.detail.fromIndex, e.detail.toIndex);
});
```

## Example 2

Example support for an active descendant model of navigation with focus on ancestor of items.

Note that this module will not highlight the active item, that is the job of an observer such as makeup-active-descendant.

```html
<div class="widget" tabindex="0">
    <ul>
        <li>Item 0</li>
        <li>Item 1</li>
        <li>Item 2</li>
    </ul>
</div>
```

```js
const NavigationEmitter = require('makeup-navigation-emitter');

const widgetEl = document.querySelector('.widget');

var emitter = NavigationEmitter.createLinear(widgetEl, 'li', { autoInit: -1, autoReset: -1 }));

widgetEl.addEventListener('navigationModelChange', function(e) {
    console.log(e.detail.fromIndex, e.detail.toIndex);
});
```

## Example 3

Example support for an active descendant model of navigation with focus on non-ancestor of items.

Note that this module will not highlight the active item, that is the job of an observer such as makeup-active-descendant.

```html
<div class="widget">
    <input type="text" />
    <ul>
        <li>Item 0</li>
        <li>Item 1</li>
        <li>Item 2</li>
    </ul>
</div>
```

```js
const NavigationEmitter = require('makeup-navigation-emitter');

const widgetEl = document.querySelector('.widget');

var emitter = NavigationEmitter.createLinear(widgetEl, 'li', { autoInit: -1, autoReset: -1 }));

widgetEl.addEventListener('navigationModelChange', function(e) {
    console.log(e.detail.fromIndex, e.detail.toIndex);
});
```

## Options

* `autoInit`: specify an integer or -1 for initial index (default: 0)
* `autoReset`: specify an integer or -1 for index position when focus exits widget (default: null)
* `wrap` : specify whether arrow keys should wrap/loop (default: false)

## Events

* `navigationModelInit` - fired when the model is auto initialised
* `navigationModelChange` - fired when the index is set by any means other than auto init or auto reset
* `navigationModelReset` - fired when the model is auto reset

For all 3 events, the event detail object contains the `fromIndex` and `toIndex`.

## Dependencies

* https://github.com/makeup-js/makeup-exit-emitter
* https://github.com/makeup-js/makeup-key-emitter

## Development

* `npm start`
* `npm test`
* `npm run lint`
* `npm run fix`
* `npm run build`
* `npm run clean`

The following hooks exist, and do not need to be invoked manually:

* `npm prepublishOnly` cleans, lints, tests and builds on every `npm publish` command
* `pre-commit` cleans, lints, tests and builds on every `git commit` command

## Test Reports

Each test run will generate the following reports:

* `/reports/coverage` contains Istanbul code coverage report
* `/reports/html` contains HTML test report

## CI Build

https://travis-ci.org/makeup-js/makeup-navigation-emitter

## Code Coverage

https://coveralls.io/github/makeup-js/makeup-navigation-emitter

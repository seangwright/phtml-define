# pHTML Define [<img src="https://phtmlorg.github.io/phtml/logo.svg" alt="pHTML" width="90" height="90" align="right">][phtml]

[![NPM Version][npm-img]][npm-url]
[![Build Status][cli-img]][cli-url]
[![Support Chat][git-img]][git-url]

[pHTML Define] lets you use custom defined elements in HTML.

```html
<!-- _define.html -->

<define tag="pricing-tier">
  <header>
    <h1>$<slot name="price" /></h1>
    <h2><slot name="name" /></h2>
  </header>
  <div class="features">
    <slot name="features" />
  </div>
</define>

<!-- index.html -->

<link rel="html" href="_define.html" />
<pricing-tier slot-name="Basic">
  <slot name="price">10</slot>
  <ul slot="features">
    <li>Unlimited foo</li>
  </ul>
</pricing-tier>

<!-- becomes -->

<header>
  <h1>$10</h1>
  <h2>Basic</h2>
</header>
<div class="features">
  <ul>
    <li>Unlimited foo</li>
  </ul>
</div>
```

## Usage

Add [pHTML Define] to your project:

```bash
npm install @phtml/define --save-dev
```

Use [pHTML Define] to process your HTML:

```js
const phtmlDefine = require('@phtml/define');

phtmlDefine.process(YOUR_HTML /*, processOptions, pluginOptions */);
```

Or use it as a [pHTML] plugin:

```js
const phtml = require('phtml');
const phtmlDefine = require('@phtml/define');

phtml([
  phtmlDefine(/* pluginOptions */)
]).process(YOUR_HTML /*, processOptions */);
```

[pHTML Define] runs in all Node environments, with special instructions for:

| [Node](INSTALL.md#node) | [pHTML CLI](INSTALL.md#phtml-cli) | [Webpack](INSTALL.md#webpack) | [Create React App](INSTALL.md#create-react-app) | [Gulp](INSTALL.md#gulp) | [Grunt](INSTALL.md#grunt) |
| --- | --- | --- | --- | --- | --- |

## Options

### preserve

The `preserve` option determines whether all custom element containers should remain. By default, custom element containers are not preserve. However when
custom elements are preserved, their original children are moved into a
`<template>` element.

```js
// preserve all custom elements
phtmlInclude({ preserve: true });
```

```html
<link rel="html" href="_define.html" />
<pricing-tier slot-name="Basic">
  <slot name="price">10</slot>
  <ul slot="features">
    <li>Unlimited foo</li>
  </ul>
</pricing-tier>

<!-- becomes -->

<link rel="html" href="_define.html" />
<pricing-tier slot-name="Basic">
  <template>
    <slot name="price">10</slot>
    <ul slot="features">
      <li>Unlimited foo</li>
    </ul>
  </template>
  <header>
    <h1>$10</h1>
    <h2>Basic</h2>
  </header>
  <div class="features">
    <ul>
      <li>Unlimited foo</li>
    </ul>
  </div>
</pricing-tier>
```

### cwd

The `cwd` option defines and overrides the current working directory of
`<link rel="html" href>`.

```js
// resolve all relative html links to /some/absolute/path
phtmlInclude({ cwd: '/some/absolute/path' });
```

[cli-img]: https://img.shields.io/travis/phtmlorg/phtml-define.svg
[cli-url]: https://travis-ci.org/phtmlorg/phtml-define
[git-img]: https://img.shields.io/badge/support-chat-blue.svg
[git-url]: https://gitter.im/phtmlorg/phtml
[npm-img]: https://img.shields.io/npm/v/@phtml/define.svg
[npm-url]: https://www.npmjs.com/package/@phtml/define

[pHTML]: https://github.com/phtmlorg/phtml
[pHTML Define]: https://github.com/phtmlorg/phtml-define
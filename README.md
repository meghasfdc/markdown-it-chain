# markdown-it-chain

[![Greenkeeper badge](https://badges.greenkeeper.io/ulivz/markdown-it-chain.svg)](https://greenkeeper.io/)

> A chaining API like [webpack-chain](https://github.com/neutrinojs/webpack-chain) but for [markdown-it](https://markdown-it.github.io/markdown-it/).

<a href="https://npmjs.com/package/markdown-it-chain"><img src="https://img.shields.io/npm/v/markdown-it-chain.svg?style=flat" alt="NPM version"></a> <a href="https://npmjs.com/package/markdown-it-chain"><img src="https://img.shields.io/npm/dm/markdown-it-chain.svg?style=flat" alt="NPM downloads"></a> <a href="https://circleci.com/gh/ulivz/markdown-it-chain"><img src="https://img.shields.io/circleci/project/ulivz/markdown-it-chain/master.svg?style=flat" alt="Build Status"></a> <a href="https://packagephobia.now.sh/result?p=markdown-it-chain"><img src="https://packagephobia.now.sh/badge?p=markdown-it-chain" alt="install size"></a>


## Install

**Yarn**

```bash
yarn add -dev markdown-it-chain
```

**npm**

```bash
npm install --save-dev markdown-it-chain
```

## Getting Started

```js
// Require the markdown-it-chain module. This module exports a single
// constructor function for creating a configuration API.
const Config = require('markdown-it-chain')

// Instantiate the configuration with a new API
const config = new Config()

// Make configuration changes using the chain API.
// Every API call tracks a change to the stored configuration.
config
  // Interact with 'options' in new MarkdownIt
  // Ref: https://markdown-it.github.io/markdown-it/#MarkdownIt.new
  .options
    .html(true) // equal to .set('html', true)
    .linkify(true)
    .end()

  // Interact with 'plugins'
  .plugin('toc')
    // The first parameter is the plugin module, which may be a function
    // while the second parameter is an array of parameters accepted by the plugin.
    .use(require('markdown-it-table-of-contents'), [{
      includeLevel: [2, 3]
    }])
    // Move up one level, like .end() in jQuery.
    .end()

  .plugin('anchor')
    .use(require('markdown-it-anchor'), [{
      permalink: true,
      permalinkBefore: true,
      permalinkSymbol: '$'
    }])
    // Apply this plugin before toc.
    .before('toc')

// Create a markdown-it instance using the above configuration
const md = config.toMd()
md.render('[[TOC]] \n # h1 \n ## h2 \n ## h3 ')
```

## Worth Reading

In order to ensure the consistency of the chained API world, `markdown-it-chain` is developed directly on the basis of [webpack-chain](https://github.com/neutrinojs/webpack-chain) and ensures that the usage is completely consistent.

Here are some things worth reading that come from `webpack-chain`:

- [ChainedMap](https://github.com/neutrinojs/webpack-chain#chainedmap)
- [Config plugins](https://github.com/neutrinojs/webpack-chain#config-plugins)

## Author

**markdown-it-chain** © [ULIVZ](https://github.com/ULIVZ), Released under the [MIT](./LICENSE) License.<br>
Authored and maintained by ULIVZ with help from contributors ([list](https://github.com/ULIVZ/markdown-it-chain/contributors)).

> [github.com/ulivz](https://github.com/ULIVZ) · GitHub [@ULIVZ](https://github.com/ULIVZ) · Twitter [@_ulivz](https://twitter.com/_ulivz)

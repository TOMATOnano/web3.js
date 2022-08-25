<p style="text-align: center;">
  <img src="assets/logo/web3js.jpg" width="200" alt="web3.js">
</p>

# web3.js - Ethereum JavaScript API

[![Discord][discord-image]][discord-url] [![StackExchange][stackexchange-image]][stackexchange-url] [![NPM Package Version][npm-image-version]][npm-url] [![NPM Package Downloads][npm-image-downloads]][npm-url] [![Build Status][actions-image]][actions-url] [![Dev Dependency Status][deps-dev-image]][deps-dev-url] [![Coverage Status][coveralls-image]][coveralls-url] [![Lerna][lerna-image]][lerna-url] [![Netlify Status][netlify-image]][netlify-url] [![GitPOAP Badge][gitpoap-image]][gitpoap-url]


これはEthereumの[JavaScript API][docs]を
[Generic JSON-RPC](https://github.com/ethereum/wiki/wiki/JSON-RPC)仕様に接続するものです。

このライブラリを使用するには、ローカルまたはリモートの[Ethereum](https://www.ethereum.org/)ノードを実行する必要があります。

詳しくは[ドキュメント][docs]をお読みください。

## Installation

### Node

```bash
npm install web3
```

### Yarn

```bash
yarn add web3
```

### In the Browser

ビルド済みの `dist/web3.min.js` を使用するか、または
[web3.js][repo]リポジトリを使ってビルドしてください。

```bash
npm run build
```

そして、html ファイルに `dist/web3.min.js` をincludeしてください。
これで、windowオブジェクトに `Web3` が公開されます。

または、jsDelivr CDN経由で:

```html
<script src="https://cdn.jsdelivr.net/npm/web3@latest/dist/web3.min.js"></script>
```

UNPKG:

```html
<script src="https://unpkg.com/web3@latest/dist/web3.min.js"></script>
```

## Usage

```js
// In Node.js
const Web3 = require('web3');
const web3 = new Web3('ws://localhost:8546');
console.log(web3);
// Output
{
    eth: ... ,
    shh: ... ,
    utils: ...,
    ...
}
```

さらに、`web3.setProvider()` を使ってプロバイダを設定することができます (例: WebsocketProvider)。

```js
web3.setProvider('ws://localhost:8546');
// or
web3.setProvider(new Web3.providers.WebsocketProvider('ws://localhost:8546'));
```

There you go, now you can use it:

```js
web3.eth.getAccounts().then(console.log);
```

### Usage with TypeScript

私たちは、レポ自体の中のタイプをサポートしています。もし、間違った型を見つけた場合は、こちらでissueを開いてください。

以下のように `web3.js` を使用します:

```typescript
import Web3 from 'web3';
import { BlockHeader, Block } from 'web3-eth' // ex. package types
const web3 = new Web3('ws://localhost:8546');
```

Nodeアプリのように `commonjs` モジュールで型を使用する場合は、 `tsconfig` で `esModuleInterop` と `allowSyntheticDefaultImports` を有効にして、型システムの互換性を確保する必要があります:

```js
"compilerOptions": {
    "allowSyntheticDefaultImports": true,
    "esModuleInterop": true,
    ....
```

## Troubleshooting and known issues.

### Web3 and Create-react-app

create-react-app のバージョン >=5 を使用している場合、ビルドに問題が発生する可能性があります。これは、NodeJS のポリフィルが最新版の create-react-app に含まれていないためです。

### Solution


- react-app-rewiredと不足しているモジュールのインストール:

yarnを使用している場合:
```bash
yarn add --dev react-app-rewired process crypto-browserify stream-browserify assert stream-http https-browserify os-browserify url buffer
```

npmを使用している場合:
```bash
npm install --save-dev react-app-rewired crypto-browserify stream-browserify assert stream-http https-browserify os-browserify url buffer process
```

- プロジェクトフォルダのrootに `config-overrides.js` を作成し、内容を記述します。

```javascript
const webpack = require('webpack');

module.exports = function override(config) {
    const fallback = config.resolve.fallback || {};
    Object.assign(fallback, {
        "crypto": require.resolve("crypto-browserify"),
        "stream": require.resolve("stream-browserify"),
        "assert": require.resolve("assert"),
        "http": require.resolve("stream-http"),
        "https": require.resolve("https-browserify"),
        "os": require.resolve("os-browserify"),
        "url": require.resolve("url")
    })
    config.resolve.fallback = fallback;
    config.plugins = (config.plugins || []).concat([
        new webpack.ProvidePlugin({
            process: 'process/browser',
            Buffer: ['buffer', 'Buffer']
        })
    ])
    return config;
}
```

-  `package.json` の中で、start, build, testのscriptsフィールドを変更します。`react-scripts` の代わりに `react-app-rewired` に置き換えてください。

before: 
```typescript
"scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
},
```

after:
```typescript
"scripts": {
    "start": "react-app-rewired start",
    "build": "react-app-rewired build",
    "test": "react-app-rewired test",
    "eject": "react-scripts eject"
},
```

Nodejs に不足しているポリフィルが含まれ、web3 でアプリが動作するようになりました。
- コンソールで作成された警告を非表示にしたい場合。

`config-overrides.js` の `override` 関数内に、以下を追加してください:

```javascript
config.ignoreWarnings = [/Failed to parse source map/];
```

### Web3 and Angular

### New solution

Angularのバージョン>11を使用していてビルドに問題が発生した場合、以下の古い解決策は機能しません。これは、ポリフィルが最新バージョンのAngularに含まれていないためです。

- 必要な依存関係をAngularプロジェクトにインストールします:

```bash
npm install --save-dev crypto-browserify stream-browserify assert stream-http https-browserify os-browserify
```

- Webpack が正しい依存関係を取得できるように、`tsconfig.json` 内の `compilerOptions` に、以下の `paths` を追加します。

```typescript
{
    "compilerOptions": {
        "paths" : {
        "crypto": ["./node_modules/crypto-browserify"],
        "stream": ["./node_modules/stream-browserify"],
        "assert": ["./node_modules/assert"],
        "http": ["./node_modules/stream-http"],
        "https": ["./node_modules/https-browserify"],
        "os": ["./node_modules/os-browserify"],
    }
}
```

- `polyfills.ts` ファイルに以下の行を追加します:

```typescript
import { Buffer } from 'buffer';

(window as any).global = window;
global.Buffer = Buffer;
global.process = {
    env: { DEBUG: undefined },
    version: '',
    nextTick: require('next-tick')
} as any;
```

### Old solution

Ionic/Angular のバージョンが >5 の場合、`crypto` と `stream` モジュールが `undefined` というビルドエラーに遭遇することがあります。

回避策としては、node-modules に移動して `/angular-cli-files/models/webpack-configs/browser.js` で `node: false` を `node: false` に変更します。{crypto: true, stream: true}` に変更してください。（https://github.com/ethereum/web3.js/issues/2260#issuecomment-458519127）

この問題の別のバリエーションは、[issue oped on angular-cli](https://github.com/angular/angular-cli/issues/1548) にありました。

## Documentation

ドキュメントは、[ReadTheDocs][docs]で見ることができます。

## Building

### Requirements

-   [Node.js](https://nodejs.org)
-   [npm](https://www.npmjs.com/)

```bash
sudo apt-get update
sudo apt-get install nodejs
sudo apt-get install npm
```

### Building (webpack)

web3.js packageをビルドします:

```bash
npm run build
```

### Testing (mocha)

```bash
npm test
```

### Contributing

[Contribution Guidelines](./CONTRIBUTIONS.md)と[Review Guidelines](./REVIEW.md)を遵守してください。

このプロジェクトは[Release Guidelines](./REVIEW.md) を遵守しています。

### Community

-   [Discord][discord-url]
-   [StackExchange][stackexchange-url]

### Similar libraries in other languages

-   Haskell: [hs-web3](https://github.com/airalab/hs-web3)
-   Java: [web3j](https://github.com/web3j/web3j)
-   PHP: [web3.php](https://github.com/web3p/web3.php)
-   Purescript: [purescript-web3](https://github.com/f-o-a-m/purescript-web3)
-   Python: [Web3.py](https://github.com/ethereum/web3.py)
-   Ruby: [ethereum.rb](https://github.com/EthWorks/ethereum.rb)
-   Scala: [web3j-scala](https://github.com/mslinn/web3j-scala)

[repo]: https://github.com/ethereum/web3.js
[docs]: http://web3js.readthedocs.io/
[npm-image-version]: https://img.shields.io/npm/v/web3.svg
[npm-image-downloads]: https://img.shields.io/npm/dm/web3.svg
[npm-url]: https://npmjs.org/package/web3
[actions-image]: https://github.com/ethereum/web3.js/workflows/Build/badge.svg
[actions-url]: https://github.com/ethereum/web3.js/actions
[deps-dev-image]: https://david-dm.org/ethereum/web3.js/1.x/dev-status.svg
[deps-dev-url]: https://david-dm.org/ethereum/web3.js/1.x?type=dev
[dep-dev-image]: https://david-dm.org/ethereum/web3.js/dev-status.svg
[dep-dev-url]: https://david-dm.org/ethereum/web3.js#info=devDependencies
[coveralls-image]: https://coveralls.io/repos/ethereum/web3.js/badge.svg?branch=1.x
[coveralls-url]: https://coveralls.io/r/ethereum/web3.js?branch=1.x
[waffle-image]: https://badge.waffle.io/ethereum/web3.js.svg?label=ready&title=Ready
[waffle-url]: https://waffle.io/ethereum/web3.js
[discord-image]: https://img.shields.io/discord/593655374469660673?label=Discord&logo=discord&style=flat
[discord-url]:  https://discord.gg/pb3U4zE8ca
[lerna-image]: https://img.shields.io/badge/maintained%20with-lerna-cc00ff.svg
[lerna-url]: https://lerna.js.org/
[netlify-image]: https://api.netlify.com/api/v1/badges/1fc64933-d170-4939-8bdb-508ecd205519/deploy-status
[netlify-url]: https://app.netlify.com/sites/web3-staging/deploys
[stackexchange-image]: https://img.shields.io/badge/web3js-stackexchange-brightgreen
[stackexchange-url]: https://ethereum.stackexchange.com/questions/tagged/web3js
[gitpoap-image]: https://public-api.gitpoap.io/v1/repo/ChainSafe/web3.js/badge
[gitpoap-url]: https://www.gitpoap.io/gh/ChainSafe/web3.js

## Semantic versioning

このプロジェクトは [semver](https://semver.org/) を **バージョン1.3.0以降**に可能な限り忠実に再現しています。それ以前のminor version bumps[might](https://github.com/ethereum/web3.js/issues/3758)は、壊れるような動作の変更を含んでいます。

# [What is Web3.js - An Introduction Into the Web3.js Libraries](https://web3.hashnode.com/what-is-web3js-an-introduction-into-the-web3js-libraries)

web3.jsについては、多くの誇大広告がなされています。

この記事では、web3.js と ethers.js という技術が何であるか、そしてそれらがどのように Ethereum ブロックチェーンと対話するために使用されるかを学びます。

また、Ethereumブロックチェーンと対話するための主要なJavaScriptライブラリであるweb3.jsライブラリの使用開始方法についても学びます。

## Overview of the article

1. web3.jsとは？
2. web3.jsとethers.jsの比較。
3. web3でJavaScriptコードを実行する方法。
4. web3.jsは何に使われるのか？

早速ですが、web3.jsの世界に飛び込んでみましょう。web3.jsの意味と、スマートコントラクトプログラムへの実装方法を徹底的に理解しましょう。

## What is Web3.js?
[Web3.js](https://web3js.readthedocs.io/en/v1.7.5/)は、HTTP、IPC、またはWebSocketを使用してローカルまたはリモートのイーサリアムノードと対話することを可能にするライブラリの集合体です。

Web3.jsを使用すると、ブロックチェーンと対話するWebサイトやクライアントを開発することができます。例えば、あるアカウントから別のアカウントにイーサを送信したり、スマートコントラクトからデータを読み書きしたり、スマートコントラクトを作成したり、その他いろいろなことができます

以下のドキュメントでは、web3.js の[インストールと実行](https://web3js.readthedocs.io/en/v1.7.5/getting-started.html)、および例題を含む API リファレンスドキュメントを案内します。

イーサリアムでブロックチェーンアプリケーションを開発するには、いくつかの異なる側面があります:

- スマートコントラクトの開発 - プログラミング言語「Solidity」でブロックチェーンにデプロイされるコードを書く。

- ブロックチェーンと相互作用するウェブサイトやクライアントの開発 - スマートコントラクトでブロックチェーンからデータを読み書きするコードを記述する。

Web 開発の経験がある人なら、jQuery を使って Web サーバーに Ajax 呼び出しを行ったことがあるかもしれません。それは、web3.jsの機能を理解する良い出発点です。jQueryを使ってウェブサーバーからデータを読み書きする代わりに、web3.jsを使ってイーサリアムブロックチェーンを読み書きすることができます。

以下は、web3.jsがEthereumブロックチェーンとどのように相互作用するかを説明するための図です。

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1645435242538/zzhO2r-VI.png?auto=compress,format&format=webp)

## Web3.js vs ethers.js

web3.jsとethers.jsはどちらもEthereum JavaScript Librariesです。

Ether.jsはRick Moore氏（カナダ人開発者）によって開発・保守されています。

web3.jsはEthereum Foundationによって開発・保守されています。そのため、より多くの開発者がweb3.jsを支持しており、より広い範囲でサポートされています。

ethers.jsとweb3.jsの大きな違いは、鍵の管理とイーサリアムのブロックチェーンとのやりとりをどのように扱うかという点です。

Web3.jsでは、アプリケーションに接続されたローカルノードがあることが前提となっています。そのノードが鍵を保管し、トランザクションに署名し、イーサリアムのブロックチェーンを読み込んで対話することを想定しています。現実には、このようなことはあまりありません。ほとんどのユーザーはローカルでgethを実行していないのです。Metamaskはブラウザアプリケーションを通じてその環境を効果的にエミュレートするため、ほとんどのWeb3アプリは鍵の保持、トランザクションへの署名、イーサリアム[メインネット](https://web3.hashnode.com/glossary/what-is-mainnet)との対話にMetamaskを必要とします。

一方、[Ethers.js](https://docs.ethers.io/v5/)は異なるアプローチをとっており、開発者により柔軟性をもたらすと私たちは考えています。Ethers.jsでは、「ノード」を2つの役割に分離しています。

- 鍵を保持し、取引に署名する「ウォレット」と
- イーサリアムネットワークへの匿名接続として、状態の確認やトランザクションの送信を行う「プロバイダー」。

ethers.jsの利点として思い浮かぶのは、主に以下の2点です。

1. ENS名はfirst-class citizensである。
2. 鍵管理と状態 - 懸念事項の分離。

## How to run JavaScript code in Web3.js

web3.jsでJavascriptのコードを実行するには、web3.jsをプロジェクトに取り込む必要があります。これは、以下の方法で行うことができます。

### 依存関係
web3.jsを使った開発を始めるにあたり、いくつかの依存関係があります。

### Node パッケージマネージャ (NPM)
最初に必要な依存関係は、Node.jsに付属しているNode Package Manager、またはNPMです。Nodeがすでにインストールされているかどうかを確認するには、ターミナルで次のように入力します。

```js
node -v
```
### Web3.js Library
You can install the Web3.js library with NPM in your terminal like this:

```js
npm install web3
```

Or using Yarn:

```js
yarn add web3
```

### Infura RPC URL
メインネットのJSON RPCでEthereumノードに接続するには、Ethereumノードにアクセスする必要があります。これにはいくつかの方法があります。

1つは、[Geth](https://github.com/ethereum/go-ethereum/wiki/geth)や[Parity](https://www.parity.io/)を使って自分のEthereumノードを動かす方法です。しかし、これにはブロックチェーンから大量のデータをダウンロードし、それを同期させ続ける必要があります。これは、これまで一度も試したことがない場合、大きな頭痛の種になります。

主に利便性のために、[Infura](https://infura.io/)を使えば、自分でEthereumノードを実行しなくても、Ethereumノードにアクセスすることができます。Infuraは、リモートEthereumノードを無料で提供するサービスです。サインアップして、APIキーと接続したいネットワークのRPC URLを取得するだけです。サインアップすると、InfuraのRPC URLは以下のようになります。

```
https://mainnet.infura.io/YOUR_INFURA_API_KEY
```
## What is web3.js used for?

Web3.jsは、フロントエンドとバックエンドで、口座残高の確認、ブロックチェーンからのデータの読み取り、取引、さらにはスマートコントラクトの導入に利用できます。

### 1. web3.jsで口座残高を確認する
依存関係がすべてインストールされたので、web3.jsで口座残高をチェックする方法を説明します。まず、ターミナルでNodeコンソールをこのように起動します。

```js
node
```

Now you've got the Node console open! Inside the Node console, you can require web3.js like this:

```js
const Web3 = require('web3');
```
これで、新しい web3 接続を作成するための変数にアクセスできるようになりました。web3接続を生成する前に、まずInfuraのURLをこのように変数に代入する必要があります。

```js
const rpcURL = "https://mainnet.infura.io/YOUR_INFURA_API_KEY";
```

`YOUR_INFURA_API_KEY` は、先ほど取得した実際の Infura API キーに置き換えてください。これで、以下のように Web3 接続のインスタンスを作成できます。

```js
const web3 = new Web3(rpcURL);
```

これで、イーサリアムのメインネットに接続するためのライブのWeb3接続ができました。この接続を使って、この口座の残高を確認してみましょう。`0x105cb19ba40384a8f2985816DA7883b076969cA7`. `web3.eth.getBalance()` で残高を確認することで、この口座がどれだけのEtherを保有しているかが分かります。

まず最初に、アドレスを変数に代入してみましょう。

```js
const address = "0x105cb19ba40384a8f2985816DA7883b076969cA7";
```

Let's now check the account balance like this:

```js
 web3.eth.getBalance(address, (err, wei) => {
  balance = web3.utils.fromWei(wei, 'ether')
})
```

で、終了です。web3.jsで口座の残高を確認する方法です。

このチュートリアルで書いたコードをまとめると、以下のようになります。

```js
const Web3 = require('web3')
const rpcURL = '' // Your RPC URL goes here
const web3 = new Web3(rpcURL)
const address = '' // Your account address goes here
web3.eth.getBalance(address, (err, wei) => {
  balance = web3.utils.fromWei(wei, 'ether')
});
```
まず、`web3.eth.getBalance()`を呼び出して残高を確認します。この関数は、`error`と`balance`の2つの引数でコールバック関数を受け取ります。`errors`引数はとりあえず無視し、`wei`引数で残高を参照することにします。イーサリアムでは残高をweiで表します。weiはイーサーの最小単位で、小さな1円玉のようなものです。`web3.utils.fromWei(wei, 'ether');`で、この残高をetherに変換することができます。

### 2. Read data from the smart contract with web3.js

ここでは、Ethereumブロックチェーンからスマートコントラクトのデータを読み取る方法について簡単に説明します。

web3.jsでスマートコントラクトからデータを読み取るには、2つのものが必要です。

1. 対話したいスマートコントラクトのJavaScript表現。
2. データを読み込む際に、スマートコントラクト上の関数を呼び出す方法。

`web3.eth.Contract()` 関数で、EthereumスマートコントラクトのJavaScript表現を取得することができます。

この関数には2つの引数が必要です。1つはスマートコントラクトのABI、もう1つはスマートコントラクトのアドレスです。

スマートコントラクトのABIは「Abstract Binary Interface」の略で、特定のスマートコントラクトがどのように機能するかを記述したJSON配列です。

以下はABIの例です。

```js
const abi = [{"constant":true,"inputs":[],"name":"mintingFinished","outputs":[{"name":"","type":"bool"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"name","outputs":[{"name":"","type":"string"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_spender","type":"address"},{"name":"_value","type":"uint256"}],"name":"approve","outputs":[],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"totalSupply","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_from","type":"address"},{"name":"_to","type":"address"},{"name":"_value","type":"uint256"}],"name":"transferFrom","outputs":[],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"decimals","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function"},{"constant":false,"inputs":[],"name":"unpause","outputs":[{"name":"","type":"bool"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_to","type":"address"},{"name":"_amount","type":"uint256"}],"name":"mint","outputs":[{"name":"","type":"bool"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"paused","outputs":[{"name":"","type":"bool"}],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"_owner","type":"address"}],"name":"balanceOf","outputs":[{"name":"balance","type":"uint256"}],"payable":false,"type":"function"},{"constant":false,"inputs":[],"name":"finishMinting","outputs":[{"name":"","type":"bool"}],"payable":false,"type":"function"},{"constant":false,"inputs":[],"name":"pause","outputs":[{"name":"","type":"bool"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"owner","outputs":[{"name":"","type":"address"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"symbol","outputs":[{"name":"","type":"string"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_to","type":"address"},{"name":"_value","type":"uint256"}],"name":"transfer","outputs":[],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_to","type":"address"},{"name":"_amount","type":"uint256"},{"name":"_releaseTime","type":"uint256"}],"name":"mintTimelocked","outputs":[{"name":"","type":"address"}],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"_owner","type":"address"},{"name":"_spender","type":"address"}],"name":"allowance","outputs":[{"name":"remaining","type":"uint256"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"newOwner","type":"address"}],"name":"transferOwnership","outputs":[],"payable":false,"type":"function"},{"anonymous":false,"inputs":[{"indexed":true,"name":"to","type":"address"},{"indexed":false,"name":"value","type":"uint256"}],"name":"Mint","type":"event"},{"anonymous":false,"inputs":[],"name":"MintFinished","type":"event"},{"anonymous":false,"inputs":[],"name":"Pause","type":"event"},{"anonymous":false,"inputs":[],"name":"Unpause","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"owner","type":"address"},{"indexed":true,"name":"spender","type":"address"},{"indexed":false,"name":"value","type":"uint256"}],"name":"Approval","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"from","type":"address"},{"indexed":true,"name":"to","type":"address"},{"indexed":false,"name":"value","type":"uint256"}],"name":"Transfer","type":"event"}]
```

本当に長く、途切れることのない配列に見えると思います。圧倒されているように見えるかもしれませんが、心配しないでください。この例はOmiseGoトークンのABIで、ERC-20トークン規格を実装しています。このトークンのABIやアドレスなどの詳細は、[Etherscan](https://etherscan.io/address/0xd26114cd6EE289AccF82350c8d8487fedB8A0C07)で確認することができます。残りの例では、このスマートコントラクトのABIを使用することにします。

ここにいる間に、EthereumメインネットからOMGトークンへのアドレスを保存してきます。

```js
const address = "0xd26114cd6EE289AccF82350c8d8487fedB8A0C07";
```

この2つの値が割り当てられたので、次のようにOMGトークンスマートコントラクトの完全なJavaScript表現を作成することができます。

```js
const contract = new web3.eth.Contract(abi, address);
```

以上で、web3.jsでスマートコントラクトからデータを読み取ることが簡単にできるようになりました。ここまでで、web3.jsを使ってスマートコントラクトから口座残高を確認できるようになりました。今度は、スマートコントラクトの関数を呼び出して、スマートコントラクトからデータを読み取る必要があります。スマートコントラクトの関数はすべて、割り当てられたweb3コントラクト内の`contract.methods`名前空間の下にリストアップされています。例えば、コントラクトが`myFunction()`を実装していれば、`contract.methods.myFunction()`を呼び出すことができます。

素晴らしい! つまり、理論的にはスマートコントラクトが実装しているあらゆる関数を呼び出すことができます。しかし、どの関数を実装しているかを知るにはどうしたらよいでしょうか？一つは、コンソールに`contract.methods`を記録して、何が返されるかを見ることができます。しかし、このスマートコントラクトはERC-20標準を実装しているので、`totalSupply()`, `name()`, `symbol()`, `balanceOf()`などのいくつかの関数を実装していることが分かります。

それらの値をそれぞれ個別に確認すると、こんな感じです。

まず、現存するすべての OMG トークンの総供給量です。

```js
contract.methods.totalSupply().call((err, result) => { console.log(result) });
// > 140245398
```

Second, the name of the OMG token:

```js
contract.methods.name().call((err, result) => { console.log(result) });
// > OMG Token
```

最後に、指定した口座の残高を確認します。EtherscanでOMGホルダーを探したところ、このアドレス `0xd26114cd6EE289AccF82350c8d8487fedB8A0C07` が見つかりました。

このアカウントの残高を確認すると、こんな感じです。

```js
contract.methods.balanceOf('0xd26114cd6EE289AccF82350c8d8487fedB8A0C07').call((err, result) => { console.log(result) });
// > Some large number...
```

で、終了です。web3.jsでスマートコントラクトからデータを読み取る方法は以上です。

このセクションの全コードをまとめると、以下のようになります。

```js
const Web3 = require('web3');
const rpcURL = '' // Your RCP URL goes here const web3 = new Web3(rpcURL)
const web3 = new Web3(rpcURL);
const abi = [{"constant":true,"inputs":[],"name":"mintingFinished","outputs":[{"name":"","type":"bool"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"name","outputs":[{"name":"","type":"string"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_spender","type":"address"},{"name":"_value","type":"uint256"}],"name":"approve","outputs":[],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"totalSupply","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_from","type":"address"},{"name":"_to","type":"address"},{"name":"_value","type":"uint256"}],"name":"transferFrom","outputs":[],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"decimals","outputs":[{"name":"","type":"uint256"}],"payable":false,"type":"function"},{"constant":false,"inputs":[],"name":"unpause","outputs":[{"name":"","type":"bool"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_to","type":"address"},{"name":"_amount","type":"uint256"}],"name":"mint","outputs":[{"name":"","type":"bool"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"paused","outputs":[{"name":"","type":"bool"}],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"_owner","type":"address"}],"name":"balanceOf","outputs":[{"name":"balance","type":"uint256"}],"payable":false,"type":"function"},{"constant":false,"inputs":[],"name":"finishMinting","outputs":[{"name":"","type":"bool"}],"payable":false,"type":"function"},{"constant":false,"inputs":[],"name":"pause","outputs":[{"name":"","type":"bool"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"owner","outputs":[{"name":"","type":"address"}],"payable":false,"type":"function"},{"constant":true,"inputs":[],"name":"symbol","outputs":[{"name":"","type":"string"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_to","type":"address"},{"name":"_value","type":"uint256"}],"name":"transfer","outputs":[],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"_to","type":"address"},{"name":"_amount","type":"uint256"},{"name":"_releaseTime","type":"uint256"}],"name":"mintTimelocked","outputs":[{"name":"","type":"address"}],"payable":false,"type":"function"},{"constant":true,"inputs":[{"name":"_owner","type":"address"},{"name":"_spender","type":"address"}],"name":"allowance","outputs":[{"name":"remaining","type":"uint256"}],"payable":false,"type":"function"},{"constant":false,"inputs":[{"name":"newOwner","type":"address"}],"name":"transferOwnership","outputs":[],"payable":false,"type":"function"},{"anonymous":false,"inputs":[{"indexed":true,"name":"to","type":"address"},{"indexed":false,"name":"value","type":"uint256"}],"name":"Mint","type":"event"},{"anonymous":false,"inputs":[],"name":"MintFinished","type":"event"},{"anonymous":false,"inputs":[],"name":"Pause","type":"event"},{"anonymous":false,"inputs":[],"name":"Unpause","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"owner","type":"address"},{"indexed":true,"name":"spender","type":"address"},{"indexed":false,"name":"value","type":"uint256"}],"name":"Approval","type":"event"},{"anonymous":false,"inputs":[{"indexed":true,"name":"from","type":"address"},{"indexed":true,"name":"to","type":"address"},{"indexed":false,"name":"value","type":"uint256"}],"name":"Transfer","type":"event"}]
const address = '0xd26114cd6EE289AccF82350c8d8487fedB8A0C07' ;
const contract = new web3.eth.Contract(abi, address); 
contract.methods.totalSupply().call((err, result) => { console.log(result) }); 
contract.methods.name().call((err, result) => { console.log(result) }); 
contract.methods.symbol().call((err, result) => { console.log(result) });
contract.methods.balanceOf('0xd26114cd6EE289AccF82350c8d8487fedB8A0C07').call((err, result) =>
{ console.log(result) }); // > Some large number...
```

### 3. Create an Ethereum transaction with web3.js

ここでは、web3.jsを使用してEthereumブロックチェーン上でトランザクションを作成する方法を紹介します。Ethereumのトランザクションが作成されると何が起こるのか、そしてweb3.jsを使用してネットワークに手動でトランザクションをブロードキャストする方法について説明します。

web3.jsの学習に加え、この記事の目的は、イーサリアムブロックチェーン上でのトランザクションの仕組みの基本を理解してもらうことです。トランザクションを作成するときはいつも、ブロックチェーンにデータを書き込み、その状態を更新していることになります。これを行うには、あるアカウントから別のアカウントにエーテルを送る、データを書き込むスマートコントラクト関数を呼び出す、ブロックチェーンにスマートコントラクトをデプロイするなど、いくつかの方法があります。web3.jsライブラリでこれらのアクションを実行し、各ステップがどのように動作するかを観察することで、これらの概念についてより深く理解することができます。

ネットワークにトランザクションをブロードキャストするためには、まずトランザクションに署名する必要があります。このために[ethereumjs-tx](https://github.com/ethereumjs/ethereumjs-tx)と呼ばれる追加のJavaScriptライブラリを使用するつもりです。この依存関係は、以下のようにコマンドラインからインストールすることができます。

```js
 npm install ethereumjs-tx
```

このライブラリを使用する理由は、すべてのトランザクションをローカルで署名したいからです。もしローカルで自分のEthereumノードを動かしていたら、ローカルに保存されているアカウントのロックを解除して、すべてのトランザクションをローカルで署名することができるはずです。そうであれば、必ずしもこのライブラリを使用する必要はないでしょう。しかし、このチュートリアルでは、Infuraがホストするリモートノードを使用しています。Infuraは信頼できるサービスですが、リモートノードに秘密鍵を管理させるよりも、ローカルでトランザクションに署名したいのです。

この記事で行うのはまさにこれです。生のトランザクションを作成し、それに署名し、そしてトランザクションを送信してネットワークにブロードキャストする。

まず、このレッスンのコードを実行するために、コンソールですべてを行うのではなく、簡単な`index.js`ファイルを作成することから始めましょう。

`index.js`ファイルの内部では、まずこのように新しくインストールしたライブラリを必要とします。

```js
const Tx = require('ethereumjs-tx')
```

const Tx = require('ethereumjs-tx')

```js
const Web3 = require('web3')
const web3 = new Web3('https://ropsten.infura.io/YOUR_INFURA_API_KEY')
```

前節で使用したEthereumメインネットとは異なるRopstenテストネットワークを使用していることに注意してください。テストネットワークを使用するのは、すべての取引にetherというガスがかかるからです。Ropstenテストネットでは、お金を使う心配なく偽物のetherを使用することができます。Ropstenテストネットワーク上のfaucet、または[Metamask faucet](https://faucet.metamask.io/)から偽のetherを入手することができます。

これから、あるアカウントから別のアカウントに偽のetherを送るトランザクションを作成します。これを行うには、2つのアカウントとその秘密鍵が必要です。

実際にweb3.jsで新しいアカウントを作成するには、このようにします。

```js
web3.eth.accounts.create()
// > {
//    address: "0xb8CE9ab6943e0eCED004cDe8e3bBed6568B2Fa01",
//    privateKey: "0x348ce564d427a3311b6536bbcff9390d69395b06ed6c486954e971d960fe8709",
//    signTransaction: function(tx){...},
//    sign: function(data){...},
//    encrypt: function(password){...}
// };
```

この2つのアカウントを作成したら、faucetから偽のetherを投入してください。さて、彼らの公開鍵をスクリプトの変数に次のように代入します。

```js
const account1 = '0xb8CE9ab6943e0eCED004cDe8e3bBed6568B2Fa01';
const account2 = '0xb8CE9ab6943e0eCED004cDe8e3bBed6568B2Fa02';
```

注意：このアカウントはこのレッスンでは使えませんので、必ず生成したアカウントを使用してください。では、秘密鍵をこのように環境に保存してみましょう。

```js
const privateKey1 = Buffer.from(process.env.PRIVATE_KEY_1); 
const privateKey1 = Buffer.from(process.env.PRIVATE_KEY_2);
```

これで、すべての変数の設定が完了しました。この時点では、少し混乱するかもしれません。しかし、すぐに理解できるようになります。

ここからは、いくつかやっておきたいことがあります。

1. トランザクション・オブジェクトを作成する。
2. トランザクションに署名する。
3. トランザクションをネットワークにブロードキャストする。

トランザクションオブジェクトはこのように作ることができる。

```js
const txObject = {
    nonce:    web3.utils.toHex(txCount),
    to:       account2,
    value:    web3.utils.toHex(web3.utils.toWei('0.1', 'ether')),
    gasLimit: web3.utils.toHex(21000),
    gasPrice: web3.utils.toHex(web3.utils.toWei('10', 'gwei'))
  };
```

このコードでは、`nonce`、`to`、`value`、`gasLimit`、`gasPrice`など、トランザクションを生成するために必要なすべての値を持つオブジェクトを構築しています。

これらの値をそれぞれ分解してみましょう。

- `nonce` - これは、指定されたアカウントの以前の取引回数です。この変数の値は、すぐに割り当てます。また、この値を16進数に変換する必要があります。web3.jsのユーティリティであるweb3.utils.toHex()でこれを行うことができます。

- `to` - エーテルを送信するアカウントです。

- `value` - 送りたいエーテルの量。この値はweiで表され、16進数に変換されなければなりません。web3.jsのユーティリティ `web3.utils.toWei() `で値をweiに変換することができます。

- `gasLimit` - これは、トランザクションによって消費されるガスの最大量です。このような基本的なトランザクションでは、常に21000ユニットのガスが消費されるので、ここではその値を使用することにします。

-`gasPrice` - これはガス1単位あたりの支払い金額です。ここでは10Gweiとします。

このトランザクションオブジェクトにはフォームフィールドがないことに注意してください。`account1's`秘密鍵でこの取引に署名するたびに、それが推測されます。

さて、nonce変数に値を代入しましょう。トランザクション`nonce`は`web3.eth.getTransactionCount()`関数で取得することができます。このように、すべてのコードをコールバック関数内にラップします。

```js
web3.eth.getTransactionCount(account1, (err, txCount) => {
  const txObject = {
    nonce:    web3.utils.toHex(txCount),
    to:       account2,
    value:    web3.utils.toHex(web3.utils.toWei('0.1', 'ether')),
    gasLimit: web3.utils.toHex(21000),
    gasPrice: web3.utils.toHex(web3.utils.toWei('10', 'gwei'))
  }
})
```

このように、トランザクションオブジェクトの構築は完了しました。では、トランザクションに`sign`してみましょう。次のようにします。

```js
const tx = new Tx(txObject)
tx.sign(privateKey1)

const serializedTx = tx.serialize()
const raw = '0x' + serializedTx.toString('hex')
```

ここでは、`etheremjs-tx` ライブラリを使用して、新しい `Tx object` を作成しました。また、このライブラリを使用して、`privateKey1` でトランザクションに署名しています。最後に、`web3.eth.sendSignedTransaction()`関数を用いて、この署名付きシリアライズトランザクションをテストネットワークに以下のように送信しています。

```js
web3.eth.sendSignedTransaction(raw, (err, txHash) => {
  console.log('txHash:', txHash)
});
```

これは、このレッスンの最後のステップで、トランザクションを送信し、ネットワークにブロードキャストするものです。この時点で、完成した`index.js`ファイルは次のようになっているはずです。

```js
var Tx     = require('ethereumjs-tx')
const Web3 = require('web3')
const web3 = new Web3('https://ropsten.infura.io/YOUR_INFURA_API_KEY')

const account1 = '' // Your account address 1
const account2 = '' // Your account address 2

const privateKey1 = Buffer.from('YOUR_PRIVATE_KEY_1', 'hex')
const privateKey2 = Buffer.from('YOUR_PRIVATE_KEY_2', 'hex')

web3.eth.getTransactionCount(account1, (err, txCount) => {
  // Build the transaction
  const txObject = {
    nonce:    web3.utils.toHex(txCount),
    to:       account2,
    value:    web3.utils.toHex(web3.utils.toWei('0.1', 'ether')),
    gasLimit: web3.utils.toHex(21000),
    gasPrice: web3.utils.toHex(web3.utils.toWei('10', 'gwei'))
  }

  // Sign the transaction
  const tx = new Tx(txObject)
  tx.sign(privateKey1)

  const serializedTx = tx.serialize()
  const raw = '0x' + serializedTx.toString('hex')

  // Broadcast the transaction
  web3.eth.sendSignedTransaction(raw, (err, txHash) => {
    console.log('txHash:', txHash)
    // Now go check etherscan to see the transaction!
  })
});
```

You can then run the index.js file from your terminal with NodeJS like this:

```js
node index.js
```

Or SImply run:

```js
node index
```

## Web3.js Utilities

web3.jsには、あなたが知らないようなクールなヒントやトリックがいくつかあります。さっそく`index.js`をセットアップして、これらのTipsを見に行きましょう。このようにイーサリアムメインネットに接続してみましょう。

```js
const Web3 = require('web3')
const web3 = new Web3('https://mainnet.infura.io/YOUR_INFURA_API_KEY')
```

まず、実際にこのようなネットワークで、現在の平均的なガス料金を知ることができます。

```js
web3.eth.getGasPrice().then((result) => {
  console.log(web3.utils.fromWei(result, 'ether')
});
```

ブロックチェーンで開発したことがあるとすると、ハッシュ関数を扱ったことがあるのではないでしょうか。Web3.jsには、ハッシュ関数を利用するためのヘルパーがたくさん組み込まれています。

このように`sha3`関数に直接アクセスすることができます。

```js
console.log(web3.utils.sha3('Hashnode blog'));
```

Or as `keccack256` :

```js
console.log(web3.utils.keccak256('Hashnode blog'));
```

また、以下のように32-byte random hexを生成することで、（疑似）ランダム性を扱うことができます。

```js
console.log(web3.utils.randomHex(32));
```

いずれにせよ、JavaScriptの配列やオブジェクトに対してアクションを実行しようとして、外部ライブラリの助けが必要になったことはありませんか？ありがたいことに、web3.jsにはunderscoreJSというライブラリが同梱されています。

```js
const _ = web3.utils._
_.each({ key1: 'value1', key2: 'value2' }, (value, key) => {
  console.log(key)
});
```

以上です。web3.jsで使えるおしゃれなTipsとトリックを紹介しました。このレッスンの完全なチュートリアルコードはこちらです。

```js
const Web3 = require('web3')
const web3 = new Web3('https://mainnet.infura.io/YOUR_INFURA_API_KEY')

// Get average gas price in wei from last few blocks median gas price
web3.eth.getGasPrice().then((result) => {
  console.log(web3.utils.fromWei(result, 'ether')
})

// Use sha256 Hashing function
console.log(web3.utils.sha3('Hashnode blog'))

// Use keccak256 Hashing function (alias)
console.log(web3.utils.keccak256('Dapp University'))

// Get a Random Hex
console.log(web3.utils.randomHex(32))

// Get access to the underscore JS library
const _ = web3.utils._

_.each({ key1: 'value1', key2: 'value2' }, (value, key) => {
  console.log(key)
});
```


```js
node index.js
```

## Conclusion

今回は、web3.jsのライブラリがどのようなものかを学びました。web3.jsとethers.jsについて、その違いと用途を紹介しました。

また、web3.js を使って口座残高を確認する方法、スマートコントラクトからデータを読み取る方法、そして web3.js を使って Ethereum トランザクションを作成する方法について学びました。

また、web3.jsのTipsやTricksについても簡単に紹介しました。

NFT、dApps、ブロックチェーン、その他のweb3コンテンツについてもっと知りたい方は、[Hashnode’s web3 blog](https://web3.hashnode.com/)をチェックしてみてください。





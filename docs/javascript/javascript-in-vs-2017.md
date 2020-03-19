---
title: JavaScript
ms.date: 01/15/2019
ms.technology: vs-javascript
ms.topic: conceptual
dev_langs:
- JavaScript
- TypeScript
- DHTML
ms.assetid: 74dca14c-5071-416f-a92b-d09f95e3dfb8
caps.latest.revision: 1
author: bowdenk7
ms.author: wilkelly
manager: jillfra
ms.openlocfilehash: 2a0d3657843dcf282e5c9aab8609efe5f9611965
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "78234957"
---
# <a name="javascript-in-visual-studio-2017"></a>Visual Studio 2017 の JavaScript

JavaScript は Visual Studio の第一級の言語です。 Visual Studio IDE で JavaScript コードを記述する場合に、ほとんどの標準的な編集補助機能 (コード スニペット、IntelliSense など) を使用できます。 多くの種類のアプリケーションやサービスの JavaScript コードを記述できます。

> [!NOTE]
> Microsoft の JavaScript API のすべてのリファレンス (500 超ページ) を docs.microsoft.com から対応する MDN にリダイレクトして、[MDN Web docs](https://developer.mozilla.org/en-US/) を Web のワンストップの主要な開発リソースにするためのコミュニティ全体の取り組みに参加しました。 詳細については、この[お知らせ](https://blogs.windows.com/msedgedev/2018/06/26/chakra-docs-mdn-web-docs/)をご覧ください。

## <a name="ES6"></a> ECMAScript 2015 (ES6) 以降のサポート

現在、Visual Studio では、ECMAScript 2015/2016 など、更新された ECMAScript 言語の構文がサポートされています。

### <a name="what-is-ecmascript-2015"></a>ECMAScript 2015 とは

JavaScript はプログラミング言語としてまだ進化しています。その更新は [TC39](https://www.ecma-international.org/memento/tc39-m.htm) という委員会で行われます。
ECMAScript 2015 は JavaScript 言語を更新したものであり、新しい便利な構文と機能を提供します。 ES6 機能の詳細については、[こちら](http://es6-features.org/#Constants)の参照サイトで確認してください。

ECMAScript 2015 のサポートに加え、Visual Studio では ECMAScript 2016 もサポートされ、今後リリースされるバージョンの ECMAScript のサポートも予定されています。 TC39 および ECMAScript の最新の変更に対応するために、[github](https://github.com/tc39) での作業をフォローしてください。

### <a name="transpile-javascript"></a>JavaScript のトランスパイル

JavaScript の一般的な問題は、最新の ES6 以降の言語機能は生産性の向上に役立つため使用したいが、ランタイム環境 (多くの場合、ブラウザー) で、これらの新機能がまだサポートされていないということです。 これは、どのブラウザーでどの機能がサポートされているかを把握する (これは単調な作業になる場合があります) 必要があるか、ターゲット ランタイムで認識されるバージョン (通常は ES5) に ES6 以降のコードを変換する手段が必要になることを意味します。 コードをランタイムが理解できるバージョンに変換することを一般に "トランスパイル" と呼んでいます。

TypeScript の主な機能の 1 つとして、ES6 以降のコードから ES5 または ES3 へのトランスパイル機能があります。この機能を使用して、生産性を最大化するコードを作成できますが、任意のプラットフォームで従来のコードを引き続き実行できます。 [!include[vs_dev15](../../docs/misc/includes/vs_dev15_md.md)] の JavaScript では TypeScript と同じ言語サービスを使用するため、ES6 以降から ES5 へのトランスパイルも利用できます。

トランスパイルを設定するには、構成オプションについてある程度、事前に理解しておく必要があります。
TypeScript は `tsconfig.json` ファイルを使用して構成します。
このようなファイルがない場合は、一部の既定値が使用されます。
互換性の理由から、JavaScript ファイル (および必要に応じて `.d.ts` ファイル) のみが存在する場合、これらの既定値は異なります。
JavaScript ファイルをコンパイルするには、`tsconfig.json` ファイルを追加する必要があり、これらのオプションの一部を明示的に設定する必要があります。

tsconfig ファイルに必要な設定について、以下に説明します。

- `allowJs`: この値は、JavaScript ファイルが認識されるように `true` に設定する必要があります。 TypeScript は JavaScript にコンパイルされ、コンパイラはコンパイルしたファイルをインクルードする必要がないので、既定値は `false` になります。
- `outDir`: この値は、出力された JavaScript ファイルが検出されず、プロジェクトに追加されるように、プロジェクトに含まれない場所に設定する必要があります (`exclude` を参照)。
- `module`: モジュールを使用する場合、この設定で、出力コードで使用する必要があるモジュール形式 (たとえば、Node、または Browserify などのバンドラーの場合は `commonjs`) をコンパイラに指示します。
- `exclude`: この設定は、プロジェクトに含めないフォルダーを示しています。
出力場所と、`node_modules` や `temp` などのプロジェクト以外のフォルダーをこの設定に追加する必要があります。
- `enableAutoDiscovery`: この設定は、前述のとおり、定義ファイルの自動検出とダウンロードを可能にします。
- `compileOnSave`: この設定で、Visual Studio にソース ファイルが保存されるたびに再コンパイルする必要があるかどうかをコンパイラに指示します。
- `typeAcquisition`: この一連の設定では、自動型取得の動作を制御します ([このセクション](/visualstudio/ide/javascript-intellisense#Auto)で詳しく説明します)。

JavaScript ファイルを CommonJS モジュールに変換し、`./out` フォルダーに配置する場合は、次の `tsconfig.json` ファイルを使用できます。

```json
{
  "compilerOptions": {
    "module": "commonjs",
    "allowJs": true,
    "outDir": "out"
  },
  "exclude": [
    "node_modules",
    "wwwroot",
    "out"
  ],
  "compileOnSave": true,
  "typeAcquisition": {
    "enable": true
  }
}
```

上記のように設定した状態で、ソース ファイル (`./app.js`) が存在し、いくつかの ECMAScript 2015 言語機能が含まれている場合は次のようになります。

```js
import {Subscription} from 'rxjs/Subscription';  // ES6 import

class Foo {  // ES6 Class
    sayHi(name) {
        return `Hi ${name}, welcome to Salsa!`;  // ES6 template string
    }
}

export let sqr = x => x * x;  //ES6 export, let, and arrow function
export default Subscription;  //ES6 default export
```

この場合、ファイルは次のような ECMAScript 5 (既定) を対象とする `./out/app.js` に出力されます。

```js
"use strict";
var Subscription_1 = require('rxjs/Subscription');
var Foo = (function () {
    function Foo() {
    }
    Foo.prototype.sayHi = function (name) {
        return "Hi " + name + ", welcome to Salsa!";
    };
    return Foo;
}());
exports.sqr = function (x) { return x * x; };
Object.defineProperty(exports, "__esModule", { value: true });
exports.default = Subscription_1.Subscription;
```

## <a name="better-intellisense"></a>IntelliSense の向上

[!include[vs_dev15](../../docs/misc/includes/vs_dev15_md.md)] の JavaScript IntelliSense では、パラメーターおよびメンバー リストにさらに多くの情報が表示されるようになります。 この新しい情報は TypeScript 言語サービスで提供されます。この言語サービスでは、コードをよりよく理解するためにバックグラウンドで静的分析が使用されます。 新しい IntelliSense エクスペリエンスとそのしくみの詳細については、[こちら](/visualstudio/ide/javascript-intellisense/)を参照してください。

## <a name="JSX"></a> JSX 構文のサポート

[!include[vs_dev15](../../docs/misc/includes/vs_dev15_md.md)] の JavaScript では、JSX 構文の豊富なサポートが提供されます。 JSX は、JavaScript ファイル内で HTML タグを許可する構文セットです。

次の図は `comps.tsx` TypeScript ファイルに定義されている React コンポーネントを示しています。`app.jsx` ファイルから使用されるこのコンポーネントには、JSX 式に入力し、文書化するために IntelliSense が備わっています。
この具体例にはたまたま TypeScript コードも含まれていますが、TypeScript は必要ありません。

![JSX 構文](../javascript/media/js-react.png)

> [!NOTE]
> JSX 構文を React 呼び出しに変換するには、設定 `"jsx": "react"` を、`compilerOptions` ファイルの `tsconfig.json` に追加する必要があります。

ビルド時に './out/app.js' で作成された JavaScript ファイルには次のようなコードが含まれます。

```js
"use strict";
var comps_1 = require('./comps');
var x = React.createElement(comps_1.RepoDisplay, {description: "test"});
```

## <a name="configure-your-javascript-project"></a>JavaScript プロジェクトの構成

言語サービスでは静的分析が採用されています。これは、IntelliSense の結果を返し、他の編集機能を提供するために、実際にソース コードを実行せずに分析することを意味します。
したがって、プロジェクト コンテキストに含まれるファイルの数量とサイズが大きいほど、分析中に使用されるメモリと CPU が増えます。
そのため、プロジェクト図形については、次のような既定の解釈がいくつかあります。

- `package.json` および `bower.json` では、プロジェクトで使用される依存関係がリストされ、既定で自動型取得 (ATA) に含まれます。
- 最上位レベルの `node_modules` フォルダーにはライブラリ ソース コードが含まれ、そのコンテンツは既定でプロジェクトのコンテキストから除外されます。
- 他のすべての `.js`、`.jsx`、`.ts`、および `.tsx` ファイルは*独自の*ソース ファイルのいずれかである可能性があり、プロジェクト コンテキストに含める必要があります。

ほとんどの場合、プロジェクトを開くだけで、既定のプロジェクト構成で優れたエクスペリエンスが得られます。 ただし、大規模なプロジェクトまたはさまざまなフォルダー構造を持つプロジェクトでは、言語サービスをさらに構成し、独自のソース ファイルにのみ、より的確に焦点を合わせることが望ましい場合があります。

### <a name="override-defaults"></a>既定値をオーバーライド

プロジェクト ルートに `tsconfig.json` ファイルを追加して、既定の構成をオーバーライドすることができます。
`tsconfig.json` には、プロジェクト コンテキストを操作できるいくつかの異なるオプションがあります。
その一部を以下に示します。使用可能なすべてのオプションについては、[スキーマ ストア](http://json.schemastore.org/tsconfig)を参照してください。

## <a name="important-tsconfigjson-options"></a>重要な `tsconfig.json` のオプション

```json
{
  "compilerOptions": {
    "allowJs": true,          // include .js and .jsx in project context (defaults to only .ts and .tsx)
    "noEmit": true            // turns off downlevel compiler
  },
  "files": [],                // list of explicit files to include in the project context. Highest priority.
  "include": [],              // list of folders or glob patterns to include in the project context.
  "exclude": [],              // list of folders or glob patterns to exclude. Overridden by files array.
  "typeAcquisition": {
    "enable": true,           // Defaulted to "false" with a tsconfig. Enables better IntelliSense in JS.
    "include": [ "jquery" ],  // Specific libs to fetch .d.ts files that weren't picked up by ATA
    "exclude": [ "node" ]     // Specific libs to not fetch .d.ts files for
  }
}
```

### <a name="example-project-configuration"></a>プロジェクト構成の例

次のようにセットアップされたプロジェクトがあるとします。

- プロジェクトのソース ファイルが `wwwroot/js` にある
- プロジェクトの lib ファイルが `wwwroot/lib` にある
- `bootstrap`、`jquery`、`jquery-validation`、および `jquery-validation-unobtrusive` が `bower.json` にリストされている
- `kendo-ui` が lib フォルダーに手動で追加されている

![フォルダー構造](../javascript/media/js-folderstructure.png)

以下の `tsconfig.json` を使用して、言語サービスは `js` フォルダー内のソース ファイルのみを分析するが、引き続き `.d.ts` フォルダー内のライブラリの `lib` ファイルをフェッチして使用することを確認できます。

```json
{
  "compilerOptions": {
    "allowJs": true,
    "noEmit": true
  },
  "exclude": ["wwwroot/lib"],  //ignore lib folders, we will get IntelliSense via ATA
  "typeAcquisition": {
    "enable": true,
    "include": [ "kendo-ui" ]  //kendo-ui wasn't added via bower, so we need to list it here
  }
}
```

## <a name="troubleshooting-the-javascript-language-service-has-been-disabled-for-the-following-projects"></a>"JavaScript Language Service は次のプロジェクトに対して無効になっています" という問題をトラブルシューティングする
大量のコンテンツを持つ JavaScript プロジェクトを開くと、"JavaScript Language Service は次のプロジェクトに対して無効になっています" という内容のメッセージが表示される場合があります。 大量の JavaScript ソースを持つ最も一般的な理由としては、20 MB というプロジェクトの上限を超えるソース コードがライブラリに含まれていることが挙げられます。

プロジェクトを最適化するための最も簡単な方法は、プロジェクトのルートに `tsconfig.json` ファイルを追加して、無視しても問題ないファイルを言語サービスに知らせてやることです。 以下のサンプルを使用して、ライブラリの格納場所である最も一般的なディレクトリを除外します。

```json
{
  "compilerOptions": {
    "allowJs": true,
    "allowSyntheticDefaultImports": true,
    "maxNodeModuleJsDepth": 2,
    "noEmit": true,
    "skipLibCheck": true
  },
  "exclude": [
    "**/bin",
    "**/bower_components",
    "**/jspm_packages",
    "**/node_modules",
    "**/obj",
    "**/platforms"
  ]
}
```

必要に応じて、他のディレクトリを追加します。 他のいくつかの例には、"vendor" または "wwwroot/lib" ディレクトリが含まれています。

> [!NOTE]
> コンパイラ プロパティ `disableSizeLimit` を使用して、20 MB のチェック制限を無効にすることもできます。 この制限を無効にすると、言語サービスでクラッシュ発生の可能性がありますので、このプロパティを使用する場合は特別な注意が必要です。

## <a name="notable-changes-from-visual-studio-2015"></a>Visual Studio 2015 からの重要な変更点

[!include[vs_dev15](../../docs/misc/includes/vs_dev15_md.md)] ではまったく新しい言語サービスが提供されるため、以前のエクスペリエンスとは異なるか、なくなる動作がいくつかあります。
最も重要な変更は、VSDoc と JSDoc の置き換え、カスタムの `.intellisense.js` 拡張子の削除、および特定のコード パターンでの IntelliSense の制限です。

### <a name="no-more-references-or-_referencesjs"></a>`///<references/>` と `_references.js` の終了

これまでは、ある時点において IntelliSense のスコープ内にあるファイルを認識するのは非常に複雑な作業でした。 スコープ内にすべてのファイルがあることが望ましい場合もあれば、そうでない場合もあるため、構成が複雑になり、参照管理を手動で行う必要がありました。 今後は、参照管理を考慮する必要がなくなるため、トリプル スラッシュ参照コメントや `_references.js` ファイルが不要になります。

IntelliSense のしくみの詳細については、「[JavaScript IntelliSense](/visualstudio/ide/javascript-intellisense/)」ページを参照してください。

### <a name="vsdoc"></a>VSDoc

これまでは、XML ドキュメント コメント (VSDoc ともいう) を使用して、IntelliSense のより適切な結果を得るために使用される追加データでソース コードを修飾できました。
この VSDoc はサポートされなくなり、代わりに作成しやすく、JavaScript の承認済み標準である [JSDoc](https://jsdoc.app/about-getting-started.html) が使用されます。

### <a name="intellisensejs-extensions"></a>`.intellisense.js` 拡張子

これまでは、サード パーティ製ライブラリのカスタムの完了結果を追加できるようにする [IntelliSense 拡張子](https://msdn.microsoft.com/library/hh874692.aspx)を作成できました。
これらの拡張子は作成が非常に難しく、インストールと参照が煩雑だったため、今後は新しい言語サービスでこれらのファイルがサポートされなくなります。
より簡単な代替手段として、TypeScript 定義ファイルを作成することで、古い `.intellisense.js` 拡張子と同じ IntelliSense の利点を得ることができます。
宣言 (`.d.ts`) ファイルの作成の詳細については、[こちら](http://www.typescriptlang.org/docs/handbook/declaration-files/introduction.html)を参照してください。

### <a name="unsupported-patterns"></a>サポートされていないパターン

新しい言語サービスでは、実行エンジンではなくスタティック分析が採用されるため (違いについては、[この問題](https://github.com/Microsoft/TypeScript/issues/4789)を参照してください)、検出できなくなる JavaScript パターンがいくつかあります。
最も一般的なパターンは、"expando"パターンです。
現在、言語サービスでは、宣言後に追加されたプロパティを持つオブジェクトで IntelliSense を提供することはできません。
次に例を示します。

```js
var obj = {};
obj.a = 10;
obj.b = "hello world";
obj. // IntelliSense won't show properties a or b
```

オブジェクトの作成時にプロパティを宣言することで、これを回避できます。

```js
var obj = {
    "a": 10,
    "b": "hello world"
}
obj. // IntelliSense shows properties a and b
```

次のように JSDoc コメントを追加することもできます。

```js
/**
 * @type {{a: number, b: string}}
 */
var obj = {};
obj.a = 10;
obj.b = "hello world";
obj. // IntelliSense shows properties a and b
```

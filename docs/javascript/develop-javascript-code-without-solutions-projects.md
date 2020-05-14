---
title: ソリューションまたはプロジェクトなしで Visual Studio で JavaScript コードを記述する
titleSuffix: ''
description: Visual Studio では、プロジェクト ファイルやソリューション ファイルに依存せずコードを作成できます
ms.custom: seodec18
ms.date: 09/24/2018
ms.topic: conceptual
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: ae8b6fd52cd2469cf7562a199b952d388b463089
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "79549933"
---
# <a name="develop-javascript-and-typescript-code-in-visual-studio-without-solutions-or-projects"></a>Visual Studio で JavaScript と TypeScript のコードをソリューションまたはプロジェクトなしで開発します

Visual Studio 2017 以降では、[プロジェクトまたはソリューションなしでコードを開発する](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)ことができます。コードのフォルダーを開いたらすぐに、IntelliSense、検索、リファクタリング、デバッグなど、豊富なエディター サポートの利用を開始できます。 これらの機能に加え、Node.js Tools for Visual Studio では、TypeScript ファイルをビルドする、npm パッケージを管理する、npm スクリプトを実行するためのサポートが追加されます。

開始するには、ツール バーで **[ファイル]**  >  **[開く]**  >  **[フォルダー]** の順に選択します。 ソリューション エクスプローラーには、フォルダーのすべてのファイルが表示されます。いずれかのファイルを開いて編集を開始できます。 バックグラウンドでは、Visual Studio によってファイルにインデックスが作成され、npm、ビルド、デバッグ機能が有効になります。

> [!IMPORTANT]
> npm 統合を含め、この記事で説明する機能の多くでは、Visual Studio 2017 バージョン 15.8 以降が必要です。 Visual Studio の **[Node.js 開発]** ワークロードがインストールされている必要があります。

## <a name="npm-integration"></a>npm 統合

開いたフォルダーに *package.json* ファイルが含まれている場合、*package.json* を右クリックして npm に固有のコンテキスト メニュー (ショートカット メニュー) を表示できます。

![ソリューション エクスプローラーの npm メニュー](../javascript/media/solution-explorer-npm-ctx.png)

ショートカット メニューでは、プロジェクト ファイルの利用時に [npm パッケージを管理する](npm-package-management.md)ときと同じ方法で、npm によってインストールされたパッケージを管理できます。

また、このメニューでは、*package.json* の `scripts` 要素に定義されているスクリプトを実行することもできます。 これらのスクリプトでは、`PATH` 環境変数で利用できる Node.js のバージョンが利用されます。 スクリプトは新しいウィンドウで実行されます。 これはビルドまたはスクリプトを実行する優れた方法です。

## <a name="build-and-debug"></a>ビルドとデバッグ

### <a name="packagejson"></a>package.json
フォルダーの *package.json* で `main` 要素が指定される場合、**Debug** コマンドを *package.json* の右クリック ショートカット メニューで利用できます。
これをクリックすると、指定のスクリプトをその引数として *node.exe* が開始されます。

### <a name="javascript-files"></a>JavaScript ファイル
ファイルを右クリックし、ショートカット メニューから **[デバッグ]** を選択すると JavaScript ファイルをデバッグできます。 これにより、その JavaScript ファイルをその引数として *node.exe* が開始されます。

### <a name="typescript-files-and-tsconfigjson"></a>TypeScript ファイルと tsconfig.json
フォルダーに *tsconfig.json* がない場合、TypeScript ファイルを右クリックすると、そのファイルをビルドし、デバッグするショートカット メニュー コマンドが表示されます。 これらのコマンドを使用するときは、*tsc.exe* と既定のオプションでビルドまたはデバッグします。 (デバッグするには、先にファイルをビルドする必要があります。)

> [!NOTE]
> TypeScript コードをビルドするとき、`C:\Program Files (x86)\Microsoft SDKs\TypeScript` にインストールされている最新版が使用されます。

フォルダーに *tsconfig.json* がない場合、TypeScript ファイルを右クリックすると、その TypeScript ファイルをビルドするメニュー コマンドが表示されます。 このオプションは、*tsconfig.json* に `outFile` が指定されていない場合にのみ表示されます。 `outFile` が指定されている場合、*tsconfig.json* を右クリックし、該当するオプションを選択するとそのファイルをデバッグできます。 `tsconfig.json` ファイルには、コンパイラ オプションを指定できるビルド オプションもあります。

> [!NOTE]
> *tsconfig.json* に関する詳細は、[tsconfig.json TypeScript ハンドブック ページ](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)にあります。

## <a name="unit-tests"></a>単体テスト
*package.json* でテスト ルートを指定することで、Visual Studio で単体テストの統合を有効にすることができます。

```json
{
    // ...
    "vsTest":{
        "testRoot": "./tests"
    }
    // ...
}
```

テスト ランナーは、どのテスト フレームワークを使用するかを判断するため、ローカルにインストールされたパッケージを列挙します。
サポートされているフレームワークのいずれも認識されない場合は、テスト ランナーは *ExportRunner* を既定にします。 その他のサポートされているフレームワークは次のとおりです。
* Mocha ([mochajs.org](https://mochajs.org/))
* Jasmine ([Jasmine.github.io](https://jasmine.github.io/))
* Tape ([github.com/substack/tape](https://github.com/substack/tape))
* Jest ([jestjs.io](https://jestjs.io/))

テスト エクスプローラーを開くと ( **[テスト]**  >  **[ウィンドウ]**  >  **[テスト エクスプローラー]** を選択)、Visual Studio によってテストが検出されて表示されます。

> [!NOTE]
> テスト ランナーが列挙するのは、テスト ルート内の JavaScript ファイルのみです。アプリケーションが TypeScript で記述されている場合は、JavaScript ファイルを最初にビルドする必要があります。

---
title: JavaScript と TypeScript の単体テスト
description: Visual Studio では、Node.js Tools for Visual Studio を使用する JavaScript と TypeScript コードの単体テストをサポートします
ms.date: 03/18/2021
ms.topic: how-to
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jmartens
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: dc44e39223fd252ae8c4130a1b358aa6af981119
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2021
ms.locfileid: "104671509"
---
# <a name="unit-testing-javascript-and-typescript-in-visual-studio"></a>Visual Studio で JavaScript と TypeScript の単体テストを実行する

Visual Studio では、いくつかのより一般的な JavaScript フレームワークを使用して単体テストを記述し実行できます。コマンド プロンプトに切り替える必要はありません。 Node.js と ASP.NET Core の両方のプロジェクトがサポートされています。

次のフレームワークがサポートされます。
* Mocha ([mochajs.org](https://mochajs.org/))
* Jasmine ([Jasmine.github.io](https://jasmine.github.io/))
* Tape ([github.com/substack/tape](https://github.com/substack/tape))
* Jest ([jestjs.io](https://jestjs.io/))
* Export Runner (このフレームワークは Node.js Tools for Visual Studio に固有です)

ASP.NET Core と JavaScript、または TypeScript については、「[ASP.NET Core 用の単体テストを記述する](#write-unit-tests-for-aspnet-core)」を参照してください。

好みのフレームワークがサポートされていない場合、サポートの追加については「[単体テスト フレームワークのサポートを追加する](#addingFramework)」をご覧ください。

## <a name="write-unit-tests-in-a-nodejs-project"></a>Node.js プロジェクトで単体テストを記述する

プロジェクトに単体テストを追加する前に、使用する予定のフレームワークがプロジェクトにローカルにインストールされていることを確認します。 これは、[npm パッケージ インストール ウィンドウ](npm-package-management.md#npmInstallWindow)を使って簡単に行うことができます。

プロジェクトに単体テストを追加する推奨される方法は、プロジェクトに *tests* フォルダーを作成し、プロジェクトのプロパティでそれをテスト ルートに設定することです。 また、使用するテスト フレームワークを選択する必要もあります。

![テスト ルートとテスト フレームワークを設定する](../javascript/media/unit-test-project-properties.png)

**[新しい項目の追加]** ダイアログ ボックスを使って、簡単な空のテストをプロジェクトに追加できます。 同じプロジェクトで JavaScript と TypeScript の両方がサポートされます。

![新しい単体テストを追加する](../javascript/media/unit-test-add-new-item.png)

Mocha 単体テストでは、次のコードを使います。

```javascript
var assert = require('assert');

describe('Test Suite 1', function() {
    it('Test 1', function() {
        assert.ok(true, "This shouldn't fail");
    })

    it('Test 2', function() {
        assert.ok(1 === 1, "This shouldn't fail");
        assert.ok(false, "This should fail");
    })
})
```

プロジェクトのプロパティで単体テストのオプションを設定していない場合は、 **[プロパティ]** ウィンドウの **[テスト フレームワーク]** プロパティが単体テスト ファイルに対する適切なテスト フレームワークに設定されていることを確認する必要があります。 これは、単体テスト ファイル テンプレートによって自動的に行われます。

![テスト フレームワーク](../javascript/media/UnitTestsFrameworkMocha.png)

> [!Note]
> 単体テストのオプションは、個々のファイルの設定より優先されます。

テスト エクスプローラーを開くと ( **[テスト]**  >  **[ウィンドウ]**  >  **[テスト エクスプローラー]** を選択)、Visual Studio によってテストが検出されて表示されます。 テストが最初に表示されない場合は、プロジェクトをリビルドして一覧を更新します。

![テスト エクスプローラー](../javascript/media/UnitTestsDiscoveryMocha.png)

> [!NOTE]
> TypeScript の場合、テスト エクスプローラーで単体テストを検出することができないため、*tsconfig.json* では、`outdir` オプション、または `outfile` オプションを使用しないでください。

## <a name="run-tests-nodejs"></a>テストを実行する (Node.js)

テストは、Visual Studio 内で、またはコマンド ラインから、実行することができます。

### <a name="run-tests-in-visual-studio"></a>Visual Studio でテストを実行する

::: moniker range=">=vs-2019"
テスト エクスプローラーで **[すべて実行]** リンクをクリックして、テストを実行することができます。 または、1 つ以上のテストまたはグループを選択し、右クリックして、ショートカット メニューから **[実行]** を選択して、テストを実行することもできます。 バックグラウンドでテストが実行され、テスト エクスプローラーが自動的に更新されて、結果が表示されます。 さらに、右クリックして、 **[デバッグ]** を選択して、選択したテストをデバッグすることもできます。
::: moniker-end
::: moniker range="vs-2017"
テスト エクスプローラーで **[すべて実行]** リンクをクリックして、テストを実行することができます。 または、1 つ以上のテストまたはグループを選択し、右クリックして、ショートカット メニューから **[選択したテストの実行]** を選択することで、テストを実行することもできます。 バックグラウンドでテストが実行され、テスト エクスプローラーが自動的に更新されて、結果が表示されます。 さらに、 **[選択したテストのデバッグ]** を選択して、選択したテストをデバッグすることもできます。
::: moniker-end

TypeScript の場合、生成された JavaScript コードに対して単体テストが実行されます。

> [!NOTE]
> ほとんどの TypeScript シナリオでは、TypeScript コードでブレークポイントを設定し、テスト エクスプローラーでテストを右クリックし、 **[デバッグ]** を選択して、単体テストをデバッグすることができます。 ソース マップを使用する一部のシナリオなど、より複雑なシナリオでは、TypeScript コードでブレークポイントに到達するのが困難な場合があります。 回避策としては、`debugger` キーワードを使用してみてください。

> [!NOTE]
> プロファイリング テストまたはコード カバレッジは、現在はサポートされていません。

### <a name="run-tests-from-the-command-line"></a>コマンド ラインからテストを実行する

次のコマンドを使用し、Visual Studio の[開発者コマンド プロンプト](../ide/reference/command-prompt-powershell.md)からテストを実行できます。

```
vstest.console.exe <path to project file>\NodejsConsoleApp23.njsproj /TestAdapterPath:<VisualStudioFolder>\Common7\IDE\Extensions\Microsoft\NodeJsTools\TestAdapter
```

このコマンドでは、次のような出力が表示されます。

```
Microsoft (R) Test Execution Command Line Tool Version 15.5.0
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...
Processing: NodejsConsoleApp23\NodejsConsoleApp23\UnitTest1.js
  Creating TestCase:NodejsConsoleApp23\NodejsConsoleApp23\UnitTest1.js::Test Suite 1 Test 1::mocha
  Creating TestCase:NodejsConsoleApp23\NodejsConsoleApp23\UnitTest1.js::Test Suite 1 Test 2::mocha
Processing finished for framework of Mocha
Passed   Test Suite 1 Test 1
Standard Output Messages:
 Using default Mocha settings
 1..2
 ok 1 Test Suite 1 Test 1

Failed   Test Suite 1 Test 2
Standard Output Messages:
 not ok 1 Test Suite 1 Test 2
   AssertionError [ERR_ASSERTION]: This should fail
       at Context.<anonymous> (NodejsConsoleApp23\NodejsConsoleApp23\UnitTest1.js:10:16)

Total tests: 2. Passed: 1. Failed: 1. Skipped: 0.
Test Run Failed.
Test execution time: 1.5731 Seconds
```

> [!NOTE]
> *vstest.console.exe* が見つからないことを示すエラーが発生する場合は、通常のコマンド プロンプトではなく開発者コマンド プロンプトを開いていることを確認してください。

## <a name="write-unit-tests-for-aspnet-core"></a>ASP.NET Core 用の単体テストを記述する

1. ASP.NET Core プロジェクトを作成し、TypeScript サポートを追加します。

   プロジェクトの例については、[TypeScript を使用した ASP.NET Core アプリの作成](../javascript/tutorial-aspnet-with-typescript.md)に関するページを参照してください。 単体テストのサポートを考慮して、標準の ASP.NET Core プロジェクト テンプレートから始めることをお勧めします。

   npm TypeScript パッケージではなく、TypeScript サポートを追加するには、NuGet パッケージを使用します。

1. NuGet パッケージ [Microsoft.JavaScript.UnitTest](https://www.nuget.org/packages/Microsoft.JavaScript.UnitTest/) をインストールします。

1. ソリューション エクスプローラーで、プロジェクト ノードを右クリックして **[プロジェクトのアンロード]** を選択します。

   Visual Studio で *.csproj* ファイルが開かれます。

1. 次の要素を `PropertyGroup` 要素内の *.csproj* ファイルに追加します。

   この例では、テスト フレームワークとして Mocha が指定されています。 代わりに、Jest、Tape、または Jasmine を指定することも可能です。

   ```xml
   <PropertyGroup>
      ...
      <JavaScriptTestRoot>tests\</JavaScriptTestRoot>
      <JavaScriptTestFramework>Mocha</JavaScriptTestFramework>
      <GenerateProgramFile>false</GenerateProgramFile>
   </PropertyGroup>
   ```

   `JavaScriptTestRoot` 要素によって、単体テストはプロジェクト ルートの *tests* フォルダーに置かれるように指定されています。

1. ソリューション エクスプローラーで、プロジェクト ノードを右クリックして **[プロジェクトの再読み込み]** を選択します。

1. 「[ASP.NET Core プロジェクト](../javascript/npm-package-management.md#aspnet-core-projects)」の npm パッケージ管理に関する記事の説明に従って、npm サポートを追加します。

   そのためには、npm サポート用の Node.js ランタイムをインストールし、プロジェクト ルートに *package.json* を追加する必要があります。

1. *package.json* で、依存関係の下に必要な npm パッケージを追加します。

   たとえば、mocha の場合は、次のものを使用します。

   ```json
   "dependencies": {
     "mocha": "8.3.0",
   ```

   Jest などの一部の単体テスト フレームワークには、追加の npm パッケージが必要です。 Jest の場合は、次の JSON を使用します。

   ```json
   "dependencies": {
     "jest": "26.6.3",
     "jest-editor-support": "28.1.0"
   ```

   >[!NOTE]
   > シナリオによっては、[こちら](https://github.com/aspnet/Tooling/issues/479)に説明されている既知の問題が原因で、npm ノードがソリューション エクスプローラーに表示されないことがあります。 npm ノードを表示する必要がある場合は、プロジェクトをアンロードし (プロジェクトを右クリックして **[プロジェクトのアンロード]** を選択)、次にプロジェクトを再度読み込んで、npm ノードを再表示させることができます。

1. テストするコードを追加します。

   [TypeScript を使用した ASP.NET Core アプリの作成](tutorial-aspnet-with-typescript.md)に関するページで説明されている例を使用する場合は、*scripts* フォルダーにある *library.ts* ファイルの末尾に次のコードを追加します。

   ```typescript
   function getData(value) {
      if (value > 1) {
         return true;
      }
   }
    
   module.exports = getData;
   ```

   TypeScript の場合、生成された JavaScript コードに対して単体テストが実行されます。

1. プロジェクト ルートの *[tests]* フォルダーに単体テストを追加します。

   たとえば、次のコードを使用するには、ご利用のテスト フレームワークに一致する適切なドキュメント タブを選択します (この例では、Mocha または Jest のいずれか)。 このコードを実行すると、`getData` という名前の関数がテストされます。

   # <a name="mocha"></a>[モカ](#tab/mocha)

   ```typescript
   const getData = require('../wwwroot/js/library.js');
   var assert = require('assert');
    
   describe('Test Suite 1', function () {
      it('getData', function () {
         assert.ok(true, getData(2));
      })
   })
   ```

   # <a name="jest"></a>[Jest](#tab/jest)

   ```typescript
   const getData = require('../wwwroot/js/library.js');
    
   test('should return true', () => {
      expect(getData(2)).toBe(true);
   });
   ```

1. テスト エクスプローラーを開きます ( **[テスト]**  >  **[Windows]**  >  **[テスト エクスプローラー]** の順に選択)。すると、Visual Studio によってテストが検出され、表示されます。 テストが最初に表示されない場合は、プロジェクトをリビルドして一覧を更新します。

   ![テスト エクスプローラーによるテストの検出](../javascript/media/unit-tests-aspnet-core-discovery.png)

   > [!NOTE]
   > TypeScript の場合は、ご利用の単体テストがテスト エクスプローラーで検出されないため、*tsconfig.json* で `outfile` オプションを使用しないでください。 `outdir` オプションを使用できますが、`package.json` や `tsconfig.json` などの構成ファイルがプロジェクト ルートにあることを確認してください。

## <a name="run-tests-aspnet-core"></a>テストを実行する (ASP.NET Core)

::: moniker range=">=vs-2019"
テスト エクスプローラーで **[すべて実行]** リンクをクリックして、テストを実行することができます。 または、1 つ以上のテストまたはグループを選択し、右クリックして、ショートカット メニューから **[実行]** を選択して、テストを実行することもできます。 バックグラウンドでテストが実行され、テスト エクスプローラーが自動的に更新されて、結果が表示されます。 さらに、右クリックして、 **[デバッグ]** を選択して、選択したテストをデバッグすることもできます。
::: moniker-end
::: moniker range="vs-2017"
テスト エクスプローラーで **[すべて実行]** リンクをクリックして、テストを実行することができます。 または、1 つ以上のテストまたはグループを選択し、右クリックして、ショートカット メニューから **[選択したテストの実行]** を選択することで、テストを実行することもできます。 バックグラウンドでテストが実行され、テスト エクスプローラーが自動的に更新されて、結果が表示されます。 さらに、 **[選択したテストのデバッグ]** を選択して、選択したテストをデバッグすることもできます。
::: moniker-end

TypeScript の場合、生成された JavaScript コードに対して単体テストが実行されます。

![テスト エクスプローラーの結果](../javascript/media/unit-tests-aspnet-core-run.png)

> [!NOTE]
> ほとんどの TypeScript シナリオでは、TypeScript コードでブレークポイントを設定し、テスト エクスプローラーでテストを右クリックし、 **[デバッグ]** を選択して、単体テストをデバッグすることができます。 ソース マップを使用する一部のシナリオなど、より複雑なシナリオでは、TypeScript コードでブレークポイントに到達するのが困難な場合があります。 回避策としては、`debugger` キーワードを使用してみてください。

> [!NOTE]
> プロファイリング テストまたはコード カバレッジは、現在はサポートされていません。

## <a name="add-support-for-a-unit-test-framework"></a><a name="addingFramework"></a>単体テスト フレームワークのサポートを追加する

JavaScript を使って検出と実行のロジックを実装することで、新しいテスト フレームワークのサポートを追加できます。 そのためには、次の場所の下に、テスト フレームワークの名前でフォルダーを追加します。

`<VisualStudioFolder>\Common7\IDE\Extensions\Microsoft\NodeJsTools\TestAdapter\TestFrameworks`

このフォルダーには、次の 2 つの関数をエクスポートする同じ名前の JavaScript ファイルが含まれている必要があります。

* `find_tests`
* `run_tests`

`find_tests` と `run_tests` の実装の例については、次の場所にある Mocha 単体テスト フレームワークの実装をご覧ください。

`<VisualStudioFolder>\Common7\IDE\Extensions\Microsoft\NodeJsTools\TestAdapter\TestFrameworks\mocha\mocha.js`

使用可能なテスト フレームワークの検出は、Visual Studio の開始時に行われます。 Visual Studio の実行中にフレームワークを追加する場合は、Visual Studio を再起動してフレームワークが検出されるようにします。 ただし、実装を変更するときは再起動する必要はありません。

## <a name="unit-tests-in-net-framework"></a>.NET Framework での単体テスト

単体テストは、Node.js および ASP.NET Core のプロジェクトで記述することだけに限定されません。 TestFramework プロパティと TestRoot プロパティを任意の C# プロジェクトまたは Visual Basic プロジェクトに追加すると、これらのテストが列挙され、[テスト エクスプローラー] ウィンドウを使用してこれらを実行することができます。

これを有効にするには、ソリューション エクスプローラーでプロジェクト ノードを右クリックし、 **[プロジェクトのアンロード]** 、 **[プロジェクトの編集]** の順に選択します。 次に、プロジェクト ファイルで、次の 2 つの要素をプロパティ グループに追加します。

> [!IMPORTANT]
> 要素を追加するプロパティ グループに、指定された条件がないことを確認します。
> これにより、予期しない動作が発生する可能性があります。

```xml
<PropertyGroup>
    <JavaScriptTestRoot>tests\</JavaScriptTestRoot>
    <JavaScriptTestFramework>Tape</JavaScriptTestFramework>
</PropertyGroup>
```

次に、指定したテスト ルート フォルダーにテストを追加すると、これらのテストがテスト エクスプローラー ウィンドウで実行できるようになります。 これらが最初に表示されない場合は、プロジェクトをリビルドする必要があります。

## <a name="unit-test-net-core-and-net-standard"></a>.NET Core と .NET Standard の単体テスト

上記のプロパティに加えて、NuGet パッケージ [Microsoft.JavaScript.UnitTest](https://www.nuget.org/packages/Microsoft.JavaScript.UnitTest/) をインストールし、プロパティを設定する必要もあります。

```xml
<PropertyGroup>
    <GenerateProgramFile>false</GenerateProgramFile>
</PropertyGroup>
```

テスト フレームワークによっては、テスト検出用に追加の npm パッケージが必要になる場合があります。 たとえば、jest では jest-editor-support npm パッケージが必要です。 必要に応じて、特定のフレームワーク用のドキュメントを確認してください。

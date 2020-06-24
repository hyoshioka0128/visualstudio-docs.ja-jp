---
title: JavaScript と TypeScript の単体テスト
description: Visual Studio では、Node.js Tools for Visual Studio を使用する JavaScript と TypeScript コードの単体テストをサポートします
ms.date: 06/06/2018
ms.topic: how-to
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: acac3eb306d12ff6976e19ae5dc1ad772691094c
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85289002"
---
# <a name="unit-testing-javascript-and-typescript-in-visual-studio"></a>Visual Studio で JavaScript と TypeScript の単体テストを実行する

Node.js Tools For Visual Studio を使用すると、いくつかの一般的な JavaScript フレームワークを使用して、単体テストを記述して実行できます。コマンド プロンプトに切り替える必要はありません。

次のフレームワークがサポートされます。
* Mocha ([mochajs.org](https://mochajs.org/))
* Jasmine ([Jasmine.github.io](https://jasmine.github.io/))
* Tape ([github.com/substack/tape](https://github.com/substack/tape))
* Jest ([jestjs.io](https://jestjs.io/))
* Export Runner (このフレームワークは Node.js Tools for Visual Studio に固有です)

好みのフレームワークがサポートされていない場合、サポートの追加については「[単体テスト フレームワークのサポートを追加する](#addingFramework)」をご覧ください。

## <a name="write-unit-tests"></a>単体テストを作成する

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
> テスト エクスプローラーは TypeScript ファイル内の単体テストを検出できないため、*tsconfig.json* では `outdir` または `outfile` オプションを使わないでください。

## <a name="run-tests"></a>テストの実行

テストは、Visual Studio 2017 内で、またはコマンド ラインから、実行することができます。

### <a name="run-tests-in-visual-studio-2017"></a>Visual Studio 2017 でテストを実行する

テスト エクスプローラーで **[すべて実行]** リンクをクリックして、テストを実行することができます。 または、1 つ以上のテストまたはグループを選択し、右クリックして、ショートカット メニューから **[選択したテストの実行]** を選択することで、テストを実行することもできます。 バックグラウンドでテストが実行され、テスト エクスプローラーが自動的に更新されて、結果が表示されます。 さらに、 **[選択したテストのデバッグ]** を選択して、選択したテストをデバッグすることもできます。

> [!Warning]
> 現在、Node 8 以降を使用する単体テストのデバッグは、JavaScript テスト ファイルについてのみ動作し、TypeScript テスト ファイルではブレークポイントにヒットしません。 回避策としては、`debugger` キーワードを使ってください。

> [!NOTE]
> プロファイリング テストまたはコード カバレッジは、現在はサポートされていません。

### <a name="run-tests-from-the-command-line"></a>コマンド ラインからテストを実行する

次のコマンドを使って、Visual Studio 2017 の[開発者コマンド プロンプト](/dotnet/framework/tools/developer-command-prompt-for-vs)からテストを実行できます。

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

## <a name="add-support-for-a-unit-test-framework"></a><a name="addingFramework"></a>単体テスト フレームワークのサポートを追加する

JavaScript を使って検出と実行のロジックを実装することで、新しいテスト フレームワークのサポートを追加できます。 そのためには、次の場所の下に、テスト フレームワークの名前でフォルダーを追加します。

`<VisualStudioFolder>\Common7\IDE\Extensions\Microsoft\NodeJsTools\TestAdapter\TestFrameworks`

このフォルダーには、次の 2 つの関数をエクスポートする同じ名前の JavaScript ファイルが含まれている必要があります。

* `find_tests`
* `run_tests`

`find_tests` と `run_tests` の実装の例については、次の場所にある Mocha 単体テスト フレームワークの実装をご覧ください。

`<VisualStudioFolder>\Common7\IDE\Extensions\Microsoft\NodeJsTools\TestAdapter\TestFrameworks\mocha\mocha.js`

使用可能なテスト フレームワークの検出は、Visual Studio の開始時に行われます。 Visual Studio の実行中にフレームワークを追加する場合は、Visual Studio を再起動してフレームワークが検出されるようにします。 ただし、実装を変更するときは再起動する必要はありません。

## <a name="unit-tests-in-other-project-types"></a>他のプロジェクト タイプでの単体テスト
単体テストは、Node.js プロジェクトで記述することだけに限定されません。 TestFramework プロパティと TestRoot プロパティを任意の C# プロジェクトまたは Visual Basic プロジェクトに追加すると、これらのテストが列挙され、[テスト エクスプローラー] ウィンドウを使用してこれらを実行することができます。

これを有効にするには、ソリューション エクスプローラーでプロジェクト ノードを右クリックし、 **[プロジェクトのアンロード]** 、 **[プロジェクトの編集]** の順に選択します。 次に、プロジェクト ファイルで、次の 2 つの要素をプロパティ グループに追加します。

> [!NOTE]
> 要素を追加するプロパティ グループに、指定された条件がないことを確認します。
> これにより、予期しない動作が発生する可能性があります。

```xml
<PropertyGroup>
    <JavaScriptTestRoot>tests\</JavaScriptTestRoot>
    <JavaScriptTestFramework>Tape</JavaScriptTestFramework>
</PropertyGroup>
```

次に、指定したテスト ルート フォルダーにテストを追加すると、これらのテストがテスト エクスプローラー ウィンドウで実行できるようになります。 これらが最初に表示されない場合は、プロジェクトをリビルドする必要があります。

### <a name="unit-test-net-core-and-net-standard"></a>.NET Core と .NET Standard の単体テスト
上記のプロパティに加えて、NuGet パッケージ [Microsoft.JavaScript.UnitTest](https://www.nuget.org/packages/Microsoft.JavaScript.UnitTest/) をインストールし、プロパティを設定する必要もあります。

```xml
<PropertyGroup>
    <GenerateProgramFile>false</GenerateProgramFile>
</PropertyGroup>
```

テスト フレームワークによっては、テスト検出用に追加の npm パッケージが必要になる場合があります。 たとえば、jest では jest-editor-support npm パッケージが必要です。 必要に応じて、特定のフレームワーク用のドキュメントを確認してください。

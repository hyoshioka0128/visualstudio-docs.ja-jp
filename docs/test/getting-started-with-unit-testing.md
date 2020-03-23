---
title: 単体テストの概要
ms.date: 03/04/2020
ms.topic: conceptual
helpviewer_keywords:
- unit testing, create unit test plans
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 90c3cbdee722c4cf12c515f06659cc03f3179e1e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "78289855"
---
# <a name="get-started-with-unit-testing"></a>単体テストの概要

Visual Studio を使用して、単体テストを定義および実行してコードの正常性を維持し、コード カバレッジを保証し、事前にエラーとフォールトを見つけます。 単体テストを頻繁に実行し、コードが正しく動作していることを確認します。

## <a name="create-unit-tests"></a>単体テストの作成

このセクションでは、単体テスト プロジェクトの作成方法を説明します。

1. Visual Studio でテストするプロジェクトを開きます。

   単体テストの例をデモすることを目的として、この記事では **HelloWorldCore** という名前のシンプルな "Hello World" プロジェクトをテストします。 そのようなプロジェクトのサンプル コードは、次のとおりです。

   ```csharp
   namespace HelloWorldCore

      public class Program
      {
         public static void Main()
         {
            Console.WriteLine("Hello World!");
         }
      }
   ```

1. **ソリューション エクスプローラー**で、ソリューション ノードを選びます。 次に、上部のメニュー バーで **[ファイル]**  >  **[追加]**  >  **[新しいプロジェクト]** を選択します。

1. 新しいプロジェクトのダイアログ ボックスで、使用するテスト フレームワーク用の単体テスト プロジェクト テンプレートを検索して選択します。

   ::: moniker range=">=vs-2019"

   ![Visual Studio 2019 の単体テスト プロジェクト テンプレート](media/vs-2019/add-new-test-project.png)

   **[次へ]** をクリックし、テスト プロジェクトの名前を選択して、 **[作成]** をクリックします。

   ::: moniker-end

   ::: moniker range="vs-2017"

   ![Visual Studio 2019 の単体テスト プロジェクト テンプレート](media/mstest-test-project-template.png)

   テスト プロジェクトの名前を選択し、 **[OK]** をクリックします。

   ::: moniker-end

   プロジェクトがソリューションに追加されます。

   ![ソリューション エクスプローラーの単体テスト プロジェクト](media/vs-2019/solution-explorer.png)

1. 単体テスト プロジェクトで、 **[参照]** または **[依存関係]** を右クリックし、 **[参照の追加]** を選択して、テストするプロジェクトに参照を追加します。

1. テストするコードを含むプロジェクトを選択し、 **[OK]** をクリックします。

   ![Visual Studio でプロジェクト参照を追加する](media/vs-2019/reference-manager.png)

1. 単体テスト メソッドにコードを追加します。

   たとえば、MSTest プロジェクトには、次のコードを使用できます。

   ```csharp
   using Microsoft.VisualStudio.TestTools.UnitTesting;
   using System.IO;
   using System;

   namespace HelloWorldTests
   {
      [TestClass]
      public class UnitTest1
      {
         private const string Expected = "Hello World!";
         [TestMethod]
         public void TestMethod1()
         {
            using (var sw = new StringWriter())
            {
               Console.SetOut(sw);
               HelloWorldCore.Program.Main();

               var result = sw.ToString().Trim();
               Assert.AreEqual(Expected, result);
            }
         }
      }
   }
   ```

   あるいは、NUnit プロジェクトの場合、次のコードを使用することもできます。

   ```csharp
   using using NUnit.Framework;
   using System.IO;
   using System;

   namespace HelloWorldTests
   {
      [TestClass]
      public class Tests
      {
         private const string Expected = "Hello World!";

         [SetUp]
         public void Setup()
         {
         }
         [Test]
         public void TestMethod1()
         {
            using (var sw = new StringWriter())
            {
               Console.SetOut(sw);
               HelloWorldCore.Program.Main();

               var result = sw.ToString().Trim();
               Assert.AreEqual(Expected, result);
            }
         }
      }
   }
   ```

> [!TIP]
> 単体テストの作成について詳しくは、[マネージド コードの単体テストの作成および実行](walkthrough-creating-and-running-unit-tests-for-managed-code.md)に関するページを参照してください。

## <a name="run-unit-tests"></a>単体テストを実行する

1. [テスト エクスプローラー](../test/run-unit-tests-with-test-explorer.md)を開きます。

   ::: moniker range=">=vs-2019"
   テスト エクスプローラーを開くには、上部のメニュー バーで **[テスト]** > **[テスト エクスプローラー]** を選択します。
   ::: moniker-end
   ::: moniker range="vs-2017"
   テスト エクスプローラーを開くには、上部のメニュー バーで **[テスト]** > **[Windows]** > **[テスト エクスプローラー]** を選択します。
   ::: moniker-end

1. **[すべて実行]** をクリックして、単体テストを実行します。

   ![テスト エクスプローラーでの単体テストの実行](media/vs-2019/test-explorer-run-all.png)

   テストが完了すると、緑色のチェック マークが、テストが成功したことを示します。 赤色の "x" アイコンは、テストが失敗したことを示します。

   ![テスト エクスプローラーで単体テストの結果を確認する](media/vs-2019/unit-test-passed.png)

> [!TIP]
> [テスト エクスプローラー](../test/run-unit-tests-with-test-explorer.md)を使用して、組み込みのテスト フレームワーク (MSTest) またはサードパーティのテスト フレームワークから、単体テストを実行できます。 テストをカテゴリにまとめたり、テストの一覧にフィルターを適用したり、テストのプレイリストを実行したりできます。 テストをデバッグし、テストのパフォーマンスとコード カバレッジを分析することもできます。

## <a name="view-live-unit-test-results"></a>ライブ単体テストの結果を表示する

Visual Studio 2017 以降で MSTest、xUnit、または NUnit テスト フレームワークを使用する場合は、単体テストのライブ結果を表示できます。

> [!NOTE]
> ライブ単体テストは、Enterprise Edition でのみ使用できます。

1. **[テスト]**  >  **[Live Unit Testing]**  >  **[開始]** を選択して、 **[テスト]** メニューでライブ単体テストをオンにします。

   ::: moniker range="vs-2017"

   ![ライブ単体テストをオンにする](media/live-test-results-start.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Visual Studio 2019 でライブ単体テストを開始する](media/vs-2019/start-live-unit-testing.png)

   ::: moniker-end

1. コードの作成および編集時に、コード エディター ウィンドウ内でテストの結果を表示します。

   ![テスト結果を表示する](media/vs-2019/live-unit-testing-results.png)

1. そのメソッドをカバーしているテストの名前などの詳細については、テスト結果インジケーターをクリックします。

   ![テスト結果インジケーターを選択します。](media/vs-2019/live-unit-testing-details.png)

ライブ単体テストの詳細については、[ライブ単体テスト](../test/live-unit-testing-intro.md)に関するページを参照してください。

## <a name="generate-unit-tests-with-intellitest"></a>IntelliTest で単体テストを生成する

IntelliTest を実行すると、どのテストが失敗しているかを把握し、必要なコードを追加して修正できます。 回帰スイートを提供するために、生成されたどのテストをテスト プロジェクトに保存するかを選択できます。 コードを変更する際に、IntelliTest を再実行して、生成されたテストとコードの変更を同期させます。 その方法については、「[IntelliTest でのコードの単体テストの生成](../test/generate-unit-tests-for-your-code-with-intellitest.md)」を参照してください。

> [!TIP]
> IntelliTest は、.NET Framework を対象とするマネージド コードでのみ使用できます。

![IntelliTest での単体テストの生成](media/intellitest.png)

## <a name="analyze-code-coverage"></a>コード カバレッジの分析

単体テストなどのコード化されたテストによって実際にテストされるプロジェクトのコードの割合を調べるには、Visual Studio のコード カバレッジ機能を使用できます。 バグを効果的に回避するには、コードの大部分を対象としたテストが必要です。 その方法については、「[コード カバレッジを使用した、テストされるプロジェクトのコード割合の確認](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md)」を参照してください。

## <a name="use-a-third-party-test-framework"></a>サードパーティのテスト フレームワークを使用する

Boost、Google、NUnit など、サードパーティのテスト フレームワークを利用して、Visual Studio で単体テストを実行できます。 **NuGet パッケージ マネージャー**を使用して、お好きなフレームワーク用の NuGet パッケージをインストールします。 また、NUnit テスト フレームワークと xUnit テスト フレームワーク用に、Visual Studio には、必要な NuGet パッケージを含む事前構成済みのテスト プロジェクト テンプレートが含まれています。

[NUnit](https://nunit.org/) を使用する単体テストを作成するには:

1. テストするコードを含むソリューションを開きます。

2. **ソリューション エクスプローラー**でソリューションを右クリックし、 **[追加]**  >  **[新しいプロジェクト]** を選択します。

3. **[NUnit テスト プロジェクト]** プロジェクト テンプレートを選択します。

   ::: moniker range=">=vs-2019"

   ![Visual Studio 2019 の NUnit テスト プロジェクト テンプレート](media/vs-2019/nunit-test-project-template.png)

   **[次へ]** をクリックし、プロジェクトに名前を設定して、 **[作成]** をクリックします。

   ::: moniker-end

   ::: moniker range="vs-2017"

   プロジェクトに名前を設定し、 **[OK]** をクリックして作成します。

   ::: moniker-end

   プロジェクト テンプレートには、NUnit と NUnit3TestAdapter への NuGet 参照が含まれています。

   ![ソリューション エクスプローラーでの NUnit NuGet の依存関係](media/vs-2019/nunit-nuget-dependencies.png)

4. テスト プロジェクトから、テストするコードを含むプロジェクトに参照を追加します。

   **ソリューション エクスプローラー**でプロジェクトを右クリックし、 **[追加]**  >  **[参照]** を選択します。 ( **[参照]** ノードまたは **[依存関係]** ノードの右クリック メニューから参照を追加することもできます。)

5. テスト メソッドにコードを追加する

   ![コードを単体テスト コード ファイルに追加する](media/vs-2019/unit-test-method.png)

6. **テスト エクスプローラー**で、またはテスト コードを右クリックして **[テストの実行]** を選択して、テストを実行します。

## <a name="see-also"></a>関連項目

* [チュートリアル: マネージド コードの単体テストを作成し、実行する](walkthrough-creating-and-running-unit-tests-for-managed-code.md)
* [単体テスト コマンドの作成](create-unit-tests-menu.md)
* [IntelliTest でのテストの生成](generate-unit-tests-for-your-code-with-intellitest.md)
* [テスト エクスプローラーを使用してテストを実行する](run-unit-tests-with-test-explorer.md)
* [コード カバレッジの分析](using-code-coverage-to-determine-how-much-code-is-being-tested.md)

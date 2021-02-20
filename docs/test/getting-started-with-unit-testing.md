---
title: 単体テストの概要
description: Visual Studio を使用すると、コードの正常性を維持するための単体テストを定義および実行し、顧客で発生する前にエラーとフォールトを見つけておくことができます。
ms.custom: SEO-VS-2020
ms.date: 04/07/2020
ms.topic: tutorial
helpviewer_keywords:
- unit testing, create unit test plans
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c83b13b852b9ae53bd2218a62b6681478369df1b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99970518"
---
# <a name="get-started-with-unit-testing"></a>単体テストの概要

Visual Studio を使用して、単体テストを定義および実行してコードの正常性を維持し、コード カバレッジを保証し、事前にエラーとフォールトを見つけます。 単体テストを頻繁に実行し、コードが正しく動作していることを確認します。

この記事では、コードと図に C# が使用されていますが、概念と機能は .NET 言語、C++、Python、JavaScript、および TypeScript に適用されます。

## <a name="create-unit-tests"></a>単体テストを作成する

このセクションでは、単体テスト プロジェクトの作成方法を説明します。

1. Visual Studio でテストするプロジェクトを開きます。

   単体テストの例をデモすることを目的として、この記事では **HelloWorldCore** という名前のシンプルな "Hello World" C# プロジェクトをテストします。 そのようなプロジェクトのサンプル コードは、次のとおりです。

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

1. **ソリューション エクスプローラー** で、ソリューション ノードを選びます。 次に、上部のメニュー バーで **[ファイル]**  >  **[追加]**  >  **[新しいプロジェクト]** を選択します。

1. 新しいプロジェクトのダイアログ ボックスで、MSTest など、使用するテスト フレームワーク用の単体テスト プロジェクト テンプレートを検索して選択します。

   Visual Studio 2017 バージョン 14.8 以降、.NET 言語には NUnit と xUnit 用の組み込みのテンプレートが含まれています。 C++ の場合、言語でサポートされているテスト フレームワークを選択する必要があります。 Python の場合、使用するテスト プロジェクトを設定するには、[Python コードでの単体テストの設定](../python/unit-testing-python-in-visual-studio.md)に関するページを参照してください。

   > [!TIP]
   > C# の場合、より高速なメソッドを使用して、単体テスト プロジェクトをコードから作成することができます。 詳細については、「[単体テスト プロジェクトとテスト メソッドを作成する](../test/unit-test-basics.md#create-unit-test-projects-and-test-methods)」を参照してください。 .NET Core または .NET Standard でこのメソッドを使用するには、Visual Studio 2019 が必要です。

   次の図に、.NET でサポートされている MSTest 単体テストを示します。

   ::: moniker range=">=vs-2019"

   ![Visual Studio 2019 の単体テスト プロジェクト テンプレート](media/vs-2019/add-new-test-project.png)

   **[次へ]** をクリックし、テスト プロジェクトの名前を選択して、**[作成]** をクリックします。

   ::: moniker-end

   ::: moniker range="vs-2017"

   ![Visual Studio 2019 の単体テスト プロジェクト テンプレート](media/mstest-test-project-template.png)

   テスト プロジェクトの名前 (HelloWorldTests など) を選択して、 **[OK]** をクリックします。

   ::: moniker-end

   プロジェクトがソリューションに追加されます。

   ![ソリューション エクスプローラーの単体テスト プロジェクト](media/vs-2019/solution-explorer.png)

1. 単体テスト プロジェクトで、**[参照]** または **[依存関係]** を右クリックし、**[参照の追加]** を選択して、テストするプロジェクトに参照を追加します。

1. テストするコードを含むプロジェクトを選択し、**[OK]** をクリックします。

   ![Visual Studio でプロジェクト参照を追加する](media/vs-2019/reference-manager.png)

1. 単体テスト メソッドにコードを追加します。

   たとえば、ご利用のテスト フレームワークに一致する適切なドキュメント タブを選択して、次のコードを使用します: MSTest、NUnit、または xUnit (.NET でのみサポートされます)。

   # <a name="mstest"></a>[MSTest](#tab/mstest)

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

   # <a name="nunit"></a>[NUnit](#tab/nunit)

   ```csharp
   using NUnit.Framework;
   using System.IO;
   using System;

   namespace HelloWorldTests
   {
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

    # <a name="xunit"></a>[xUnit](#tab/xunit)

    ```csharp
    using System;
    using Xunit;
    using System.IO;
    
    namespace HelloWorldTests
    {
        public class UnitTest1
        {
            private const string Expected = "Hello World!";
            [Fact]
            public void Test1()
            {
                using (var sw = new StringWriter())
                {
                    Console.SetOut(sw);
                    HelloWorldCore.Program.Main();
    
                    var result = sw.ToString().Trim();
                    Assert.Equal(Expected, result);
                }
            }
        }
    }
    ```

## <a name="run-unit-tests"></a>単体テストを実行する

1. [テスト エクスプローラー](../test/run-unit-tests-with-test-explorer.md)を開きます。

   ::: moniker range=">=vs-2019"
   テスト エクスプローラーを開くには、上部のメニュー バーで **[テスト]** > **[テスト エクスプローラー]** を選択します (または **Ctrl** + **E**、**T** キーを押します)。
   ::: moniker-end
   ::: moniker range="vs-2017"
   テスト エクスプローラーを開くには、上部のメニュー バーで **[テスト]** > **[Windows]** > **[テスト エクスプローラー]** を選択します。
   ::: moniker-end

1. **[すべて実行]** をクリックして、単体テストを実行します (または **Ctrl** + **R**、**V** キーを押します)。

   ![テスト エクスプローラーでの単体テストの実行](media/vs-2019/test-explorer-run-all.png)

   テストが完了すると、緑色のチェック マークが、テストが成功したことを示します。 赤色の "x" アイコンは、テストが失敗したことを示します。

   ![テスト エクスプローラーで単体テストの結果を確認する](media/vs-2019/unit-test-passed.png)

> [!TIP]
> [テスト エクスプローラー](../test/run-unit-tests-with-test-explorer.md)を使用して、組み込みのテスト フレームワーク (MSTest) またはサードパーティのテスト フレームワークから、単体テストを実行できます。 テストをカテゴリにまとめたり、テストの一覧にフィルターを適用したり、テストのプレイリストを実行したりできます。 テストをデバッグし、テストのパフォーマンスとコード カバレッジを分析することもできます。

## <a name="view-live-unit-test-results-visual-studio-enterprise"></a>ライブ単体テストの結果を表示する (Visual Studio Enterprise)

Visual Studio 2017 以降で MSTest、xUnit、または NUnit テスト フレームワークを使用する場合は、単体テストのライブ結果を表示できます。

> [!NOTE]
> これらの手順に従うには、Visual Studio Enterprise が必要です。

1. **[テスト]** > **[Live Unit Testing]** > **[開始]** を選択して、**[テスト]** メニューでライブ単体テストをオンにします。

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

## <a name="use-a-third-party-test-framework"></a>サードパーティのテスト フレームワークを使用する

ご利用のプログラミング言語に応じて、Boost、Google、NUnit など、サードパーティのテスト フレームワークを利用して、Visual Studio で単体テストを実行できます。 サードパーティのフレームワークを使用するには:

- **NuGet パッケージ マネージャー** を使用して、お好きなフレームワーク用の NuGet パッケージをインストールします。

- (.NET) Visual studio 2017 バージョン 14.6 以降、Visual Studio には、NUnit および xUnit テスト フレームワーク用に構成済みのテスト プロジェクト テンプレートが含まれています。 これらのテンプレートには、サポートを有効にするために必要な NuGet パッケージも含まれています。

- (C++) Visual Studio 2017 以降のバージョンには、Boost などの一部のフレームワークが既に含まれています。 詳細については、「[Visual Studio で C/C++ 用の単体テストを作成する](../test/writing-unit-tests-for-c-cpp.md)」を参照してください。

単体テスト プロジェクトを作成するには:

1. テストするコードを含むソリューションを開きます。

2. **ソリューション エクスプローラー** でソリューションを右クリックし、**[追加]** > **[新しいプロジェクト]** を選択します。

3. 単体テスト プロジェクト テンプレートを選択します。

   この例では、[NUnit](https://nunit.org/) を選択します

   ::: moniker range=">=vs-2019"

   ![Visual Studio 2019 の NUnit テスト プロジェクト テンプレート](media/vs-2019/nunit-test-project-template.png)

   **[次へ]** をクリックし、プロジェクトに名前を設定して、**[作成]** をクリックします。

   ::: moniker-end

   ::: moniker range="vs-2017"

   プロジェクトに名前を設定し、**[OK]** をクリックして作成します。

   ::: moniker-end

   プロジェクト テンプレートには、NUnit と NUnit3TestAdapter への NuGet 参照が含まれています。

   ![ソリューション エクスプローラーでの NUnit NuGet の依存関係](media/vs-2019/nunit-nuget-dependencies.png)

4. テスト プロジェクトから、テストするコードを含むプロジェクトに参照を追加します。

   **ソリューション エクスプローラー** でプロジェクトを右クリックし、**[追加]** > **[参照]** を選択します。 (**[参照]** ノードまたは **[依存関係]** ノードの右クリック メニューから参照を追加することもできます。)

5. テスト メソッドにコードを追加する

   ![コードを単体テスト コード ファイルに追加する](media/vs-2019/unit-test-method.png)

6. **テスト エクスプローラー** で、またはテスト コードを右クリックして **[テストの実行]** を選択して、テストを実行します (または **Ctrl** + **R**、**T** キーを押します)。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [単体テストの基本](../test/unit-test-basics.md)

> [!div class="nextstepaction"]
> [マネージド コードの単体テストを作成し、実行する](walkthrough-creating-and-running-unit-tests-for-managed-code.md)

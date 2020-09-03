---
title: ストアアプリの単体テストを実行する
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 5a6f5b32-bfce-4a63-81e9-02d54c592539
caps.latest.revision: 14
author: alexhomer1
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b70e3a24cd4cb05dc1a28ff855498496f5665ddc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85542858"
---
# <a name="run-unit-tests-for-store-apps-in-visual-studio"></a>Visual Studio での ストア アプリの単体テストの実行
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、Microsoft Visual Studio でテスト エクスプローラーを使用して単体テストを実行する方法について説明します。

> [!NOTE]
> このセクションのトピックでは、Visual Studio Express for Windows 8 の機能について解説します。 Visual Studio Community、Enterprise、および Professional には、単体テストの追加機能が備わっています。
>
> - Microsoft テスト エクスプローラーのアドオン アダプターを作成したサードパーティまたはオープン ソースの単体テスト フレームワークを使用します。 また、テストのコード カバレッジ情報を分析して表示することもできます。
>   - ビルドの後に毎回テストを実行します。 Microsoft Fakes を使用することもできます。これは、システムおよびサードパーティの機能をテスト コードに置き換えることにより、自分のコードにテストの重点を置くことができる、マネージド コードの分離フレームワークです。
>
>   詳細については、「[コードの単体テスト](../test/unit-test-your-code.md)」を参照してください。

## <a name="in-this-topic"></a><a name="BKMK_In_this_topic"></a> このトピックの内容
 [単体テストフレームワークとテストプロジェクト](#BKMK_Unit_test_frameworks_and_test_projects)

 [テスト エクスプローラーでテストを実行する](#BKMK_Running_tests_in_Test_Explorer)

- [テストを実行する](#BKMK_Running_tests)

  [テスト結果の表示](#BKMK_Viewing_test_results)

- [テストの詳細の表示](#BKMK_Viewing_test_details)

- [テストメソッドのソースコードの表示](#BKMK_Viewing_the_source_code_of_a_test_method)

  [テストリストの整理](#BKMK_Organizing_the_test_list)

- [テストのグループ化](#BKMK_Grouping_tests)

- [テストリストの検索とフィルター処理](#BKMK_Searching_and_filtering_the_test_list)

  [単体テストのデバッグ](#BKMK_Debugging_unit_tests)

## <a name="unit-test-frameworks-and-test-projects"></a><a name="BKMK_Unit_test_frameworks_and_test_projects"></a> 単体テスト フレームワークとテスト プロジェクト
 Visual Studio Express for Windows Store Apps には、マネージド コードとネイティブ C++ コード用の Microsoft 単体テスト フレームワークが含まれています。 テスト エクスプローラーは、ソリューション内の複数のテスト プロジェクト、および運用コード プロジェクトに含まれるテスト クラスからテストを実行できます。 テスト プロジェクトには、Visual C++ または Visual C# と Visual Basic の単体テスト フレームワークを自由に組み合わせることができます。 テスト対象のコードを .NET Framework 用に記述する場合、対象コードの言語にかかわらず、テスト プロジェクトをどの .NET Framework 言語でも記述できます。 ネイティブ C/C++ コード プロジェクトは、C++ の単体テスト フレームワークを使用してテストする必要があります。

## <a name="running-tests-in-test-explorer"></a><a name="BKMK_Running_tests_in_Test_Explorer"></a> テストエクスプローラーでのテストの実行
 テスト プロジェクトをビルドすると、テストはテスト エクスプローラーに表示されます。 テスト エクスプローラーが表示されない場合は、Visual Studio メニューの **[テスト]** をクリックし、 **[Windows]** 、 **[テスト エクスプローラー]** の順に選択します。

 ![単体テスト エクスプローラー](../ide/media/ute-failedpassednotrunsummary.png "UTE_FailedPassedNotRunSummary")

 テストを実行して、記述し、再実行すると、テスト エクスプローラーに **[失敗したテスト]** 、 **[成功したテスト]** 、 **[スキップされたテスト]** 、および **[テストを実行しない]** の既定のグループの結果が表示されます。 テスト エクスプローラーでテストをグループ化する方法を変更できます。

 テスト エクスプローラーのツール バーからテストの検索、整理、および実行の作業の多くを実行できます。

 ![テスト エクスプローラー ツールバーからテストを実行](../test/media/ute-toolbar.png "UTE_ToolBar")

### <a name="running-tests"></a><a name="BKMK_Running_tests"></a> テストの実行
 ソリューション内のすべてのテスト、グループ内のすべてのテスト、または選択した一連のテストを実行できます。 次のいずれかの操作を行います。

- ソリューション内のすべてのテストを実行するには、 **[すべて実行]** をクリックします。

- 既定のグループ内のすべてのテストを実行するには、[ **実行.** ..] を選択し、メニューの [グループ] を選択します。

- 実行する個々のテストを選択し、選択したテストのショートカット メニューを開いて、**[選択したテストの実行]** を選択します。

  テストの実行中、テスト エクスプローラー ウィンドウの一番上にある成功/失敗ステータス バーがアニメーション化されます。 テストの実行の終了時に、すべてのテストが成功した場合は、成功/失敗ステータス バーが緑色に変わり、いずれかのテストが失敗した場合は、赤色に変わります。

## <a name="viewing-test-results"></a><a name="BKMK_Viewing_test_results"></a> テスト結果の表示
 テストを実行して、記述し、再実行すると、テスト エクスプローラーに **[失敗したテスト]** 、 **[成功したテスト]** 、 **[スキップされたテスト]** 、および **[テストを実行しない]** のグループの結果が表示されます。 テスト エクスプローラーの下部の詳細ペインに、テストの実行の概要が表示されます。

### <a name="viewing-test-details"></a><a name="BKMK_Viewing_test_details"></a> テストの詳細を表示する
 個々のテストの詳細を表示するには、そのテストを選択します。

 テストの詳細ペインに次の情報が表示されます。

- テスト メソッドのソース ファイル名と行番号。

- テストの状態。

- テスト メソッドの実行に要した経過時間。

  テストが失敗した場合、詳細ペインには次の情報も表示されます。

- テストの単体テスト フレームワークによって返されたメッセージ。

- テストが失敗した時刻のスタック トレース。

### <a name="viewing-the-source-code-of-a-test-method"></a><a name="BKMK_Viewing_the_source_code_of_a_test_method"></a> テスト メソッドのソース コードの表示
 Visual Studio エディターのテスト メソッドのソース コードを表示するには、テストを選択し、ショートカット メニューの **[テストを開く]** を選択します (キーボードの F12 キー)。

## <a name="organizing-the-test-list"></a><a name="BKMK_Organizing_the_test_list"></a> テスト一覧の整理

### <a name="grouping-tests"></a><a name="BKMK_Grouping_tests"></a> テストのグループ化
 既定では、テスト エクスプローラーに **[失敗したテスト]**、**[成功したテスト]**、**[スキップされたテスト]**、および **[未実行のテスト]** の子ノードとしてテストが表示されます。

|Image|説明|
|-|-|
|![テスト エクスプローラー グループ ボタン](../test/media/ute-groupby-btn.png "UTE_GroupBy_btn")|これらのテストの実行に要する時間によってテストをグループ化するには、**[グループ化]** ボックスの一覧を開き、**[期間]** を選択します。 元のグループに切り替えるには、**[テスト成果]** を選択します。|

### <a name="searching-and-filtering-the-test-list"></a><a name="BKMK_Searching_and_filtering_the_test_list"></a> テスト一覧の検索およびフィルター処理
 多数のテストがある場合、テスト エクスプローラーの検索ボックスに入力し、指定した文字列によって一覧をフィルター処理できます。 検索文字列を入力する前に、フィルターの一覧から選択して、フィルターを特定の種類の文字列に制限できます。

 ![フィルターの検索カテゴリ](../test/media/ute-searchfilter.png "UTE_SearchFilter")

## <a name="debugging-unit-tests"></a><a name="BKMK_Debugging_unit_tests"></a> 単体テストのデバッグ
 テスト エクスプローラーを使用して、テストのデバッグ セッションを開始できます。 Visual Studio デバッガーを使用してコードをシームレスにステップ実行すると、テスト対象のプロジェクトと単体テストの間を切り替えることができます。 デバッグを開始するには:

1. Visual Studio エディターで、デバッグする 1 つ以上のテスト メソッドにブレークポイントを設定します。

   > [!NOTE]
   > テスト メソッドを任意の順序で実行できるため、デバッグするすべてのテスト メソッドにブレークポイントを設定します。

2. テスト エクスプローラーでテスト メソッドを選択し、ショートカット メニューの **[選択したテストのデバッグ]** を選択します。

   デバッガーについて詳しくは、「 [Debugging in Visual Studio](../debugger/debugging-in-visual-studio.md)」をご覧ください。

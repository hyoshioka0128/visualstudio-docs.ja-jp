---
title: Visual Studio for Mac テスト ツール
ms.date: 08/03/2020
ms.topic: conceptual
helpviewer_keywords:
- testing tools [Visual Studio for Mac]
- unit tests [Visual Studio for Mac]
ms.author: jomatthi
author: jmatthiesen
ms.openlocfilehash: 758bdcb0d854247847e4d0d56152840643402bf4
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91580962"
---
# <a name="testing-tools-in-visual-studio-for-mac"></a>Visual Studio for Mac のテスト ツール

Visual Studio for Mac のテスト ツールを使用することで、チームと共に高水準の優れたコードを開発し、維持できます。 単体テストは、Microsoft 単体テスト フレームワーク (MSTest)、xUnit、または NUnit を利用して作成したり、実行したりできます。

## <a name="creating-tests"></a>テストの作成
テストを開始するには、ソリューションを右クリックし、 **[追加]、[新しいプロジェクト...]** メニューの順に選択し、ソリューションで新しいテスト プロジェクトを作成できます。 次に、ダイアログの左側で [テスト] カテゴリの 1 つを選択します (たとえば、 **[Web and Console]\(Web とコンソール\)、[テスト]** カテゴリの順に選択します)。 作成するテスト プロジェクトの種類を選択し、[次へ] をクリックします。 表示されたダイアログ内の指示に従うと、新しいテスト プロジェクトがソリューションに追加されます。

![新しいプロジェクト ダイアログで [Web and Console]\(Web とコンソール\) の [テスト] セクションが選択され、xUnit、MSTest、NUnit の各プロジェクトが表示されています](media/create-new-test-project.PNG)

> [!NOTE]
> .NET Core アプリケーションを単体テストする方法と単体テスト フレームワークを選択する方法の詳細については、「[.NET Core と .NET Standard の単体テスト](/dotnet/core/testing/?pivots=xunit)」ドキュメントを参照してください。

## <a name="running-tests"></a>テストを実行する
**[単体テスト]** ウィンドウは単体テストの実行に使用され、 **[表示]、[パッド]、[単体テスト]** メニューの順に選択して開きます。 ソリューションの単体テストが自動的に検出され、このウィンドウに表示されます。このウィンドウでは、すべてのテストを実行するか、選択した一連のテストを実行できます。

![テスト ウィンドウに、単体テストの一覧と、テストを実行したり、停止したりするためのツール バーが表示されています。](media/test-window.PNG)

単体テストが含まれる C# クラスを編集するとき、テスト クラスまたはテスト メソッド内で右クリックし、 **[テストの実行]** または **[テストのデバッグ]** メニューを選択することでテストを実行できます。 メニュー項目の **[テストの実行]** を選択すると、テスト ウィンドウでテストが実行されます。 **[テストのデバッグ]** メニューを選択すると同じことが行われ、さらにデバッガーがアタッチされるのでコードの問題を解決できます。

![エディターの右クリック メニューの [テストの実行] オプションと [テストのデバッグ] オプション](media/run-tests-context-menu.PNG)

テストの実行中、 **[テスト結果]** ウィンドウが表示されます。成功したテストや失敗したテストを見直したり、そのようなテストの実行からの出力を確認したりできます。

![テスト結果ウィンドウに失敗したテストが 1 つ表示されています。合格したテストの数は 21 で、失敗したテストの数は 1 です。](media/test-results-window.PNG)

## <a name="see-also"></a>関連項目

- [.NET Core と .NET Standard の単体テスト](/dotnet/core/testing)
- [単体テストの概要 (Windows 上の Visual Studio)](/visualstudio/test/getting-started-with-unit-testing)
- [単体テストの基本 (Windows 上の Visual Studio)](/visualstudio/test/unit-test-basics)
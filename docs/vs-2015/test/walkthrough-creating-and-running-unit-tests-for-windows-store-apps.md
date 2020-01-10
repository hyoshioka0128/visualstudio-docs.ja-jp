---
title: 'チュートリアル: Windows ストア アプリに対する単体テストの作成と実行 | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- unit tests, creating
- unit tests
- unit tests, Windows Store apps
- unit tests, running
ms.assetid: dd3e8a6a-b366-433e-a409-b9a9b89da89a
caps.latest.revision: 23
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f5e62fe83d644b577d7d0a5f87312642f438c490
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75851181"
---
# <a name="walkthrough-creating-and-running-unit-tests-for-windows-store-apps"></a>チュートリアル: Windows ストア アプリに対する単体テストの作成と実行
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio には、 [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] マネージド アプリの単体テストのサポートと、Visual C#、Visual Basic、および Visual C++ 用の単体テスト ライブラリ テンプレートが含まれています。

> [!TIP]
> [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] アプリの開発の詳細については、「 [Windows ストア アプリ開発の開始](https://msdn.microsoft.com/windows/apps/br211386.aspx)」を参照してください。

 Visual Studio は、次の単体テスト機能を備えています。

- [単体テスト プロジェクトの作成](#CreateAndRunUnitTestWin8Tailored_Create)

- [単体テスト プロジェクトのマニフェストを編集します。](#CreateAndRunUnitTestWin8Tailored_Manifest)

- [単体テストのコーディング](#CreateAndRunUnitTestWin8Tailored_Code)

- [単体テストの実行](#CreateAndRunUnitTestWin8Tailored_Run)

  次の手順は、管理された Windows 8 [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] アプリケーションに対して、単体テストを作成、実行、およびデバッグする手順について説明します。

## <a name="prerequisites"></a>[前提条件]
 Visual Studio

## <a name="CreateAndRunUnitTestWin8Tailored_Create"></a> 単体テスト プロジェクトの作成

#### <a name="to-create-a-unit-test-project-for-a-windows-store-app"></a>Windows ストア アプリの単体テスト プロジェクトを作成するには

1. **[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。

     [新しいプロジェクト] ダイアログ ボックスが表示されます。

2. テンプレートで、単体テストを作成するプログラミング言語を選択した後、関連する [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] 単体テスト ライブラリを選択します。 たとえば、 **[Visual C#]** 、 **[Windows ストア]** 、 **[単体テスト ライブラリ (Windows ストア アプリ)]** の順に選択します。

    > [!NOTE]
    > Visual Studio には、Visual C#、Visual Basic、および Visual C++ 用の単体テスト ライブラリ テンプレートがあります。

3. (省略可能) **[名前]** テキストボックスで、 [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)]の単体テスト プロジェクトで使用する名前を入力します。

4. (省略可能) **[位置]** テキストボックスにデータを入力するか、 **[参照]** ボタンを選択することにより、プロジェクトを作成する場所のパスを変更します。

5. (省略可能) **[ソリューション]** 名テキストボックスに、ソリューションで使用する名前を入力します。

6. **[ソリューションのディレクトリを作成]** をクリックしたまま、 **[OK]** をクリックします。

     ![調整した単体テストライブラリ](../test/media/unit-test-win8-1.png "Unit_Test_Win8_1")

     ソリューション エクスプローラーに新しい [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)]単体テスト プロジェクトが設定され、コード エディターに UnitTest1 という既定の単体テストが表示されます。

     ![新しい調整した単体テストプロジェクト](../test/media/unit-test-win8-unittestexplorer-newprojectcreated.png "Unit_Test_Win8_UnitTestExplorer_NewProjectCreated")

## <a name="CreateAndRunUnitTestWin8Tailored_Manifest"></a> 単体テスト プロジェクトのマニフェストを編集します。
 アプリケーションを実行するために必要な機能を提供するように単体テスト プロジェクトのマニフェストを編集する必要があります。

#### <a name="to-edit-the-unit-test-projects-windows-store-application-manifest-file"></a>単体テスト プロジェクトの Windows ストア アプリ マニフェスト ファイルを編集するには

1. ソリューション エクスプローラーで、新しい [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)]の単体テスト プロジェクト内の Package.appxmanifest ファイルを右クリックし、 **[開く]** を選択します。

     マニフェスト デザイナーが編集のために表示されます。

2. マニフェスト デザイナーで、 **[機能]** タブをクリックします。

3. **[機能]** リストで、単体テストを必要とする機能とコードを選択します。 たとえば、単体テストが必要で、テストするコードにインターネットにアクセスする機能が必要な場合は、 **[インターネット]** チェック ボックスをオンにします。

    > [!NOTE]
    > 選択する機能には、 [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] の単体テストが正しく機能するために必要な機能だけが含まれる必要があります。 機能は、テスト中の [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] アプリケーションの一部ではない機能を含む必要はなく、一般に、テスト対象の [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] アプリケーションに指定された機能のサブセットです。

     マニフェスト デザイナーの詳細については、「[マニフェスト デザイナーを使用した Windows 8.1 アプリ パッケージの構成](https://msdn.microsoft.com/library/24c58b7f-9c6d-41c3-b385-c1e8497d5b2d)」を参照してください。

     ![単体テストマニフェスト](../test/media/unit-test-win8.png "Unit_Test_Win8_")

## <a name="CreateAndRunUnitTestWin8Tailored_Code"></a> 単体テストのコーディング

#### <a name="to-code-the-unit-test-for-a-windows-store-app"></a>Windows ストア アプリの単体テストをコーディングするには

1. コード エディターで、単体テストを編集し、テストに必要なアサートとロジックを追加します。

     詳細については、MSDN ライブラリの「 [Assert クラスの使用](https://msdn.microsoft.com/library/ms182530.aspx) 」を参照してください。

## <a name="CreateAndRunUnitTestWin8Tailored_Run"></a> 単体テストの実行

#### <a name="to-build-the-solution-and-run-the-unit-test-using-test-explorer"></a>ソリューションをビルドしテスト エクスプローラーを使用して単体テストを実行するには

1. **[テスト]** メニューで **[Windows]** を選択し、 **[テスト エクスプローラー]** を選択します。

     テスト エクスプローラーが表示されます。テストは表示されません。

2. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。

     これで、単体テストが一覧に含まれます。

    > [!NOTE]
    > テスト エクスプローラーの単体テストの一覧を更新するソリューションをビルドする必要があります。

    > [!WARNING]
    > Visual Studio の既知の問題: テスト プロジェクトをビルドする前にテスト エクスプローラーを開く必要があります。

3. テスト エクスプローラーで、作成した単体テストを選択します。

    > [!TIP]
    > テスト エクスプローラーでは、 **[ソース]** の横のソース コードへのリンクが表示されます。

4. **[すべて実行]** をクリックします。

     ![単体テストエクスプローラー &#45;の実行単体テスト](../test/media/unit-test-win8-unittestexplorer-contextmenurun.png "Unit_Test_Win8_UnitTestExplorer_ContextMenuRun")

    > [!TIP]
    > エクスプローラーに一覧表示された 1 つ以上の単体テストを選択し、 **[選択したテストの実行]** を右クリックして選択します。
    >
    >  また、 **[選択されたテストをデバッグ]** 、 **[テストを開く]** をクリックし、 **[プロパティ]** オプションを使用できます。
    >
    >  ![単体テストエクスプローラー &#45;の uni テストコンテキストメニュー](../test/media/unit-test-win8-unittestexplorer-contextmenu.png "Unit_Test_Win8_UnitTestExplorer_ContextMenu")

     単体テストが実行されます。 完了すると、テスト エクスプローラーは、テストの状態、経過時間、およびソースへのリンクを表示します。

     ![単体テストエクスプローラー &#45;のテストが完了しました](../test/media/unit-test-win8-unittestexplorer-done.png "Unit_Test_Win8_UnitTestExplorer_Done")

## <a name="external-resources"></a>外部資料

### <a name="videos"></a>Videos
 [Channel 9: XAML を使用した Windows ストア アプリのビルドの単体テスト](https://channel9.msdn.com/Events/BUILD/BUILD2011/TOOL-529T)

### <a name="forums"></a>Forums
 [Visual Studio の単体テスト](https://social.msdn.microsoft.com/Forums/en/vsunittest/threads)

### <a name="msdn-library"></a>MSDN ライブラリ
 [MSDN ライブラリ – 既存コードの単体テストの作成と実行 (Visual Studio 2010)](https://msdn.microsoft.com/library/hh270865(v=vs.110).aspx)

## <a name="see-also"></a>参照
 [Visual Studio を使用したストアアプリのテスト](../test/testing-store-apps-with-visual-studio.md) [Team Foundation ビルドを使用した Windows ストアアプリのビルドとテスト](https://msdn.microsoft.com/library/d0ca17bb-deae-4f3d-a18d-1a99bebceaa9)

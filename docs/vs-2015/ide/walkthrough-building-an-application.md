---
title: 'チュートリアル: アプリケーションをビルドする | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 4842955d-8959-4e4e-98b8-2358360179b3
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f2d9b958dacfb35877abc9ad1e83a349e43a7af0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "74296870"
---
# <a name="walkthrough-building-an-application"></a>チュートリアル: アプリケーションをビルドする

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルを完了すると、Visual Studio を使用してアプリケーションをビルドする際に構成できるオプションの使用方法を習得できます。 サンプル アプリケーション用に、カスタムのビルド構成の作成、特定の警告メッセージの非表示設定、ビルド出力情報の拡張などを行います。

このトピックには、次のセクションが含まれます。

[サンプルアプリケーションをインストールする](../ide/walkthrough-building-an-application.md)

[カスタムビルド構成を作成する](../ide/walkthrough-building-an-application.md#BKMK_CreateBuildConfig)

[アプリケーションをビルドする](../ide/walkthrough-building-an-application.md#BKMK_building)

[コンパイラ警告の非表示](../ide/walkthrough-building-an-application.md#BKMK_hidewarning)

[出力ウィンドウに追加のビルド詳細を表示する](../ide/walkthrough-building-an-application.md#BKMK_outputdetails)

[リリースビルドを作成する](../ide/walkthrough-building-an-application.md)

#### <a name="to-install-the-sample-application"></a>サンプル アプリケーションをインストールするには

1. メニュー バーで、**[ツール]**、**[拡張機能と更新プログラム]** の順にクリックします。

2. **[オンライン]** カテゴリ、**[サンプル ギャラリー]** カテゴリの順にクリックします。

3. 検索ボックスに「`Introduction`」と指定してサンプルを検索します。

    ![[拡張機能と更新プログラム] ダイアログ ボックス](../ide/media/buildwalk-extensionsdialogsampledownload.png "BuildWalk_ExtensionsDialogSampleDownload")

4. 結果リストで、**Introduction to Building WPF Applications (Visual C#)** または **Introduction to Building WPF Applications (Visual Basic)** を選択します。

5. **[ダウンロード]**、**[閉じる]** の順にクリックします。

   Introduction to Building WPF Applications サンプルが、**[新しいプロジェクト]** ダイアログ ボックスに表示されます。

#### <a name="to-create-a-solution-for-the-sample-application"></a>サンプル アプリケーションのソリューションを作成するには

1. **[新しいプロジェクト]** ダイアログ ボックスを開きます。

     ![メニューバーで、[ファイル]、[新規作成]、[プロジェクト] の順に選択します。](../ide/media/exploreide-filenewproject.png "Exploreide-newprojectcsharp-FileNewProject")

2. **[インストール済み]** カテゴリの **[サンプル]** カテゴリを選択して、Introduction to Building WPF Applications サンプルを表示します。

3. ソリューションに「`IntroWPFcsharp`」という名前を付けます (Visual C# 用)。

     ![[新しいプロジェクト] ダイアログ ボックス、インストールされているサンプル](../ide/media/buildwalk-newprojectdlgintrotowpfsample.png "BuildWalk_NewProjectdlgIntrotoWPFsample")

     OR

     ソリューションに「`IntroWPFvb`」という名前を付けます (Visual Basic 用)。

     ![[新しいプロジェクト] ダイアログ ボックス、Visual Basic サンプル](../ide/media/buildwalk-newprojectdlgintrotowpfsamplevb.png "BuildWalk_NewProjectdlgIntrotoWPFsampleVB")

4. **[OK]** を選択します。

## <a name="create-a-custom-build-configuration"></a><a name="BKMK_CreateBuildConfig"></a> カスタムビルド構成を作成する

ソリューションを作成すると、デバッグ ビルド構成およびリリース ビルド構成と、これらの既定のプラットフォーム ターゲットがソリューションに対して自動的に定義されます。 これらの構成をカスタマイズすることも、独自に作成することもできます。 ビルド構成では、ビルドの種類を指定します。 ビルド プラットフォームでは、その構成でアプリケーションが対象とするオペレーティング システムを指定します。 詳細については、「[Understanding Build Configurations](../ide/understanding-build-configurations.md)」(ビルド構成の概要)、「[Understanding Build Platforms](../ide/understanding-build-platforms.md)」(ビルド プラットフォームの概要)、「[デバッグ構成およびリリース プロジェクト構成](https://msdn.microsoft.com/0440b300-0614-4511-901a-105b771b236e)」を参照してください。

**[構成マネージャー]** ダイアログ ボックスを使用すると、構成とプラットフォームの設定を変更または作成できます。 この手順では、テスト用のビルド構成を作成します。

#### <a name="to-create-a-build-configuration"></a>ビルド構成を作成するには

1. **[構成マネージャー]** ダイアログ ボックスを開きます。

    ![[ビルド] メニュー、[構成マネージャー] コマンド](../ide/media/buildwalk-configurationmanagerdialogbox.png "BuildWalk_ConfigurationManagerDialogBox")

2. [ **アクティブソリューション構成** ] ボックスの一覧の [ **新規作成**] をクリックします。

3. **[新しいソリューション構成]** ダイアログ ボックスで、新しい構成の名前として「`Test`」と入力し、既存のデバッグ構成から設定をコピーして、**[OK]** を選びます。

    ![[新しいソリューション構成] ダイアログ ボックス](../ide/media/buildwalk-newsolutionconfigdlgbox.png "BuildWalk_NewSolutionConfigDlgBox")

4. [ **アクティブソリューションプラットフォーム** ] ボックスの一覧の [ **新規作成**] をクリックします。

5. **[新しいソリューション プラットフォーム]** ダイアログ ボックスで、**[x64]** を選択します。x86 プラットフォームの設定はコピーしません。

    ![[新しいソリューション プラットフォーム] ダイアログ ボックス](../ide/media/buildwalk-newsolutionplatform.png "BuildWalk_NewSolutionPlatform")

6. **[OK]** を選択します。

   アクティブなソリューション構成が Test に変更され、アクティブなソリューション プラットフォームが x64 に設定されました。

   ![テスト構成を使用した構成マネージャー](../ide/media/buildwalk-configmanagertestconfig.png "BuildWalk_ConfigManagerTestconfig")

   **[標準]** ツール バーの **[ソリューション構成]** ボックスの一覧を使用すると、アクティブなソリューション構成を簡単に確認または変更することができます。

   ![[ソリューション構成] オプション (標準ツール バー)](../ide/media/buildwalk-standardtoolbarsolutioncongfig.png "BuildWalk_StandardToolbarSolutionCongfig")

## <a name="build-the-application"></a><a name="BKMK_building"></a> アプリケーションをビルドする

次に、カスタム ビルド構成を使用してソリューションをビルドします。

#### <a name="to-build-the-solution"></a>ソリューションをビルドするには

- メニュー バーの **[ビルド]**、 **[ソリューションのビルド]** の順にクリックします。

  **[出力]** ウィンドウに、ビルドの結果が表示されます。 ビルドは成功していますが、複数の警告メッセージが生成されました。

  図 1: Visual Basic の警告

  ![出力ウィンドウ、Visual Basic](../ide/media/buildwalk-vbbuildoutputwnd.png "BuildWalk_VBBuildOutputWnd")

  図 2: Visual C# の警告

  ![Visual C&#35;の出力ウィンドウ ](../ide/media/buildwalk-csharpbuildoutputwnd.png "BuildWalk_CsharpBuildOutputWnd")

## <a name="hide-compiler-warnings"></a><a name="BKMK_hidewarning"></a> コンパイラ警告の非表示

ビルド出力が見やすくなるように、ビルド時に特定の警告メッセージを一時的に非表示にすることができます。

#### <a name="to-hide-a-specific-visual-c-warning"></a>Visual C# の特定の警告を非表示にするには

1. **ソリューション エクスプローラー**で、最上位のプロジェクト ノードを選択します。

2. メニュー バーの **[表示]**、 **[プロパティ ページ]** の順にクリックします。

     **プロジェクト デザイナー**が開きます。

3. **[ビルド]** ページを選択し、**[警告の表示なし]** ボックスで、警告番号 `1762` を指定します。

     ![[ビルド] ページ (プロジェクトデザイナー)](../ide/media/buildwalk-csharpsuppresswarnings.png "BuildWalk_CsharpSuppressWarnings")

     詳細については、「[Build Page, Project Designer (C#)](../ide/reference/build-page-project-designer-csharp.md)」([ビルド] ページ (プロジェクト デザイナー) (C#)) を参照してください。

4. ソリューションをビルドします。

     **[出力]** ウィンドウには、ビルドの概要情報のみが表示されます。

     ![出力ウィンドウ、Visual C&#35; ビルドの警告](../ide/media/buildwalk-visualcsharpbuildwarnings.png "BuildWalk_VisualCsharpBuildWarnings")

#### <a name="to-suppress-all-visual-basic-build-warnings"></a>Visual Basic のすべてのビルド警告を非表示にするには

1. **ソリューション エクスプローラー**で、最上位のプロジェクト ノードを選択します。

2. メニュー バーの **[表示]**、 **[プロパティ ページ]** の順にクリックします。

    **プロジェクト デザイナー**が開きます。

3. **[コンパイル]** ページで、**[すべての警告を表示しない]** チェック ボックスをオンにします。

    ![[コンパイル] ページ、[プロジェクト デザイナー]](../ide/media/buildwalk-vbsuppresswarnings.png "BuildWalk_VBSuppressWarnings")

    詳細については、「 [Visual Basic での警告の構成](../ide/configuring-warnings-in-visual-basic.md)」を参照してください。

4. ソリューションをビルドします。

   **[出力]** ウィンドウには、ビルドの概要情報のみが表示されます。

   ![出力ウィンドウ、Visual Basic ビルド警告](../ide/media/buildwalk-visualbasicbuildwarnings.png "BuildWalk_VisualBasicBuildWarnings")

   詳細については、「 [方法: コンパイラの警告を非表示にする](../ide/how-to-suppress-compiler-warnings.md)」を参照してください。

## <a name="display-additional-build-details-in-the-output-window"></a><a name="BKMK_outputdetails"></a> 出力ウィンドウに追加のビルド詳細を表示する

**[出力]** ウィンドウに表示されるビルド プロセスに関する情報量を変更できます。 ビルドの詳細度は通常、[最小] に設定されます。つまり、[ **出力** ] ウィンドウには、ビルド処理の概要と、優先度の高い警告またはエラーが表示されます。 [ [オプション] ダイアログボックス、[プロジェクトおよびソリューション]、[ビルドと実行](../ide/reference/options-dialog-box-projects-and-solutions-build-and-run.md)] の順に選択すると、ビルドに関する詳細情報を表示できます。

> [!IMPORTANT]
> 詳細情報を表示する場合は、ビルドの完了までにかかる時間が長くなります。

#### <a name="to-change-the-amount-of-information-in-the-output-window"></a>[出力] ウィンドウの情報量を変更するには

1. **[オプション]** ダイアログ ボックスを開きます。

    ![[ツール] メニューの [オプション] コマンド](../ide/media/exploreide-toolsoptionsmenu.png "Exploreide-newprojectcsharp-ToolsOptionsmenu")

2. **[プロジェクトおよびソリューション]** カテゴリを選択し、**[ビルド/実行]** ページを選択します。

3. **[MSBuild プロジェクト ビルドの出力の詳細]** ボックスの一覧の **[標準]** を選択し、**[OK]** をクリックします。

4. メニュー バーで、**[ビルド]**、**[ソリューションのクリーン]** の順にクリックします。

5. ソリューションをビルドし、**[出力]** のウィンドウの情報をレビューします。

    ビルド情報には、ビルドの開始時刻 (出力の先頭にあります)、ファイルが処理された順序、プロセスの完了までにかかった時間 (出力の末尾にあります) が含まれています。 この情報には、ビルド時に Visual Studio で実行される実際のコンパイラ構文も含まれています。

    たとえば、Visual C# のビルドの場合、[/nowarn](https://msdn.microsoft.com/library/7ebf2106-0652-4fdc-bf60-70fc86465d83) オプションには、このトピックで指定した警告コード 1762 が、他の 3 つの警告と共に示されます。

    Visual Basic のビルドの場合、[/nowarn](https://msdn.microsoft.com/library/7ebf2106-0652-4fdc-bf60-70fc86465d83) には除外する特定の警告が含まれていないため、警告は表示されません。

   > [!TIP]
   > Ctrl + F キーを押して [**検索**] ダイアログボックスを表示すると、[**出力**] ウィンドウの内容を検索できます。

   詳細については、[ビルド ログ ファイルを表示、保存、および構成する](../ide/how-to-view-save-and-configure-build-log-files.md)」を参照してください。

## <a name="create-a-release-build"></a>リリース ビルドを作成する

出荷用に最適化されたバージョンとしてサンプル アプリケーションをビルドすることができます。 リリース ビルドでは、ビルドの開始前に実行可能ファイルをネットワーク共有にコピーすることを指定します。

詳細については、「[How to: Change the Build Output Directory](../ide/how-to-change-the-build-output-directory.md)」(方法: ビルドの出力ディレクトリを変更する) と「[Building and Cleaning Projects and Solutions in Visual Studio](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)」(Visual Studio のプロジェクトとソリューションのビルドと消去) を参照してください。

#### <a name="to-specify-a-release-build-for-visual-basic"></a>Visual Basic 用にリリース ビルドを指定するには

1. **プロジェクト デザイナー**を開きます。

     ![[表示] メニュー、[プロパティ ページ] コマンド](../ide/media/buildwalk-viewpropertypages.png "BuildWalk_ViewPropertyPages")

2. **[コンパイル]** ページをクリックします。

3. **[構成]** ボックスの一覧の **[リリース]** をクリックします。

4. **[プラットフォーム]** ボックスの一覧の **[x86]** をクリックします。

5. **[ビルド出力パス]** ボックスに、ネットワーク パスを指定します。

     たとえば、「\\\myserver\builds」のように指定できます。

    > [!IMPORTANT]
    > メッセージ ボックスが表示され、指定したネットワーク共有が信頼できる場所ではない可能性があるという警告が示されることがあります。 指定した場所を信頼できる場合は、メッセージ ボックスの **[OK]** をクリックします。

6. アプリケーションをビルドします。

     ![[ビルド] メニューの [ソリューションのビルド] コマンド](../ide/media/exploreide-buildsolution.png "Exploreide-newprojectcsharp-BuildSolution")

#### <a name="to-specify-a-release-build-for-visual-c"></a>Visual C 用にリリース ビルドを指定するには\#

1. **プロジェクト デザイナー**を開きます。

    ![[表示] メニュー、[プロパティ ページ] コマンド](../ide/media/buildwalk-viewpropertypages.png "BuildWalk_ViewPropertyPages")

2. **[ビルド]** ページを選びます。

3. **[構成]** ボックスの一覧の **[リリース]** をクリックします。

4. **[プラットフォーム]** ボックスの一覧の **[x86]** をクリックします。

5. **[出力パス]** ボックスに、ネットワーク パスを指定します。

    たとえば、「\\\myserver\builds」のように指定できます。

   > [!IMPORTANT]
   > メッセージ ボックスが表示され、指定したネットワーク共有が信頼できる場所ではない可能性があるという警告が示されることがあります。 指定した場所を信頼できる場合は、メッセージ ボックスの **[OK]** をクリックします。

6. アプリケーションをビルドします。

    ![[ビルド] メニューの [ソリューションのビルド] コマンド](../ide/media/exploreide-buildsolution.png "Exploreide-newprojectcsharp-BuildSolution")

   指定したネットワーク パスに、実行可能ファイルがコピーされます。 このパスは \\\myserver\builds\\*FileName*.exe になります。

   これで、このチュートリアルを完了できました。

## <a name="see-also"></a>参照

- [チュートリアル: プロジェクトの構築 (C++)](https://msdn.microsoft.com/library/d459bc03-88ef-48d0-9f9a-82d17f0b6a4d)
- [ASP.NET Web アプリケーションプロジェクトのプリコンパイルの概要](https://msdn.microsoft.com/b940abbd-178d-4570-b441-52914fa7b887)
- [チュートリアル: MSBuild の使用](../msbuild/walkthrough-using-msbuild.md)

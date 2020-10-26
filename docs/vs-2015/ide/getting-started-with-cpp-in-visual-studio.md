---
title: C++ の概要
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 99c73344-86ba-4b08-9e15-f6111cc04185
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 001b394d86e56b172bb1a50c335bd8ba5bcacb15
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72645631"
---
# <a name="getting-started-with-c-in-visual-studio"></a>Visual Studio 内の C++ の概要
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルを完了すると、Visual Studio を使用してアプリケーションを開発する際に使用できるさまざまなツールおよびダイアログ ボックスの使用方法を習得できます。 簡単な "Hello, World" スタイルのアプリケーションを作成しながら、統合開発環境 (IDE) での作業方法について学習します。

 このトピックには、次のセクションが含まれます。

 [Visual Studio にサインインする](../ide/getting-started-with-cpp-in-visual-studio.md#BKMK_Configure)

 [単純なアプリケーションを作成する](../ide/getting-started-with-cpp-in-visual-studio.md#BKMK_CreateApp)

 [アプリケーションへのコードの追加](../ide/getting-started-with-cpp-in-visual-studio.md#BKMK_AddCode)

 [アプリケーションのデバッグとテスト](../ide/getting-started-with-cpp-in-visual-studio.md#BKMK_DebugTest)

 [アプリのリリース バージョンのビルド](../ide/getting-started-with-cpp-in-visual-studio.md#BKMK_BuildRelease)

## <a name="sign-in-to-visual-studio"></a><a name="BKMK_Configure"></a> Visual Studio にサインインする
 Visual Studio を初めて起動する際には、Live や Outlook などの Microsoft アカウントを使ってサインインする機会があります。 サインインすると、設定をすべてのデバイス間で同期できます。 詳細については、「 [Visual Studio へのサインイン](../ide/signing-in-to-visual-studio.md)」を参照してください。

 図 1: Visual Studio IDE

 ![Visual C&#43;&#43; 設定が適用された IDE](../ide/media/c-ide-defaultenvironmentlayout.png "C++ IDE_DefaultEnvironmentLayout")

 Visual Studio を開くと、IDE の 3 つの基本的なパーツを確認できます。ツール ウィンドウ、メニューとツール バー、およびメイン ウィンドウ領域です。 ツール ウィンドウは、アプリ ウィンドウの左側および右側にドッキングされており、上部には **[クイック起動]**、メニュー バー、および標準ツール バーがあります。 アプリケーション ウィンドウの中央には、 **[スタート ページ]** が表示されます。 ソリューションまたはプロジェクトを開くと、この領域にはエディターとデザイナーが表示されます。 アプリケーションを開発する場合は、ほとんどの時間をこの中央の領域での作業に費やします。

## <a name="create-a-simple-application"></a><a name="BKMK_CreateApp"></a> 単純なアプリケーションを作成する
 Visual Studio でアプリを作成するには、最初にプロジェクトおよびソリューションを作成します。 この例では、Windows コンソール アプリケーションを作成します。

#### <a name="to-create-a-console-app"></a>コンソール アプリを作成するには

1. メニュー バーで、 **[ファイル]** 、 **[新規作成]** 、 **[プロジェクト]** の順にクリックします。

    ![メニューバーで、[ファイル]、[新規作成]、[プロジェクト] の順に選択します。](../ide/media/exploreide-filenewproject.png "Exploreide-newprojectcsharp-FileNewProject")

2. **[Visual C++]** カテゴリで、**[Win32 コンソール アプリケーション]** テンプレートを選択し、プロジェクトに `GreetingsConsoleApp` という名前を付けます。

    ![Win32 コンソール アプリケーション テンプレート](../ide/media/c-ide-newprojectdlg.png "C++ IDE_NewProjectDlg")

3. Win32 アプリケーション ウィザードが表示されたら、 **[完了]** を選択します。

    ![Win32 コンソール アプリケーション ウィザード](../ide/media/c-ide-win32consoleappwizard.png "C++ IDE_Win32ConsoleAppWizard")

   Win32 コンソール アプリの基本的なファイルを含む GreetingsConsoleApp プロジェクトとソリューションが作成され、 **ソリューション エクスプローラー**に自動的に読み込まれます。 GreetingsConsoleApp.cpp ファイルがコード エディターで開きます。 次の項目が **ソリューション エクスプローラー**に表示されます。

   図 4: プロジェクト項目

   ![ソリューション エクスプローラーでのソリューションのファイル](../ide/media/c-ide-solutioncontents.png "C++ IDE_SolutionContents")

## <a name="add-code-to-the-application"></a><a name="BKMK_AddCode"></a> アプリケーションにコードを追加する
 次に、コンソール ウィンドウに "Hello" と表示するコードを追加します。

#### <a name="to-display-hello-in-the-console-window"></a>コンソール ウィンドウに "Hello" と表示するには

1. GreetingsConsoleApp.cpp ファイルの `return 0;` という行の前に空白行を挿入し、次のコードを入力します。

    ```
    cout << "Hello\n";
    ```

     `cout`の下に赤い波線が表示されます。 その波線をポイントすると、エラー メッセージが表示されます。

     ![cout のエラー テキスト](../ide/media/c-ide-couterror.png "C++ IDE_CoutError")

     エラー メッセージは、 **[エラー一覧]** ウィンドウにも表示されます。 そのウィンドウを表示するには、メニュー バーで **[表示]**、 **[エラー一覧]** の順に選択します。

     [cout](https://msdn.microsoft.com/library/d87db6c3-e4e1-4d09-9ec5-458f55018257) は、ヘッダーファイルに含まれてい \<iostream\> ます。

2. iostream ヘッダーを組み込むには、 `#include "stdafx.h"`の次に、以下のコードを入力します。

    ```
    #include \<iostream\>
    using namespace std;
    ```

     コードを入力したときにボックスが表示され、入力した文字に対応する候補が提示されたはずです。 このボックスは、C++ の IntelliSense の一部で、コーディングの一連のヒントを提供します。それには、クラスやインターフェイスのメンバーの一覧と、パラメーター情報が含まれます。 定義済みのコード ブロックであるコード スニペットを使用することもできます。 詳細については、 [Using IntelliSense](../ide/using-intellisense.md) および [Code Snippets](../ide/code-snippets.md)を参照してください。

     エラーを修正すると、 `cout` の下の赤い波線が消えます。

3. 変更をファイルに保存します。

     ![cout のエラーを修復するコード](../ide/media/c-ide-coutfix.png "C++ IDE_CoutFix")

## <a name="debug-and-test-the-application"></a><a name="BKMK_DebugTest"></a> アプリケーションのデバッグとテスト
 GreetingsConsoleApp をデバッグして、コンソール ウィンドウに "Hello" という語が表示されるかどうかを確認できます。

#### <a name="to-debug-the-application"></a>アプリケーションをデバッグするには

- デバッガーを起動します。

     ![[デバッグ] メニューの [デバッグの開始] コマンド](../ide/media/exploreide-startdebugging.png "Exploreide-newprojectcsharp-StartDebugging")

     デバッガーが起動し、コードが実行されます。 コンソール ウィンドウ (コマンド プロンプトのように見える別のウィンドウ) が数秒間表示されますが、デバッガーが実行を停止するとすぐに閉じます。 テキストを表示するには、ブレークポイントを設定してプログラムの実行を停止する必要があります。

#### <a name="to-add-a-breakpoint"></a>ブレークポイントを追加するには

1. メニュー バーからブレークポイントを `return 0;`の行に追加します。 左側の余白内でクリックするだけでも、ブレークポイントを設定できます。

    ![[デバッグ] メニューの [ブレークポイントの設定/解除] コマンド](../ide/media/exploreide-togglebreakpoint.png "Exploreide-newprojectcsharp-ToggleBreakpoint")

    コード行の横の、エディター ウィンドウの左端の余白部分に、赤い円が表示されます。

2. F5 キーを押してデバッグを開始します。

    デバッガーが起動し、コンソール ウィンドウが表示されて **Hello**という語が示されます。

    ![Windows のコマンド プロンプト ウィンドウに表示された文字列 "Hello"](../ide/media/c-ide-hellocommandwindow.png "C++ IDE_HelloCommandWindow")

3. SHIFT + F5 キーを押してデバッグを停止します。

   詳細については、[コンソール プロジェクト](../debugger/debugging-preparation-console-projects.md)に関する記事を参照してください。

## <a name="build-a-release-version-of-the-app"></a><a name="BKMK_BuildRelease"></a> アプリのリリースバージョンをビルドする
 すべてが機能することを確認したら、アプリケーションのリリース ビルドを準備できます。

#### <a name="to-clean-the-solution-files-and-build-a-release-version"></a>ソリューション ファイルをクリーンアップし、リリース バージョンをビルドするには

1. メニュー バーで、前のビルドで作成された中間ファイルと出力ファイルを削除します。

    ![[ビルド] メニューの [ソリューションのクリーン] コマンド](../ide/media/exploreide-cleansolution.png "Exploreide-newprojectcsharp-CleanSolution")

2. GreetingsConsoleApp のビルド構成を **[デバッグ]** から **[リリース]** に変更します。

    ![アプリケーションのリリース バージョンのビルド](../ide/media/c-ide-changingbuildtorelease.png "C++ IDE_ChangingBuildtoRelease")

3. ソリューションをビルドします。

    ![[ビルド] メニューの [ソリューションのビルド] コマンド](../ide/media/exploreide-buildsolution.png "Exploreide-newprojectcsharp-BuildSolution")

   このチュートリアルは完了しました。 その他の例については、「[Visual Studio Samples](../ide/visual-studio-samples.md)」を参照してください。

## <a name="see-also"></a>参照
 [チュートリアル: 簡単なアプリケーションの作成](../ide/walkthrough-create-a-simple-application-with-visual-csharp-or-visual-basic.md) [生産性に関するヒント](../ide/productivity-tips-for-visual-studio.md) [Visual Studio のサンプル](../ide/visual-studio-samples.md) [Visual Studio を使用した開発の開始](../ide/get-started-developing-with-visual-studio.md)

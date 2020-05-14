---
title: Razor Web アプリの作成
description: Visual Studio for Mac の ASP.NET Core アプリの Razor サポートに関する情報を提供します。
author: sayedihashimi
ms.author: sayedha
ms.date: 05/03/2018
ms.technology: vs-ide-general
ms.assetid: F898CB6E-05ED-44CD-8DB6-427B2592CCC6
ms.openlocfilehash: fe9ef921ccfc42b77bd08925805aeac6f4aec777
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "73715878"
---
# <a name="create-razor-web-apps"></a>Razor Web アプリの作成

このガイドでは、最初の Razor Web アプリの作成に関する概要について説明します。 詳しいガイダンスが必要であれば、「[ASP.NET Core での Razor ページの概要](/aspnet/core/razor-pages/index)」を参照してください。

Visual Studio for Mac には、 *.cshtml* ファイルでの IntelliSense や構文の強調表示など、Razor 編集のサポートが用意されています。 Visual Studio 2019 for Mac 8.3+ の新機能として、Razor ファイル内で IntelliSense がコンテキストを認識できるようになりました。ドキュメント内で現在編集中の言語に一致する IntelliSense が表示されます。

![Visual Studio for Mac での Razor 編集](media/razor-2019.png)

## <a name="creating-a-new-razor-project"></a>新しい Razor プロジェクトの作成

1. ようこそ画面で、 **[新規]** を選択して新しいプロジェクトを作成します。

   ![Visual Studio for Mac での新しいプロジェクト](media/razor-new.png)
1. **[新しいプロジェクト]** ダイアログ ボックスで、 **[.NET Core]** 、 **[アプリ]** 、 **[Web アプリケーション]** の順に移動し、 **[次へ]** ボタンをクリックします。

   ![Razor プロジェクト テンプレート](media/razor-new-project1.png)
1. お使いの .NET Core ターゲット フレームワークを選択し (バージョン 2.2 以降推奨)、 **[次へ]** を選択します。 自分のプロジェクトの名前を選択し、必要に応じて Git サポートを追加します。 **[作成]** を選択して、プロジェクトを作成します。

   ![Razor プロジェクト名](media/razor-new-project2.png)

   Visual Studio for Mac により、お客様のプロジェクトがコード レイアウト ウィンドウで開かれます。
1. **Command + Option + F5** キーを使用し、デバッグなしでプロジェクトを実行します。

   Visual Studio で [Kestrel](/aspnet/core/fundamentals/servers/kestrel) が起動し、ブラウザーが開いて `https://localhost:5001` にアクセスし、初めての Razor Web アプリが表示されます。

   ![Safari での Razor Web アプリ](media/razor-webapp.png)

## <a name="project-anatomy"></a>プロジェクトの構造

Razor Web アプリには次の構成要素が含まれています。

### <a name="pages-folder"></a>Pages フォルダー

このフォルダーには、プロジェクトの Web ページと各ページのコードビハインドが含まれています。
   - HTML マークアップと Razor 構文のための " *\*.cshtml*" ファイル。
   - ページ イベントを処理するための C# コードビハインドの " *\*.cshtml.cs*" ファイル。

サポート ファイルには、アンダー スコアで始まる名前が付けられます。 たとえば、_Layout.cshtml ファイルでは、すべてのページに共通の UI 要素が構成されます。 このファイルでは、ページの上部に表示されるナビゲーション メニューと下部に表示される著作権の通知が設定されます。 詳細については、「[ASP.NET Core でのレイアウト](/aspnet/core/mvc/views/layout)」をご覧ください。

### <a name="launch-settings"></a>起動設定

*launchSettings.json* ファイルには、IIS 設定、アプリケーションの URL、その他の関連する設定が含まれています。

### <a name="app-settings"></a>アプリの設定

*appSettings.json* ファイルには、接続文字列などの構成データが含まれています。

構成について詳しくは、[ASP.NET での構成ガイド](/aspnet/core/fundamentals/configuration/index)に関する記事をご覧ください。

### <a name="wwwroot-folder"></a>wwwroot フォルダー

このフォルダーには、HTML ファイル、JavaScript ファイル、CSS ファイルなど、静的ファイルが含まれています。 詳細については、「[ASP.NET Core の静的ファイル](/aspnet/core/fundamentals/static-files)」をご覧ください。

### <a name="programcs"></a>Program.cs

このファイルには、プログラムのエントリ ポイントが含まれています。 詳細については、「[ASP.NET Core の Web ホスト](/aspnet/core/fundamentals/host/web-host)」をご覧ください。

### <a name="startupcs"></a>Startup.cs

このファイルには、cookie に対する同意をアプリで要求するかなど、アプリの動作を構成するコードが含まれています。 詳細については、「[ASP.NET Core でのアプリケーションのスタートアップ](/aspnet/core/fundamentals/startup)」をご覧ください。

## <a name="see-also"></a>関連項目

Razor Web アプリの作成に関するより包括的なガイドについては、「[ASP.NET Core での Razor ページの概要](/aspnet/core/razor-pages/index)」をご覧ください。

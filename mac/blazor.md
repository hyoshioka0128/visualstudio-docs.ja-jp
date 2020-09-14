---
title: Blazor Web アプリを作成する
description: Visual Studio for Mac の ASP.NET Core アプリの Blazor サポートに関する情報を提供します。
author: jongalloway
ms.author: jogallow
ms.date: 08/31/2020
ms.technology: vs-ide-general
ms.assetid: D2717D3A-9225-40A8-8155-7D0143B2CA60
no-loc:
- Blazor
- Blazor WebAssembly
ms.topic: how-to
ms.openlocfilehash: 0dcc254366e0d652ab7a8442a4d0c526fd72c403
ms.sourcegitcommit: 703c68667261df5985a73282c1cbb0541118989c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402532"
---
# <a name="create-no-locblazor-web-apps"></a>Blazor Web アプリを作成する

このガイドでは、最初の Blazor Web アプリの作成に関する概要について説明します。 詳細なガイダンスについては、「[ASP.NET Core Blazor の概要](/aspnet/core/blazor/index)」を参照してください。

ASP.NET Core Blazor では、2 つの異なるホスティング オプションである Blazor WebAssembly (WASM) または Blazor サーバーがサポートされています。 Visual Studio for Mac では両方のホスティング モデルがサポートされています。 Visual Studio for Mac 8.4 + では Blazor Server がサポートされており、Visual Studio for Mac 8.6 + では両方がサポートされています。 Blazor ホスティング モデルの詳細については、「[ASP.NET Core Blazor のホスティング モデル](https://docs.microsoft.com/aspnet/core/blazor/hosting-models?view=aspnetcore-3.1)」を参照してください。 Visual Studio for Mac での Blazor WebAssembly プロジェクトのデバッグのサポートは、v8.8 のプレビュー リリースで利用できます ( **[Visual Studio] > [更新プログラムの確認]** メニューのプレビュー更新プログラム チャネルで利用可能)。

Blazor の概要 Blazor は、.NET を使って対話型のクライアント側 Web UI を構築するためのフレームワークです。Web 開発者にとって次のような利点があります。

* JavaScript ではなく C# でコードを記述します。
* .NET ライブラリの既存の .NET エコシステムを活用します。
* サーバーとクライアント全体でアプリ ロジックを共有します。
* .NET のパフォーマンス、信頼性、およびセキュリティから利点が得られます。
* PC、Linux、macOS 上の Visual Studio を使って生産性を維持します。
* 多機能で使いやすい安定した言語、フレームワーク、およびツールの共通セットに基づいて構築します。

## <a name="create-a-new-no-locblazor-webassembly-project"></a>新しい Blazor WebAssembly プロジェクトを作成する
1. **[スタート ウィンドウ]** で、 **[新規]** を選択して新しいプロジェクトを作成します。

   ![[新規] 選択項目が強調表示されている Visual Studio for Mac のスタート ウィンドウ](media/blazor-new-project.png)

1. **[新しいプロジェクト]** ダイアログ ボックスで、 **[.NET Core]** > **[アプリ]** > **[Blazor WebAssembly アプリ]** の順に選択し、 **[次へ]** を選択します。![Blazor サーバー アプリ テンプレートが選択された [新しいプロジェクト用のテンプレートの選択] ダイアログ](media/blazor-wasm-project-template.png)

1. ターゲット フレームワークとして .NET Core 3.1 を選択し、 **[次へ]** を選択します。 
   ![ターゲット フレームワークとして .NET Core 3.1 が選択された [新しい Blazor WebAssembly アプリの構成] ダイアログ](media/blazor-wasm-select-target-framework.png)

1. 使用するプロジェクトの名前を選び、必要な場合は Git サポートを追加します。 **[作成]** を選択して、プロジェクトを作成します。
    ![プロジェクト名の入力中に表示される [新しい Blazor WebAssembly アプリの構成] ダイアログ](media/blazor-wasm-name-project.png)

   Visual Studio for Mac により、お客様のプロジェクトがコード レイアウト ウィンドウで開かれます。

1. **[実行]**  >  **[デバッグなしで開始]** の順に選択して、アプリを実行します。

   Visual Studio によって [Kestrel](/aspnet/core/fundamentals/servers/kestrel) が起動され、ブラウザーで`https://localhost:5001` が開かれ、Blazor Web アプリが表示されます。

   ![Microsoft Edge での Blazor Web アプリ](media/blazor-new-app-in-edge.png)

## <a name="creating-a-new-no-locblazor-server-project"></a>新しい Blazor Server プロジェクトの作成

1. **[スタート ウィンドウ]** で、 **[新規]** を選択して新しいプロジェクトを作成します。

   ![[新規] 選択項目が強調表示されている Visual Studio for Mac のスタート ウィンドウ](media/blazor-new-project.png)
1. **[新しいプロジェクト]** ダイアログ ボックスで、 **[.NET Core]** > **[アプリ]** > **[Blazor サーバー アプリ]** の順に選択し、 **[次へ]** を選択します。![Blazor サーバー アプリ テンプレートが選択された [新しいプロジェクト用のテンプレートの選択] ダイアログ](media/blazor-project-template.png)

1. ターゲット フレームワークとして .NET Core 3.1 を選択し、 **[次へ]** を選択します。 
   ![ターゲット フレームワークとして .NET Core 3.1 が選択された [新しい Blazor サーバー アプリの構成] ダイアログ](media/blazor-select-target-framework.png)

1. 使用するプロジェクトの名前を選び、必要な場合は Git サポートを追加します。 **[作成]** を選択して、プロジェクトを作成します。
   ![ターゲット フレームワークとして .NET Core 3.1 が選択された [新しい Blazor サーバー アプリの構成] ダイアログ](media/blazor-name-project.png)

   Visual Studio for Mac により、お客様のプロジェクトがコード レイアウト ウィンドウで開かれます。
1. **[実行]**  >  **[デバッグなしで開始]** の順に選択して、アプリを実行します。

   Visual Studio によって [Kestrel](/aspnet/core/fundamentals/servers/kestrel) が起動され、ブラウザーで`https://localhost:5001` が開かれ、Blazor Web アプリが表示されます。

   ![Microsoft Edge での Blazor Web アプリ](media/blazor-new-app-in-edge.png)

## <a name="no-locblazor-support-in-visual-studio-for-mac"></a>Visual Studio for Mac での Blazor のサポート

Visual Studio for Mac (バージョン 8.4 以降) には、新しい Blazor Server プロジェクトを作成するための新機能が含まれています。 また、Blazor プロジェクトのビルド、実行、デバッグなど、期待される標準サポートが提供されます。 Visual Studio for Mac 8.6 では、Blazor WebAssembly プロジェクトの作成、ビルド、実行のサポートが追加されました。

ここまでは、Blazor サーバー アプリ プロジェクト テンプレートを使用して、新しい Blazor サーバー アプリ プロジェクトまたは Blazor WebAssembly アプリ プロジェクトを作成する方法について説明しました。 Blazor プロジェクトの開発をサポートするための Visual Studio for Mac の追加機能をいくつか見てみましょう。

### <a name="editor-support-for-razor-files"></a>*.razor* ファイルのエディターのサポート
Visual Studio for Mac には、Blazor アプリケーションの作成時に使用するファイルの大部分を占める、.razor ファイルを編集するためのサポートが含まれています。 Visual Studio for Mac では、プロジェクトで宣言されている Razor コンポーネントの入力候補を含め、razor ファイルに対する完全な色付けと入力候補のサポートが提供されています。

![Blazor の Intellisense を表示する Visual Studio for Mac エディター ウィンドウ](media/blazor-intellisense.png)

### <a name="publishing-no-locblazor-applications-to-azure-app-service"></a>Blazor アプリケーションの Azure App Service への発行
Blazor アプリケーションを Azure App Service に直接発行することもできます。 Azure に Blazor アプリを実行するための Azure アカウントがない場合は、いつでも[こちらから無料でサインアップする](https://azure.microsoft.com/free)ことができます。サインアップすると、人気のあるサービスへの 12 か月間無料のアクセス、200 ドル分の無料 Azure クレジット、25 以上のサービスへの常時無料のアクセスの特典を受けることができます。

![Azure の発行エクスペリエンスを示す Visual Studio for Mac](media/blazor-azure-publish.png)

## <a name="project-anatomy"></a>プロジェクトの構造

Blazor Web アプリには、既定でいくつかのディレクトリとファイルが含まれています。 使用を開始する際に理解しておく必要がある主なものは、次のとおりです。

### <a name="pages-folder"></a>Pages フォルダー

このフォルダーには、プロジェクトの Web ページが含まれています。 *.razor* ファイル拡張子が使用されています。

### <a name="shared-folder"></a>Shared フォルダー

このフォルダーには、共有コンポーネントが含まれています。やはり *.razor* 拡張子が使用されています。 これには *MainLayout.razor* が含まれています。これは、アプリケーション全体で共通のレイアウトを定義するために使用されます。 また、共有 *NavMenu.razor* コンポーネントも含まれています。これはすべてのページで使用されます。 再利用可能なコンポーネントを作成している場合は、**Shared** フォルダーに含まれます。

### <a name="app-settings"></a>アプリの設定

*appSettings.json* ファイルには、接続文字列などの構成データが含まれています。

構成について詳しくは、[ASP.NET での構成ガイド](/aspnet/core/fundamentals/configuration/index)に関する記事をご覧ください。

### <a name="wwwroot-folder"></a>wwwroot フォルダー

このフォルダーには、HTML ファイル、JavaScript ファイル、CSS ファイルなど、静的ファイルが含まれています。 詳細については、「[ASP.NET Core の静的ファイル](/aspnet/core/fundamentals/static-files)」をご覧ください。

### <a name="programcs"></a>Program.cs

このファイルには、プログラムのエントリ ポイントが含まれています。 詳細については、「[ASP.NET Core の Web ホスト](/aspnet/core/fundamentals/host/web-host)」をご覧ください。

### <a name="no-locblazor-server-app-specific-files"></a>Blazor サーバー アプリ固有のファイル
#### <a name="app-settings"></a>アプリの設定

*appSettings.json* ファイルには、接続文字列などの構成データが含まれています。

構成について詳しくは、[ASP.NET での構成ガイド](/aspnet/core/fundamentals/configuration/index)に関する記事をご覧ください。

#### <a name="startupcs"></a>Startup.cs

このファイルには、cookie に対する同意をアプリで要求するかなど、アプリの動作を構成するコードが含まれています。 詳細については、「[ASP.NET Core でのアプリケーションのスタートアップ](/aspnet/core/fundamentals/startup)」をご覧ください。

## <a name="summary"></a>まとめ
このチュートリアルでは、Visual Studio for Mac で新しい Blazor サーバー アプリまたは Blazor WebAssembly アプリを作成する方法について説明しました。また、Blazor アプリケーションの作成に役立つ Visual Studio for Mac の機能の一部について説明しました。

## <a name="see-also"></a>関連項目

Blazor Web アプリの作成に関するより包括的なガイドについては、「[ASP.NET Core Blazor の概要](/aspnet/core/blazor/index)」をご覧ください。

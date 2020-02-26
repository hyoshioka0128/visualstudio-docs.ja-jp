---
title: '手順 2: 最初の ASP.NET Core Web アプリを作成する'
description: ASP.NET Core Web アプリを初めて作成するときは、このビデオ チュートリアルとステップ バイ ステップの手順に従って行います。
ms.custom: get-started
ms.date: 03/31/2019
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
monikerRange: vs-2019
ms.topic: tutorial
ms.devlang: CSharp
author: ardalis
ms.author: ornella
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: 1d382e83aa9672cfdcbdca64b89be79d090f2aac
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2020
ms.locfileid: "77580074"
---
# <a name="step-2-create-your-first-aspnet-core-web-app"></a>手順 2: 最初の ASP.NET Core Web アプリを作成する

ASP.NET Core Web アプリを初めて作成するときは、このビデオ チュートリアルとステップ バイ ステップの手順に従って行います。

_ASP.NET Core アプリを初めて作成するときは、このビデオをご覧になり、手順を理解してください。_

> [!VIDEO https://www.youtube.com/embed/-79RkpyFB6E]

## <a name="start-visual-studio-2019-and-create-a-new-project"></a>Visual Studio 2019 を起動して新しいプロジェクトを作成する

Visual Studio 2019 を起動し、 **[新しいプロジェクトの作成]** をクリックします。 **[ASP.NET Core Web アプリケーション]** を選択します。 **[Web アプリケーション]** テンプレートを選択し、既定のプロジェクト名と場所をそのまま使用します。 ASP.NET Core バージョンのドロップダウンで、 **[ASP.NET Core 2.1]** または **[ASP.NET Core 2.2]** を選択します。 **[作成]** をクリックします。 詳細な手順については、[このチュートリアル シリーズの前のビデオ](tutorial-aspnet-core-ef-step-01.md)をご覧ください。

![Visual Studio 2019 の ASP.NET Core プロジェクトのオプションの選択](media/vs-2019/vs2019-choose-aspnetcore-project.png)

> [!WARNING]
> ASP .NET Core 2.1 または ASP.NET Core 2.2 を選択していることを確認します。 このチュートリアルは ASP.NET Core 3.x と互換性がありません。

## <a name="explore-the-new-project"></a>新しいプロジェクトを調べる

右側の [ソリューション エクスプローラー] ウィンドウでは、新しいプロジェクトの内容を見ることができます。 以下ではそれについて説明します。

![Visual Studio 2019 ASP.NET Core プロジェクト](media/vs-2019/vs2019-solution-explorer.png)

### <a name="wwwroot"></a>wwwroot

*Wwwroot* フォルダーには、Web アプリケーションからパブリックにアクセス可能な静的ファイルが入っています。 通常、スタイルシート、クライアント側スクリプト ファイル、イメージが保持されています。

### <a name="pages"></a>Pages

*Pages* フォルダーには、サイトの Razor ページが入っています。 既定のテンプレートでは、アプリケーションのホーム ページである *Index.cshtml* や、バージョン情報、連絡先など、複数のページが提供されています。

### <a name="appsettingsjson"></a>appsettings.json

このファイルには、サイトの構成設定が JSON 形式で保持されています。

### <a name="programcs"></a>Program.cs

このファイルは、アプリケーションのエントリ ポイントとして機能します。 アプリを実行すると、その Main メソッドが最初のメソッドとして実行され、アプリケーションを含む Web ホストの作成を行います。

### <a name="startupcs"></a>Startup.cs

*Program.cs* で作成された Web ホストでは、Startup クラスが参照され、そのメソッドが呼び出されてアプリケーションが構成されます。 ConfigureServices メソッドで、アプリが使用するすべてのサービスのセットアップが行われます。 `Configure` メソッドでは、アプリの HTTP 要求パイプラインが設定されます。 各要求は、このパイプラインを通過して、"*ミドルウェア*" の各部分と相互作用します。

### <a name="indexcshtml"></a>Index.cshtml

サイトのホーム ページには、いくつかの HTML マークアップと、いくつかのサーバー側 Razor コードが含まれています。 Razor を使用してページ モデル `IndexModel` が指定され、それは関連付けられた *Index.cshtml.cs* ファイルに格納されます。 また、ViewData に値を設定することで、ページ タイトルが設定されます。 この ViewData の値は、Pages フォルダー内の共有フォルダーにある *\_Layout.cshtml* ファイルに読み取られます。 Layout ファイルは多くの Razor ページによって共有され、このファイルによりアプリケーションの共通のルック アンド フィールが提供されます。 各ページのコンテンツは、Layout ファイルの HTML 内にレンダリングされます。

## <a name="run-the-application"></a>アプリケーションの実行

それでは、アプリケーションを実行し、ブラウザーで表示します。 アプリケーションは、**Ctrl**+**F5** キーを押すか、Visual Studio のメニューから **[デバッグ]**  >  **[デバッグなしで開始]** を選択して、実行できます。

## <a name="customize-the-application"></a>アプリケーションをカスタマイズする

プロパティを *Index.cshtml.cs* ファイルに追加し、`OnGet` ハンドラーでその値に現在の時刻を設定します。

```csharp
public string Time { get; set; }
public void OnGet()
{
    Time = DateTime.Today.ToShortTimeString();
}
```

*Index.cshtml* の `<div>` の内容を、次のマークアップに置き換えます。

```cshtml
<h2>It's @Model.Time right now on the server!</h2>
```

アプリケーションをもう一度実行します。 ページに現在の時刻が表示されるようになりますが、常に午前 0 時です。 それでは正しくありません。

![ブラウザーでの Visual Studio 2019 ASP.NET Core プロジェクト](media/vs-2019/vs2019-app-in-browser.png)

## <a name="debug-the-application"></a>アプリケーションのデバッグ

`Time` に値を割り当てている `OnGet` メソッドにブレークポイントを追加し、今度はアプリケーションのデバッグを開始します。

実行がその行で停止し、`DateTime.Today` に日付が含まれていることを確認できますが、時刻データが含まれないため、時刻は常に午前 0 時です。 

![ブラウザーでの Visual Studio 2019 ASP.NET Core プロジェクト](media/vs-2019/vs2019-breakpoint.png)

`DateTime.Now` を使用するように変更し、実行を続けます。 `OnGet` の新しいコードは次のようになっているはずです。

```csharp
public void OnGet()
{
    Time = DateTime.Now.ToShortTimeString();
}
```

アプリに移動すると、今度はブラウザーにサーバーの実際の時刻が表示されます。

> [!NOTE]
> ToShortDateTimeString の出力形式は、現在のカルチャ設定によって異なるため、出力がこのイメージと異なる場合があります。 以下を参照してください。<xref:System.DateTime.ToShortTimeString>

![ブラウザーでの Visual Studio 2019 ASP.NET Core プロジェクト](media/vs-2019/vs2019-app-fixed-in-browser.png)

## <a name="next-steps"></a>次の手順

次のビデオでは、アプリにデータのサポートを追加する方法を学びます。

[チュートリアル: ASP.NET Core アプリでのデータの処理](tutorial-aspnet-core-ef-step-03.md)

## <a name="see-also"></a>関連項目

- [チュートリアル: ASP.NET Core で Razor Pages Web アプリを作成する](/aspnet/core/tutorials/razor-pages/?view=aspnetcore-2.1)

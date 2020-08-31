---
title: Entity Framework と Visual Studio 2019 を使った ASP.NET Core Web アプリ
titleSuffix: ''
description: ASP.NET Core Web アプリを作成する前に、まず、このビデオ チュートリアルとステップ バイ ステップの手順に従って Visual Studio 2019 をインストールする方法を学びます。
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
ms.openlocfilehash: f6d069bfa462b8aa75fc9247c08b3662c4a445fd
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88801803"
---
# <a name="tutorial-create-your-first-aspnet-core-app-using-entity-framework-with-visual-studio-2019"></a>チュートリアル: Entity Framework と Visual Studio 2019 を使用して、最初の ASP.NET Core アプリを作成する

このチュートリアルでは、データを使用する ASP.NET Core Web アプリを作成して、Azure にデプロイします。 このチュートリアルは、以下の手順から構成されています。

- [手順 1:Visual Studio 2019 をインストールする](#step-1-install-visual-studio-2019)
- [手順 2:最初の ASP.NET Core Web アプリを作成する](tutorial-aspnet-core-ef-step-02.md)
- [手順 3:Entity Framework を使用してデータを処理する](tutorial-aspnet-core-ef-step-03.md)
- [手順 4:ASP.NET Core アプリから Web API を公開する](tutorial-aspnet-core-ef-step-04.md)
- [手順 5:Azure に ASP.NET Core アプリをデプロイする](tutorial-aspnet-core-ef-step-05.md)

## <a name="step-1-install-visual-studio-2019"></a>手順 1: Visual Studio 2019 をインストールする

このビデオ チュートリアルとステップ バイ ステップの手順に従って Visual Studio 2019 をインストールする方法を学びます。 Visual Studio が既にインストールされている場合は、「[Step 2:Create your first ASP.NET Core web app (手順 2: 最初の ASP.NET Core Web アプリを作成する)](tutorial-aspnet-core-ef-step-02.md)」に進みます。

_Visual Studio をインストールして、最初の ASP.NET Core アプリを作成するには、以下のビデオを見て、手順を理解してください。_

> [!VIDEO https://www.youtube.com/embed/Fz_HAqQGLtY]

## <a name="download-the-installer"></a>インストーラーをダウンロードする

[visualstudio.com](https://visualstudio.com) にアクセスして、インストーラーを探します。 Visual Studio 2019 のリンクを見つけたら、リンクをクリックして、ダウンロードを開始します。 無料バージョンの Visual Studio をダウンロードするには、[Visual Studio Community] を選択します。

## <a name="start-the-installer"></a>インストーラーを起動する

ダウンロードが完了したら、 **[実行]** をクリックして、インストーラーを起動します。

![Visual Studio 2019 のインストーラー](media/vs-2019/vs2019-installer.png)

## <a name="choose-workloads"></a>ワークロードを選択する

Visual Studio は、さまざまなタイプの開発に使用できます。また、ワークロードを使うとビルドするアプリに必要なすべてのソフトウェアを簡単にダウンロードできます。 ここでは、ワークロードとして **[ASP.NET と Web 開発]** および **[.NET Core クロスプラットフォームの開発]** を選択します。 インストーラーを再起動すれば、いつでも別のワークロードやコンポーネントをインストールできます。

![Visual Studio 2019 のワークロードの選択](media/vs-2019/vs2019-choose-workloads.png)

## <a name="install"></a>インストール

**[インストール]** をクリックすると、インストーラーにより、Visual Studio がダウンロードされ、インストールされます。

## <a name="run-visual-studio-for-the-first-time"></a>Visual Studio を初めて実行する

Visual Studio は、インストーラーの処理が完了すると自動的に起動します。 サインインを要求される場合がありますが (サインインを行うと、便利な機能を利用できます)、ここでは、後でサインインすることを選択します。 次に、テーマと開発の設定を選択します。 これらの設定を選択すると、最初のプロジェクトを開始する準備が整います。 **[新しいプロジェクトの作成]** をクリックしてから、 **[ASP.NET Core Web アプリケーション]** を選択します。

![Visual Studio 2019 の ASP.NET Core Web アプリケーション プロジェクトの新規作成](media/vs-2019/vs2019-create-new-project.png)

## <a name="explore-aspnet-core-project-types"></a>ASP.NET Core プロジェクト タイプを探索する

プロジェクトの名前と場所を選択したら、 **[作成]** を選択します。 ASP.NET Core アプリケーションに使用するテンプレートを選択します。 次のオプションから選択できます。

- [空]。 ゼロから開始できる空のプロジェクト テンプレートです。
- [API]。 Web API に最適です。
- [Web アプリケーション]。 Razor Pages を使用して構築される標準の ASP.NET Core Web アプリケーションです。
- [Web アプリケーション (モデル ビュー コントローラー)]。 モデル ビュー コントローラー パターンを使用する標準の ASP.NET Core Web アプリケーションです。
- [Angular]\(アンギュラー\)。
- [React.js]。
- [React.js/Redux]。
- [Razor クラス ライブラリ]。 プロジェクト間で Razor 資産を共有するために使用されます。

ほとんどのプロジェクト テンプレートでは、チェック ボックスをオンして Docker サポートを有効にすることも選択できることに注意してください。 [認証の変更] ボタンをクリックして、認証サポートを追加することもできます。 ここでは、以下のオプションから選択できます。

- [認証なし]。
- [個人のユーザー アカウント]。 この情報は、ローカルまたは Azure ベースのデータベースに保管されます。
- [職場または学校アカウント]。 このオプションでは、認証用に Active Directory、Azure AD、または Microsoft 365 が使用されます。
- [Windows 認証]。 イントラネット アプリケーションに適しています。

認証なしの標準の Web アプリケーション テンプレートを選択して、 **[作成]** をクリックします。

![Visual Studio 2019 の ASP.NET Core プロジェクトのオプションの選択](media/vs-2019/vs2019-choose-aspnetcore-project.png)

## <a name="next-steps"></a>次の手順

次のビデオでは、最初の ASP.NET Core プロジェクトの詳細について学びます。

[チュートリアル: 最初の ASP.NET Core Web アプリを作成する](tutorial-aspnet-core-ef-step-02.md)

## <a name="see-also"></a>関連項目

- [チュートリアル: C# および ASP.NET Core の開始](tutorial-aspnet-core.md)に関するページ (ビデオ チュートリアルを含まない詳細なチュートリアル)

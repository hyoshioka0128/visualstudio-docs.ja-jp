---
title: Visual Studio for Mac ツアー
description: Visual Studio for Mac は、iOS、Android、Mac、Xamarin.Forms 用に、ASP.NET Core Web サイトや Xamarin プロジェクトなどの .NET アプリケーションを macOS 上で構築する統合開発環境 (IDE) として利用できます。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 02/07/2019
ms.assetid: 7DC64A52-AA41-4F3A-A8A1-8A20BCD81CC7
ms.custom: video
ms.openlocfilehash: 1a187796f4f867d397662224509f8a5f72d1cc74
ms.sourcegitcommit: e38419bb842d587fd9e37c24b6cf3fc5c2e74817
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91862482"
---
# <a name="visual-studio-2017-for-mac-tour"></a>Visual Studio 2017 for Mac ツアー

> [!NOTE]
> Visual Studio 2019 for Mac が[利用できるように](installation.md)なりました。

Visual Studio for Mac は、コードを編集、デバッグ、ビルドし、その後にアプリを発行できる Mac 上の .NET _統合開発環境_です。 Visual Studio for Mac には、期待されている標準エディターおよびデバッガーなどの機能に加えて、コンパイラ、コード補完ツール、グラフィック デザイナー、ソース管理など、ソフトウェア開発プロセスを容易にする機能があります。

Visual Studio for Mac は、`.csproj`、`.fsproj`、または `.sln` など、対応する Windows 版と同じ種類のファイルを多くサポートしています。また、EditorConfig などの機能もサポートしており、これはご自分に最適な IDE を使用できることを意味しています。
Windows で Visual Studio を使用したことがあれば、使い慣れた方法でアプリの作成、起動、開発を行うことができます。 また、Visual Studio for Mac は、Windows 版を強力な IDE にしている強力なツールの多くを採用しています。 Roslyn コンパイラ プラットフォームは、リファクタリングと IntelliSense に使用されます。 そのプロジェクト システムとビルド エンジンは MSBuild を使用し、ソース エディターは TextMate バンドルをサポートしています。 Xamarin アプリと .NET Core アプリに同じデバッグ エンジンを使用し、Xamarin.iOS と Xamarin.Android に同じデザイナーを使用しています。

## <a name="what-can-i-do-in-visual-studio-for-mac"></a>Visual Studio for Mac で実行できること

Visual Studio for Mac では、次の種類での開発をサポートしています。

- C#、F# を使用した ASP.NET Core Web アプリケーション、および Razor ページ、JavaScript および TypeScript のサポート
- C# または F# を使用した .NET Core コンソール アプリケーション
- C# を使用したクロスプラットフォーム Unity ゲームおよびアプリケーション
- C# または F# および XAML を使用した Xamarin での Android、iOS、tvOS および watchOS アプリケーション
- C# または F# での Cocoa デスクトップ アプリ

この記事では、Visual Studio for Mac の多様なセクションについて説明し、これらのアプリケーションを作成する場合に強力なツールになる機能の一部を紹介します。

## <a name="ide-tour"></a>IDE ツアー

Visual Studio for Mac は、アプリケーションのファイルと設定の管理、アプリケーション ノードの作成、およびデバッグのセクションに分かれています。

## <a name="welcome-screen"></a>ようこそ画面

Visual Studio for Mac を起動すると、*ようこそ画面*が表示されます。

![ようこそ画面](media/ide-tour-image1.png)

ようこそ画面には次のセクションが含まれています。

- **ツールバー** - 検索バーにすばやくアクセスできます。 ソリューションを読み込むときに、ツールバーを使用して、アプリ構成の設定、デバッグ、およびエラーの表示を行います。
- **はじめに** - Visual Studio for Mac を初めて使用する開発者に役立つトピックにすばやくアクセスできます。
- **最近のソリューション** - 最近開いたソリューションにすばやくアクセスできます。また、プロジェクトを開いたり作成したりできる便利なボタンも表示されます。
- **開発者向け情報** - Microsoft 開発者向けの最新情報を提供するニュース フィードです。

## <a name="solutions-and-projects"></a>ソリューションとプロジェクト

次の図は、アプリケーションが読み込まれた Visual Studio for Mac を示しています。

![アプリケーションが読み込まれた Visual Studio for Mac](media/ide-tour-image17.png)

以下のセクションでは、Visual Studio for Mac の主な領域について概要を説明します。

## <a name="solution-pad"></a>Solution Pad

Solution Pad では、ソリューション内のプロジェクトが整理されています。

![Solution Pad に整理されているプロジェクト](media/ide-tour-image18.png)

これは、ソース コード、リソース、ユーザー インターフェイス、および依存関係のファイルが、プラットフォーム固有のプロジェクトに整理されている場所です。

Visual Studio for Mac でプロジェクトとソリューションを使用する方法の詳細については、「[プロジェクトおよびソリューション](./projects-and-solutions.md)」を参照してください。

## <a name="assembly-references"></a>アセンブリ参照

各プロジェクトのアセンブリ参照は、[参照] フォルダーの下に表示されます。

![Solution Pad の [参照] フォルダー](media/ide-tour-image19.png)

その他の参照は、**[参照の編集]** ダイアログを使用して追加されます。このダイアログを表示するには、[参照] フォルダーをダブルクリックするか、コンテキスト メニュー操作で **[参照の編集]** を選択します。

![[参照の編集] ダイアログ](media/ide-tour-image20.png)

Visual Studio for Mac で参照を使用する方法については、「[プロジェクト内の参照の管理](./managing-references-in-a-project.md)」を参照してください。

## <a name="dependencies--packages"></a>依存関係/パッケージ

アプリで使用されるすべての外部依存関係は、[依存関係] フォルダーまたは [パッケージ] フォルダーに格納されます。格納される場所は、.NET Core プロジェクトか Xamarin.iOS/Xamarin.Android プロジェクトかによって変わります。 通常、NuGet の形式で提供されます。

NuGet は、.NET 開発用の最も人気のあるパッケージ マネージャーです。 Visual Studio は NuGet をサポートしているので、簡単にパッケージを検索し、プロジェクトをアプリケーションに追加できます。

依存関係をアプリケーションに追加するには、[依存関係]/[パッケージ] フォルダーを右クリックし、**[パッケージの追加]** を選択します。

![NuGet パッケージの追加](media/ide-tour-image21.png)

アプリケーションで NuGet パッケージを使用する方法については、「[プロジェクトに NuGet パッケージを含める](./nuget-walkthrough.md)」を参照してください。

## <a name="refactoring"></a>リファクタリング

Visual Studio for Mac には、コンテキスト アクションとソース分析という、コードをリファクターする 2 つの便利な方法があります。 詳細については、「[リファクタリング](./refactoring.md)」を参照してください。

## <a name="debugging"></a>デバッグ

Visual Studio for Mac には、Xamarin.iOS、Xamarin.Mac、Xamarin.Android アプリケーションのデバッグをサポートするネイティブ デバッガーが備わっています。 Visual Studio for Mac では、IDE ですべてのプラットフォームでマネージド コードをデバッグするために、Mono ランタイムに実装されている Mono Soft Debugger を使用しています。 デバッグの詳細については、「[Xamarin を使ったデバッグ](./debugging.md)」を参照してください。

デバッガーには、文字列、色、URL だけでなく、サイズ、座標、ベジエ曲線などの特殊な種類の高機能なビジュアライザーが含まれています。

デバッガーのデータの視覚化の詳細については、「[データの視覚化](./data-visualizations.md)」を参照してください。

## <a name="version-control"></a>バージョン コントロール

Visual Studio for Mac は、Git と Subversion ソース管理システムと統合されています。 ソース管理下にあるプロジェクトは、ソリューション名の横にブランチとして一覧表示されます。

![ソース管理下にあるプロジェクトを示すブランチ名](media/ide-tour-image22.png)

コミットされていない変更があるファイルは、次の図に示すように、ソリューション ウィンドウにアイコンで示されます。

![Solution Pad のコミットされていないファイル](media/ide-tour-image23.png)

Visual Studio でバージョン管理を使用する方法については、「[バージョン管理](./version-control.md)」を参照してください。

## <a name="related-video"></a>関連ビデオ

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Overview/player]

## <a name="see-also"></a>関連項目

- [Visual Studio IDE (Windows)](/visualstudio/ide/visual-studio-ide)
---
title: Visual Studio for Mac ツアー
description: Visual Studio for Mac は、iOS、Android、Mac、Xamarin.Forms 用に、ASP.NET Core Web サイトや Xamarin プロジェクトなどの .NET アプリケーションを macOS 上で構築する統合開発環境 (IDE) として利用できます。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 11/09/2020
ms.assetid: 7DC64A52-AA41-4F3A-A8A1-8A20BCD81CC7
ms.custom: video
ms.openlocfilehash: a2caadd454564b389f48987e69e1bc08475affea
ms.sourcegitcommit: 2cf3a03044592367191b836b9d19028768141470
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2020
ms.locfileid: "94493271"
---
# <a name="visual-studio-2019-for-mac-tour"></a>Visual Studio 2019 for Mac ツアー

Visual Studio for Mac は、コードを編集、デバッグ、ビルドし、その後にアプリを発行できる Mac 上の .NET _統合開発環境_ です。 Visual Studio for Mac には、コード エディターやデバッガーに加えて、コンパイラ、コード補完ツール、グラフィック デザイナー、ソース管理など、ソフトウェア開発プロセスを容易にする機能があります。

Visual Studio for Mac は、`.csproj`、`.fsproj`、または `.sln` など、対応する Windows 版と同じ種類のファイルを多くサポートしています。また、EditorConfig などの機能もサポートしており、これはご自分に最適な IDE を使用できることを意味しています。
Windows で Visual Studio を使用したことがあれば、使い慣れた方法でアプリの作成、起動、開発を行うことができます。 また、Visual Studio for Mac は、Windows 版を強力な IDE にしている強力なツールの多くを採用しています。 Roslyn コンパイラ プラットフォームは、リファクタリングと IntelliSense に使用されます。 そのプロジェクト システムとビルド エンジンでは MSBuild が使用されており、ソース エディターでは、Windows での Visual Studio と同じ基盤が使用されています。 Xamarin アプリと .NET Core アプリに同じデバッグ エンジンを使用し、Xamarin.iOS と Xamarin.Android に同じデザイナーを使用しています。

## <a name="what-can-i-do-in-visual-studio-for-mac"></a>Visual Studio for Mac で実行できること

Visual Studio for Mac では、次の種類での開発をサポートしています。

- C#、F# を使用した ASP.NET Core Web アプリケーション、および Razor ページ、JavaScript、TypeScript のサポート
- C# または F# を使用した .NET Core コンソール アプリケーション
- C# を使用したクロスプラットフォーム Unity ゲームおよびアプリケーション
- C# または F# および XAML を使用した Xamarin での Android、iOS、tvOS および watchOS アプリケーション
- C# または F# での Cocoa デスクトップ アプリ

この記事では、Visual Studio for Mac の多様なセクションについて説明し、これらのアプリケーションを作成する場合に強力なツールになる機能の一部を紹介します。

## <a name="ide-tour"></a>IDE ツアー

Visual Studio for Mac は、アプリケーションのファイルと設定の管理、アプリケーション ノードの作成、およびデバッグのセクションに分かれています。

## <a name="getting-started"></a>作業の開始

Visual Studio 2019 for Mac を初めて起動すると、新規ユーザーにはサインイン ウィンドウが表示されます。 ご自分の Microsoft アカウントでサインインして、有料ライセンス (ある場合) をアクティブ化するか、Azure サブスクリプションにリンクします。 **[後で行う]** を押し、**Visual Studio > [サインイン]** メニュー項目を使用して、後でサインインすることができます。

![Microsoft アカウントへのサインイン](media/ide-tour-2019-start-signin.png)

次に、優先するキーボード ショートカットを選択すると、IDE をカスタマイズするためのオプションが表示されます: Visual Studio for Mac、Visual Studio、Visual Studio Code、または Xcode。

![お気に入りのキーボード ショートカットを選択する](media/ide-tour-2019-keyboard-shortcut.png)

この初期セットアップ エクスペリエンスの後は、Visual Studio 2019 for Mac を開くと常に "_開始ウィンドウ_" が表示され、最近使用したプロジェクトの一覧と、既存のプロジェクトを開いたり新しいプロジェクトを作成したりするためのボタンが表示されます。

![最近使用したプロジェクトから選択するか、新しいものを作成する](media/ide-tour-2019-start-projects.png)

## <a name="solutions-and-projects"></a>ソリューションとプロジェクト

次の図は、アプリケーションが読み込まれた Visual Studio for Mac を示しています。

![アプリケーションが読み込まれた Visual Studio for Mac](media/ide-tour-image17.png)

以下のセクションでは、Visual Studio for Mac の主な領域について概要を説明します。

## <a name="solution-window"></a>[ソリューション] ウィンドウ

[ソリューション] ウィンドウでは、ソリューション内のプロジェクトが整理されています。

![[ソリューション] ウィンドウに整理されているプロジェクト](media/ide-tour-image18.png)

これは、ソース コード、リソース、ユーザー インターフェイス、および依存関係のファイルが、プラットフォーム固有のプロジェクトに整理されている場所です。

Visual Studio for Mac でプロジェクトとソリューションを使用する方法の詳細については、「[プロジェクトおよびソリューション](./projects-and-solutions.md)」を参照してください。

## <a name="assembly-references"></a>アセンブリ参照

各プロジェクトのアセンブリ参照は、[参照] フォルダーの下に表示されます。

![[ソリューション] ウィンドウの [参照] フォルダー](media/ide-tour-image19.png)

その他の参照は、**[参照の編集]** ダイアログを使用して追加されます。このダイアログを表示するには、[参照] フォルダーをダブルクリックするか、コンテキスト メニュー操作で **[参照の編集]** を選択します。

![[参照の編集] ダイアログ](media/ide-tour-image20.png)

Visual Studio for Mac で参照を使用する方法については、「[プロジェクト内の参照の管理](./managing-references-in-a-project.md)」を参照してください。

## <a name="dependencies--packages"></a>依存関係/パッケージ

アプリで使用されるすべての外部依存関係は、.NET Core プロジェクトか Xamarin.iOS/Xamarin.Android プロジェクトかに応じて、[依存関係] フォルダーまたは [パッケージ] フォルダーに格納されます。 通常、NuGet の形式で提供されます。

NuGet は、.NET 開発用の最も人気のあるパッケージ マネージャーです。 Visual Studio は NuGet をサポートしているので、簡単にパッケージを検索し、プロジェクトをアプリケーションに追加できます。

依存関係をアプリケーションに追加するには、[依存関係]/[パッケージ] フォルダーを右クリックし、**[パッケージの追加]** を選択します。

![NuGet パッケージの追加](media/ide-tour-image21.png)

アプリケーションで NuGet パッケージを使用する方法については、「[プロジェクトに NuGet パッケージを含める](./nuget-walkthrough.md)」を参照してください。

## <a name="source-editor"></a>ソース エディター

C#、XAML、JavaScript のいずれで作成するかに関係なく、コード エディターでは、完全にネイティブなユーザー インターフェイスが提供され、Visual Studio Windows と同じコア コンポーネントが共有されます。

これには、次のような利点がいくつかあります。

* ネイティブ macOS (Cocoa ベース) のユーザー インターフェイス (ツールヒント、エディター画面、余白のデザイン、テキストのレンダリング、IntelliSense)
* IntelliSense の型によるフィルター処理と "インポート項目を表示"
* ネイティブ テキスト入力のサポート
* RTL/BiDi 言語のサポート
* Roslyn 3
* マルチキャレットのサポート
* 右端で折り返す
* 更新された IntelliSense UI
* 改善された検索/置換
* スニペットのサポート 
* 選択範囲のフォーマット
* インラインの電球

Visual Studio for Mac でのソース エディターの使用に関する詳細については、「[ソース エディター](./source-editor.md)」のドキュメントを参照してください。

タブを常に表示しておくには、ピン留めを利用できます。 これにより、プロジェクトを起動するたびに、必要なタブが常に表示されるようになります。 タブをピン留めするには、タブの上にマウス ポインターを移動し、_ピン_ アイコンをクリックします。

![タブのピン留め](media/ide-tour-tabpin.png)

## <a name="refactoring"></a>リファクタリング

Visual Studio for Mac には、コンテキスト アクションとソース分析という、コードをリファクターする 2 つの便利な方法があります。 詳細については、「[リファクタリング](./refactoring.md)」を参照してください。

## <a name="debugging"></a>デバッグ

Visual Studio for Mac には、.NET Core、.NET Framework、Unity、および Xamarin プロジェクトをサポートするデバッガーが用意されています。 Visual Studio for Mac では、.NET Core デバッガーと Mono Soft Debugger が使用されており、この IDE であらゆるプラットフォームにわたるマネージド コードをデバッグできます。 デバッグの詳細については、「[Xamarin を使ったデバッグ](./debugging.md)」を参照してください。

デバッガーには、文字列、色、URL だけでなく、サイズ、座標、ベジエ曲線などの特殊な種類の高機能なビジュアライザーが含まれています。

デバッガーのデータの視覚化の詳細については、「[データの視覚化](./data-visualizations.md)」を参照してください。

## <a name="version-control"></a>バージョン コントロール

Visual Studio for Mac は、Git と Subversion ソース管理システムと統合されています。 ソース管理下にあるプロジェクトは、ソリューション名の横にブランチとして一覧表示されます。

![ソース管理下にあるプロジェクトを示すブランチ名](media/ide-tour-image22.png)

コミットされていない変更があるファイルは、次の図に示すように、[ソリューション] ウィンドウにアイコンで示されます。

![[ソリューション] ウィンドウのコミットされていないファイル](media/ide-tour-image23.png)

Visual Studio でバージョン管理を使用する方法については、「[バージョン管理](./version-control.md)」を参照してください。

## <a name="next-steps"></a>次のステップ

- [Visual Studio for Mac をインストールする](installation.md)
- [使用できるワークロードを確認する](workloads.md)

## <a name="related-video"></a>関連ビデオ

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Overview/player]

## <a name="see-also"></a>関連項目

- [Visual Studio IDE (Windows)](/visualstudio/ide/visual-studio-ide)
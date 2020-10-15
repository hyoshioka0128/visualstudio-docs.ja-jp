---
title: Visual Studio 拡張機能の開発を開始しています |Microsoft Docs
ms.date: 09/18/2017
ms.topic: conceptual
helpviewer_keywords:
- getting started, Visual Studio integration
- Visual Studio, integration
ms.assetid: 8fe5e2ab-a424-4173-9d39-dd082c4d58d0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 812c5b2366e40226011a15acfc1cae2327e4b897
ms.sourcegitcommit: 9c57730000d5ced37d3887f3928b17076f49d0f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2020
ms.locfileid: "92099389"
---
# <a name="starting-to-develop-visual-studio-extensions"></a>Visual Studio 拡張機能の開発を始める

以前に Visual Studio 拡張機能を作成したことがない場合は、いくつかの質問があります。 ここでは、最も一般的なものをいくつか紹介しました。 探している情報が表示されない場合は、フィードバックボタン (画面の右上にある [**このページは役に立ちますか?** ]) を使用して、必要な情報を確認してください。

> [!NOTE]
> この記事は、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、「 [Visual Studio for Mac の拡張](/visualstudio/mac/extending-visual-studio-mac)」を参照してください。 Visual Studio Code については、「 [Visual Studio Code 拡張 API](https://code.visualstudio.com/api)」を参照してください。

## <a name="what-software-do-i-need-to-develop-visual-studio-extensions"></a>Visual Studio 拡張機能を開発するために必要なソフトウェア

Visual studio 拡張機能を開発するには、visual studio に加えて visual studio SDK をインストールする必要があります。 通常のセットアップの一環として Visual Studio SDK をインストールすることも、後でインストールすることもできます。 Visual Studio SDK のインストールの詳細については、「 [Visual STUDIO sdk のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="what-kinds-of-things-can-i-do-with-visual-studio-extensions"></a>Visual Studio 拡張機能では、どのような処理を行うことができますか。

さまざまな Visual Studio 拡張機能を練りする場合、空の制限があります。 もちろん、ほとんどの拡張機能にはコードを記述することがありますが、そのような処理は必要ありません。 次に、作成できる拡張機能の例をいくつか示します。

- 構文の色分け、IntelliSense、コンパイラおよびデバッグサポートを含む、Visual Studio に含まれていない言語のサポート

- 追加のテンプレート、コードリファクタリング、新しいダイアログ、またはツールウィンドウを使用して IDE のコアエクスペリエンスを拡張する生産性向上ツール

- データ設計やクラウドサポートなどのシナリオ向けのドメイン固有のデザイナー

拡張機能の例については、 [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs)をご覧ください。 多くの拡張機能はオープンソースであり、Marketplace には GitHub リポジトリへのリンクが含まれています。

## <a name="which-visual-studio-features-can-i-extend"></a>拡張できる Visual Studio の機能

理論的には、メニュー、ツールバー、コマンド、ウィンドウ、ソリューション、プロジェクト、エディターなど、Visual Studio の任意の部分を拡張できます。

実際には、ほとんどの場合、拡張が必要な機能は、コマンド、メニュー、ツールバー、ウィンドウ、IntelliSense、およびプロジェクトです。 関連するセクションへのリンクを次に示します。

- [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md): 独自の項目を Visual Studio のメニューおよびツールバーに追加します。 これらの機能を使用して、新しい Visual Studio 機能または独自の外部ヘルパーアプリケーションを起動できます。 メニュー項目のカスタムショートカットを指定することもできます。

- [ツールウィンドウの拡張とカスタマイズ](../extensibility/extending-and-customizing-tool-windows.md): 既存のツールウィンドウを拡張するか、独自のツールウィンドウを作成します。 たとえば、 **プロパティ**に新しいプロパティを追加したり、新しいツールウィンドウを作成して機能を追加したりすることができます。

- [エディターと言語サービス拡張機能](../extensibility/editor-and-language-service-extensions.md): Visual Studio 言語用に用意されている IntelliSense に独自のカスタマイズを追加したり、新しいプログラミング言語のサポートを作成したりできます。 新しいステートメント入力候補、提案、および新しい QuickInfo ツールヒントを作成できます。 電球を使用すると、リファクタリング候補とコード修正を追加して、新しいプログラミング言語をサポートできます。

- [プロジェクトの拡張](../extensibility/extending-projects.md)

- [ユーザー設定とオプションの拡張](../extensibility/extending-user-settings-and-options.md)

- [プロパティとプロパティ ウィンドウの拡張](../extensibility/extending-properties-and-the-property-window.md)

- [Visual Studio の他の部分の拡張](../extensibility/extending-other-parts-of-visual-studio.md)

- [Visual Studio の分離シェル](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)

## <a name="what-project-templates-are-provided-by-the-vssdk"></a><a name="BKMK_ProjectTemplate"></a> VSSDK にはどのようなプロジェクトテンプレートが用意されていますか。
 拡張機能には、Vspackage と MEF の2つの主な種類があります。 一般に、VSPackage 拡張機能は、コマンド、ツールウィンドウ、およびプロジェクトを使用または拡張する拡張機能に使用されます。 MEF 拡張機能は、Visual Studio エディターを拡張またはカスタマイズするために使用されます。

 Visual C# および Visual Basic 拡張機能の場合、VSSDK には、メニューコマンド、ツールウィンドウ、およびエディターの拡張機能を作成する新しい項目テンプレートと共に使用できる空の VSIX プロジェクトテンプレートが用意されています。 このテンプレートを使用して、プロジェクトテンプレート、コードスニペット、および他のユーザーに配布するためのその他の成果物をパッケージ化することもできます。

 C++ の場合、VSPackage ウィザードには、メニューコマンド、ツールウィンドウ、およびカスタムエディターを追加するためのコードが用意されています。

 分離シェルテンプレートは、Visual Studio シェルのバージョンに拡張機能をパッケージ化するために使用されます。これは、独自にブランド化して配布することができます。 次のトピックでは、各種類の拡張機能の使用を開始する方法について説明します。

- メニューコマンド: [メニューコマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)

- ツールウィンドウ: [ツールウィンドウを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)

- エディター拡張機能: [エディター項目テンプレートを使用した拡張機能の作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)

- 基本的な Vspackage: [VSPackage を使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-vspackage.md)

- VSIX プロジェクトテンプレート: [Vsix プロジェクトテンプレートを使用したはじめに](../extensibility/getting-started-with-the-vsix-project-template.md)

## <a name="how-do-i-get-my-extension-to-look-like-visual-studio"></a>拡張機能を Visual Studio のように表示する操作方法ますか?
 [Visual Studio のユーザーエクスペリエンスガイドライン](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)で、拡張機能の UI を設計するためのヒントを入手します。

## <a name="where-can-i-find-examples-of-vssdk-code"></a>VSSDK コードの例はどこで入手できますか。
 前のセクションに記載されている各リンクには、特定の機能を実装する方法を示すステップバイステップのチュートリアルがあります。 また、 [Visual Studio のサンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)では、GitHub でオープンソースの vssdk サンプルを見つけることもできます。

## <a name="how-can-i-distribute-my-extension"></a>拡張機能を配布するにはどうすればよいですか。
 拡張機能を別のコンピューターにインストールしたり、vsix ファイルとして友人に送信したりすることができます。これは、ダブルクリックしてインストールできます。 VSIX パッケージの詳細については、「 [Visual Studio 拡張機能の配布](../extensibility/shipping-visual-studio-extensions.md)」を参照してください。

 また、拡張機能を Visual Studio Marketplace に発行することもできます。これにより、Visual Studio の多くのユーザーが表示できるようになります。 Marketplace に拡張機能をパッケージ化する例については、「 [チュートリアル: Visual Studio 拡張機能の発行](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)」を参照してください。 Marketplace で発行するために必要な作業の詳細については、「 [Visual Studio の製品と拡張機能](/azure/devops/extend/overview?view=vsts&preserve-view=true)」を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio for Mac の拡張](/visualstudio/mac/extending-visual-studio-mac)
- [Visual Studio Code の拡張](https://code.visualstudio.com/api)
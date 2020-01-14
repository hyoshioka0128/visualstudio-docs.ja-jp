---
title: 拡張機能の開発を開始しています |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- getting started, Visual Studio integration
- Visual Studio, integration
ms.assetid: 8fe5e2ab-a424-4173-9d39-dd082c4d58d0
caps.latest.revision: 30
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d62a4c6cc45681fe6a66ae57df2e1da1d1cc12e0
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75850591"
---
# <a name="starting-to-develop-visual-studio-extensions"></a>Visual Studio 拡張機能の開発を始める
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

以前に Visual Studio 拡張機能を作成したことがない場合は、いくつかの質問があります。 ここでは、最も一般的なものをいくつか紹介しました。 探している情報が表示されない場合は、フィードバックボタン (画面の下部にある **[このページは役に立ちましたか?** ]) を使用して、必要な情報を確認してください。

## <a name="what-software-do-i-need-to-develop-visual-studio-extensions"></a>Visual Studio 拡張機能を開発するために必要なソフトウェアは何ですか？
 Visual studio の拡張機能を開発するには、visual studio 2015 に加えて、visual studio 2015 SDK もインストールする必要があります。   通常のセットアップの一環として Visual Studio 2015 SDK をインストールすることも、後でインストールすることもできます。 Visual Studio SDK のインストールに関する詳細は、次の [Visual Studio SDK](../extensibility/visual-studio-sdk.md) を参照してください。

## <a name="what-kinds-of-things-can-i-do-with-visual-studio-extensions"></a>Visual Studio 拡張機能でどのような種類の項目を行えるのでしょうか？
 さまざまな Visual Studio 拡張機能を練りする場合、空の制限があります。 もちろん、ほとんどの拡張機能にはコードを記述することがありますが、そのような処理は必要ありません。 拡張機能作成のいくつかの例を次に示します。

- 構文の色分け、IntelliSense、コンパイラおよびデバッグサポートを含む、Visual Studio に含まれていない言語のサポート

- 追加のテンプレート、コードのリファクタリング、新しいダイアログ ボックスまたはツール ウィンドウを使用したIDE の利便性を拡張させる生産性向上ツール。

- データ設計やクラウドサポートなどのシナリオ向けのドメイン固有のデザイナー

  拡張機能の例については、[Visual Studio Marketplace](https://marketplace.visualstudio.com/)を参照してください。 また、 [Visual Studio のオープンソースの拡張機能](https://github.com/Microsoft/extendvs/blob/master/CommunityExtensions.md)についても確認できます。

## <a name="which-visual-studio-features-can-i-extend"></a>Visual Studio 機能を拡張できますか？
 理論的には、メニュー、ツールバー、コマンド、ウィンドウ、ソリューション、プロジェクト、エディターなど、Visual Studio の任意の部分を拡張できます。

 実際には、ほとんどの人が望んでいる機能は、コマンド、メニューとツールバー、windows、IntelliSense、およびプロジェクトの拡張機能で見つかります。 関連するセクションへのリンクを次に示します。

- [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md): 独自の項目を Visual Studio のメニューおよびツールバーに追加します。 これらの機能を使用して、新しい Visual Studio 機能または独自の外部ヘルパーアプリケーションを起動できます。 メニュー項目のカスタムショートカットを指定することもできます。

- [拡張とカスタマイズ ツール Windows](../extensibility/extending-and-customizing-tool-windows.md): 既存のツール ウィンドウを拡張または独自のツール ウィンドウを作成します。 たとえば複数の**プロパティ**を持つものに新しいプロパティを追加したり、追加機能を追加した新しいツール ウィンドウを作成したりできます。

- [エディターと言語サービスの拡張機能](../extensibility/editor-and-language-service-extensions.md): Visual Studio の言語に対して IntelliSense が提供する独自のカスタマイズを追加するか、新しいプログラミング言語のサポートを作成します。 新しいステートメント入力候補、提案、および新しいクイックヒントのツールチップ表示を作成することができます。 電球アイコンから、新しいプログラミング言語をサポートするためにリファクタリングの提案を追加したり、コード修正プログラムを追加したりすることができます。

- [プロジェクトの拡張](../extensibility/extending-projects.md)

- [ユーザー設定とオプションの拡張](../extensibility/extending-user-settings-and-options.md)

- [プロパティとプロパティ ウィンドウの拡張](../extensibility/extending-properties-and-the-property-window.md)

- [Visual Studio の他の部分の拡張](../extensibility/extending-other-parts-of-visual-studio.md)

- [Visual Studio の分離シェル](../extensibility/visual-studio-isolated-shell.md)

## <a name="BKMK_ProjectTemplate"></a> VSSDK によってどのようなプロジェクト テンプレートが提供されますか。
 2 つの主な種類の拡張機能は、VSPackage および MEF 拡張機能です。 一般に、VSPackage 拡張機能はコマンド、ツール ウィンドウ、およびプロジェクトを拡張する場合に使用されます。 MEF 拡張機能は、Visual Studio エディターを拡張またはカスタマイズするために使用されます。

 Visual c# および Visual Basic の拡張機能の場合、VSSDK には、メニュー コマンド、ツール ウィンドウおよびエディターの拡張機能を作成する新しい項目テンプレートと共に使用できる空の VSIX プロジェクト テンプレートが用意されています。 詳細については、「 [Visual Studio 2015 SDK の新機能](../extensibility/what-s-new-in-the-visual-studio-2015-sdk.md)」を参照してください。 パッケージ プロジェクト テンプレート、コード スニペット、およびその他の成果物を他のユーザーに配布するために、このテンプレートを使用することもできます。

 C++ の場合は、VSPackage のウィザードは、メニュー コマンド、ツール ウィンドウ、およびカスタム エディターを追加するコードが用意されています。

 分離シェル テンプレートは、ブランド化して独自として配布する Visual Studio シェルのバージョンの拡張機能をパッケージ化するために使用されます。 次のトピックでは、各種類の拡張機能の使用を開始する方法について説明します。

- メニューコマンド:[メニューコマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)

- ツールウィンドウ:[ツールウィンドウを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)

- エディター拡張機能:[エディター項目テンプレートを使用した拡張機能の作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)

- 基本的な VSPackage: [VSPackage を使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-vspackage.md)

- VSIX プロジェクトテンプレート: [Vsix プロジェクトテンプレートを使用したはじめに](../extensibility/getting-started-with-the-vsix-project-template.md)

- Visual Studio 分離シェル:[チュートリアル: 基本的な分離シェルアプリケーションの作成](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)

## <a name="how-do-i-get-my-extension-to-look-like-visual-studio"></a>私の拡張をVisual Studio のように見せる方法はありますか？
 [Visual Studio のユーザーエクスペリエンスガイドライン](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)で、拡張機能の UI を設計するためのヒントを入手します。

## <a name="where-can-i-find-examples-of-vssdk-code"></a>VSSDK のコードの例についてはどこで確認できますか？
 前のセクションに記載のリンクは、ある特定の機能を実装する方法を説明するチュートリアルです。 GitHub の [Visual Studio のサンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples) でオープン ソースの VSSDK のサンプルを見つけることができます。

## <a name="how-can-i-distribute-my-extension"></a>私の拡張機能を配布する方法は?
 別のコンピューターにあなたの拡張機能をインストールするか、ダブルクリックするとインストールできる.vsix ファイルを友人に送信することができます。 VSIX パッケージの詳細については [Visual Studio 拡張機能の配布](../extensibility/shipping-visual-studio-extensions.md) を参照してください。

 また、拡張機能を Visual Studio ギャラリーに発行することもできます。これにより、多数の Visual Studio ユーザーに拡張機能が表示されます。 ギャラリーの拡張機能をパッケージ化する例については、「[チュートリアル: Visual Studio 拡張機能の発行](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)」を参照してください。 ギャラリーで発行するために必要な操作の詳細については、「 [Visual Studio の製品と拡張機能](https://visualstudiogallery.msdn.microsoft.com/)」を参照してください。

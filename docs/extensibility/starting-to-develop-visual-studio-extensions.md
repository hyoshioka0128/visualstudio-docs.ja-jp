---
title: Visual Studio 拡張機能の開発を開始する |マイクロソフトドキュメント
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
ms.openlocfilehash: 744475e61458f7b91ce08fba4d17046df36f5558
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699741"
---
# <a name="starting-to-develop-visual-studio-extensions"></a>Visual Studio 拡張機能の開発を始める

これまで Visual Studio 拡張機能を作成したことがない場合は、いくつかの質問があります。 ここでは、最も一般的なもののいくつかを挙げました。 探している情報が表示されない場合は、フィードバック ボタン (この**ページは役に立ちましたか?** 画面の下部) を使用して、必要な情報を尋ねてください。

> [!NOTE]
> この資料は、Windows の Visual Studio に適用されます。 Mac 用の Visual Studio の場合は[、「Mac 用の Visual Studio の拡張](/visualstudio/mac/extending-visual-studio-mac)」を参照してください。 Visual Studio コードについては[、「Visual Studio コード拡張機能 API](https://code.visualstudio.com/api)」を参照してください。

## <a name="what-software-do-i-need-to-develop-visual-studio-extensions"></a>Visual Studio 拡張機能を開発するには、どのようなソフトウェアが必要ですか?

Visual Studio 拡張機能を開発するには、Visual Studio に加えて、Visual Studio SDK をインストールする必要があります。 Visual Studio SDK は、通常のセットアップの一部としてインストールすることも、後でインストールすることもできます。 Visual Studio SDK のインストールの詳細については[、「Visual Studio SDK」](../extensibility/visual-studio-sdk.md)を参照してください。

## <a name="what-kinds-of-things-can-i-do-with-visual-studio-extensions"></a>Visual Studio 拡張機能では、どのような操作ができますか?

異なる Visual Studio 拡張機能を想像する場合の制限は空です。 もちろん、ほとんどの拡張機能はコードの記述と関係がありますが、そうである必要はありません。 ビルドできる拡張機能の種類の例を次に示します。

- Visual Studio に含まれていない言語のサポート (構文の色付け、IntelliSense、コンパイラとデバッグのサポートなど)

- 追加のテンプレート、コードリファクタリング、新しいダイアログ、またはツールウィンドウでコア IDE の操作性を拡張する生産性向上ツール

- データ設計やクラウドサポートなどのシナリオに対応したドメイン固有の設計者

拡張機能の例については[、Visual Studio マーケットプレース](https://marketplace.visualstudio.com/vs)を参照してください。 多くの拡張機能はオープンソースであり、マーケットプレイスには GitHub リポジトリへのリンクが含まれています。

## <a name="which-visual-studio-features-can-i-extend"></a>拡張できる Visual Studio の機能

理論的には、メニュー、ツール バー、コマンド、ウィンドウ、ソリューション、プロジェクト、エディターなど、Visual Studio の任意の部分を拡張できます。

実際には、ほとんどの人が拡張したい機能は、コマンド、メニューとツールバー、ウィンドウ、IntelliSense、およびプロジェクトであることがわかりました。 関連するセクションへのリンクを次に示します。

- [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md): Visual Studio のメニューとツール バーに独自の項目を追加します。 これらを使用して、新しい Visual Studio 機能や独自の外部ヘルパー アプリケーションを起動できます。 メニュー項目にカスタム ショートカットを提供することもできます。

- [拡張およびカスタマイズ ツール ウィンドウ](../extensibility/extending-and-customizing-tool-windows.md): 既存のツール ウィンドウを拡張するか、独自のツール ウィンドウを作成します。 たとえば、新しいプロパティを**プロパティ**に追加したり、新しいツール ウィンドウを作成して機能を追加したりできます。

- [エディターと言語サービス拡張機能](../extensibility/editor-and-language-service-extensions.md): Visual Studio 言語用に提供される IntelliSense に独自のカスタマイズを追加するか、新しいプログラミング言語のサポートを作成します。 新しいステートメント入力候補、候補、および新しいクイック ヒントヒントを作成できます。 電球を使用すると、リファクタリングの提案やコード修正を追加して、新しいプログラミング言語をサポートできます。

- [プロジェクトの拡張](../extensibility/extending-projects.md)

- [ユーザー設定とオプションの拡張](../extensibility/extending-user-settings-and-options.md)

- [プロパティとプロパティ ウィンドウの拡張](../extensibility/extending-properties-and-the-property-window.md)

- [Visual Studio の他の部分の拡張](../extensibility/extending-other-parts-of-visual-studio.md)

- [Visual Studio の分離シェル](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)

## <a name="what-project-templates-are-provided-by-the-vssdk"></a><a name="BKMK_ProjectTemplate"></a>VSSDK によって提供されるプロジェクト テンプレートは何ですか?
 主な 2 種類の拡張機能は、VSPackage と MEF 拡張機能です。 一般に、VSPackage 拡張機能は、コマンド、ツール ウィンドウ、およびプロジェクトを使用または拡張する拡張機能に使用されます。 MEF 拡張機能は、Visual Studio エディターを拡張またはカスタマイズするために使用されます。

 Visual C# および Visual Basic 拡張機能の VSSDK には、メニュー コマンド、ツール ウィンドウ、およびエディター拡張機能を作成する新しい項目テンプレートと共に使用できる空の VSIX プロジェクト テンプレートが用意されています。 このテンプレートを使用して、プロジェクト テンプレート、コード スニペット、その他の成果物をパッケージ化して他のユーザーに配布することもできます。

 C++ では、VSPackage ウィザードは、メニュー コマンド、ツール ウィンドウ、およびカスタム エディターを追加するコードを提供します。

 分離シェル テンプレートは、独自のブランドと配布が可能な Visual Studio シェルのバージョンで拡張機能をパッケージ化するために使用されます。 次のトピックでは、各種類の拡張機能を使用する方法を示します。

- メニュー コマンド:[メニュー コマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)

- ツール ウィンドウ:[ツール ウィンドウを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)

- エディター拡張機能:[エディター項目テンプレートを使用した拡張機能の作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)

- 基本的な VS パッケージ: [VS パッケージを使用して拡張機能を作成します。](../extensibility/creating-an-extension-with-a-vspackage.md)

- VSIX プロジェクト テンプレート: [VSIX プロジェクト テンプレートの使用の開始](../extensibility/getting-started-with-the-vsix-project-template.md)

## <a name="how-do-i-get-my-extension-to-look-like-visual-studio"></a>拡張機能を Visual Studio のように見せるようにするにはどうすればよいですか?
 拡張機能の UI を設計するためのヒントについては[、「Visual Studio ユーザー エクスペリエンスガイドライン](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)」を参照してください。

## <a name="where-can-i-find-examples-of-vssdk-code"></a>VSSDK コードの例はどこにありますか?
 前のセクションに記載されている各リンクには、特定の機能を実装する方法を示すステップ バイ ステップのチュートリアルがあります。 また、オープン ソース VSSDK サンプルは[、GitHub で見つけることができます](https://github.com/Microsoft/VSSDK-Extensibility-Samples)。

## <a name="how-can-i-distribute-my-extension"></a>拡張機能を配布する方法
 拡張機能を別のコンピューターにインストールするか、.vsix ファイルとして友人に送信できます。 VSIX パッケージの詳細については[、「Visual Studio 拡張機能の出荷」を参照してください](../extensibility/shipping-visual-studio-extensions.md)。

 拡張機能を Visual Studio マーケットプレースで発行することもできます。 マーケットプレースに拡張機能をパッケージ化する例については、「[チュートリアル: Visual Studio 拡張機能の発行](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)」を参照してください。 マーケットプレースで発行するために必要な操作の詳細については、「 Visual [Studio の製品と拡張機能](/azure/devops/extend/overview?view=vsts)」を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio for Mac の拡張](/visualstudio/mac/extending-visual-studio-mac)
- [ビジュアル スタジオ コードの拡張](https://code.visualstudio.com/api)

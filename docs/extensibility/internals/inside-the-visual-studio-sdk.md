---
title: Visual Studio SDK の内部 |Microsoft Docs
description: Visual studio のアーキテクチャ、コンポーネント、サービス、スキーマ、ユーティリティなど、Visual Studio SDK の拡張機能について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- roadmap, Visual Studio integration SDK
- Visual Studio integration SDK roadmap
- integration roadmap, Visual Studio SDK
ms.assetid: 9118eaa4-0453-4dc5-9e16-c7062d254869
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e11ee862f43ead3605d8e07dc159e18da13413b8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074705"
---
# <a name="inside-the-visual-studio-sdk"></a>Visual Studio SDK の内部

このセクションでは、visual studio のアーキテクチャ、コンポーネント、サービス、スキーマ、ユーティリティなど、Visual Studio の拡張機能に関する詳細な情報を提供します。

## <a name="extensibility-architecture"></a>拡張性のアーキテクチャ
 次の図は、Visual Studio の機能拡張アーキテクチャを示しています。 Vspackage は、サービスとして IDE 全体で共有されるアプリケーション機能を提供します。 標準 IDE には、 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> ide ウィンドウ機能へのアクセスを提供するなど、さまざまなサービスも用意されています。

 ![環境アーキテクチャグラフィック](../../extensibility/internals/media/environment.gif "環境") Visual Studio アーキテクチャの一般化されたビュー

## <a name="vspackages"></a>VSPackages
 VSPackage は、UI 要素、サービス、プロジェクト、エディター、およびデザイナーで Visual Studio を構成および拡張するソフトウェア モジュールです。 Vspackage は、Visual Studio の中心的なアーキテクチャ単位です。 詳細については、「 [VSPackages](../../extensibility/internals/vspackages.md)」を参照してください。

## <a name="visual-studio-shell"></a>Visual Studio Shell
 Visual Studio シェルは、基本機能を提供し、コンポーネント Vspackage と MEF 拡張機能間の相互通信をサポートします。 詳細については、「 [Visual Studio Shell](../../extensibility/internals/visual-studio-shell.md)」を参照してください。

## <a name="user-experience-guidelines"></a>ユーザー エクスペリエンス ガイドライン
 Visual Studio の新機能の設計を計画している場合は、「 [Visual Studio ユーザーエクスペリエンスガイドライン](../../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)」のデザインとユーザビリティのヒントに関するガイドラインを参照してください。

## <a name="commands"></a>コマンド
 コマンドは、ドキュメントの印刷、ビューの更新、ファイルの新規作成などのタスクを実行する関数です。

 Visual Studio を拡張すると、コマンドを作成し、Visual Studio シェルに登録できます。 これらのコマンドを IDE でどのように表示するか (メニューやツールバーなど) を指定できます。 通常、カスタムコマンドは [**ツール**] メニューに表示され、ツールウィンドウを表示するためのコマンドは、[**表示**] メニューの [**その他のウィンドウ**] サブメニューに表示されます。

 コマンドを作成する場合は、そのコマンドのイベントハンドラーも作成する必要があります。 イベントハンドラーは、コマンドを表示するか有効にするかを決定し、そのテキストを変更できるようにします。また、コマンドがアクティブになったときに、コマンドが適切に応答することを保証します。 ほとんどの場合、IDE はインターフェイスを使用してコマンドを処理し <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ます。 Visual Studio のコマンドは、ローカルの選択に基づいて最も内側のコマンドコンテキストから処理され、グローバルの選択に基づいて最も外側のコンテキストに進みます。 メイン メニューに追加したコマンドは、すぐにスクリプトに利用できます。

 詳細については、「 [コマンド、メニュー、およびツールバー](../../extensibility/internals/commands-menus-and-toolbars.md)」を参照してください。

## <a name="menus-and-toolbars"></a>メニューとツールバー
 メニューとツールバーを使用すると、ユーザーがコマンドを呼び出すことができます。 メニューは、通常、ツールウィンドウの上部に個々のテキスト項目として表示される、コマンドの行または列です。 サブメニューは、ユーザーが小さな矢印を含むコマンドをクリックしたときに表示されるセカンダリメニューです。 コンテキストメニューは、ユーザーが特定の UI 要素を右クリックしたときに表示されます。 一般的なメニュー名には、[ **ファイル**]、[ **編集**]、[ **表示**]、および [ **ウィンドウ]** があります。 詳細については、「 [メニューとコマンドの拡張](../../extensibility/extending-menus-and-commands.md)」を参照してください。

 ツールバーは、ボタンやその他のコントロール (コンボボックス、リストボックス、テキストボックスなど) の行または列です。 ツールバーボタンには、通常、開いている **ファイル** コマンドのフォルダーアイコンや **印刷** コマンド用のプリンターなどのアイコンイメージがあります。 すべてのツールバー要素は、コマンドに関連付けられています。 ツールバーボタンをクリックすると、関連付けられたコマンドが実行されます。 ドロップダウンコントロールの場合は、ドロップダウンリストの各項目が別のコマンドに関連付けられます。 分割コントロールなど、一部のツールバーコントロールはハイブリッドです。 コントロールの一方の側はツールバーボタンで、もう一方の側は下向きの矢印で、クリックすると複数のコマンドが表示されます。

## <a name="tool-windows"></a>ツール ウィンドウ
 ツールウィンドウは、IDE で情報を表示するために使用されます。 ツール **ボックス**、**ソリューションエクスプローラー**、**プロパティ** ウィンドウ、および **Web ブラウザー** は、ツールウィンドウの例です。

 通常、ツールウィンドウには、ユーザーが対話できるさまざまなコントロールが用意されています。 たとえば、[ **プロパティ** ] ウィンドウでは、特定の目的に対応するオブジェクトのプロパティをユーザーが設定できます。 [ **プロパティ** ] ウィンドウはこの意味で特化されていますが、さまざまな状況で使用できるため、一般的にもあります。 同様に、 **出力** ウィンドウはテキストベースの出力を提供するため、特に、visual studio の多くのサブシステムが visual studio ユーザーに出力を提供するために使用できるため、一般的です。

 いくつかのツールウィンドウを含む Visual Studio の次の図を考えてみましょう。

 ![スクリーン ショット](../../extensibility/internals/media/t1gui.png "T1gui")

 一部のツールウィンドウは、ソリューションエクスプローラーツールウィンドウを表示し、他のツールウィンドウを非表示にして、タブをクリックして使用できるようにする1つのウィンドウにまとめてドッキングされます。 この図には、2つのツールウィンドウである [ **エラー一覧** ] ウィンドウと [ **出力** ] ウィンドウが1つのウィンドウにまとめてドッキングされています。

 また、[メインドキュメント] ウィンドウには、複数のエディターウィンドウが表示されています。 ツールウィンドウには通常1つのインスタンスしかありませんが (たとえば、1つの **ソリューションエクスプローラー** のみを開くことができます)、エディターウィンドウには複数のインスタンスを含めることができます。各ドキュメントは、それぞれ同じウィンドウにドッキングされています。 この図は、2つのエディターウィンドウ (1 つのフォームデザイナーウィンドウ) を持つドキュメントペインを示しています。 ドキュメントペイン内のすべてのウィンドウは、[タブ] をクリックすると使用できますが、EditorPane .cs ファイルを含むエディターウィンドウは表示され、アクティブになります。

 Visual Studio を拡張すると、Visual Studio ユーザーが拡張機能と対話できるツールウィンドウを作成できます。 また、Visual Studio ユーザーがドキュメントを編集できる独自のエディターを作成することもできます。 ツールウィンドウとエディターは Visual Studio に統合されるため、タブに正しくドッキングしたり、タブに表示したりする必要はありません。 Visual Studio に正しく登録されると、Visual Studio のツールウィンドウとドキュメントウィンドウの標準的な機能が自動的に設定されます。 詳細については、「 [ツールウィンドウの拡張とカスタマイズ](../../extensibility/extending-and-customizing-tool-windows.md)」を参照してください。

## <a name="document-windows"></a>ドキュメント ウィンドウ
 ドキュメントウィンドウは、マルチドキュメントインターフェイス (MDI) ウィンドウのフレーム化された子ウィンドウです。 通常、ドキュメントウィンドウは、テキストエディター、フォームエディター (デザイナーとも呼ばれます)、またはコントロールを編集するために使用されますが、他の機能型をホストすることもできます。 [ **新しいファイル** ] ダイアログボックスには、Visual Studio に用意されているドキュメントウィンドウの例が含まれています。

 ほとんどのエディターは、プログラミング言語や、HTML ページ、フレームセット、C++ ファイル、ヘッダーファイルなどのファイルの種類に固有です。 [ **新しいファイル** ] ダイアログボックスでテンプレートを選択すると、ユーザーは、テンプレートに関連付けられているファイルの種類のエディターのドキュメントウィンドウを動的に作成します。 ドキュメントウィンドウは、ユーザーが既存のファイルを開いたときにも作成されます。

 ドキュメントウィンドウは、MDI クライアント領域に制限されています。 各ドキュメントウィンドウには上部にタブがあり、タブオーダーは MDI 領域で開いている他のウィンドウにリンクされています。 ドキュメントウィンドウのタブを右クリックすると、ショートカットメニューが表示されます。このメニューには、MDI 領域を水平または垂直の複数のタブグループに分割するオプションがあります。 MDI 領域を分割すると、複数のファイルを同時に表示できます。 詳細については、「 [ドキュメントウィンドウ](../../extensibility/internals/document-windows.md)」を参照してください。

## <a name="editors"></a>エディター
 Visual Studio エディターでは、Managed Extensibility Framework (MEF) を使用して、それをカスタマイズし、独自の種類のコンテンツに使用することができます。 多くの場合、エディターを拡張するために VSPackage を作成する必要はありませんが、シェルの機能 (メニューコマンドやショートカットキーなど) を含める場合は、MEF 拡張と VSPackage を組み合わせることができます。

 また、カスタムエディターを作成することもできます。たとえば、データベースの読み取りと書き込みを行う場合や、デザイナーを使用する場合です。 メモ帳や Microsoft ワードパッドなどの外部エディターを使用することもできます。 詳細については、「 [エディターと言語サービスの拡張機能](../../extensibility/editor-and-language-service-extensions.md)」を参照してください。

## <a name="language-services"></a>言語サービス
 Visual Studio エディターで新しいプログラミングキーワードをサポートする場合、または新しいプログラミング言語を使用する場合は、言語サービスを作成します。 各言語サービスは、特定のエディター機能を完全に、部分的に、またはまったく実装できません。 言語サービスでは、構成方法に応じて、構文の強調表示、かっこの一致、IntelliSense のサポート、およびエディターのその他の機能を使用できます。

 言語サービスの中核となるのは、パーサーとスキャナーです。 スキャナー (または字句解析器) は、ソースファイルをトークンと呼ばれる要素に分割し、パーサーはそれらのトークン間の関係を確立します。 言語サービスを作成する場合は、Visual Studio が言語のトークンと文法を理解できるように、パーサーとスキャナーを実装する必要があります。 マネージまたはアンマネージ言語サービスを作成できます。 詳細については、「 [従来の言語サービスの機能拡張](../../extensibility/internals/legacy-language-service-extensibility.md)」を参照してください。

## <a name="projects"></a>プロジェクト

Visual Studio では、プロジェクトは、開発者がソースコードやその他のリソースを整理して構築するために使用するコンテナーです。 プロジェクトを使用すると、ソースコード、Web サービスおよびデータベースへの参照、およびその他のリソースを整理、ビルド、デバッグ、および配置できます。 Vspackage は、プロジェクトの種類、プロジェクトのサブタイプ、およびカスタムツールを提供することで、Visual Studio プロジェクトシステムを拡張できます。

プロジェクトは、 *ソリューション* 内でまとめて収集することもできます。これは、アプリケーションを作成するために連携して動作する1つ以上のプロジェクトをグループ化したものです。 ソリューションに関連するプロジェクトと状態の情報は、2つのソリューションファイル、テキストベースの [ソリューション (.sln) ファイル](solution-dot-sln-file.md) 、およびバイナリ [ソリューションユーザーオプション (.suo) ファイル](solution-user-options-dot-suo-file.md)に格納されます。 これらのファイルは、以前のバージョンの Visual Basic で使用されていたグループ (vbg) ファイルに似ています。また、以前のバージョンの C++ で使用されていたワークスペース (dsw) およびユーザーオプション (. opt) ファイルに似ています。

詳細については、「 [プロジェクト](../../extensibility/internals/projects.md) と [ソリューション](../../extensibility/internals/solutions-overview.md)」を参照してください。

## <a name="project-and-item-templates"></a>プロジェクト テンプレートと項目テンプレート
 Visual Studio には、定義済みのプロジェクトテンプレートとプロジェクト項目テンプレートが含まれています。 また、独自のテンプレートを作成したり、コミュニティからテンプレートを取得して、それらを Visual Studio に統合したりすることもできます。 [MSDN コードギャラリー](https://code.msdn.microsoft.com/site/search?query=visual%20studio)は、テンプレートと拡張機能のための場所です。

 テンプレートには、特定の種類のアプリケーション、コントロール、ライブラリ、またはクラスを構築するために必要なプロジェクトの構造と基本ファイルが含まれています。 いずれかのテンプレートに似たソフトウェアを開発する場合は、テンプレートに基づくプロジェクトを作成し、そのプロジェクト内のファイルを変更します。

> [!NOTE]
> このテンプレートアーキテクチャは、プロジェクトではサポートされていません [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 。

 詳細については、「 [プロジェクトおよびプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)」を参照してください。

## <a name="properties-and-options"></a>プロパティとオプション
 [ **プロパティ** ] ウィンドウには、1つまたは複数の選択した項目のプロパティが表示されます。 [ [プロパティの拡張](../../extensibility/internals/extending-properties.md) ] オプションページには、プログラミング言語や VSPackage: [オプションページやオプションページ](../../extensibility/internals/options-and-options-pages.md)など、特定のコンポーネントに関連するオプションのセットが含まれています。 設定は、通常、インポートおよびエクスポート可能な UI 関連の機能です。 [ユーザー設定のサポート](../../extensibility/internals/support-for-user-settings.md)。

## <a name="visual-studio-services"></a>Visual Studio のサービス
 サービスは、コンポーネントが使用する特定のインターフェイスのセットを提供します。 Visual Studio には、拡張機能を含む任意のコンポーネントで使用できる一連のサービスが用意されています。 たとえば、Visual Studio サービスを使用すると、ツールウィンドウを動的に表示または非表示にしたり、ヘルプ、ステータスバー、または UI イベントへのアクセスを有効にしたりできます。 Visual Studio エディターには、エディター拡張機能によってインポートできるサービスも用意されています。 詳細については、「 [サービスの使用と提供](../../extensibility/using-and-providing-services.md)」を参照してください。

## <a name="debugger"></a>デバッガー
 デバッガーは、言語固有のデバッグコンポーネントに対するユーザーインターフェイスです。 新しい言語サービスを作成した場合は、デバッガーにフックする特定のデバッグエンジンを作成する必要があります。 詳細については、「 [Visual Studio デバッガーの機能拡張](../../extensibility/debugger/visual-studio-debugger-extensibility.md)」を参照してください。

## <a name="source-control"></a>ソース管理
 ソース管理プラグインまたは VSPackage の実装の詳細については、「 [ソース管理](../../extensibility/internals/source-control.md)」を参照してください。

## <a name="wizards"></a>ウィザード
 ウィザードを新しいプロジェクトの種類と組み合わせて作成すると、ウィザードを使用して、ユーザーがその種類の新しいプロジェクトを作成するときに適切な決定を行うのに役立ちます。 詳細については、「 [ウィザード](../../extensibility/internals/wizards.md)」を参照してください。

## <a name="custom-tools"></a>カスタム ツール
 カスタムツールを使用すると、プロジェクト内の項目にツールを関連付け、ファイルが保存されるたびにそのツールを実行できます。 詳細については、「 [カスタムツール](../../extensibility/internals/custom-tools.md)」を参照してください。

## <a name="vssdk-utilities"></a>VSSDK ユーティリティ
 VSSDK には、Vspackage のさまざまな側面を操作するために必要になる可能性のある一連のユーティリティが含まれています。 詳細については、「 [Vssdk ユーティリティ](../../extensibility/internals/vssdk-utilities.md)」を参照してください。

## <a name="using-windows-installer"></a>Windows インストーラーの使用
 場合によっては、VSIX インストーラーではなく Windows インストーラーの使用が必要になることがあります。たとえば、レジストリへの書き込みが必要になる場合があります。 拡張機能での Windows インストーラーの使用の詳細については、「 [Windows インストーラーを使用した Vspackage のインストール](../../extensibility/internals/installing-vspackages-with-windows-installer.md)」を参照してください。

## <a name="help-viewer"></a>ヘルプ ビューアー
 ヘルプビューアーには、独自のヘルプおよび F1 ページを統合できます。 詳細については、「 [MICROSOFT ヘルプビューアー SDK](../../extensibility/internals/microsoft-help-viewer-sdk.md)」を参照してください。

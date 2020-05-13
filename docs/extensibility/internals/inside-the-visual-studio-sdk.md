---
title: 内部のビジュアル スタジオ SDK |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- roadmap, Visual Studio integration SDK
- Visual Studio integration SDK roadmap
- integration roadmap, Visual Studio SDK
ms.assetid: 9118eaa4-0453-4dc5-9e16-c7062d254869
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0e72020795bc3181e11f0f90eff580a2365d4000
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707580"
---
# <a name="inside-the-visual-studio-sdk"></a>Visual Studio SDK の内部

このセクションでは、Visual Studio の拡張機能に関する詳細な情報を提供します。

## <a name="extensibility-architecture"></a>拡張性アーキテクチャ
 次の図は、Visual Studio の機能拡張アーキテクチャを示しています。 VSPackages は、IDE 全体でサービスとして共有されるアプリケーション機能を提供します。 標準の IDE には、 などの<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>IDE ウィンドウ機能へのアクセスを提供するさまざまなサービスも用意されています。

 ![環境アーキテクチャグラフィック](../../extensibility/internals/media/environment.gif "環境")Visual Studio アーキテクチャの一般化されたビュー

## <a name="vspackages"></a>VSPackages
 VSPackage は、UI 要素、サービス、プロジェクト、エディター、およびデザイナーで Visual Studio を構成および拡張するソフトウェア モジュールです。 VS パッケージは、Visual Studio の中心的なアーキテクチャ単位です。 詳細については、「 [VSPackages](../../extensibility/internals/vspackages.md)」を参照してください。

## <a name="visual-studio-shell"></a>Visual Studio Shell
 Visual Studio シェルには、基本的な機能が用意されており、コンポーネント VSPackages と MEF 拡張機能間の相互通信がサポートされています。 詳細については、「 [Visual Studio シェル](../../extensibility/internals/visual-studio-shell.md)」を参照してください。

## <a name="user-experience-guidelines"></a>ユーザー エクスペリエンス ガイドライン
 Visual Studio の新機能を設計する場合は、デザインと使いやすさのヒントに関する次のガイドラインを参照[してください。](../../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)

## <a name="commands"></a>コマンド
 コマンドは、ドキュメントの印刷、ビューの更新、ファイルの新規作成などのタスクを実行する関数です。

 Visual Studio を拡張すると、コマンドを作成し、Visual Studio シェルに登録できます。 メニューやツールバーなど、これらのコマンドを IDE で表示する方法を指定できます。 通常、ツール**メニューには**カスタム コマンドが表示され、ツール ウィンドウを表示するコマンドは **[表示**] メニューの **[その他のウィンドウ**] サブメニューに表示されます。

 コマンドを作成する場合は、そのコマンドのイベント ハンドラーも作成する必要があります。 イベント ハンドラーは、コマンドが表示または有効になっている場合を決定し、そのテキストを変更し、コマンドがアクティブになったときに適切に応答することを保証します。 ほとんどの場合、IDE はインターフェイスを使用してコマンドを<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>処理します。 Visual Studio のコマンドは、ローカル選択に基づいて最も内側のコマンド コンテキストから処理され、グローバル選択に基づいて最も外側のコンテキストに進みます。 メイン メニューに追加したコマンドは、すぐにスクリプトに利用できます。

 詳細については、「[コマンド、メニュー、およびツールバー](../../extensibility/internals/commands-menus-and-toolbars.md)」を参照してください。

## <a name="menus-and-toolbars"></a>メニューとツールバー
 メニューとツールバーは、ユーザーがコマンドを呼び出すための方法を提供します。 メニューは、通常、ツール ウィンドウの上部に個々のテキスト アイテムとして表示されるコマンドの行または列です。 サブメニューは、小さい矢印を含むコマンドをユーザーがクリックしたときに表示されるセカンダリ メニューです。 コンテキスト メニューは、ユーザーが特定の UI 要素を右クリックしたときに表示されます。 一般的なメニュー名には、**ファイル**、**編集**、**表示**、および**ウィンドウ**があります。 詳細については、「[メニューとコマンドの拡張](../../extensibility/extending-menus-and-commands.md)」を参照してください。

 ツールバーは、ボタンや、コンボ ボックス、リスト ボックス、テキスト ボックスなどの他のコントロールの行または列です。 ツール バー ボタンには、通常、[**ファイルを開く]** コマンドのフォルダ アイコンや**印刷**コマンドのプリンターなどのアイコン イメージがあります。 すべてのツールバー要素はコマンドに関連付けられます。 ツールバー ボタンをクリックすると、関連付けられたコマンドが実行されます。 ドロップダウン コントロールの場合、ドロップダウン リスト内の各項目は別のコマンドに関連付けられます。 分割コントロールなどの一部のツール バー コントロールは、ハイブリッドです。 コントロールの一方の側はツールバー ボタンで、もう一方の側はクリックされたときにいくつかのコマンドを表示する下向き矢印です。

## <a name="tool-windows"></a>ツール ウィンドウ
 ツール ウィンドウは、IDE で情報を表示するために使用されます。 **ツール**ウィンドウの例として、ツールボックス、**ソリューション エクスプローラ**、**プロパティ**ウィンドウ、および**Web ブラウザ**が挙げられており、その例は次のとおりです。

 ツール ウィンドウには、通常、ユーザーが対話できるさまざまなコントロールが用意されています。 たとえば、[**プロパティ]** ウィンドウでは、特定の目的を果たすオブジェクトのプロパティをユーザーが設定できます。 **プロパティ**ウィンドウは、この意味で特化されていますが、多くの異なる状況で使用できるため一般的です。 同様に、**出力**ウィンドウはテキスト ベースの出力を提供するため特化されていますが、Visual Studio の多くのサブシステムでは Visual Studio ユーザーに出力を提供するために使用できるため、一般的です。

 いくつかのツール ウィンドウを含む Visual Studio の次の図を考えてみましょう。

 ![スクリーン ショット](../../extensibility/internals/media/t1gui.png "T1gui")

 一部のツール ウィンドウは、ソリューション エクスプローラのツール ウィンドウを表示し、他のツール ウィンドウを非表示にする 1 つのペインにドッキングされていますが、タブをクリックして使用できます。 この図は、他の 2 つのツール ウィンドウである **[エラー一覧**] と **[出力**] ウィンドウを 1 つのペインにドッキングした様子を示しています。

 また、いくつかのエディター ウィンドウを表示するメイン のドキュメント ウィンドウも示します。 ツール ウィンドウには通常 1 つのインスタンスしかありません (たとえば、ソリューション**エクスプローラー**を 1 つだけ開くことができます) は、エディター ウィンドウに複数のインスタンスを持つことができます。 図は、2 つのエディター ウィンドウ、1 つのフォーム デザイナー ウィンドウを持つドキュメント ウィンドウを示しています。 ドキュメント ウィンドウ内のすべてのウィンドウはタブをクリックして使用できますが、ファイルを含むエディター ウィンドウEditorPane.cs表示され、アクティブになります。

 Visual Studio を拡張すると、Visual Studio ユーザーが拡張機能を操作できるツール ウィンドウを作成できます。 また、Visual Studio ユーザーがドキュメントを編集できる独自のエディターを作成することもできます。 ツール ウィンドウとエディターは Visual Studio に統合されるため、ドッキングしたりタブに正しく表示されるようにプログラムする必要はありません。 これらのファイルが Visual Studio に正しく登録されると、ツール ウィンドウとドキュメント ウィンドウの一般的な機能が自動的に Visual Studio に表示されます。 詳細については、「 [Windows の拡張とカスタマイズ 」を](../../extensibility/extending-and-customizing-tool-windows.md)参照してください。

## <a name="document-windows"></a>ドキュメント ウィンドウ
 ドキュメント ウィンドウは、マルチ ドキュメント インターフェイス (MDI) ウィンドウのフレーム化された子ウィンドウです。 ドキュメント ウィンドウは、通常、テキスト エディタ、フォーム エディター (デザイナー) 、または編集コントロールをホストするために使用されますが、他の機能型をホストすることもできます。 [**新しいファイル]** ダイアログ ボックスには、Visual Studio で提供されるドキュメント ウィンドウの例が含まれています。

 ほとんどのエディターは、プログラミング言語または HTML ページ、フレームセット、C++ ファイル、ヘッダー ファイルなどのファイルの種類に固有です。 [**新しいファイル]** ダイアログ ボックスでテンプレートを選択すると、ユーザーはテンプレートに関連付けられているファイルの種類のエディター用にドキュメント ウィンドウを動的に作成します。 ドキュメント ウィンドウは、ユーザーが既存のファイルを開いたときにも作成されます。

 ドキュメント ウィンドウは、MDI クライアント領域に制限されます。 各ドキュメント ウィンドウの上部にタブがあり、MDI 領域で開いている他のウィンドウにタブ オーダーがリンクされています。 ドキュメント ウィンドウのタブを右クリックすると、MDI 領域を複数の水平または垂直タブ グループに分割するオプションを含むショートカット メニューが表示されます。 MDI 領域を分割すると、複数のファイルを同時に表示できます。 詳細については、「ドキュメント[ウィンドウ](../../extensibility/internals/document-windows.md)」を参照してください。

## <a name="editors"></a>エディター
 Visual Studio エディターをカスタマイズし、マネージ機能拡張フレームワーク (MEF) を使用して、独自の種類のコンテンツに使用できます。 多くの場合、エディターを拡張するために VSPackage を作成する必要はありませんが、シェルから機能を含める (メニュー コマンドやショートカット キーなど) 場合は、MEF 拡張機能を VSPackage と組み合わせることができます。

 データベースの読み取りや書き込みを行う場合や、デザイナーを使用する場合など、カスタム エディターを作成することもできます。 メモ帳や Microsoft ワードパッドなどの外部エディタを使用することもできます。 詳細については、「[エディタおよび言語サービス拡張](../../extensibility/editor-and-language-service-extensions.md)」を参照してください。

## <a name="language-services"></a>言語サービス
 Visual Studio エディターで新しいプログラミング キーワードや新しいプログラミング言語をサポートする場合は、言語サービスを作成します。 各言語サービスは、特定のエディター機能を完全に実装する場合があります。 言語サービスでは、構成方法に応じて、構文の強調表示、中かっこの一致、IntelliSense のサポート、およびエディターのその他の機能を提供できます。

 言語サービスの中心には、パーサーとスキャナーがあります。 スキャナ (またはレキサー) は、ソース ファイルをトークンと呼ばれる要素に分割し、パーサーはそれらのトークン間の関係を確立します。 言語サービスを作成する場合、Visual Studio が言語のトークンと文法を理解できるように、パーサーとスキャナーを実装する必要があります。 マネージ言語サービスまたはアンマネージ言語サービスを作成できます。 詳細については、「[レガシ言語サービスの機能拡張](../../extensibility/internals/legacy-language-service-extensibility.md)」を参照してください。

## <a name="projects"></a>プロジェクト

Visual Studio では、プロジェクトは、開発者がソース コードやその他のリソースを編成およびビルドするために使用するコンテナーです。 プロジェクトを使用すると、ソース コード、Web サービスやデータベース、およびその他のリソースを整理、ビルド、デバッグ、および配置できます。 VSPackage は、プロジェクトの種類、プロジェクトのサブタイプ、およびカスタム ツールを提供することで、Visual Studio プロジェクト システムを拡張できます。

プロジェクトは、アプリケーションを作成するために連携して動作する 1 つ以上のプロジェクトのグループである*ソリューション*に集めることもできます。 ソリューションに関連するプロジェクトと状態の情報は、テキスト ベースの[ソリューション (.sln) ファイル](solution-dot-sln-file.md)とバイナリ ソリューション ユーザー[オプション (.suo) ファイル](solution-user-options-dot-suo-file.md)の 2 つのソリューション ファイルに格納されます。 これらのファイルは、以前のバージョンの Visual Basic で使用されていたグループ (.vbg) ファイル、および以前のバージョンの C++ で使用されていたワークスペース (.dsw) ファイルおよびユーザー オプション (.opt) ファイルに似ています。

詳細については、「[プロジェクト](../../extensibility/internals/projects.md)と[ソリューション](../../extensibility/internals/solutions-overview.md)」を参照してください。

## <a name="project-and-item-templates"></a>プロジェクト テンプレートと項目テンプレート
 Visual Studio には、定義済みのプロジェクト テンプレートとプロジェクト項目テンプレートが含まれています。 独自のテンプレートを作成したり、コミュニティからテンプレートを取得したりして、Visual Studio に統合することもできます。 [MSDN コード ギャラリー](https://code.msdn.microsoft.com/site/search?query=visual%20studio)は、テンプレートと拡張機能を提供する場所です。

 テンプレートには、特定の種類のアプリケーション、コントロール、ライブラリ、またはクラスをビルドするために必要なプロジェクト構造と基本ファイルが含まれています。 テンプレートのいずれかと類似したソフトウェアを開発する場合は、テンプレートに基づくプロジェクトを作成し、そのプロジェクト内のファイルを変更します。

> [!NOTE]
> このテンプレート アーキテクチャは、プロジェクト[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]ではサポートされていません。

 詳細については、「[プロジェクトおよびプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)」を参照してください。

## <a name="properties-and-options"></a>プロパティとオプション
 **[プロパティ]** ウィンドウには、選択した 1 つまたは複数の項目のプロパティが表示されます:[拡張プロパティ](../../extensibility/internals/extending-properties.md)のオプション ページには、プログラミング言語や VSPackage:[オプションとオプション ページ](../../extensibility/internals/options-and-options-pages.md)など、特定のコンポーネントに関連するオプションのセットが含まれています。 設定は一般的に、インポートおよびエクスポートできる UI 関連[の](../../extensibility/internals/support-for-user-settings.md)機能です。

## <a name="visual-studio-services"></a>ビジュアル スタジオ サービス
 サービスは、コンポーネントが使用する特定のインターフェイス のセットを提供します。 Visual Studio には、拡張機能を含む任意のコンポーネントで使用できる一連のサービスが用意されています。 たとえば、Visual Studio サービスを使用すると、ツール ウィンドウを動的に表示または非表示にしたり、ヘルプ、ステータス バー、UI イベントにアクセスしたりできます。 また、Visual Studio エディターには、エディター拡張機能によってインポートできるサービスも用意されています。 詳細については、「[サービスの使用と提供](../../extensibility/using-and-providing-services.md)」を参照してください。

## <a name="debugger"></a>デバッガー
 デバッガーは、言語固有のデバッグ コンポーネントへのユーザー インターフェイスです。 新しい言語サービスを作成した場合は、デバッガーにフックする特定のデバッグ エンジンを作成する必要があります。 詳細については、「 [Visual Studio デバッガーの機能拡張](../../extensibility/debugger/visual-studio-debugger-extensibility.md)」を参照してください。

## <a name="source-control"></a>ソース管理
 ソース管理プラグインまたは VSPackage の実装については、「[ソース管理](../../extensibility/internals/source-control.md)」を参照してください。

## <a name="wizards"></a>ウィザード
 新しいプロジェクトの種類と共にウィザードを作成すると、ユーザーがその種類の新しいプロジェクトを作成するときに、ウィザードを使用して適切な判断を行うことができます。 詳細については、「[ウィザード](../../extensibility/internals/wizards.md)」を参照してください。

## <a name="custom-tools"></a>カスタム ツール
 カスタム ツールを使用すると、ツールをプロジェクト内の項目に関連付け、ファイルが保存されるたびにそのツールを実行できます。 詳細については、「[カスタム ツール](../../extensibility/internals/custom-tools.md)」を参照してください。

## <a name="vssdk-utilities"></a>VSSDK ユーティリティ
 VSSDK には、VS パッケージのさまざまな側面を操作するために必要なユーティリティのセットが含まれています。 詳細については、「 [VSSDK ユーティリティ](../../extensibility/internals/vssdk-utilities.md)」を参照してください。

## <a name="using-windows-installer"></a>Windows インストーラの使用
 場合によっては、VSIX インストーラーではなく Windows インストーラーを使用する必要があります。 拡張機能で Windows インストーラーを使用する方法については、「 [Windows インストーラーを使用した VSPackage のインストール](../../extensibility/internals/installing-vspackages-with-windows-installer.md)」を参照してください。

## <a name="help-viewer"></a>ヘルプ ビューアー
 ヘルプ ビューアーに独自のヘルプと F1 ページを統合できます。 詳細については、 [Microsoft ヘルプ ビューアー SDK](../../extensibility/internals/microsoft-help-viewer-sdk.md)を参照してください。

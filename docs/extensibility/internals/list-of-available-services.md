---
title: 利用可能なサービスの一覧 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- services, Visual Studio
- Visual Studio, services
ms.assetid: 724eb24b-b87c-4971-a2e7-adee7afc03b2
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6bd7aea3adbb3a732b83736e5824d775824cccdb
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66344850"
---
# <a name="list-of-available-services"></a>使用可能なサービスの一覧

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Visual Studio SDK は、次のサービスをサポートします。 一部のパッケージは、ここに記載されていない独自のサービスを提供するなど、言語サービスには 1 つのサービス GUID はありません。 言語の名前を使用して、レジストリ内で、言語サービスの GUID を検索する必要があります。

次のとおり、またはその他のソース (たとえば、言語サービス) から取得したサービスの Guid を使用すると、プライマリ インターフェイスまたはサービスごとに示されるインターフェイスを取得します。

## <a name="the-services"></a>サービス

| サービス | Interface | Visual Studio | Visual Studio 2005 | 説明 |
| - | - |---------------|--------------------| - |
| <xref:Microsoft.VisualStudio.OLE.Interop.SBindHost> | <xref:Microsoft.VisualStudio.OLE.Interop.IBindHost> | はい | はい | Vspackage を取得するために使用する<xref:Microsoft.VisualStudio.OLE.Interop.IBindHost>非同期データ転送を容易に ActiveX コントロールからのインターフェイス。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SDTE> | <xref:EnvDTE.DTE> | いいえ | はい | 自動化に使用されるデザイン時の機能拡張 (DTE) オブジェクトを取得します。<br /><br /> C と C++ の ID。SID_SDTE |
| <xref:Microsoft.VisualStudio.Shell.Interop.SCodeNavigate> | <xref:Microsoft.VisualStudio.Shell.Interop.ICodeNavigate> | はい | はい | コントロールの既定のイベント ハンドラーを表示するフォーム デザイナーによって実装されます。 |
| <xref:Microsoft.VisualStudio.OLE.Interop.SContainerDispatch> | IDispatch | はい | はい | 別の VSPackage またはコントロールのオートメーション インターフェイスにアクセスするために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SExtendedTypeLib> | <xref:Microsoft.VisualStudio.Shell.Interop.IExtendedTypeLib> | はい | はい | 追加または拡張型ライブラリを作成するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SDirList> | <xref:Microsoft.VisualStudio.Shell.Interop.IDirList> | いいえ | はい | という名前のリストの一覧のコンテナーへのアクセスを提供します。たとえばのようにを検索するディレクトリのリスト、**検索し、置換** ダイアログ ボックスで、**検索対象の**ドロップダウン リスト。 <xref:Microsoft.VisualStudio.Shell.Interop.IDirList>オブジェクトできるから読み取るように書き込まれます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SIVsPackageDynamicToolOwner> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwner> | はい | はい | VSPackage が、独自のツール ウィンドウに動的に表示または非表示を有効にします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SLicensedClassManager> | <xref:Microsoft.VisualStudio.Shell.Interop.ILicensedClassManager> | はい | はい | によりに示すために VSPackage[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ライセンス キーの一覧を指定することで、必要なクラスです。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SLocalRegistry> | <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2> | はい | はい | により、ローカルの基準とした、レジストリにアクセスするために VSPackage[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]レジストリ ハイブ。 |
| <xref:Microsoft.VisualStudio.OLE.Interop.SOleComponentManager> | <xref:Microsoft.VisualStudio.OLE.Interop.IOleComponentManager> | はい | はい | メッセージ ループ、キーボードのループ、およびイベント通知などのコンポーネントの連携サービスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager> | はい | はい | さまざまなユーザー インターフェイス (UI) 要素にアクセスするために VSPackage をにより[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ヘルプ、ステータス バー、および UI イベントなど。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SOleInPlaceComponent> | <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent> | はい | はい | UI とその UI を統合するために VSPackage をにより[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SOleInPlaceComponentSite> | <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentSite> | はい | はい | ツールに固有の UI の変更を制御するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.OLE.Interop.SOleUndoManager> | <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager> | はい | はい | コンテナーの元に戻すマネージャーか、そのコンテナーの元に戻すスタックに参加する、またはそのコンテナーの元に戻すスタックへのアクセスにアクセスするために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SProfferService> | <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService> | はい | はい | 独自のサービスを提供するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SProfferTypeLib> | <xref:Microsoft.VisualStudio.Shell.Interop.IProfferTypeLib> | はい | はい | タイプ ライブラリを参照できるようにするフォーム デザイナーを有効にします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> | <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> | はい | はい | 選択コンテナーの選択項目へのアクセスを提供します。 フォーム デザイナーによって使用されます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SUIHostCommandDispatcher> | <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> | はい | はい | コマンド ハンドラーのチェーンに参加しており、統合開発環境 (IDE)、または自身の代わりのコマンドを処理するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SUIHostLocale> | <xref:Microsoft.VisualStudio.Shell.Interop.IUIHostLocale> | はい | はい | ホストの UI のロケール情報へのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> | いいえ | はい | ログ記録をオンにすると、高度なメッセージを記録するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsAddProjectItemDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddProjectItemDlg> | はい | はい | アクセスを提供します、**プロジェクト項目の追加** ダイアログ ボックスを実装する Vspackage 独自**項目の追加**メニュー オプション。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsAddWebReferenceDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddWebReferenceDlg> | はい | はい | 表示、**参照の追加** ダイアログ ボックス。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsAppCommandLine> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine> | はい | はい | Devenv.exe にコマンド ライン スイッチが指定されたかどうかを判断するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCallBrowser> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCallBrowser> | いいえ | はい | により、新しいを作成するために VSPackage**呼び出しブラウザー**のデバッグに使用します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsClassView> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsClassView> | はい | はい | 同期するために VSPackage をできるように、**クラス ビュー**特定のオブジェクトにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCmdNameMapping> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCmdNameMapping> | はい | はい | Guid とコマンド名をマッピングし、すべての使用可能なコマンドと名の名前を決定するためのサポートを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCodeDefView> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCodeDefView> | いいえ | はい | 操作するために VSPackage をできるように、**コード定義ビュー**します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCodeShareHandler> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCodeShareHandler> | はい | はい | 内部サービスです。 使用しないでください。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsCodeWindow> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> | はい | はい | 1 つまたは複数のドキュメントを含むことのできるコード ウィンドウへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsCodeWindowManager> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> | はい | はい | ドロップダウン バーなどのコード ウィンドウに変更を追加するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCommandWindow> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommandWindow><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommandWindow2> | はい | はい | コマンドを実行するために VSPackage をできるように、**コマンド ウィンドウ**し、それ以外の場合との対話、**コマンド ウィンドウ**します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCommandWindowsCollection> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommandWindowsCollection> | いいえ | はい | リストを操作するために VSPackage をにより**コマンド**によって管理される windows[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsComplusLibrary> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsLibraryReferenceManager> | はい | はい | 参照情報を提供する VSPackage をできるように、**オブジェクト ブラウザー**します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsComponentSelectorDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsComponentSelectorDlg> | いいえ | はい | サポートするために VSPackage をできるように、**参照の追加**オプションは、ユーザーがプロジェクトに追加する外部コンポーネントを選択できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsComponentSelectorDlg2> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsComponentSelectorDlg2> | いいえ | はい | サポートするために VSPackage をできるように、**参照の追加**オプションは、ユーザーがプロジェクトに追加する外部コンポーネントを選択できます。 ダイアログ ボックスのこのバージョンに表示される前に、コンポーネント一覧の事前設定できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsConfigurationManagerDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsConfigurationManagerDlg> | いいえ | はい | 表示、 **Configuration Manager**  ダイアログ ボックス。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCreateAggregateProject> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject> | いいえ | はい | その他のプロジェクトのコレクションを含むプロジェクトを作成するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsDebuggableProtocol> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProtocol> | はい | はい | 特定のデバッグ エンジンを開始する、IDE で使用するデバッグ可能なプロトコルの一覧を更新するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsDebugLaunch> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugLaunch> | はい | はい | デバッガーの起動をサポートするために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsDiscoveryService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDiscoveryService> | はい | はい | Web サービスの検出に使用される探索セッションを作成するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsEnumHierarchyItemsFactory> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumHierarchyItemsFactory> | はい | はい | 作成するファクトリを提供します。<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumHierarchyItemsFactory>階層 (プロジェクト) を指定するオブジェクトを列挙するために使用します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsErrorList> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsErrorList> | いいえ | はい | 操作するための追加のメソッドを提供します、**ビルド エラー一覧**タスク ウィンドウ。 具体的には、表示、**ビルド エラー一覧**タスク ウィンドウに強制的に表示されるすべてのエラーとします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsExternalFilesManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager> | はい | はい | アクセスできるように、**その他のファイル**プロジェクト ノードの現在のソリューションです。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChange> | | はい | はい | 互換性のために残されています。 使用`SVsFileChangeEx`代わりにサービスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEx> | はい | はい | IDE によってトリガーされるさまざまなファイルの変更イベントにアクセスするために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFilterAddProjectItemDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg> | はい | はい | 表示される項目をフィルター処理するために VSPackage をできるように、**項目の追加** ダイアログ ボックス。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFilterKeys> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterKeys> | はい | はい | キーボードの高度なフィルター処理を実行するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFontAndColorCacheManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager> | いいえ | はい | フォントの一連のキャッシュにアクセスを提供し、色[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を更新またはオフに特定のキャッシュまたはすべてのキャッシュ。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFontAndColorStorage> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorUtilities> | はい | はい | によって管理されるフォントと色の設定を操作するために VSPackage をにより[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]します。 さらに、このサービスは、フォントと色のデータを操作するためのユーティリティ メソッドのコレクションへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsGeneralOutputWindowPane> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> | はい | はい | [全般] にアクセスを提供します**出力ウィンドウ**ウィンドウで、必要に応じて作成します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsHelpService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsHelpSystem> | はい | はい | ヘルプ システムへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsHTMLConverter> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsHTMLConverter> | はい | はい | 使用される、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]デバッガー ハンドル HTML の出力を書式設定します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIME> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIME> | はい | はい | 入力方式エディター (IME) から API VSPackage 内へのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntegratedHelp> | <xref:Microsoft.VisualStudio.VSHelp.SVsHelp> | はい | はい | アクセスを提供します、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]ヘルプ キーワードまたは URL のシステムへのアクセスおよびナビゲーションの管理、ヘルプ ファイルを使用します。 このサービスは、ヘルプを統合する場合にのみ使用可能な[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE と外部のプログラムとして実行されていません。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntelliMouseHandler> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntelliMouseHandler> | はい | はい | マウス ホイールを使用して、マウス ホイールがクリックされたときに、スクロール、パンのビットマップを処理などの IntelliMouse 機能にアクセスするために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntellisenseEngine> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseEngine> | いいえ | はい | 読み込みまたは IntelliSense 操作のサポートの一部としてファイルをアンロードするプロジェクト階層ノードを有効にします。 読み込みとアンロード プロジェクトの IntelliSense のツールヒントに表示される内容に影響を与えるイベントをトリガーするプロセス。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntellisenseProjectHost> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProjectHost> | いいえ | はい | により、入れ子になった IntelliSense プロジェクトに関する情報を提供するプロジェクト階層ノード (実装する、<xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProject>インターフェイス)、IntelliSense のツールヒントを表示できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntellisenseProjectManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProjectManager> | いいえ | はい | 参照または IntelliSense のツールヒントに表示される内容に影響する可能性の構成の変更などのイベントのリスナーに通知する、プロジェクト階層ノードを有効にします。 含まれている言語で使用するように設計します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsInvisibleEditorManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsInvisibleEditorManager> | はい | はい | VSPackage は、「非表示」のエディターを登録する完全な編集機能を提供しますが、ユーザーには表示されませんが、エディターを使用できます。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsLanguageFilter> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> | はい | はい | データのヒントなどのテキスト ビューと単語の範囲に追加の情報を提供するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsLaunchPad> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsLaunchPad> | はい | はい | 出力は、出力ウィンドウに送信するコマンド ライン プログラムを実行する標準的な警告と、エラー ウィンドウに送信されるエラー メッセージを解析して、一時的なバッチ スクリプトを実行するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsLaunchPadFactory> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsLaunchPadFactory> | はい | はい | 作成するためのファクトリを提供します。<xref:Microsoft.VisualStudio.Shell.Interop.IVsLaunchPad>オブジェクト。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsLinkedUndoTransactionManager> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkedUndoTransactionManager> | はい | はい | リンクされた undo マネージャーにアクセスをできます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsMenuEditor> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsMenuEditorFactory> | はい | はい | 共有メニュー エディターにアクセスするフォーム デザイナーを有効にします。 IVsMenuEditorFactory を照会できます<xref:Microsoft.VisualStudio.Shell.Interop.IVsMenuEditor>します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsMonitorUserContext> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorUserContext> | はい | はい | 「コンテキスト バッグ」、特定のコンテキストのヘルプ キーワードを関連付けるために使用を作成するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjBrowser> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjBrowser> | はい | はい | 特定のオブジェクトに移動するために VSPackage をできるように、**オブジェクト ブラウザー**します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager> | はい | はい | 有効では、そのライブラリ マネージャーを登録するために VSPackage[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]など、名前空間、クラスと列挙型のオブジェクトを管理するためです。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectSearch> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectSearch> | はい | はい | 特定のオブジェクトを検索するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsOpenProjectOrSolutionDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsOpenProjectOrSolutionDlg> | いいえ | はい | により、標準を使用するために VSPackage[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]プロジェクトまたはソリューションを開く ダイアログ ボックス。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsOutputWindow> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> | はい | はい | [全般] の [出力] ウィンドウで追加の出力ウィンドウを作成するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsParseCommandLine> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsParseCommandLine> | はい | はい | 実装できるように、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>コマンドラインを解析するインターフェイス。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsPathVariableResolver> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPathVariableResolver> | いいえ | はい | 固有の変数を解決する方法を提供します[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]最後のパスを生成するパスに埋め込まれているとします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsPreviewChangesService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPreviewChangesService> | いいえ | はい | 表示、**変更のプレビュー**  ダイアログ ボックスのコードのリファクタリングのために使用します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsProfileDataManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsProfileDataManager> | いいえ | はい | プロファイル マネージャーへのアクセスを提供[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]をインポートして設定データをエクスポートすると、現在のユーザーのプロファイル設定の UI を表示することができます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsProfilesManagerUI> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsProfilesManagerUI> | いいえ | はい | 現在のユーザーのプロファイル設定を表示するダイアログ ボックスが表示されます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsPropertyPageFrame> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPageFrame> | はい | はい | 有効にするプロパティ ページが最初に示したをオーバーライドするために VSPackage、**プロパティ**ウィンドウ。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> | いいえ | はい | Vspackage によってファイルがメモリ内で変更または保存にソース管理プロバイダーに通知するために使用します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterDebugTargetProvider> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectDebugTargetProvider> | いいえ | はい | プログラムで、デバッガーで起動するターゲットをオーバーライドする VSPackage プロジェクトを有効にします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterEditors> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors> | はい | はい | IDE で、エディター ファクトリを登録するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsRegisterFindScope> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsRegisterFindScope> | いいえ | はい | 検索スコープを登録するために VSPackage をできるように、**ファイル内の検索** ダイアログ ボックス。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterPriorityCommandTarget> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterPriorityCommandTarget> | はい | はい | すべてのコマンドを表示する VSPackage は、優先度の高いコマンドのハンドラーとして登録するために VSPackage を使用できます。 すべての場合を使用します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterProjectTypes> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes> | はい | はい | IDE でプロジェクトの種類を登録するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsResourceManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsResourceManager> | いいえ | はい | サテライト Dll からマネージ コードとアンマネージ リソースをロードするために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsResourceView> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsResourceView> | はい | はい | 使用<xref:Microsoft.VisualStudio.Shell.Interop.SVsClassView>代わりにサービスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> | はい | はい | アクセスを IDE を実行しているドキュメント テーブル (RDT) 現在のすべてを追跡するがドキュメントを開いたを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> | いいえ | はい | ソース管理に参加できるように、そのコンピューター自体をソース管理プロバイダーを登録する Vspackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccToolsOptions> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccToolsOptions> | はい | はい | 取得し、ソース管理プロバイダーのオプションを設定するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSettingsReader> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsReader> | いいえ | はい | ユーザーのプロファイル設定を読み取りアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsShell> | はい | はい | 直接対話し、その他の Vspackage を操作するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellDebugger> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugger> | はい | はい | アクセスできるように、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]デバッガー。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection> | はい | はい | 現在の選択範囲にアクセスし、コマンドの UI コンテキストを管理するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDCodeDomProvider> | IVSMDCodeDomProvider | いいえ | はい | ネイティブ コードで使用できるコード ドキュメント オブジェクト モデル (DOM) プロバイダーにアクセスできます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDDesignerService> | IVSMDCodeDomCreator<br /><br /> IVSMDDesignerService | いいえ | はい | マネージ フォーム デザイナーには、IDE のサポートへのアクセスを提供します。 `IVSMDCodeDomCreator` DOM プロバイダー コードを作成するために使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDPropertyBrowser> | IVSMDPropertyBrowser | いいえ | はい | デザイナーのプロパティの windows サービスへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDTypeResolutionService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVSMDTypeResolutionService> | いいえ | はい | 返すことができるインターフェイスにアクセスできるように、<xref:System.ComponentModel.Design.ITypeResolutionService>ネイティブ コードで使用可能なオブジェクト。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSmartOpenScope> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSmartOpenScope> | いいえ | はい | 必要に応じて、ロックを考慮して、アセンブリのスコープを表示する方法を提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution> | はい | はい | 現在のソリューションに最上位レベルのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionBuildManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager> | はい | はい | ソリューションのビルド プロセスと対話するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionObject> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution> | はい | はい | 使用して、<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>代わりにサービスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionPersistence> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> | はい | はい | 格納し、現在のソリューションの .sln ファイルから情報を取得するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSQLCLRReferences> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSQLCLRReferences> | いいえ | はい | では、追加し、マネージ コード アセンブリの参照を更新します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStartPageDownload> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStartPageDownload> | いいえ | はい | 開始およびバック グラウンド スレッドで、ダウンロード サービスを停止するための Visual Studio 2017 のスタート ページのダウンロード サービスへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbar> | はい | はい | IDE のステータス バーへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStrongNameKeys> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStrongNameKeys> | いいえ | はい | マネージ コード アセンブリの署名で使用されるパスワードで強力なキー名とキー ファイルを作成するためのメソッドへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStructuredFileIO> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStructuredFileIO> | はい | はい | 複数の形式でデータを保存するためのサポートを提供するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList> | はい | はい | IDE のタスク一覧 ウィンドウへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextImageUtilities> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextImageUtilities> | いいえ | はい | テキスト ファイルの読み込みと保存のユーティリティを提供します。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager> | はい | はい | すべてのテキスト バッファーには、IDE で使用できる (非表示の領域) の非表示のテキストのセッションへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTextOut> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTextOut> | はい | はい | Win32 のバージョンを提供します`TextOut`デバイス コンテキスト (DC のハンドルが必要) にテキストを書き込むための関数。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextSpanSet> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextSpanSet> | はい | はい | テキスト イメージまたはバッファー内のテキスト範囲の一覧へのアクセスを提供します。 このサービスは、ドキュメントのコンテナーでは、通常実装し、現在のドキュメントを参照します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsThreadedWaitDialog> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsThreadedWaitDialog> | いいえ | はい | (バック グラウンド タスクの待機に使用)、別のスレッドが待機するダイアログ ボックスを表示するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsThreadPool> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsThreadPool> | いいえ | はい | 保持して、バック グラウンド タスクを開始するために VSPackage をできるように[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolbox> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox> | はい | はい | IDE へのアクセスを提供**ツールボックス**します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolboxActiveXDataProvider> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxDataProvider> | はい | はい | 情報を取得するために VSPackage をにより**ツールボックス**項目。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolboxDataProviderRegistry> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxDataProviderRegistry> | いいえ | はい | により、全体を事前読み込みのパフォーマンス コストをかけずにツールボックス データ プロバイダーを登録するために VSPackage**ツールボックス**します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolsOptions> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolsOptions> | いいえ | はい | かを判断するために VSPackage を使用、**オプション** ダイアログ ボックスが開いているすべてのオプション ページの表示を更新するとします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments3> | いいえ | はい | プロジェクトのファイルの変更を監視して、バッチのソース管理プロバイダーに制御を提供する VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx> | はい | はい | 選択項目には、現在選択されているプロジェクト項目に影響を与える変更の IDE に通知するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIHierWinClipboardHelper> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierWinClipboardHelper> | はい | はい | その他の階層を使用して、クリップボードの使用を調整するには、VSPackage プロジェクト) などの階層を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> | はい | はい | ツール ウィンドウおよびドキュメント ウィンドウなどの IDE の UI 要素へのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellDocumentWindowMgr> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellDocumentWindowMgr> | はい | はい | データのストリームの内容に基づくすべての windows の位置を復元するか、すべてのウィンドウの位置をストリームに保存する VSPackage を使用できます。 ほとんど使用しません。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument> | はい | はい | さまざまな方法でドキュメントを開くと、どのようなドキュメントの所有者を決定する VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUpgradeLogger> | いいえ | はい | 実装によって使用される、<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory>レポート エラーおよび情報メッセージへのインターフェイス。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebBrowsingService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebBrowsingService> | はい | はい | 作成および Web のブラウズ セッションを制御するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebFavorites> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebFavorites> | はい | はい | により、ユーザーの追加する VSPackage**お気に入り**一覧。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebPreview> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebPreview> | はい | はい | 子ウィンドウに通常の Web ページをプレビューするために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebURLMRU> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebURLMRU> | はい | はい | Url の最近使用 (MRU) の一覧に URL を追加し、MRU 一覧のすべての Url の一覧を取得する VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWindowFrame> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> | はい | はい | パッケージまたはパッケージのパーツを配置する場合がある、ウィンドウ フレームを取得するために VSPackage を使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsXMLMemberIndexService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsXMLMemberIndexService> | はい | はい | 特定のメタデータ ファイルに関連付けられたドキュメントを XML 形式のファイルへのアクセスを提供します。 |

## <a name="see-also"></a>関連項目

- [サービスの使用と提供](../../extensibility/using-and-providing-services.md)

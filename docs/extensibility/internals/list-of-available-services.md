---
title: 利用可能なサービスの一覧 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- services, Visual Studio
- Visual Studio, services
ms.assetid: 724eb24b-b87c-4971-a2e7-adee7afc03b2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 302d4bcff647a74acc973c47e0b62e66c86e5859
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707340"
---
# <a name="list-of-available-services"></a>使用可能なサービスの一覧

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]と、Visual Studio SDK は、次のサービスをサポートしています。 一部のパッケージは、ここに記載されていない独自のサービスを提供します。 言語サービスの GUID をレジストリで検索するには、言語の名前を使用する必要があります。

ここに記載されているサービス GUID を使用するか、または他のソース (言語サービスなど) から取得した GUID を使用して、各サービスに表示されるプライマリ インターフェイスを取得します。

## <a name="the-services"></a>サービス

| サービス | インターフェイス | Visual Studio | Visual Studio 2005 | 説明 |
| - | - |---------------|--------------------| - |
| <xref:Microsoft.VisualStudio.OLE.Interop.SBindHost> | <xref:Microsoft.VisualStudio.OLE.Interop.IBindHost> | はい | はい | 非同期データ転送を容易にするために、ActiveX コントロールから<xref:Microsoft.VisualStudio.OLE.Interop.IBindHost>インターフェイスを取得するために VSPackages によって使用されます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SDTE> | <xref:EnvDTE.DTE> | いいえ | はい | オートメーションに使用されるデザイン時機能拡張 (DTE) オブジェクトを取得します。<br /><br /> C/C++ ID: SID_SDTE |
| <xref:Microsoft.VisualStudio.Shell.Interop.SCodeNavigate> | <xref:Microsoft.VisualStudio.Shell.Interop.ICodeNavigate> | はい | はい | コントロールの既定のイベント ハンドラーを表示するためにフォーム デザイナーによって実装されます。 |
| <xref:Microsoft.VisualStudio.OLE.Interop.SContainerDispatch> | IDispatch | はい | はい | 別の VSPackage またはコントロールのオートメーション インターフェイスにアクセスする VSPackage を有効にします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SExtendedTypeLib> | <xref:Microsoft.VisualStudio.Shell.Interop.IExtendedTypeLib> | はい | はい | VSPackage が拡張タイプ ライブラリを追加または作成できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SDirList> | <xref:Microsoft.VisualStudio.Shell.Interop.IDirList> | いいえ | はい | コンテナーの名前付きリストへのアクセスを提供します。たとえば、[検索対象] ドロップダウン リストの [**検索と置換**] ダイアログ ボックスに表示される検索ディレクトリの一覧**など**です。 オブジェクト<xref:Microsoft.VisualStudio.Shell.Interop.IDirList>は、読み取りと書き込みが可能です。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SIVsPackageDynamicToolOwner> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwner> | はい | はい | VSPackage が動的に表示または非表示に独自のツール ウィンドウを持つことができます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SLicensedClassManager> | <xref:Microsoft.VisualStudio.Shell.Interop.ILicensedClassManager> | はい | はい | VSPackage ライセンス キーの[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]一覧を指定することによって、必要なクラスを示します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SLocalRegistry> | <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2> | はい | はい | VSPackage がローカル[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]レジストリ ハイブに対する相対レジストリにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.OLE.Interop.SOleComponentManager> | <xref:Microsoft.VisualStudio.OLE.Interop.IOleComponentManager> | はい | はい | メッセージ ループ、キーボード ループ、イベント通知などのコンポーネント調整サービスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager> | はい | はい | VSPackage が、ヘルプ、ステータス バー、UI イベントなど[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、さまざまなユーザー インターフェイス (UI) 要素にアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SOleInPlaceComponent> | <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent> | はい | はい | VSPackage が UI を[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]の UI と統合できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SOleInPlaceComponentSite> | <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentSite> | はい | はい | VSPackage がツールに固有の UI の変更を制御できるようにします。 |
| <xref:Microsoft.VisualStudio.OLE.Interop.SOleUndoManager> | <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager> | はい | はい | VSPackage がコンテナーの元に戻すマネージャーにアクセスして、コンテナーの元に戻すスタックに参加するか、コンテナーの元に戻すスタックにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SProfferService> | <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService> | はい | はい | VSPackage が独自のサービスを提供できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SProfferTypeLib> | <xref:Microsoft.VisualStudio.Shell.Interop.IProfferTypeLib> | はい | はい | フォーム デザイナーが、タイプ ライブラリを参照可能にできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> | <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> | はい | はい | 選択コンテナー内の選択項目にアクセスできます。 フォーム デザイナーによって使用されます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SUIHostCommandDispatcher> | <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> | はい | はい | VSPackage がコマンド ハンドラー チェーンに参加し、統合開発環境 (IDE) またはそれ自体の代わりにコマンドを処理できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SUIHostLocale> | <xref:Microsoft.VisualStudio.Shell.Interop.IUIHostLocale> | はい | はい | ホストの UI ロケール情報へのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> | いいえ | はい | ログが有効になっているときに、VSPackage が高レベルのメッセージをログに記録できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsAddProjectItemDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddProjectItemDlg> | はい | はい | VSPackages が独自の **[項目の追加**] メニュー オプションを実装できるように、[プロジェクト項目の**追加**] ダイアログ ボックスへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsAddWebReferenceDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddWebReferenceDlg> | はい | はい | [**参照の追加]** ダイアログ ボックスを表示します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsAppCommandLine> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine> | はい | はい | コマンド ライン スイッチが devenv.exe に与えられたかどうかを VSPackage が確認できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCallBrowser> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCallBrowser> | いいえ | はい | デバッグで使用される新しい**呼び出しブラウザー**を作成する VSPackage を有効にします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsClassView> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsClassView> | はい | はい | VSPackage が**クラス ビュー**を特定のオブジェクトに同期できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCmdNameMapping> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCmdNameMapping> | はい | はい | コマンド名を GUID と戻り値にマップし、使用可能なすべてのコマンドと名前の名前を決定するサポートを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCodeDefView> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCodeDefView> | いいえ | はい | VSPackage が**コード定義ビュー**を操作できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCodeShareHandler> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCodeShareHandler> | はい | はい | 内部サービス。 使用しないでください。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsCodeWindow> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> | はい | はい | 1 つ以上のドキュメントを含めることができるコード ウィンドウへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsCodeWindowManager> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> | はい | はい | VSPackage が、ドロップダウン バーなどのコード ウィンドウに変更を追加できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCommandWindow> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommandWindow><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommandWindow2> | はい | はい | VSPackage が**コマンド ウィンドウ**を介してコマンドを実行し、それ以外の場合はコマンド**ウィンドウ**と対話できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCommandWindowsCollection> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommandWindowsCollection> | いいえ | はい | VSPackage がによって管理されている**コマンド**ウィンドウの一覧を[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]操作できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsComplusLibrary> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsLibraryReferenceManager> | はい | はい | VSPackage が**オブジェクト ブラウザー**に参照情報を提供できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsComponentSelectorDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsComponentSelectorDlg> | いいえ | はい | VSPackage が **[参照の追加]** オプションをサポートするように設定します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsComponentSelectorDlg2> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsComponentSelectorDlg2> | いいえ | はい | VSPackage が **[参照の追加]** オプションをサポートするように設定します。 このバージョンのダイアログ ボックスでは、コンポーネントリストを表示する前に事前に設定できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsConfigurationManagerDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsConfigurationManagerDlg> | いいえ | はい | **[構成マネージャー]** ダイアログ ボックスを表示します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCreateAggregateProject> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject> | いいえ | はい | VSPackage が、他のプロジェクトのコレクションを含むプロジェクトを作成できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsDebuggableProtocol> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProtocol> | はい | はい | 特定のデバッグ エンジンを起動するために IDE によって使用されるデバッグ可能なプロトコルの一覧を更新する VSPackage を有効にします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsDebugLaunch> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugLaunch> | はい | はい | VSPackage がデバッガーの起動をサポートできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsDiscoveryService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDiscoveryService> | はい | はい | VsPackage が Web サービスの探索に使用される探索セッションを作成できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsEnumHierarchyItemsFactory> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumHierarchyItemsFactory> | はい | はい | 指定した階層 (<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumHierarchyItemsFactory>プロジェクト) を列挙するために使用するオブジェクトを作成するファクトリを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsErrorList> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsErrorList> | いいえ | はい | **[ビルド エラー一覧**] タスク ウィンドウを操作するための追加メソッドを提供します。 具体的には、**ビルド エラー一覧**タスク ウィンドウを前面に表示し、すべてのエラーを強制的に表示します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsExternalFilesManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager> | はい | はい | 現在のソリューションの **[その他のファイル]** プロジェクト ノードへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChange> | | はい | はい | 互換性のために残されています。 代`SVsFileChangeEx`わりにサービスを使用してください。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEx> | はい | はい | VSPackage IDE によってトリガーされたさまざまなファイル変更イベントにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFilterAddProjectItemDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg> | はい | はい | VSPackage を有効にして、**項目の追加**] ダイアログ ボックスに表示される項目をフィルター処理します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFilterKeys> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterKeys> | はい | はい | VSPackage が高度なキーボード フィルター処理を実行できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFontAndColorCacheManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager> | いいえ | はい | 特定のキャッシュまたはすべてのキャッシュを更新またはクリアするために、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]でのフォントと色のキャッシュ セットへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFontAndColorStorage> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorUtilities> | はい | はい | VSPackage がによって保持されているフォントと色の設定を操作[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]できるようにします。 さらに、このサービスは、フォントと色データを操作するためのユーティリティ メソッドのコレクションへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsGeneralOutputWindowPane> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> | はい | はい | 必要に応じて、一般的な **[出力ウィンドウ]** ウィンドウにアクセスして作成します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsHelpService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsHelpSystem> | はい | はい | ヘルプ システムへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsHTMLConverter> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsHTMLConverter> | はい | はい | 出力を[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]書式設定するために HTML を処理するためにデバッガーで使用されます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIME> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIME> | はい | はい | VSPackage 内から入力メソッド エディター (IME) API へのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntegratedHelp> | <xref:Microsoft.VisualStudio.VSHelp.SVsHelp> | はい | はい | ヘルプ ファイルを[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]介したナビゲーション コントロールだけでなく、キーワードまたは URL アクセス用のヘルプ システムへのアクセスを提供します。 このサービスは、ヘルプが[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE に統合され、外部プログラムとして実行されていない場合にのみ使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntelliMouseHandler> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntelliMouseHandler> | はい | はい | VSPackage は、マウス ホイールを使用して、マウス ホイールがクリックされたときにスクロールビットマップとパン ビットマップを処理するなど、IntelliMouse 機能へのアクセスを取得できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntellisenseEngine> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseEngine> | いいえ | はい | プロジェクト階層ノードが IntelliSense 操作のサポートの一部としてファイルをロードまたはアンロードできるようにします。 読み込みとアンロードのプロセスは、プロジェクトの IntelliSense ツールチップに表示される内容に影響を与える可能性のあるイベントをトリガーします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntellisenseProjectHost> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProjectHost> | いいえ | はい | プロジェクト階層ノードが、IntelliSense ツールヒントに表示できる入れ子になった<xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProject>IntelliSense プロジェクト (インターフェイスを実装する) に関する情報を提供できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntellisenseProjectManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProjectManager> | いいえ | はい | プロジェクト階層ノードが、参照や構成の変更など、イベントのリスナーに通知を行い、IntelliSense ツールチップに表示される内容に影響を与える可能性があります。 包含言語で使用するように設計されています。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsInvisibleEditorManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsInvisibleEditorManager> | はい | はい | VSPackage が「非表示」エディター、つまり、完全な編集機能を提供するが、ユーザーには表示されないエディターを登録できるようにします。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsLanguageFilter> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> | はい | はい | VSPackage データ ヒントや単語の範囲などの追加情報をテキスト ビューに提供できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsLaunchPad> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsLaunchPad> | はい | はい | VSPackage が一時的なバッチ スクリプトを実行し、出力が出力ペインに送信されるコマンド ライン プログラムを実行し、エラー ウィンドウに送信される標準の警告メッセージとエラー メッセージを解析できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsLaunchPadFactory> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsLaunchPadFactory> | はい | はい | オブジェクトを作成<xref:Microsoft.VisualStudio.Shell.Interop.IVsLaunchPad>するためのファクトリを提供します。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsLinkedUndoTransactionManager> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkedUndoTransactionManager> | はい | はい | リンクされた元に戻すマネージャーへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsMenuEditor> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsMenuEditorFactory> | はい | はい | フォーム デザイナーが共有メニュー エディターにアクセスできるようにします。 IVsMenu エディタファクトリーを照会<xref:Microsoft.VisualStudio.Shell.Interop.IVsMenuEditor>できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsMonitorUserContext> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorUserContext> | はい | はい | VSPackage が特定のコンテキストのヘルプ キーワードを関連付けるために使用される "コンテキスト バッグ" を作成できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjBrowser> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjBrowser> | はい | はい | VSPackage が**オブジェクト ブラウザー**で特定のオブジェクトに移動できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager> | はい | はい | VSPackage 名前空間、クラス、列挙体などの[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]オブジェクトを管理するためのライブラリ マネージャーを登録できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectSearch> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectSearch> | はい | はい | VSPackage が特定のオブジェクトを検索できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsOpenProjectOrSolutionDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsOpenProjectOrSolutionDlg> | いいえ | はい | VSPackage が標準[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]のダイアログ ボックスを使用してプロジェクトまたはソリューションを開くことを有効にします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsOutputWindow> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> | はい | はい | VSPackage が一般的な出力ウィンドウに追加の出力ペインを作成できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsParseCommandLine> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsParseCommandLine> | はい | はい | インターフェイスの実装者がコマンド<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>ラインを解析できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsPathVariableResolver> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPathVariableResolver> | いいえ | はい | パスに固有[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]の変数を解決し、最終的なパスを作成するためのパスを解決する方法を提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsPreviewChangesService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPreviewChangesService> | いいえ | はい | リファクタリング コードで使用される **[変更のプレビュー** ] ダイアログ ボックスを表示します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsProfileDataManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsProfileDataManager> | いいえ | はい | プロファイル マネージャーへのアクセスを提供[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]し、設定データのインポートとエクスポート、および現在のユーザーのプロファイル設定の UI の表示を行うことができます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsProfilesManagerUI> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsProfilesManagerUI> | いいえ | はい | 現在のユーザーのプロファイル設定を示すダイアログ ボックスを表示します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsPropertyPageFrame> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPageFrame> | はい | はい | VSPackage を有効にして、プロパティ**ウィンドウに**最初に表示されるプロパティ ページをオーバーライドします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> | いいえ | はい | VSPackages が、ファイルがメモリ内で変更または保存されることをソース管理プロバイダに通知するために使用されます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterDebugTargetProvider> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectDebugTargetProvider> | いいえ | はい | VSPackage プロジェクトがデバッガーで起動するターゲットをプログラムによってオーバーライドできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterEditors> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors> | はい | はい | エディター ファクトリを IDE に登録する VSPackage を有効にします。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsRegisterFindScope> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsRegisterFindScope> | いいえ | はい | VSPackage を有効にして、**ファイル内の検索**ダイアログ ボックスの検索範囲を登録します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterPriorityCommandTarget> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterPriorityCommandTarget> | はい | はい | VSPackage がすべてのコマンドを表示できるように、高優先度のコマンド ハンドラーとして自身を登録する VSPackage を有効にします。 少しも使って下さいます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterProjectTypes> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes> | はい | はい | VSPackage が IDE にプロジェクトの種類を登録できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsResourceManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsResourceManager> | いいえ | はい | VSPackage がマネージ リソースとアンマネージ リソースをサテライト DLL から読み込むようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsResourceView> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsResourceView> | はい | はい | 代<xref:Microsoft.VisualStudio.Shell.Interop.SVsClassView>わりにサービスを使用してください。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> | はい | はい | 現在開いているすべてのドキュメントを追跡する IDE の実行中のドキュメント テーブル (RDT) へのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> | いいえ | はい | VSPackages がソース管理に参加できるように、VSPackages が自身をソース管理プロバイダーに登録できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccToolsOptions> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccToolsOptions> | はい | はい | VSPackage がソース管理プロバイダーのオプションを取得および設定できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSettingsReader> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsReader> | いいえ | はい | ユーザーのプロファイル設定への読み取りアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsShell> | はい | はい | VSPackage が直接対話し、他の VS パッケージを操作できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellDebugger> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugger> | はい | はい | デバッガーへのアクセスを[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection> | はい | はい | VSPackage が現在の選択にアクセスし、コマンド UI コンテキストを管理できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDCodeDomProvider> | アイヴスドムコードドムプロバイダー | いいえ | はい | ネイティブ コードで使用できるコード ドキュメント オブジェクト モデル (DOM) プロバイダーへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDDesignerService> | アイヴスMDコードドムクリエーター<br /><br /> アイヴスMDデザイナーサービス | いいえ | はい | マネージ フォーム デザイナーに対する IDE のサポートへのアクセスを提供します。 を`IVSMDCodeDomCreator`使用して、コード DOM プロバイダーを作成できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDPropertyBrowser> | プロパティブラウザー | いいえ | はい | デザイナー プロパティ ウィンドウ サービスへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDTypeResolutionService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVSMDTypeResolutionService> | いいえ | はい | ネイティブ コードで使用できるオブジェクトを返<xref:System.ComponentModel.Design.ITypeResolutionService>すことができるインターフェイスへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSmartOpenScope> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSmartOpenScope> | いいえ | はい | 必要に応じてロックを考慮して、アセンブリのスコープを開く方法を提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution> | はい | はい | 現在のソリューションへのトップレベル アクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionBuildManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager> | はい | はい | VSPackage がソリューションのビルド プロセスと対話できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionObject> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution> | はい | はい | 代わりに<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>サービスを使用してください。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionPersistence> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> | はい | はい | VSPackage が現在のソリューションの .sln ファイルから情報を格納および取得できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSQLCLRReferences> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSQLCLRReferences> | いいえ | はい | マネージ コード アセンブリで参照を追加および更新する機能を提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStartPageDownload> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStartPageDownload> | いいえ | はい | バックグラウンド スレッドでダウンロード サービスを開始および停止するための Visual Studio 2017 スタート ページのダウンロード サービスへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbar> | はい | はい | IDE のステータスバーにアクセスできます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStrongNameKeys> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStrongNameKeys> | いいえ | はい | マネージ コード アセンブリの署名に使用されるパスワードを使用して、強力なキー名とキー ファイルを作成するためのメソッドへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStructuredFileIO> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStructuredFileIO> | はい | はい | VSPackage が複数の形式でデータを保存するためのサポートを提供できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList> | はい | はい | IDE の [タスク一覧] ウィンドウにアクセスします。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextImageUtilities> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextImageUtilities> | いいえ | はい | テキスト ファイルを読み込み、保存するためのユーティリティを提供します。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager> | はい | はい | IDE で使用できるすべてのテキスト バッファーと、非表示のテキスト セッション (非表示の領域) へのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTextOut> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTextOut> | はい | はい | デバイス コンテキストにテキストを書き`TextOut`込む Win32 関数のバージョンを提供します (DC ハンドルが必要です)。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextSpanSet> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextSpanSet> | はい | はい | テキスト イメージまたはバッファー内のテキスト範囲のリストへのアクセスを提供します。 このサービスは、通常、ドキュメントのコンテナーに実装され、現在のドキュメントを参照します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsThreadedWaitDialog> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsThreadedWaitDialog> | いいえ | はい | VSPackage が別のスレッドで待機するダイアログ ボックスを表示できるようにします (バックグラウンド タスクを待機するために使用されます)。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsThreadPool> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsThreadPool> | いいえ | はい | VSPackage がバックグラウンド タスクを開始し、その後で[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]管理できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolbox> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox> | はい | はい | IDE の**ツールボックス**へのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolboxActiveXDataProvider> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxDataProvider> | はい | はい | **VSPackage**がツールボックス項目から情報を取得できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolboxDataProviderRegistry> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxDataProviderRegistry> | いいえ | はい | ツールボックス全体を事前に読み込む際のパフォーマンスコストを発生させることなく、VSPackage がツールボックス データ プロバイダを登録**できるようにします**。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolsOptions> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolsOptions> | いいえ | はい | VSPackage を有効にして、**オプション**ダイアログ ボックスが開いているかどうかを確認し、すべてのオプション ページの表示を更新します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments3> | いいえ | はい | VSPackage プロジェクトのファイルの変更を監視し、ソース管理プロバイダーのバッチ制御を提供できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx> | はい | はい | VSPackage が、現在選択されているプロジェクト項目に影響を与える可能性のある選択項目の変更を IDE に通知できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIHierWinClipboardHelper> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierWinClipboardHelper> | はい | はい | 階層 (プロジェクト VSPackage など) がクリップボードの使用を他の階層と連携できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> | はい | はい | ツール ウィンドウやドキュメント ウィンドウなどの IDE の UI 要素にアクセスできます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellDocumentWindowMgr> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellDocumentWindowMgr> | はい | はい | VSPackage を有効にして、データストリームの内容に基づいてすべてのウィンドウの位置を復元したり、すべてのウィンドウの位置をストリームに保存します。 めったに使用されません。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument> | はい | はい | VSPackage がさまざまな方法でドキュメントを開き、どのドキュメントを所有するかを決定できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUpgradeLogger> | いいえ | はい | インターフェイスの実装者が<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory>エラーメッセージおよび情報メッセージを報告するために使用します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebBrowsingService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebBrowsingService> | はい | はい | VSPackage が Web 閲覧セッションを作成および制御できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebFavorites> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebFavorites> | はい | はい | VSPackage がユーザー**のお気に入りの**一覧に追加できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebPreview> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebPreview> | はい | はい | VSPackage が Web ページをプレビューできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebURLMRU> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebURLMRU> | はい | はい | VSPackage が、URL の最も最近使用された (MRU) リストに URL を追加し、MRU リスト内のすべての URL のリストを取得できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWindowFrame> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> | はい | はい | VSPackage パッケージまたはパッケージの一部が配置されているウィンドウ フレームを取得できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsXMLMemberIndexService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsXMLMemberIndexService> | はい | はい | 特定のメタデータ ファイルに関連付けられた XML 形式のドキュメント ファイルへのアクセスを提供します。 |

## <a name="see-also"></a>関連項目

- [サービスの使用と提供](../../extensibility/using-and-providing-services.md)

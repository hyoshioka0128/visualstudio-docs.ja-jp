---
title: 利用可能なサービスの一覧 |Microsoft Docs
description: 各サービスのインターフェイスを取得するためのサービス Guid を含む、Visual Studio と Visual Studio SDK でサポートされている利用可能なサービスの一覧を表示します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 53ab3531e67be540f7c66da52b7e5152a510fa27
ms.sourcegitcommit: a436ba564717b992eb1984b28ea0aec801eacaec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98204645"
---
# <a name="list-of-available-services"></a>使用可能なサービスの一覧

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] また、Visual Studio SDK では次のサービスがサポートされています。 一部のパッケージには、ここには記載されていない独自のサービスが用意されています。たとえば、言語サービスには1つのサービス GUID がありません。 言語の名前を使用して、レジストリ内の言語サービスの GUID を検索する必要があります。

ここに記載されているサービス Guid を使用するか、他のソース (言語サービスなど) から取得したサービス Guid を使用して、各サービスに表示される主要なインターフェイスまたはインターフェイスを取得します。

## <a name="the-services"></a>サービス

| サービス | インターフェイス | Visual Studio | Visual Studio 2005 | 説明 |
| - | - |---------------|--------------------| - |
| <xref:Microsoft.VisualStudio.OLE.Interop.SBindHost> | <xref:Microsoft.VisualStudio.OLE.Interop.IBindHost> | はい | Yes | <xref:Microsoft.VisualStudio.OLE.Interop.IBindHost>非同期データ転送を容易にするために、ActiveX コントロールからインターフェイスを取得するために vspackage によって使用されます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SDTE> | <xref:EnvDTE.DTE> | いいえ | はい | オートメーションに使用されるデザイン時拡張機能 (DTE) オブジェクトを取得します。<br /><br /> C/C + + ID: SID_SDTE |
| <xref:Microsoft.VisualStudio.Shell.Interop.SCodeNavigate> | <xref:Microsoft.VisualStudio.Shell.Interop.ICodeNavigate> | Yes | Yes | コントロールの既定のイベントハンドラーを表示するためにフォームデザイナーによって実装されます。 |
| <xref:Microsoft.VisualStudio.OLE.Interop.SContainerDispatch> | IDispatch | Yes | Yes | VSPackage が別の VSPackage またはコントロールのオートメーションインターフェイスにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SExtendedTypeLib> | <xref:Microsoft.VisualStudio.Shell.Interop.IExtendedTypeLib> | Yes | Yes | VSPackage が拡張タイプライブラリを追加または作成できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SDirList> | <xref:Microsoft.VisualStudio.Shell.Interop.IDirList> | いいえ | はい | リストのコンテナーの名前付きリストへのアクセスを提供します。たとえば、検索するディレクトリの一覧は、[検索 **対象**] ドロップダウンリストの [**検索と置換**] ダイアログボックスに表示されます。 オブジェクトは、 <xref:Microsoft.VisualStudio.Shell.Interop.IDirList> に書き込むことができるだけでなく、読み取ることもできます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SIVsPackageDynamicToolOwner> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwner> | Yes | Yes | VSPackage が独自のツールウィンドウを動的に表示または非表示にできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SLicensedClassManager> | <xref:Microsoft.VisualStudio.Shell.Interop.ILicensedClassManager> | Yes | Yes | ライセンスキーの一覧を指定することによって、VSPackage が必要なクラスを示すことができるようにし [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SLocalRegistry> | <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2> | Yes | Yes | VSPackage がローカルレジストリハイブに対してレジストリにアクセスできるように [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] します。 |
| <xref:Microsoft.VisualStudio.OLE.Interop.SOleComponentManager> | <xref:Microsoft.VisualStudio.OLE.Interop.IOleComponentManager> | Yes | Yes | メッセージループ、キーボードループ、イベント通知などのコンポーネント調整サービスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager> | Yes | Yes | VSPackage が、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ヘルプ、ステータスバー、UI イベントなど、のさまざまなユーザーインターフェイス (ui) 要素にアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SOleInPlaceComponent> | <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent> | Yes | Yes | VSPackage が UI をの UI と統合できるように [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SOleInPlaceComponentSite> | <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentSite> | Yes | Yes | ツールに固有の UI の変更を VSPackage が制御できるようにします。 |
| <xref:Microsoft.VisualStudio.OLE.Interop.SOleUndoManager> | <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager> | Yes | Yes | VSPackage がコンテナーの元に戻すマネージャーにアクセスし、そのコンテナーの元に戻すスタックに参加させるか、またはそのコンテナーの元に戻すスタックにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SProfferService> | <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService> | Yes | Yes | VSPackage が独自のサービスを提供できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SProfferTypeLib> | <xref:Microsoft.VisualStudio.Shell.Interop.IProfferTypeLib> | Yes | Yes | フォームデザイナーで、タイプライブラリを参照できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> | <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> | Yes | Yes | 選択コンテナー内の選択項目へのアクセスを提供します。 フォームデザイナーによって使用されます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SUIHostCommandDispatcher> | <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> | Yes | Yes | VSPackage をコマンドハンドラーチェーンに参加させ、統合開発環境 (IDE: integrated development environment) またはそれ自体の代わりにコマンドを処理できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SUIHostLocale> | <xref:Microsoft.VisualStudio.Shell.Interop.IUIHostLocale> | Yes | Yes | ホストの UI ロケール情報へのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> | いいえ | はい | ログ記録が有効になっている場合に、VSPackage が高レベルのメッセージをログに記録できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsAddProjectItemDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddProjectItemDlg> | Yes | Yes | [ **プロジェクト項目の追加** ] ダイアログボックスへのアクセスを提供し、vspackage が独自の [ **項目の追加** ] メニューオプションを実装できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsAddWebReferenceDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddWebReferenceDlg> | Yes | Yes | [ **参照の追加** ] ダイアログボックスを表示します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsAppCommandLine> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine> | Yes | Yes | コマンドラインスイッチが devenv.exe に与えられたかどうかを VSPackage が判断できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCallBrowser> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCallBrowser> | いいえ | はい | VSPackage がデバッグで使用する新しい **呼び出しブラウザー** を作成できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsClassView> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsClassView> | Yes | Yes | VSPackage が特定のオブジェクトと **クラスビュー** を同期できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCmdNameMapping> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCmdNameMapping> | Yes | Yes | では、コマンド名を Guid にマップしたり、使用可能なすべてのコマンドと名前を取得したり、名前を指定したりするためのサポートを提供しています。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCodeDefView> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCodeDefView> | いいえ | はい | VSPackage が **コード定義ビュー** を操作できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCodeShareHandler> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCodeShareHandler> | Yes | Yes | 内部サービス。 使用しないでください。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsCodeWindow> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> | Yes | Yes | 1つ以上のドキュメントを含むことができるコードウィンドウへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsCodeWindowManager> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> | Yes | Yes | VSPackage がドロップダウンバーなどのコードウィンドウに変更を追加できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCommandWindow> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommandWindow><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommandWindow2> | Yes | Yes | VSPackage がコマンド **ウィンドウ** でコマンドを実行できるようにします。それ以外の場合は、コマンド **ウィンドウ** と対話します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCommandWindowsCollection> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommandWindowsCollection> | いいえ | はい | VSPackage が、によって管理される **コマンド** ウィンドウの一覧を操作できるように [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsComplusLibrary> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsLibraryReferenceManager> | Yes | Yes | VSPackage が参照情報を **オブジェクトブラウザー** に提供できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsComponentSelectorDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsComponentSelectorDlg> | いいえ | はい | VSPackage が [ **参照の追加** ] オプションをサポートできるようにします。これにより、ユーザーは、プロジェクトに追加する外部コンポーネントを選択できるようになります。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsComponentSelectorDlg2> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsComponentSelectorDlg2> | いいえ | はい | VSPackage が [ **参照の追加** ] オプションをサポートできるようにします。これにより、ユーザーは、プロジェクトに追加する外部コンポーネントを選択できるようになります。 このバージョンのダイアログボックスを使用すると、コンポーネントリストが表示される前に事前設定できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsConfigurationManagerDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsConfigurationManagerDlg> | いいえ | はい | [ **Configuration Manager** ] ダイアログボックスを表示します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCreateAggregateProject> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject> | いいえ | はい | VSPackage が、他のプロジェクトのコレクションを含むプロジェクトを作成できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsDebuggableProtocol> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProtocol> | Yes | Yes | 特定のデバッグエンジンを開始するために IDE によって使用されるデバッグ可能なプロトコルのリストを VSPackage が更新できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsDebugLaunch> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugLaunch> | Yes | Yes | VSPackage がデバッガーの開始をサポートできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsDiscoveryService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDiscoveryService> | Yes | Yes | VSPackage が、Web サービスの検出に使用される探索セッションを作成できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsEnumHierarchyItemsFactory> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumHierarchyItemsFactory> | Yes | Yes | <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumHierarchyItemsFactory>指定された階層 (プロジェクト) を列挙するために使用するオブジェクトを作成するためのファクトリを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsErrorList> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsErrorList> | いいえ | はい | [ **ビルドエラー一覧** タスク] ウィンドウを操作するための追加のメソッドを提供します。 具体的には、は [ **ビルドエラー一覧** タスク] ウィンドウを forefront に取り込み、すべてのエラーを強制的に表示します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsExternalFilesManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager> | Yes | Yes | 現在のソリューションの [ **その他のファイル** プロジェクトノードへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChange> | | Yes | Yes | 互換性のために残されています。 `SVsFileChangeEx`代わりにサービスを使用してください。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEx> | Yes | Yes | VSPackage が IDE によってトリガーされるさまざまなファイル変更イベントにアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFilterAddProjectItemDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg> | Yes | Yes | VSPackage が [ **項目の追加** ] ダイアログボックスに表示される項目をフィルター処理できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFilterKeys> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterKeys> | Yes | Yes | VSPackage が高度なキーボードフィルター処理を実行できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFontAndColorCacheManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager> | いいえ | はい | [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]特定のキャッシュまたはすべてのキャッシュを更新またはクリアするために、のフォントおよび色のキャッシュセットへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFontAndColorStorage> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorUtilities> | Yes | Yes | VSPackage が、によって保持されるフォントと色の設定を操作できるように [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] します。 また、このサービスでは、フォントおよびカラーデータを操作するためのユーティリティメソッドのコレクションにアクセスできます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsGeneralOutputWindowPane> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> | Yes | Yes | [全般 **出力ウィンドウ** ] ウィンドウへのアクセスを提供し、必要に応じて作成します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsHelpService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsHelpSystem> | Yes | Yes | ヘルプシステムへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsHTMLConverter> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsHTMLConverter> | Yes | Yes | HTML を処理して出力を書式設定するために、デバッガーによって使用され [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIME> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIME> | Yes | Yes | VSPackage 内から入力方式エディター (IME) API へのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntegratedHelp> | <xref:Microsoft.VisualStudio.VSHelp.SVsHelp> | Yes | Yes | [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]キーワードまたは URL アクセスのヘルプシステムへのアクセス、およびヘルプファイルを使用したナビゲーションコントロールへのアクセスを提供します。 このサービスは、ヘルプが IDE に統合され、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 外部プログラムとして実行されていない場合にのみ使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntelliMouseHandler> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntelliMouseHandler> | Yes | Yes | マウスホイールを使用したり、マウスホイールをクリックしたときに、スクロールやパンのビットマップを処理したりするなど、VSPackage が IntelliMouse 機能にアクセスできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntellisenseEngine> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseEngine> | いいえ | はい | IntelliSense 操作のサポートの一部として、プロジェクト階層ノードがファイルの読み込みまたはアンロードを行うことができるようにします。 プロジェクトの IntelliSense のツールヒントに表示される内容に影響する可能性があるトリガーイベントの読み込みとアンロードのプロセス。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntellisenseProjectHost> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProjectHost> | いいえ | はい | プロジェクト階層ノードが、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProject> intellisense のツールヒントに表示できる入れ子になった intellisense プロジェクト (インターフェイスを実装する) に関する情報を提供できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntellisenseProjectManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProjectManager> | いいえ | はい | プロジェクト階層ノードが、参照や構成の変更などのイベントのリスナーをアドバイスできるようにします。これは、IntelliSense のツールヒントに表示される内容に影響を与えます。 含まれている言語で使用するように設計されています。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsInvisibleEditorManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsInvisibleEditorManager> | Yes | Yes | VSPackage が "不可視" エディターを登録できるようにします。これは、完全な編集機能を提供するが、ユーザーには表示されないエディターです。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsLanguageFilter> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> | Yes | Yes | VSPackage で、データヒントや単語の範囲などの追加情報をテキストビューに提供できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsLaunchPad> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsLaunchPad> | Yes | Yes | VSPackage が一時バッチスクリプトを実行し、出力が出力ウィンドウに送信されたコマンドラインプログラムを実行し、エラーウィンドウに送信される標準の警告メッセージとエラーメッセージを解析できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsLaunchPadFactory> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsLaunchPadFactory> | Yes | Yes | オブジェクトを作成するためのファクトリを提供 <xref:Microsoft.VisualStudio.Shell.Interop.IVsLaunchPad> します。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsLinkedUndoTransactionManager> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkedUndoTransactionManager> | Yes | Yes | リンクされた元に戻すマネージャーへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsMenuEditor> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsMenuEditorFactory> | Yes | Yes | フォームデザイナーが共有メニューエディターにアクセスできるようにします。 IVsMenuEditorFactory は、に対してクエリを実行でき <xref:Microsoft.VisualStudio.Shell.Interop.IVsMenuEditor> ます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsMonitorUserContext> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorUserContext> | Yes | Yes | VSPackage が "コンテキストバッグ" を作成できるようにします。これは、特定のコンテキストにヘルプキーワードを関連付けるために使用されます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjBrowser> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjBrowser> | Yes | Yes | VSPackage が **オブジェクトブラウザー** 内の特定のオブジェクトに移動できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager> | Yes | Yes | VSPackage がライブラリマネージャーをに登録し、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 名前空間、クラス、列挙などのオブジェクトを管理できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectSearch> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectSearch> | Yes | Yes | VSPackage が特定のオブジェクトを検索できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsOpenProjectOrSolutionDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsOpenProjectOrSolutionDlg> | いいえ | はい | VSPackage が標準ダイアログボックスを使用して、プロジェクトまたはソリューションを開くことができるようにし [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsOutputWindow> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> | Yes | Yes | VSPackage を使用して、[全般出力] ウィンドウに追加の出力ウィンドウを作成できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsParseCommandLine> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsParseCommandLine> | Yes | Yes | インターフェイスの実装者が <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> コマンドラインを解析できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsPathVariableResolver> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPathVariableResolver> | いいえ | はい | に固有の、パスに埋め込まれている変数を解決して [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 最終的なパスを生成する方法を提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsPreviewChangesService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPreviewChangesService> | いいえ | はい | リファクタリングコードで使用される [ **変更のプレビュー** ] ダイアログボックスを表示します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsProfileDataManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsProfileDataManager> | いいえ | はい | [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]設定データのインポートとエクスポート、および現在のユーザーのプロファイル設定の UI の表示を可能にする、のプロファイルマネージャーへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsProfilesManagerUI> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsProfilesManagerUI> | いいえ | はい | 現在のユーザーのプロファイル設定を示すダイアログボックスを表示します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsPropertyPageFrame> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPageFrame> | Yes | Yes | [ **プロパティ** ] ウィンドウに最初に表示されるプロパティページを VSPackage がオーバーライドできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> | いいえ | はい | ファイルがメモリ内で変更されようとしているか、保存されようとしていることをソース管理プロバイダーに通知するために、Vspackage によって使用されます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterDebugTargetProvider> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectDebugTargetProvider> | いいえ | はい | VSPackage プロジェクトが、デバッガーで起動するターゲットをプログラムによってオーバーライドできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterEditors> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors> | Yes | Yes | VSPackage が IDE にエディターファクトリを登録できるようにします。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsRegisterFindScope> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsRegisterFindScope> | いいえ | はい | VSPackage が [フォルダーを選択して **検索** ] ダイアログボックスに検索スコープを登録できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterPriorityCommandTarget> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterPriorityCommandTarget> | Yes | Yes | VSPackage がそれ自体を優先順位の高いコマンドハンドラーとして登録できるようにします。これにより、VSPackage はすべてのコマンドを表示できます。 まったく使用しない場合は、控えめに使用します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterProjectTypes> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes> | Yes | Yes | VSPackage がプロジェクトの種類を IDE に登録できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsResourceManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsResourceManager> | いいえ | はい | VSPackage がサテライト Dll からマネージリソースとアンマネージリソースを読み込むことができるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsResourceView> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsResourceView> | Yes | Yes | <xref:Microsoft.VisualStudio.Shell.Interop.SVsClassView>代わりにサービスを使用してください。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> | Yes | Yes | 現在開いているすべてのドキュメントを追跡する IDE の実行中ドキュメントテーブル (RDT) へのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> | いいえ | はい | Vspackage をソース管理プロバイダーに登録して、ソース管理に参加させることができるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccToolsOptions> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccToolsOptions> | Yes | Yes | VSPackage がソース管理プロバイダーオプションを取得および設定できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSettingsReader> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsReader> | いいえ | はい | ユーザーのプロファイル設定への読み取りアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsShell> | Yes | Yes | VSPackage が他の Vspackage と直接対話して操作できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellDebugger> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugger> | Yes | Yes | デバッガーへのアクセスを提供 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection> | Yes | Yes | VSPackage が現在の選択項目にアクセスし、コマンド UI コンテキストを管理できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDCodeDomProvider> | IVSMDCodeDomProvider | いいえ | はい | ネイティブコードで使用できるコードドキュメントオブジェクトモデル (DOM) プロバイダーへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDDesignerService> | IVSMDCodeDomCreator<br /><br /> IVSMDDesignerService | いいえ | はい | マネージフォームデザイナーに対する IDE のサポートへのアクセスを提供します。 は、 `IVSMDCodeDomCreator` コード DOM プロバイダーを作成するために使用できます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDPropertyBrowser> | IVSMDPropertyBrowser | いいえ | はい | デザイナープロパティ windows サービスへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDTypeResolutionService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVSMDTypeResolutionService> | いいえ | はい | ネイティブコードで使用可能なオブジェクトを返すことができるインターフェイスへのアクセスを提供 <xref:System.ComponentModel.Design.ITypeResolutionService> します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSmartOpenScope> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSmartOpenScope> | いいえ | はい | 必要に応じて、ロックを考慮して、アセンブリのスコープを開く方法を提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution> | Yes | Yes | 現在のソリューションへの最上位レベルのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionBuildManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager> | Yes | Yes | VSPackage がソリューションのビルドプロセスと対話できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionObject> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution> | Yes | Yes | <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>代わりにサービスを使用してください。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionPersistence> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> | Yes | Yes | VSPackage が現在のソリューションの .sln ファイルの情報を格納および取得できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSQLCLRReferences> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSQLCLRReferences> | いいえ | はい | マネージコードアセンブリに参照を追加および更新する機能を提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStartPageDownload> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStartPageDownload> | いいえ | はい | バックグラウンドスレッドでダウンロードサービスを開始および停止するための、Visual Studio 2017 のスタートページのダウンロードサービスへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbar> | Yes | Yes | IDE のステータスバーへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStrongNameKeys> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStrongNameKeys> | いいえ | はい | マネージコードアセンブリの署名に使用されるパスワードを使用して、厳密なキー名とキーファイルを作成するためのメソッドへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStructuredFileIO> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStructuredFileIO> | Yes | Yes | VSPackage で、データを複数の形式で保存するためのサポートを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList> | Yes | Yes | IDE の [タスク一覧] ウィンドウへのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextImageUtilities> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextImageUtilities> | いいえ | はい | テキストファイルを読み込んで保存するためのユーティリティを提供します。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager> | Yes | Yes | IDE で使用できるすべてのテキストバッファーおよび非表示のテキストセッション (非表示領域用) へのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTextOut> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTextOut> | Yes | Yes | `TextOut`デバイスコンテキストにテキストを書き込むための Win32 関数のバージョンを提供します (DC ハンドルが必要です)。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextSpanSet> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextSpanSet> | Yes | Yes | テキストイメージまたはバッファー内のテキスト範囲のリストへのアクセスを提供します。 通常、このサービスはドキュメントのコンテナーに実装され、現在のドキュメントを参照します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsThreadedWaitDialog> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsThreadedWaitDialog> | いいえ | はい | 別のスレッドで待機する (バックグラウンドタスクを待機するために使用される) ダイアログボックスを VSPackage が表示できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsThreadPool> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsThreadPool> | いいえ | はい | によって管理されるバックグラウンドタスクを VSPackage が開始できるように [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolbox> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox> | Yes | Yes | IDE の **ツールボックス** へのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolboxActiveXDataProvider> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxDataProvider> | Yes | Yes | VSPackage が **ツールボックス** 項目から情報を取得できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolboxDataProviderRegistry> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxDataProviderRegistry> | いいえ | はい | **ツールボックス** 全体をプリロードすることによるパフォーマンスコストを発生させることなく、VSPackage がツールボックスデータプロバイダーを登録できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolsOptions> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolsOptions> | いいえ | はい | VSPackage が、[ **オプション** ] ダイアログボックスが開いているかどうかを判断し、[すべてのオプション] ページの表示を更新できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments3> | いいえ | はい | VSPackage を使用して、プロジェクトのファイル内の変更を監視し、ソース管理プロバイダーに対するバッチ制御を提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx> | Yes | Yes | VSPackage が、現在選択されているプロジェクト項目に影響を与える可能性がある選択の変更を IDE に通知できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIHierWinClipboardHelper> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierWinClipboardHelper> | Yes | Yes | 階層 (プロジェクト VSPackage など) で、クリップボードの使用を他の階層と調整できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> | Yes | Yes | ツールウィンドウやドキュメントウィンドウなど、IDE の UI 要素へのアクセスを提供します。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellDocumentWindowMgr> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellDocumentWindowMgr> | Yes | Yes | VSPackage を使用すると、データストリームの内容に基づいてすべてのウィンドウの位置を復元したり、すべてのウィンドウの位置をストリームに保存したりできます。 ほとんど使用されません。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument> | Yes | Yes | VSPackage がさまざまな方法でドキュメントを開いて、どのドキュメントを所有しているかを判別できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUpgradeLogger> | いいえ | はい | インターフェイスの実装によって、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory> エラーメッセージと情報メッセージを報告するために使用されます。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebBrowsingService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebBrowsingService> | Yes | Yes | VSPackage が Web 閲覧セッションを作成および制御できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebFavorites> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebFavorites> | Yes | Yes | VSPackage がユーザーの **お気に入り** の一覧に追加されるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebPreview> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebPreview> | Yes | Yes | VSPackage が、通常は子ウィンドウで Web ページをプレビューできるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebURLMRU> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebURLMRU> | Yes | Yes | VSPackage で、最近使用した (MRU) の url の一覧に URL を追加し、MRU リスト内のすべての Url の一覧を取得できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWindowFrame> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> | Yes | Yes | パッケージまたはパッケージの一部が配置されている可能性のあるウィンドウフレームを VSPackage が取得できるようにします。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsXMLMemberIndexService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsXMLMemberIndexService> | Yes | Yes | 特定のメタデータファイルに関連付けられている XML 形式のドキュメントファイルへのアクセスを提供します。 |

## <a name="see-also"></a>こちらもご覧ください

- [サービスの使用と提供](../../extensibility/using-and-providing-services.md)

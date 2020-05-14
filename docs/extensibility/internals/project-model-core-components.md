---
title: プロジェクト モデルのコア コンポーネント |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project models, objects and interfaces
- project models, services
ms.assetid: b2f572d3-b26d-4846-92d1-84055fac141a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 34f65973f0f3edc1dd6264c32d165503dca78681
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706535"
---
# <a name="project-model-core-components"></a>プロジェクト モデルのコア コンポーネント
次の表は、プロジェクト モデルに展開します。 表は、モデルで識別されるインターフェースとサービス、および特定のオブジェクトに関連するインターフェースおよびサービスの簡単な説明を示しています。 また、テーブルには、特定のプロジェクトタイプの要件に応じて、プロジェクトの作成および保守でオプションであるその他のインタフェースが詳しく示されています。

 詳細については、「[シンボル参照ツールのサポート](../../extensibility/internals/supporting-symbol-browsing-tools.md)」を参照してください。

### <a name="package-object"></a>パッケージ オブジェクト

|インターフェイス|説明|
|---------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>|IDE で VSPackage を初期化し、そのサービスを IDE で使用できるようにします。|

### <a name="project-factory-object"></a>プロジェクト ファクトリ オブジェクト

|インターフェイス|説明|
|---------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>|新しいプロジェクトの作成と既存のプロジェクトのオープンを管理します。|

### <a name="project-objects"></a>プロジェクト オブジェクト

|インターフェイス|説明|
|----------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>|プロジェクト項目の追加と削除を管理し、エディターを開き、各ドキュメント モニカーと`VSITEMID`. `IVsProject` と `IVsProject2` から継承されます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>|ナビゲーションと表示のプロパティを管理し、イベントを提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>|ソリューション エクスプローラーにフォーカスがある場合`IOleCommandTarget`にのみ適用される[切り取り]や[名前の変更]などのコマンドに対するコマンド実行を有効にします。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|プロジェクト階層のプライマリ コマンド ターゲット インターフェイスとして機能します。 これは、オブジェクトに対してコマンドの状態または状態を照会し、コマンドを実行するための標準インタフェースです。 プロジェクトウィンドウにフォーカスがない場合に使用できます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>|プロジェクトの状態の永続化を調整します。 通常、プロジェクトの状態はプロジェクト ファイルとして保存されますが、ファイル ベースではないストレージ システムに適合させることができます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2>|プロジェクトが、ディスク上のファイルまたは他のストレージ システム内のオブジェクトとして、プロジェクト項目の永続性のすべての側面を管理できるようにします。 インターフェイス`IVsPersistHierarchyItem2`は、インターフェイスを実装していない項目に使用されます<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>|ソース コード管理との対話を調整します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfgProvider>|プロジェクトで構成情報を管理できるようにします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2>|デバッグ/リリース構成などのプロジェクト構成オブジェクトを管理します。 ビルド、配置、およびデバッグの各操作は、プロジェクト構成オブジェクトを通じて調整されます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDeleteHandler>|階層項目の削除 (破壊) または削除 (非破壊的) オプションを制御するために階層によって実装されます。 インターフェイスから、インターフェイス上`IVsHierarchyDeleteHandler`のクエリ`IVsHierarchy`インターフェイスを呼び出します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsGetCfgProvider>|`IVsCfgProvider2`インターフェイスを実装するプロジェクト オブジェクトとは異なる COM ID でインターフェイスをサポートするオブジェクトを持つ`IVsHierarchy`実装オプションを提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectStartupServices>|他の開発者がプロジェクトを拡張できるように実装されたオプションのインターフェイス。 `IVsProjectStartupServices`インターフェイスを使用すると、プロジェクト ファイルに保持する GUID を登録するサードパーティの VSPackage を使用すると、プロジェクトが読み込まれるたびに、プロジェクト ファイルにサード パーティ`QueryService`のサービス GUID を読み込み、その GUID を呼び出します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierWinClipboardHelperEvents>|切り取り、コピー、貼`UIHierarchy`り付けなどのクリップボード操作を調整するために、ウィンドウ内のソース階層によって実装されます。 このインターフェイス`AdviseClipboardHelperEvents`を使用して、クリップボード イベントを登録します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDropDataSource2>|UI 階層ウィンドウでのドラッグ アンド ドロップ操作中に、ドラッグされた項目のデータ ソースに対する相対的な情報を提供します。 インターフェイスから呼`IVsHierarchy`び出されます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDropDataTarget>|UI 階層ウィンドウでのドラッグ アンド ドロップ操作中に、ドロップ ターゲットに対するドラッグされた項目に関する情報を提供します。 インターフェイスから呼`IVsHierarchy`び出されます。|

### <a name="configuration-object"></a>構成オブジェクト

|インターフェイス|説明|
|----------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg>|構成に関する情報を提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2>|プロジェクトで構成情報を管理できるようにします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>|デバッガーの制御下でプロジェクトを実行できるようにします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>|他のプロジェクトの配置操作を実行する配置プロジェクトによって実装されます。|

### <a name="configuration-builder-object"></a>構成ビルダー オブジェクト

|インターフェイス|説明|
|----------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg>|プロジェクト構成のビルド操作を管理します。|

### <a name="additional-project-objects"></a>追加のプロジェクト オブジェクト

|インターフェイス|説明|
|----------------|--------------|
|`IDispatch`<br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.ISpecifyPropertyPages>|**[プロパティ]** ウィンドウに項目のプロパティを表示します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumOutputs>|展開の出力を表示します。|

 次の表に、プロジェクト モデルで識別されるサービスの簡単な説明を示します。

### <a name="services"></a>サービス

|サービス|説明|
|-------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterProjectTypes>|プロジェクトの種類を実装する VSPackages によって使用され、プロジェクト ファクトリが IDE に存在することを登録します。 VSPackage は、`QueryService`このサービスを呼び出し、メソッド`IVsPackage::SetSite`が呼び出されたときにプロジェクト ファクトリを登録する必要があります。 メソッドが`SetSite`呼び出されない場合、プロジェクトはインスタンス化されません。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>|プロジェクトの列挙、新しいプロジェクトの作成、プロジェクトの変更の注意など、IDE の内部の組み込みの現在のソリューションの概念へのアクセスを提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>|ソース管理に参加するプロジェクトによって呼び出されます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>|開いているドキュメントのテーブルを保持して、1 つ以上のプロジェクト アイテムが既に開かれているかどうかを確認します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument>|標準エディターまたは特定のエディターを使用してプロジェクト項目を実際に開くために呼び出されるインターフェイスとメソッドが含まれています。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>|すべてのプロジェクトが項目を追加、削除、または名前変更するときに呼び出す必要があります。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx>|ファイルまたはディレクトリへの変更を管理し、選択したファイルがディスク上で変更されたときにクライアントに通知します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>|すべてのプロジェクトと編集者が、アイテムを汚したり保存したりする前に呼び出す必要があります。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionBuildManager>|プロジェクト構成のビルド操作と配置操作の順序を管理します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellDebugger>|ほとんどのデバッグ コントロールに使用される低レベルのデバッガー サービスへのアクセスを提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>|VSPackages が現在の選択に関する情報にアクセスできるようにし、[**プロパティ]** ウィンドウとの通信を有効にします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>|ツール ウィンドウやドキュメント ウィンドウを作成および列挙したり、エラーをユーザーに報告したりするなど、UI 関連の基本的な機能を提供します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar>|IDE のステータスバーにアクセスできます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibility3>|オートメーション モデルの実装に使用します。 プロジェクト モデルでは、そのオブジェクトのインスタンスを作成できる properties オブジェクトを返します。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIHierWinClipboardHelper>|階層内のプロジェクト オブジェクトにクリップボード イベントを実装するために使用します。 `SVsUIHierWinClipboardHelper`を使用すると、切り取り、コピー、および貼り付け操作を正しく処理できます。|

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [チェック リスト: 新しいプロジェクト タイプの作成](../../extensibility/internals/checklist-creating-new-project-types.md)
- [ビルドにない: HierUtil7 プロジェクト クラスを使用してプロジェクトの種類を実装する (C++)](https://msdn.microsoft.com/library/a5c16a09-94a2-46ef-87b5-35b815e2f346)
- [シンボル参照ツールのサポート](../../extensibility/internals/supporting-symbol-browsing-tools.md)
- [プロジェクト モデルの要素](../../extensibility/internals/elements-of-a-project-model.md)

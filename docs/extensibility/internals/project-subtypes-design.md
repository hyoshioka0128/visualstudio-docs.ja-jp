---
title: プロジェクト サブタイプの設計 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, design
ms.assetid: 405488bb-1362-40ed-b0f1-04a57fc98c56
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0b939d197bfd7e58b555ca7698f08643e3d38ef2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706440"
---
# <a name="project-subtypes-design"></a>プロジェクト サブタイプのデザイン

プロジェクト サブタイプを使用すると、VSPackage は Microsoft ビルド エンジン (MSBuild) に基づいてプロジェクトを拡張できます。 集約を使用すると、実装されたコアマネージ プロジェクト システムの大部分を再利用[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]できます。

 以下のトピックでは、プロジェクトの基本設計とプロジェクトサブタイプの実装について詳しく説明します。

- プロジェクト サブタイプ設計。

- マルチレベル集計。

- サポート インターフェイス。

## <a name="project-subtype-design"></a>プロジェクト サブタイプの設計

プロジェクトサブタイプの初期化は、メイン<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>と<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>オブジェクトを集約することによって行われます。 この集計により、プロジェクトのサブタイプは、基本プロジェクトのほとんどの機能をオーバーライドまたは拡張できます。 プロジェクト のサブタイプは、 を使用して<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>、 および<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget><xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>を使用して、 および<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>プロジェクト項目の管理を使用して、 プロパティを処理する最初の機会を得ます。 プロジェクトのサブタイプは、次の項目を拡張することもできます。

- プロジェクト構成オブジェクト。

- 構成依存オブジェクト。

- 構成に依存しない参照オブジェクト。

- プロジェクトオートメーションオブジェクト。

- プロジェクトオートメーションプロパティコレクション。

プロジェクト サブタイプによる機能拡張の詳細については、「 プロジェクト サブ[タイプによって拡張されるプロパティとメソッド](../../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)」を参照してください。

### <a name="policy-files"></a>ポリシー ファイル

環境[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]は、ポリシー ファイルの実装でプロジェクト のサブタイプを使用して基本プロジェクト システムを拡張する例を提供します。 ポリシー ファイルを使用すると、ソリューション[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]エクスプローラ、[**プロジェクトの追加]** ダイアログ ボックス、[**新しい項目の追加**] ダイアログ ボックス、[**プロパティ]** ダイアログ ボックスなどの機能を管理することで、環境の整形を行うことができます。 ポリシー サブタイプは、これらの機能を オーバーライドし<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg>、`IOleCommandTarget`<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>実装を通じて強化します。

### <a name="aggregation-mechanism"></a>集約機構

環境のプロジェクトサブタイプ集約メカニズムは、複数のレベルの集計をサポートしているため、フレーバー・プロジェクトをさらにフレーバー化することによって、高度なサブタイプを実装できます。 また、プロジェクト サブタイプのサポート オブジェクト (<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg>など) は、複数のレベルのレイヤリングを許可するように設計されています。 COM および COM の集計規則の制約に従って、内部サブタイプまたは基本プロジェクトがメソッド呼び出しの委任および参照カウントの管理に適切に参加できるように、プロジェクトのサブタイプと基本プロジェクトを協調的にプログラムする必要があります。 つまり、集計されるプロジェクトは、集計をサポートするようにプログラムする必要があります。

次の図は、複数レベルのプロジェクト サブタイプ集計の概略図を示しています。

![Visual Studio マルチレベル projectflavor グラフィック](../../extensibility/internals/media/vs_multilevelprojectflavor.gif)

マルチレベル プロジェクト サブタイプ集計は、プロジェクト サブタイプによって集計された基本プロジェクトの 3 つのレベルから構成され、さらに高度なプロジェクト サブタイプによって集計されます。 この図は、プロジェクトのサブタイプ アーキテクチャの一部として提供されるサポート[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]インターフェイスの一部に焦点を当てています。

### <a name="deployment-mechanisms"></a>展開メカニズム

プロジェクト のサブタイプによって拡張された多くの基本プロジェクト システムの機能の中には、配置メカニズムがあります。 プロジェクト サブタイプは、 で QueryInterface を呼び出<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>すことによって<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg>取得される構成インターフェイス ( や など<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider>) を実装することで、配置メカニズムに影響を与えます。 プロジェクト のサブタイプと高度なプロジェクトサブタイプの両方が異なる構成実装を追加するシナリオでは、基本`QueryInterface`プロジェクトは、高度なプロジェクトのサブ`IUnknown`タイプの を呼び出します。 内部プロジェクトのサブタイプに基本プロジェクトが求める構成実装が含まれている場合、拡張プロジェクトのサブタイプは内部プロジェクトのサブタイプによって提供される実装に委任されます。 ある集計レベルから別の集計レベルに状態を保持するメカニズムとして、プロジェクト サブタイプのすべての<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>レベルは、ビルド以外の関連 XML データをプロジェクト ファイルに保持するために実装されます。 詳細については、「 [MSBuild プロジェクト ファイルでデータを保存する](../../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)」を参照してください。 <xref:EnvDTE80.IInternalExtenderProvider>は、プロジェクトのサブタイプからオートメーション エクステンダーを取得するメカニズムとして実装されます。

次の図は、オートメーション エクステンダーの実装、特にプロジェクトの構成参照オブジェクトに焦点を当て、プロジェクトのサブタイプが基本プロジェクト システムを拡張するために使用します。

![VS プロジェクト フレーバー オート エクステンダー グラフィック](../../extensibility/internals/media/vs_projectflavorautoextender.gif)

プロジェクト のサブタイプは、オートメーション オブジェクト モデルを拡張することで、基本プロジェクト システムをさらに拡張できます。 これらは、DTE オートメーション オブジェクトの一部として定義され、Project オブジェクト、オブジェクト、および`ProjectItem``Configuration`オブジェクトを拡張するために使用されます。 詳細については、「[基本プロジェクトのオブジェクト モデルの拡張](../../extensibility/internals/extending-the-object-model-of-the-base-project.md)」を参照してください。

## <a name="multi-level-aggregation"></a>マルチレベル集計

下位レベルのプロジェクトサブタイプをラップするプロジェクトサブタイプの実装は、内部プロジェクトのサブタイプが正しく機能するように協調してプログラムする必要があります。 プログラミングの責任の一覧は次のとおりです。

- 内部<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>サブタイプをラップするプロジェクトサブタイプの実装は、両方<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Load%2A>の<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Save%2A>メソッドの内部<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>プロジェクトサブタイプの実装に委任する必要があります。

- ラッパー<xref:EnvDTE80.IInternalExtenderProvider>プロジェクトサブタイプの実装は、その内部プロジェクトサブタイプの実装に委譲する必要があります。 特に、 の<xref:EnvDTE80.IInternalExtenderProvider.GetExtenderNames%2A>実装では、内部のプロジェクトサブタイプから名前の文字列を取得し、エクステンダとして追加する文字列を連結する必要があります。

- ラッパー<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider>プロジェクトサブタイプの実装では、その内部<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg>プロジェクトサブタイプのオブジェクトをインスタンス化し、プライベートデリゲートとして保持する必要があります。 外部プロジェクトサブタイプは、最初に直接処理する構成インターフェイスを選択し、その後、内部プロジェクト サブタイプの<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg.get_CfgType%2A>実装に残りをデリゲートできます。

## <a name="supporting-interfaces"></a>サポートインターフェイス

基本プロジェクトは、プロジェクトのサブタイプによって追加されたサポート インターフェイスへの呼び出しを委任し、その実装のさまざまな側面を拡張します。 これには、プロジェクト構成オブジェクトおよびさまざまなプロパティ ブラウザー オブジェクトの拡張が含まれます。 これらのインタフェースは、最も外側`QueryInterface`の`punkOuter`プロジェクトサブタイプアグリ`IUnknown`ゲータの ( へのポインタ ) を呼び出すことによって取得されます。

|インターフェイス|プロジェクトのサブタイプ|
|---------------|---------------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg>|プロジェクトのサブタイプで次の操作を行うことができます。<br /><br /> - の実装を<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>提供します。<br />- プロジェクトのサブタイプが 独自の実装を提供できるようにすることで、デバッガーの<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>起動を制御します。<br />- の実装で`DBGLAUNCH_DesignTimeExprEval`ケースを適切に処理することで、デザイン時の式の<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.QueryDebugLaunch%2A>評価を無効にします。|
|<xref:EnvDTE80.IInternalExtenderProvider>|プロジェクトのサブタイプで次の操作を行うことができます。<br /><br /> - プロジェクト<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject>のを拡張して、プロジェクトの構成に依存しないプロパティを追加または削除します。<br />- プロジェクトのプロジェクトオートメーションオブジェクト<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_ExtObject>( ) を拡張します。<br /><br /> 上記のプロパティ値は列挙<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>体から取得されます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject>|プロジェクトの構成参照オブジェクトを指定して、プロジェクト<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg>のサブタイプをオブジェクトにマップします。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBrowseObject>|プロジェクトの構成参照オブジェクトを指定して、プロジェクト<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>サブ`VSITEMID`タイプを オブジェクトまたは オブジェクトにマップし直すことができます。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>|プロジェクト サブタイプが任意の XML 構造化データをプロジェクト ファイル (.vbproj または .csproj) に永続化できるようにします。 このデータは MSBuild からは表示されません。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>|プロジェクトのサブタイプで次の操作を行うことができます。<br /><br /> - 永続化する新しい MSBuild プロパティを追加します。<br />- MSBuild から不要なプロパティを削除します。<br />- MSBuild プロパティの現在の値を照会します。<br />- MSBuild プロパティの現在の値を変更します。|

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID>
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID2>

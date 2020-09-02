---
title: プロジェクトのサブタイプのデザイン |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, design
ms.assetid: 405488bb-1362-40ed-b0f1-04a57fc98c56
caps.latest.revision: 33
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0e7cd96324e5a2bbd6c9b0acf4125bc0450cfd06
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62430543"
---
# <a name="project-subtypes-design"></a>プロジェクト サブタイプのデザイン
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

プロジェクトのサブタイプを使用すると、Microsoft Build Engine (MSBuild) に基づいてプロジェクトを拡張できます。 集計を使用すると、に実装されているコアマネージプロジェクトシステムの大部分を再利用しながら、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 特定のシナリオの動作をカスタマイズできます。  
  
 次のトピックでは、プロジェクトのサブタイプの基本的な設計と実装について説明します。  
  
- プロジェクトのサブタイプのデザイン。  
  
- 複数レベルの集計。  
  
- サポートインターフェイス。  
  
## <a name="project-subtype-design"></a>プロジェクトのサブタイプのデザイン  
 プロジェクトのサブタイプの初期化は、メインのオブジェクトとオブジェクトを集計することによって実現され <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> ます。 この集計により、プロジェクトのサブタイプは、基本プロジェクトのほとんどの機能をオーバーライドまたは拡張できます。 プロジェクトのサブタイプは、、、およびを使用したコマンド、およびを使用したプロジェクト項目管理を使用して、プロパティを処理する最初の機会に <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3> なります。 プロジェクトのサブタイプも次のように拡張できます。  
  
- プロジェクト構成オブジェクト。  
  
- 構成に依存するオブジェクト。  
  
- 構成に依存しない参照オブジェクト。  
  
- プロジェクトオートメーションオブジェクト。  
  
- プロジェクトオートメーションのプロパティコレクション。  
  
  プロジェクトのサブタイプごとの機能拡張の詳細については、「 [プロジェクトのサブタイプ別に拡張されたプロパティとメソッド](../../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)」を参照してください。  
  
##### <a name="policy-files"></a>ポリシー ファイル  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]環境では、ポリシーファイルの実装でプロジェクトのサブタイプを使用して、基本プロジェクトシステムを拡張する例を示します。 ポリシーファイルを使用すると、[ソリューションエクスプローラー]、[ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **プロジェクトの追加** ] ダイアログボックス、[ **新しい項目の追加** ] ダイアログボックス、および [ **プロパティ** ] ダイアログボックスを含む機能を管理して、環境を整えることができます。 ポリシーのサブタイプは、、およびの実装を通じて、これらの機能をオーバーライドし、拡張し <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg> `IOleCommandTarget` <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> ます。  
  
##### <a name="aggregation-mechanism"></a>集計メカニズム  
 環境のプロジェクトサブタイプ集計メカニズムでは、複数レベルの集計がサポートされているため、さらに flavoring a flavored プロジェクトによって高度なサブタイプを実装できます。 また、などのプロジェクトサブタイプのサポートオブジェクトは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg> 複数レベルのレイヤーを許可するように設計されています。 COM と COM の集計規則の制約を考慮して、プロジェクトのサブタイプまたは基本プロジェクトが、メソッド呼び出しの委任と参照カウントの管理に適切に参加するように、内部サブタイプまたは基本プロジェクトを協調的にプログラミングする必要があります。 つまり、集計の対象となるプロジェクトは、集計をサポートするようにプログラミングされている必要があります。  
  
 次の図は、複数レベルのプロジェクトサブタイプ集計の概略図を示しています。  
  
 ![Visual Studio マルチレベル projectflavor グラフィック](../../extensibility/internals/media/vs-multilevelprojectflavor.gif "VS_MultilevelProjectFlavor")  
複数レベルのプロジェクトサブタイプ  
  
 複数レベルのプロジェクトサブタイプ集計は、3つのレベルで構成されます。基本プロジェクトは、プロジェクトのサブタイプによって集計され、さらに高度なプロジェクトのサブタイプによって集計されます。 この図は、プロジェクトのサブタイプアーキテクチャの一部として提供されるサポートインターフェイスの一部に焦点を当ててい [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
##### <a name="deployment-mechanisms"></a>配置メカニズム  
 プロジェクトのサブタイプによって強化された基本プロジェクトシステムの機能の中には、配置メカニズムがあります。 プロジェクトのサブタイプは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> で QueryInterface を呼び出すことによって取得される構成インターフェイス (やなど) を実装することによって、配置メカニズムに影響を及ぼし <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider> ます。 プロジェクトのサブタイプと詳細なプロジェクトのサブタイプの両方で異なる構成の実装を追加するシナリオでは、基本プロジェクトは `QueryInterface` 高度なプロジェクトサブタイプのを呼び出し `IUnknown` ます。 内部プロジェクトのサブタイプに、基本プロジェクトで要求されている構成の実装が含まれている場合、高度なプロジェクトのサブタイプは、内部プロジェクトのサブタイプによって提供される実装に委任されます。 ある集計レベルから別の集計レベルに状態を永続化するメカニズムとして、プロジェクトのサブタイプのすべてのレベルは、 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> ビルドに関連しない XML データをプロジェクトファイルに保存するために実装されます。 詳細については、「 [MSBuild プロジェクトファイルのデータの永続](../../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)化」を参照してください。 <xref:EnvDTE80.IInternalExtenderProvider> は、プロジェクトのサブタイプからオートメーションエクステンダーを取得するためのメカニズムとして実装されます。  
  
 次の図は、プロジェクトのサブタイプによって使用され、基本プロジェクトシステムを拡張するオートメーションエクステンダーの実装について説明しています。  
  
 ![VS プロジェクト フレーバー オート エクステンダー グラフィック](../../extensibility/internals/media/vs-projectflavorautoextender.gif "VS_ProjectFlavorAutoExtender")  
プロジェクトのサブタイプオートメーションエクステンダー。  
  
 プロジェクトのサブタイプは、オートメーションオブジェクトモデルを拡張することで、基本プロジェクトシステムをさらに拡張することができます。 これらは、DTE オートメーションオブジェクトの一部として定義され、プロジェクトオブジェクト、オブジェクト、およびオブジェクトを拡張するために使用され `ProjectItem` `Configuration` ます。 詳細については、「 [基本プロジェクトのオブジェクトモデルの拡張](../../extensibility/internals/extending-the-object-model-of-the-base-project.md)」を参照してください。  
  
## <a name="multi-level-aggregation"></a>複数レベルの集計  
 下位レベルのプロジェクトのサブタイプをラップするプロジェクトのサブタイプの実装は、内部プロジェクトのサブタイプが正常に機能するように、協調的にプログラミングする必要があります。 プログラミングの役割の一覧には、次のものが含まれます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>内部サブタイプをラップしているプロジェクトのサブタイプの実装は、 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> メソッドとメソッドの両方について、内部プロジェクトのサブタイプの実装にデリゲートする必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Load%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Save%2A> ます。  
  
- <xref:EnvDTE80.IInternalExtenderProvider>ラッパープロジェクトのサブタイプの実装は、その内部プロジェクトのサブタイプのをデリゲートする必要があります。 特に、の実装では、 <xref:EnvDTE80.IInternalExtenderProvider.GetExtenderNames%2A> 内部プロジェクトのサブタイプから名前の文字列を取得し、エクステンダーとして追加する文字列を連結する必要があります。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider>ラッパープロジェクトのサブタイプの実装では、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg> その内部プロジェクトのサブタイプのオブジェクトをインスタンス化し、プライベートデリゲートとして保持する必要があります。これは、ラッパープロジェクトのサブタイプの構成オブジェクトが存在することを直接認識しているのは基本プロジェクトのプロジェクト構成オブジェクトだけであるためです。 外側のプロジェクトのサブタイプでは、最初に直接処理する構成インターフェイスを選択し、その他の部分を内部プロジェクトのサブタイプの実装に委任でき <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg.get_CfgType%2A> ます。  
  
## <a name="supporting-interfaces"></a>サポートインターフェイス  
 基本プロジェクトは、プロジェクトのサブタイプによって追加されたサポートインターフェイスへの呼び出しを代行させることで、実装のさまざまな側面を拡張します。 これには、プロジェクト構成オブジェクトおよびさまざまなプロパティブラウザーオブジェクトの拡張が含まれます。 これらのインターフェイスは、 `QueryInterface` `punkOuter` `IUnknown` 最も外側のプロジェクトのサブタイプアグリゲーターの on (へのポインター) を呼び出すことによって取得されます。  
  
|インターフェイス|プロジェクトのサブタイプ|  
|---------------|---------------------|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg>|プロジェクトのサブタイプを次のように許可します。<br /><br /> -の実装を提供 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> します。<br />-プロジェクトのサブタイプが独自のの実装を提供できるようにすることで、デバッガーの起動を制御し <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg> ます。<br />- `DBGLAUNCH_DesignTimeExprEval` の実装で大文字と小文字を適切に処理することにより、デザイン時の式の評価を無効にし <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.QueryDebugLaunch%2A> ます。|  
|<xref:EnvDTE80.IInternalExtenderProvider>|プロジェクトのサブタイプを次のように許可します。<br /><br /> -プロジェクトのを拡張して、 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> プロジェクトの構成に依存しないプロパティを追加または削除します。<br />-プロジェクトのプロジェクトオートメーションオブジェクト () を拡張し <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> ます。<br /><br /> 上記のプロパティ値は列挙から取得され <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> ます。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject>|プロジェクト構成の参照オブジェクトを指定して、プロジェクトのサブタイプをオブジェクトにマップし直すことを許可し <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg> ます。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBrowseObject>|プロジェクト <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 構成の参照オブジェクトを指定して、プロジェクトのサブタイプをまたはオブジェクトにマップし直すことを許可し `VSITEMID` ます。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>|プロジェクトのサブタイプが任意の XML 構造化データをプロジェクトファイル (.vbproj または .csproj) に保持できるようにします。 このデータは MSBuild には表示されません。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>|プロジェクトのサブタイプを次のように許可します。<br /><br /> -永続化する新しい MSBuild プロパティを追加します。<br />-MSBuild から不要なプロパティを削除します。<br />-MSBuild プロパティの現在の値を照会します。<br />-MSBuild プロパティの現在の値を変更します。|  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID>   
 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID2>

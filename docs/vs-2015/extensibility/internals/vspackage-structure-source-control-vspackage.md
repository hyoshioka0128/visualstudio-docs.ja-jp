---
title: VSPackage 構造体 (ソース管理 VSPackage) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, structure
- source control packages, VSPackage overview
ms.assetid: 92722be7-b397-48c3-a7a7-0b931a341961
caps.latest.revision: 27
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 08bb0a296daca0de1c02b905a75fb10ce05f254e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68206006"
---
# <a name="vspackage-structure-source-control-vspackage"></a>VSPackage 構造 (ソース管理 VSPackage)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ソース管理パッケージ SDK は、ソース管理の実装者がソース管理機能を環境と統合できるようにする VSPackage を作成するためのガイドラインを提供し [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 VSPackage は、通常、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] レジストリエントリでパッケージによって提供されるサービスに基づいて、統合開発環境 (IDE: integrated development environment) によってオンデマンドで読み込まれる COM コンポーネントです。 すべての VSPackage は、を実装する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> ます。 VSPackage は、通常、IDE によって提供されるサービスを使用し、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 独自のサービスを提供します。  
  
 VSPackage は、そのメニュー項目を宣言し、vsct ファイルを介して既定の項目の状態を確立します。 IDE では [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 、VSPackage が読み込まれるまで、この状態のメニュー項目が表示されます。 その後、VSPackage のメソッドの実装を呼び出して、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> メニュー項目を有効または無効にします。  
  
## <a name="source-control-package-characteristics"></a>ソース管理パッケージの特性  
 ソース管理 VSPackage はに緊密に統合されてい [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
 VSPackage セマンティクスは次のとおりです。  
  
- VSPackage (インターフェイス) であることによって実装されるインターフェイス `IVsPackage`  
  
- UI コマンドの実装 (vsct ファイルとインターフェイスの実装 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> )  
  
- に VSPackage を登録 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] します。  
  
  ソース管理 VSPackage は、次の他のエンティティと通信する必要があり [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。  
  
- プロジェクト  
  
- エディター  
  
- ソリューション  
  
- Windows  
  
- 実行中のドキュメントテーブル  
  
### <a name="visual-studio-environment-services-that-may-be-consumed"></a>使用可能な Visual Studio 環境サービス  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>  
  
 SVsRegisterScciProvider サービス  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>  
  
### <a name="vsip-interfaces-implemented-and-called"></a>実装および呼び出される VSIP インターフェイス  
 ソース管理パッケージは VSPackage であるため、に登録されている他の Vspackage と直接やり取りでき [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 ソース管理機能を最大限に活用するために、ソース管理 VSPackage は、プロジェクトまたはシェルによって提供されるインターフェイスを扱うことができます。  
  
 の各プロジェクトは [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3> IDE 内でプロジェクトとして認識されるようにを実装する必要があり [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 ただし、このインターフェイスは、ソース管理には特に特殊化されていません。 ソース管理下にあると予想されるプロジェクトは、を実装し <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> ます。 このインターフェイスは、ソース管理 VSPackage によって使用されます。このインターフェイスは、プロジェクトのコンテンツを照会し、そのコンテンツ (サーバーの場所とソース管理下にあるプロジェクトのディスクの場所との間の接続を確立するために必要な情報) を提供します。  
  
 ソース管理 VSPackage はを実装します <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> 。これにより、プロジェクトはソース管理のために自身を登録し、状態のグリフを取得できます。  
  
 ソース管理 VSPackage で考慮する必要があるインターフェイスの完全な一覧については、「 [関連するサービスとインターフェイス](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [要素のデザイン](../../extensibility/internals/source-control-vspackage-design-elements.md)   
 [関連サービスとインターフェイス](../../extensibility/internals/related-services-and-interfaces-source-control-vspackage.md)

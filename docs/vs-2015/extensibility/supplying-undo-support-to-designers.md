---
title: デザイナーに取り消しサポートを提供する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- designers [Visual Studio SDK], undo support
ms.assetid: 43eb1f14-b129-404a-8806-5bf9b099b67b
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6136caaec0cb8f0d79e3fb7b96245fc3fd070710
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65675339"
---
# <a name="supplying-undo-support-to-designers"></a>デザイナー向けの元に戻す操作のサポート提供
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通常、エディターと同様に、デザイナーは、コード要素を変更するときにユーザーが最新の変更を元に戻すことができるように、元に戻す操作をサポートする必要があります。  
  
 Visual Studio で実装されているほとんどのデザイナーでは、環境によって自動的に元に戻す機能がサポートされています。  
  
 元に戻す機能のサポートを提供する必要があるデザイナーの実装:  
  
- 抽象基本クラスを実装して、元に戻す管理を提供する <xref:System.ComponentModel.Design.UndoEngine>  
  
- クラスとクラスを実装して、永続化および CodeDOM サポートを提供し <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService> <xref:System.ComponentModel.Design.IComponentChangeService> ます。  
  
  を使用したデザイナーの作成の詳細について [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] は、「 [デザイン時サポートの拡張](https://msdn.microsoft.com/library/d6ac8a6a-42fd-4bc8-bf33-b212811297e2)」を参照してください。  
  
  は、 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] 次のように既定の元に戻すインフラストラクチャを提供します。  
  
- クラスとクラスを使用して、元に戻す管理の実装を提供し <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine.UndoUnit> ます。  
  
- 既定の実装とを使用して、永続化および CodeDOM サポートを提供し <xref:System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService> <xref:System.ComponentModel.Design.IComponentChangeService> ます。  
  
## <a name="obtaining-undo-support-automatically"></a>取り消しサポートを自動的に取得する  
 で作成されたデザイナーでは [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 、デザイナーで次の操作を行うと、自動および完全復元がサポートされます。  
  
- <xref:System.Windows.Forms.Control>ユーザーインターフェイスに基づいたクラスを使用します。  
  
- は、コードの生成と永続化のために、CodeDOM ベースの標準的なコード生成および解析システムを使用します。  
  
     Visual Studio CodeDOM サポートの使用方法の詳細については、「[動的なソースコードの生成とコンパイル](https://msdn.microsoft.com/library/d077a3e8-bd81-4bdf-b6a3-323857ea30fb)」を参照してください。  
  
## <a name="when-to-use-explicit-designer-undo-support"></a>明示的なデザイナーの取り消しのサポートを使用する場合  
 デザイナーは、で提供されているもの以外のグラフィカルユーザーインターフェイス (ビューアダプター) を使用する場合、独自の元に戻す管理を提供する必要があり <xref:System.Windows.Forms.Control> ます。  
  
 この例としては、ベースのグラフィカルインターフェイスではなく、web ベースのグラフィカルデザインインターフェイスを使用して製品を作成することが考えら [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] れます。  
  
 このような場合は、を使用してこのビューアダプターを登録し、明示的な取り消しの管理を提供する必要があり [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] <xref:Microsoft.VisualStudio.Shell.Design.ProvideViewAdapterAttribute> ます。  
  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]名前空間に用意されているコード生成モデルを使用しない場合、デザイナーは CodeDOM および永続化サポートを提供する必要があり <xref:System.CodeDom> ます。  
  
## <a name="undo-support-features-of-the-designer"></a>デザイナーのサポート機能を元に戻す  
 環境 SDK には、 <xref:System.Windows.Forms.Control> ユーザーインターフェイスまたは標準の CodeDOM および永続化モデルに対してベースクラスを使用しないデザイナーが使用できる、元に戻す機能を提供するために必要なインターフェイスの既定の実装が用意されています。  
  
 クラスは、クラスの <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] <xref:System.ComponentModel.Design.UndoEngine> 実装を使用してクラスから派生し、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager> 元に戻す操作を管理します。  
  
 Visual Studio では、デザイナーを元に戻すための次の機能が用意されています。  
  
- 複数のデザイナー間でリンクされた元に戻す機能。  
  
- デザイナー内の子単位は、およびを実装することによって、親と対話でき <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoUnit> <xref:Microsoft.VisualStudio.OLE.Interop.IOleParentUndoUnit> <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine.UndoUnit> ます。  
  
  環境 SDK では、次のように指定することで、CodeDOM および永続化をサポートしています。  
  
- <xref:System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService> の実装として <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService>  
  
  <xref:System.ComponentModel.Design.IComponentChangeService>"" デザインホストによって提供される [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。  
  
## <a name="using-the-environment-sdk-features-to-supply-undo-support"></a>環境 SDK 機能を使用して取り消しサポートを提供する  
 元に戻すサポートを取得するには、デザイナーを実装するオブジェクトは次の操作を行う必要があります。  
  
- 有効な実装を使用して、クラスのインスタンスをインスタンス化および初期化し <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> <xref:System.IServiceProvider> ます。  
  
- この <xref:System.IServiceProvider> クラスは、次のサービスを提供する必要があります。  
  
  - <xref:System.ComponentModel.Design.IDesignerHost>.  
  
  - <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService>  
  
       CodeDOM シリアル化を使用するデザイナーは、の [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 実装として、で提供されるを使用することができ <xref:System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService> [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService> ます。  
  
       この場合、 <xref:System.IServiceProvider> コンストラクターに提供されるクラスは、 <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> このオブジェクトをクラスの実装として返す必要があり <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService> ます。  
  
  - <xref:System.ComponentModel.Design.IComponentChangeService>  
  
       デザインホストによって提供される既定のを使用するデザイナーに <xref:System.ComponentModel.Design.DesignSurface> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] は、クラスの既定の実装があることが保証され <xref:System.ComponentModel.Design.IComponentChangeService> ます。  
  
  ベースの元に戻すメカニズムを実装するデザイナーは、 <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> 次の場合に変更を自動的に追跡します。  
  
- プロパティの変更は、オブジェクトを使用して行われ <xref:System.ComponentModel.TypeDescriptor> ます。  
  
- <xref:System.ComponentModel.Design.IComponentChangeService> イベントは、取り消し可能な変更がコミットされると、手動で生成されます。  
  
- デザイナーでの変更は、のコンテキスト内で作成されました <xref:System.ComponentModel.Design.DesignerTransaction> 。  
  
- デザイナーは、の実装によって提供される標準の取り消し単位、またはから派生した Visual Studio 固有の実装のいずれかを使用して、元に戻す単位を明示的に作成することを選択し <xref:System.ComponentModel.Design.UndoEngine.UndoUnit> <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine.UndoUnit> ます。また、 <xref:System.ComponentModel.Design.UndoEngine.UndoUnit> との両方の実装も提供し <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoUnit> <xref:Microsoft.VisualStudio.OLE.Interop.IOleParentUndoUnit> ます。  
  
## <a name="see-also"></a>参照  
 <xref:System.ComponentModel.Design.UndoEngine>   
 <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine>   
 [デザイン時サポートの拡張](https://msdn.microsoft.com/library/d6ac8a6a-42fd-4bc8-bf33-b212811297e2)

---
title: デザイナーに取り消しサポートを提供する |Microsoft Docs
description: デザイナーで、自動的に、または Visual Studio SDK の機能を使用して、元に戻す機能を提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- designers [Visual Studio SDK], undo support
ms.assetid: 43eb1f14-b129-404a-8806-5bf9b099b67b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6b56eb762cf4a2746af04ed69c7c4c49afc15dec
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056312"
---
# <a name="supply-undo-support-to-designers"></a>デザイナーに取り消しサポートを提供する

通常、エディターと同様に、デザイナーは、コード要素を変更するときにユーザーが最新の変更を元に戻すことができるように、元に戻す操作をサポートする必要があります。

Visual Studio で実装されているほとんどのデザイナーには、環境によって自動的に提供される "元に戻す" サポートがあります。

元に戻す機能のサポートを提供する必要があるデザイナーの実装:

- 抽象基本クラスを実装して、元に戻す管理を提供する <xref:System.ComponentModel.Design.UndoEngine>

- クラスとクラスを実装して、永続化および CodeDOM サポートを提供し <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService>  <xref:System.ComponentModel.Design.IComponentChangeService> ます。

.NET Framework を使用したデザイナーの作成の詳細については、「 [Design-Time サポートの拡張](/previous-versions/37899azc(v=vs.140))」を参照してください。

は、 [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] 次のように既定の元に戻すインフラストラクチャを提供します。

- クラスとクラスを使用して、元に戻す管理の実装を提供し <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine.UndoUnit> ます。

- 既定の実装とを使用して、永続化および CodeDOM サポートを提供し <xref:System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService> <xref:System.ComponentModel.Design.IComponentChangeService> ます。

## <a name="obtain-undo-support-automatically"></a>元に戻すサポートを自動的に取得する

Visual Studio で作成されたすべてのデザイナーでは、デザイナーで次のように自動および完全な復元がサポートされています。

- <xref:System.Windows.Forms.Control>ユーザーインターフェイスに基づいたクラスを使用します。

- は、コードの生成と永続化のために、CodeDOM ベースの標準的なコード生成および解析システムを使用します。

   Visual Studio CodeDOM サポートの使用方法の詳細については、「 [動的ソースコードの生成とコンパイル](/dotnet/framework/reflection-and-codedom/dynamic-source-code-generation-and-compilation)」を参照してください。

## <a name="when-to-use-explicit-designer-undo-support"></a>明示的なデザイナーの取り消しのサポートを使用する場合
 デザイナーは、で提供されているもの以外のグラフィカルユーザーインターフェイス (ビューアダプター) を使用する場合、独自の元に戻す管理を提供する必要があり <xref:System.Windows.Forms.Control> ます。

 この例としては、.NET Framework ベースのグラフィカルインターフェイスではなく、web ベースのグラフィカルデザインインターフェイスを使用して製品を作成することが考えられます。

 このような場合は、を使用してこのビューアダプターを Visual Studio に登録し、明示的な取り消しの管理を提供する必要があり <xref:Microsoft.VisualStudio.Shell.Design.ProvideViewAdapterAttribute> ます。

 名前空間に用意されている Visual Studio コード生成モデルを使用しない場合、デザイナーは CodeDOM および永続化サポートを提供する必要があり <xref:System.CodeDom> ます。

## <a name="undo-support-features-of-the-designer"></a>デザイナーのサポート機能を元に戻す
 環境 SDK には、 <xref:System.Windows.Forms.Control> ユーザーインターフェイスまたは標準の CodeDOM および永続化モデルに対してベースクラスを使用しないデザイナーが使用できる、元に戻す機能を提供するために必要なインターフェイスの既定の実装が用意されています。

 クラスは、 <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> <xref:System.ComponentModel.Design.UndoEngine> 元に <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager> 戻す操作を管理するクラスの実装を使用して .NET Framework クラスから派生します。

 Visual Studio では、デザイナーを元に戻すための次の機能が用意されています。

- 複数のデザイナー間でリンクされた元に戻す機能。

- デザイナー内の子単位は、およびを実装することによって、親と対話でき <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoUnit> <xref:Microsoft.VisualStudio.OLE.Interop.IOleParentUndoUnit> <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine.UndoUnit> ます。

環境 SDK では、次のように指定することで、CodeDOM および永続化をサポートしています。

- <xref:System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService> の実装として <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService>

- <xref:System.ComponentModel.Design.IComponentChangeService>Visual Studio デザインホストによって提供される。

## <a name="use-the-environment-sdk-features-to-supply-undo-support"></a>環境 SDK 機能を使用して取り消しサポートを提供する

元に戻すサポートを取得するには、デザイナーを実装するオブジェクトが、有効な実装を使用してクラスのインスタンスをインスタンス化し、初期化する必要があり <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> <xref:System.IServiceProvider> ます。 この <xref:System.IServiceProvider> クラスは、次のサービスを提供する必要があります。

- <xref:System.ComponentModel.Design.IDesignerHost>.

- <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService>

   Visual Studio CodeDOM シリアル化を使用するデザイナーは、の実装として、で提供されるを使用することができ <xref:System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService> [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService> ます。

   この場合、 <xref:System.IServiceProvider> コンストラクターに提供されるクラスは、 <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> このオブジェクトをクラスの実装として返す必要があり <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService> ます。

- <xref:System.ComponentModel.Design.IComponentChangeService>

   <xref:System.ComponentModel.Design.DesignSurface>Visual Studio デザインホストによって提供される既定のを使用するデザイナーには、クラスの既定の実装があることが保証され <xref:System.ComponentModel.Design.IComponentChangeService> ます。

ベースの元に戻すメカニズムを実装するデザイナーは、 <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine> 次の場合に変更を自動的に追跡します。

- プロパティの変更は、オブジェクトを使用して行われ <xref:System.ComponentModel.TypeDescriptor> ます。

- <xref:System.ComponentModel.Design.IComponentChangeService> イベントは、取り消し可能な変更がコミットされると、手動で生成されます。

- デザイナーでの変更は、のコンテキスト内で作成されました <xref:System.ComponentModel.Design.DesignerTransaction> 。

- デザイナーは、の実装によって提供される標準の取り消し単位、またはから派生した Visual Studio 固有の実装のいずれかを使用して、元に戻す単位を明示的に作成することを選択し <xref:System.ComponentModel.Design.UndoEngine.UndoUnit> <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine.UndoUnit> ます。また、 <xref:System.ComponentModel.Design.UndoEngine.UndoUnit> との両方の実装も提供し <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoUnit> <xref:Microsoft.VisualStudio.OLE.Interop.IOleParentUndoUnit> ます。

## <a name="see-also"></a>こちらもご覧ください

- <xref:System.ComponentModel.Design.UndoEngine>
- <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine>
- [Design-Time サポートの拡張](/previous-versions/37899azc(v=vs.140))

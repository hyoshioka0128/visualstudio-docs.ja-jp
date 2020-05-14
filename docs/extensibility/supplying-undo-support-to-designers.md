---
title: デザイナへの取り消しサポートの提供 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- designers [Visual Studio SDK], undo support
ms.assetid: 43eb1f14-b129-404a-8806-5bf9b099b67b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0580f974c362a71c3e400946f2ad34f565ad1232
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699672"
---
# <a name="supply-undo-support-to-designers"></a>デザイナに元に戻すサポートを提供する

デザイナーは、エディターと同様に、コード要素を変更するときにユーザーが最近の変更を元に戻すことができるように、通常、元に戻す操作をサポートする必要があります。

Visual Studio に実装されているほとんどのデザイナーは、環境によって自動的に提供される "元に戻す" サポートを持っています。

元に戻す機能のサポートを提供する必要があるデザイナーの実装:

- 抽象基本クラスを実装して元に戻す管理を提供する<xref:System.ComponentModel.Design.UndoEngine>

- のクラスを実装して、永続性と<xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService> <xref:System.ComponentModel.Design.IComponentChangeService> CodeDOM のサポートを提供します。

.NET Framework を使用してデザイナーを記述する方法の詳細については、「[デザイン時サポートの拡張](/previous-versions/37899azc(v=vs.140))」を参照してください。

では[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]、次の方法で既定の復元インフラストラクチャが提供されます。

- クラスと<xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine.UndoUnit>クラスを通じて<xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine>元に戻す管理の実装を提供します。

- 既定<xref:System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService>と実装を通じて永続化と<xref:System.ComponentModel.Design.IComponentChangeService>CodeDOM のサポートを提供します。

## <a name="obtain-undo-support-automatically"></a>取り消しサポートを自動的に取得する

Visual Studio で作成されたデザイナーは、次の場合に自動および完全な取り消しのサポートを提供します。

- 基になるクラスを<xref:System.Windows.Forms.Control>ユーザー インターフェイスに使用します。

- コードの生成と永続性のために、標準の CodeDOM ベースのコード生成および解析システムを採用します。

   Visual Studio CodeDOM サポートの操作の詳細については、「[動的ソース コードの生成とコンパイル](/dotnet/framework/reflection-and-codedom/dynamic-source-code-generation-and-compilation)」を参照してください。

## <a name="when-to-use-explicit-designer-undo-support"></a>明示的なデザイナーの取り消しサポートを使用する場合
 デザイナーは、ビュー アダプターと呼ばれるグラフィカル ユーザー インターフェイスを使用する場合は、独自の元に戻す管理を<xref:System.Windows.Forms.Control>提供する必要があります。

 たとえば、.NET Framework ベースのグラフィカル インターフェイスではなく、Web ベースのグラフィカル デザイン インターフェイスを使用して製品を作成する場合があります。

 このような場合は、このビュー アダプターをを使用して<xref:Microsoft.VisualStudio.Shell.Design.ProvideViewAdapterAttribute>Visual Studio に登録し、明示的な元に戻す管理を提供する必要があります。

 デザイナーは、名前空間で提供される Visual Studio のコード生成モデルを使用しない場合は、CodeDOM と永続化のサポートを提供する<xref:System.CodeDom>必要があります。

## <a name="undo-support-features-of-the-designer"></a>デザイナのサポート機能を元に戻す
 Environment SDK は、ユーザー インターフェイスまたは標準 CodeDOM および永続化モデルに基づくクラス<xref:System.Windows.Forms.Control>を使用しない設計者が使用できる、元に戻すサポートを提供するために必要なインターフェイスの既定の実装を提供します。

 この<xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine>クラスは、元に戻す操作<xref:System.ComponentModel.Design.UndoEngine>を管理するクラスの実装<xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager>を使用して.NET Framework クラスから派生します。

 Visual Studio には、デザイナーを元に戻す次の機能が用意されています。

- 複数のデザイナー間でリンクされた元に戻す機能。

- デザイナー内の子ユニットは、<xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoUnit><xref:Microsoft.VisualStudio.OLE.Interop.IOleParentUndoUnit><xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine.UndoUnit>を実装して 親と対話できます。

環境 SDK は、次の情報を提供することで、CodeDOM と永続性のサポートを提供します。

- <xref:System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService>の実装として、<xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService>

- Visual <xref:System.ComponentModel.Design.IComponentChangeService> Studio デザイン ホストによって提供される。

## <a name="use-the-environment-sdk-features-to-supply-undo-support"></a>環境 SDK 機能を使用して元に戻すサポートを提供する

元に戻すサポートを取得するには、デザイナーを実装するオブジェクトは、有効な<xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine><xref:System.IServiceProvider>実装を使用してクラスのインスタンスをインスタンス化し、初期化する必要があります。 この<xref:System.IServiceProvider>クラスは、次のサービスを提供する必要があります。

- <xref:System.ComponentModel.Design.IDesignerHost>.

- <xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService>

   Visual Studio CodeDOM シリアル化を使用<xref:System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService>するデザイナーは[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]、 の実装として<xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService>提供される を使用することを選択できます。

   この場合、<xref:System.IServiceProvider><xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine>コンストラクターに提供されるクラスは、このオブジェクトを<xref:System.ComponentModel.Design.Serialization.IDesignerSerializationService>クラスの実装として返す必要があります。

- <xref:System.ComponentModel.Design.IComponentChangeService>

   Visual Studio<xref:System.ComponentModel.Design.DesignSurface>デザイン ホストによって提供される既定を使用するデザイナーは、クラスの既定の<xref:System.ComponentModel.Design.IComponentChangeService>実装を持つ保証されます。

ベースの元<xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine>に戻すメカニズムを実装しているデザイナーは、次の場合に自動的に変更を追跡します。

- プロパティは<xref:System.ComponentModel.TypeDescriptor>オブジェクトを通じて変更されます。

- <xref:System.ComponentModel.Design.IComponentChangeService>イベントは、取り消し可能な変更がコミットされると手動で生成されます。

- デザイナーの変更は、 のコンテキスト内で作成<xref:System.ComponentModel.Design.DesignerTransaction>されました。

- デザイナーは、実装によって提供される標準の取り消し単位または Visual Studio 固有<xref:System.ComponentModel.Design.UndoEngine.UndoUnit>の実装<xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine.UndoUnit>を使用して、元に戻す単位を<xref:System.ComponentModel.Design.UndoEngine.UndoUnit>明示的に作成することを選択<xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoUnit>します。 <xref:Microsoft.VisualStudio.OLE.Interop.IOleParentUndoUnit>

## <a name="see-also"></a>関連項目

- <xref:System.ComponentModel.Design.UndoEngine>
- <xref:Microsoft.VisualStudio.Shell.Design.OleUndoEngine>
- [デザイン時サポートの拡張](/previous-versions/37899azc(v=vs.140))

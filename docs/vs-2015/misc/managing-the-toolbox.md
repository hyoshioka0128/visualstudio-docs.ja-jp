---
title: ツールボックスの管理 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- Toolbox [Visual Studio SDK], automatic tab selection
- Toolbox [Visual Studio SDK], managing
ms.assetid: 3b052047-f6db-46dd-b3bf-da1c348ee410
caps.latest.revision: 33
manager: jillfra
ms.openlocfilehash: 5eeb5d06b0e689391f450fec8744fa58a41f4508
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65681541"
---
# <a name="managing-the-toolbox"></a>Managing the Toolbox
[!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] では、エディターやデザイナーなどの VSPackage を使用して **ツールボックス**のメンバーシップと外観を管理できます。  
  
 さらに、オートメーションを使用して **ツールボックス** 自体を管理できます。 オートメーションによるツールボックスの管理の詳細については、「 [How to: Control the Toolbox](https://msdn.microsoft.com/library/c9d8a18a-d2bc-43d4-a803-601bfc6a6599)」を参照してください。  
  
## <a name="automatic-toolbox-tab-selection"></a>ツールボックスのタブの自動選択  
 現在アクティブなエディターまたはデザイナーに基づいて、 **ツールボックス** の特定のタブまたはカテゴリを自動的にアクティブにできます。 たとえば、フォーム デザイナーがアクティブになっている場合、 **すべての Windows フォーム** のタブを選択できます。  
  
 このサポートは、次を必要とするエディターおよびデザイナーに限定されます。  
  
1. エディターまたはデザイナーのインスタンスを提供するファクトリ オブジェクトの実装。 デザイナーまたはエディターのファクトリ オブジェクトの実装の詳細については、「 [Editor Factories](../extensibility/editor-factories.md)」を参照してください。  
  
2. エディターまたはデザイナーが存在する場合に自動的にアクティブにするツールボックスのタブの登録。  
  
## <a name="controlling-the-toolbox"></a>ツールボックスの制御  
 オートメーションのサポートを補うために、 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] は次のインターフェイスを提供して、 **ツールボックス** の管理方法を VSPackage でより詳細に制御できるようにします。  
  
|インターフェイス|説明|  
|---------------|-----------------|  
|<xref:System.Drawing.Design.IToolboxService>|アプリケーションが <xref:System.Drawing.Design.ToolboxItem> **ツールボックス**からオブジェクトを管理、追加、および削除できるようにします。 外観および **ツールボックス** のカテゴリも構成できるようにします。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2>|アプリケーションでアクティブベースの **ツールボックス** コントロールを管理、追加、および削除したり、 **ツールボックス** のカテゴリと外観を構成したりできるようにします。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3>|永続化とローカリゼーションを完全にサポートすることで、<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> にある機能を拡張します。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox4>||  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox5>||  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox6>||  
  
 これらのインターフェイスを使用する場合に注意が必要な、いくつかの重要な点があります。  
  
- <xref:System.Drawing.Design.IToolboxService> は、Managed Package Framework ベースの VSPackage でのみ使用できます。  
  
- を使用してコントロールを **ツールボックス** に直接追加することはできません <xref:System.Drawing.Design.IToolboxService> 。  
  
- VSPackage で <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> を使用してコントロールを追加するか、<xref:System.Windows.Forms.AxHost> から派生したラッパー コントロールでコントロールをホストする必要があります。  
  
   Visual Studio には、<xref:System.Windows.Forms.AxHost> から派生したコントロールに ActiveX コントロールを自動的にラッピングするための `Aximp.exe` ツールがあります。 詳細については、「[Aximp.exe (Windows フォーム ActiveX コントロール インポーター)](https://msdn.microsoft.com/library/482c0d83-7144-4497-b626-87d2351b78d0)」をご覧ください。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox>、<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2>、および <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3> は、相互運用機能アセンブリを介して利用できる COM ベースのインターフェイスです。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> は <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox> から派生し、そのすべてのメソッドを実装します。  
  
   オブジェクトでは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> のインスタンスのみを取得します。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3> は <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> から派生せず、そのメソッドを実装しません。  
  
   両方のインターフェイスの機能が必要なオブジェクトでは、環境から両方のインターフェイスのインスタンスを取得する必要があります。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox2> と <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3> を使用するときに、タブの正規 (ローカライズされていない) 名に関する情報が <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3.GetIDOfTab%2A> および <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox3.SetIDOfTab%2A> メソッドによって処理されます。  
  
- <xref:System.Drawing.Design.IToolboxService> を使用する場合、カテゴリの名前などのローカライズされた情報は、実装者が管理します。  
  
  設定メカニズムを使用して、ユーザーがアクセスする **ツールボックス** 設定を IDE の **[ツール]** メニューの **[設定のインポートとエクスポート]** コマンドからユーザーが保存できるようにします。 設定の使用方法の詳細については、「 [Extending User Settings and Options](../extensibility/extending-user-settings-and-options.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ツールボックスの拡張](../misc/extending-the-toolbox.md)
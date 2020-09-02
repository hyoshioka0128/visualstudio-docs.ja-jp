---
title: コマンドルーティングアルゴリズム |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands, routing
- command routing
ms.assetid: 998b616b-bd08-45cb-845f-808efb8c33bc
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e3b8602df40045a3f4e1fc91fee92151bf5dd4ea
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68195108"
---
# <a name="command-routing-algorithm"></a>コマンド ルーティング アルゴリズム
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio のコマンドは、さまざまなコンポーネントによって処理されます。 コマンドは、現在の選択内容に基づいて最も内側のコンテキストから最も外側のコンテキスト (グローバルとも呼ばれます) にルーティングされます。 詳細については、「 [Availability](../../extensibility/internals/command-availability.md)」を参照してください。  
  
## <a name="order-of-command-resolution"></a>コマンドの解決順序  
 コマンドは、次のレベルのコマンドコンテキストを通じて渡されます。  
  
1. アドイン: 環境では、まず、存在するすべてのアドインに対してコマンドを提供します。  
  
2. 優先順位コマンド: これらのコマンドは、を使用して登録され <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterPriorityCommandTarget> ます。 これらは、Visual Studio のすべてのコマンドに対して呼び出され、登録された順序で呼び出されます。  
  
3. コンテキストメニューコマンド: コンテキストメニューに配置されたコマンドは、最初にコンテキストメニューに用意されているコマンドターゲットと、その後の通常のルーティングに提供されます。  
  
4. ツールバーのコマンドターゲットの設定: これらのコマンドターゲットは、を呼び出すと登録され <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell4.SetupToolbar2%2A> ます。 `pCmdTarget`パラメーターにはを指定でき `null` ます。 そうでない場合は `null` 、このコマンドターゲットを使用して、設定しているツールバーにあるすべてのコマンドを更新します。 シェルがツールバーを設定している場合は、ウィンドウフレームがとして渡され `pCmdTarget` ます。これにより、ツールバーのコマンドに対するすべての更新が、フォーカスされていない場合でも、ウィンドウフレームを通過します。  
  
5. ツールウィンドウ: 通常、インターフェイスを実装するツールウィンドウは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ツールウィンドウがアクティブなウィンドウの場合に Visual Studio がコマンドターゲットを取得できるように、インターフェイスも実装する必要があります。 ただし、フォーカスのあるツールウィンドウが **プロジェクト** ウィンドウである場合は、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> 選択された項目の共通の親であるインターフェイスにコマンドがルーティングされます。 この選択範囲が複数のプロジェクトにまたがる場合、コマンドは階層にルーティングされ <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution> ます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>インターフェイスには、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> インターフェイスの対応する <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A> コマンドに似たメソッドとメソッドが含まれてい <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ます。  
  
6. ドキュメントウィンドウ: コマンドの場合、その vsct ファイルに RouteToDocs フラグが設定されていると、Visual Studio はドキュメントビューオブジェクトでコマンドターゲットを検索します。これは、インターフェイスのインスタンスか、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> ドキュメントオブジェクトのインスタンス (通常は <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines> インターフェイスまたは <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> インターフェイス) です。 ドキュメントビューオブジェクトがコマンドをサポートしていない場合、Visual Studio は、返されたインターフェイスにコマンドをルーティングし <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ます。 (これは、ドキュメントデータオブジェクトの省略可能なインターフェイスです)。  
  
7. 現在の階層: 現在の階層は、アクティブなドキュメントウィンドウを所有するプロジェクトまたは **ソリューションエクスプローラー**で選択されている階層にすることができます。 Visual Studio は、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 現在の、またはアクティブな階層に実装されているインターフェイスを検索します。 階層では、プロジェクト項目のドキュメントウィンドウにフォーカスがある場合でも、階層がアクティブなときは常に有効なコマンドをサポートする必要があります。 ただし、 **ソリューションエクスプローラー** にフォーカスがある場合にのみ適用されるコマンドは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> インターフェイスとその <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> メソッドとメソッドを使用してサポートする必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A> ます。  
  
     **切り取り**、 **コピー**、 **貼り付け**、 **削除**、 **名前の変更**、 **Enter**、 **DoubleClick** の各コマンドでは、特別な処理が必要です。 階層内の **Delete** および **Remove** コマンドを処理する方法の詳細については、インターフェイスを参照してください <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDeleteHandler> 。  
  
8. グローバル: コマンドが前に説明したコンテキストによって処理されていない場合、Visual Studio は、インターフェイスを実装するコマンドを所有する VSPackage へのルーティングを試み <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ます。 VSPackage がまだ読み込まれていない場合は、Visual Studio がメソッドを呼び出すと読み込まれません <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 。 VSPackage は、メソッドが呼び出されたときにのみ読み込まれ <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> ます。  
  
## <a name="see-also"></a>参照  
 [コマンド デザイン](../../extensibility/internals/command-design.md)

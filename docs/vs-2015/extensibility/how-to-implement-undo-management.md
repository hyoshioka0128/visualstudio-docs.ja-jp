---
title: '方法: 元に戻す管理を実装する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - undo management
ms.assetid: 1942245d-7a1d-4a11-b5e7-a3fe29f11c0b
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0f3d56ae02718f5dfdf373eeeb6aff774d11931e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842216"
---
# <a name="how-to-implement-undo-management"></a>方法: 元に戻すの管理を実装する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

復元の管理に使用される主なインターフェイスは <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager> で、環境によって実装されます。 元に戻す管理をサポートするには、個別の取り消し単位を実装します (つまり、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoUnit> 複数の個別の手順を含めることができます)。  
  
 元に戻す管理を実装する方法は、エディターで複数のビューがサポートされているかどうかによって異なります。 各実装の手順については、次のセクションで詳しく説明します。  
  
## <a name="cases-where-an-editor-supports-a-single-view"></a>エディターが単一のビューをサポートする場合  
 このシナリオでは、エディターは複数のビューをサポートしていません。 エディターとドキュメントは1つだけであり、元に戻す機能がサポートされています。 元に戻す管理を実装するには、次の手順に従います。  
  
#### <a name="to-support-undo-management-for-a-single-view-editor"></a>単一ビューエディターの元に戻す管理をサポートするには  
  
1. `QueryInterface` `IServiceProvider` `IOleUndoManager` ドキュメントビューオブジェクトから、元に戻すマネージャー () にアクセスするために、ウィンドウフレームのインターフェイスでを呼び出し `IID_IOLEUndoManager` ます。  
  
2. ビューがウィンドウフレームに配置されると、の呼び出しに使用できるサイトポインターが取得され `QueryInterface` `IServiceProvider` ます。  
  
## <a name="cases-where-an-editor-supports-multiple-views"></a>エディターが複数のビューをサポートする場合  
 ドキュメントとビューの分離がある場合は、通常、ドキュメント自体に関連付けられている元に戻すマネージャーが1つあります。 すべての取り消し単位は、ドキュメントデータオブジェクトに関連付けられた1つの取り消しマネージャーに配置されます。  
  
 ビューに対してクエリを実行するのではなく、ビューごとに1つの元に戻すマネージャーに対してクエリデータオブジェクトを呼び出して、 <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A> CLSID_OLEUndoManager のクラス識別子を指定して、元に戻すマネージャーをインスタンス化します。 クラス識別子は、OCUNDOID ファイルで定義されています。  
  
 を使用して <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A> 独自の undo マネージャーインスタンスを作成する場合は、次の手順を使用して、元に戻すマネージャーを環境にフックします。  
  
#### <a name="to-hook-your-undo-manager-into-the-environment"></a>Undo マネージャーを環境にフックするには  
  
1. `QueryInterface`に対してから返されたオブジェクトに対してを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2> `IID_IOleUndoManager` ます。 へのポインターを格納 <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager> します。  
  
2. に `QueryInterface` 対してを呼び出し `IOleUndoManager` `IID_IOleCommandTarget` ます。 へのポインターを格納 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> します。  
  
3. をリレー <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> し、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> `IOleCommandTarget` 次の StandardCommandSet97 コマンドのためにストアドインターフェイスに呼び出します。  
  
   - cmdidUndo  
  
   - cmdidMultiLevelUndo  
  
   - cmdidRedo  
  
   - cmdidMultiLevelRedo  
  
   - cmdidMultiLevelUndoList  
  
   - cmdidMultiLevelRedoList  
  
4. に `QueryInterface` 対してを呼び出し `IOleUndoManager` `IID_IVsChangeTrackingUndoManager` ます。 へのポインターを格納 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager> します。  
  
    、、およびメソッドを呼び出すには、へのポインターを使用し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager.MarkCleanState%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager.AdviseTrackingClient%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager.UnadviseTrackingClient%2A> ます。  
  
5. に `QueryInterface` 対してを呼び出し `IOleUndoManager` `IID_IVsLinkCapableUndoManager` ます。  
  
6. ドキュメントでを呼び出し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkCapableUndoManager.AdviseLinkedUndoClient%2A> ます。このとき、インターフェイスも実装する必要があり <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkedUndoClient> ます。 ドキュメントが閉じられたら、を呼び出し `IVsLinkCapableUndoManager::UnadviseLinkedUndoClient` ます。  
  
7. ドキュメントを閉じるときに、 `QueryInterface` の undo マネージャーでを呼び出し `IID_IVsLifetimeControlledObject` ます。  
  
8. <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLifetimeControlledObject.SeverReferencesToOwner%2A> を呼び出します。  
  
9. ドキュメントに変更が加えられたら、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager.Add%2A> クラスを使用してマネージャーでを呼び出し `OleUndoUnit` ます。 メソッドは、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager.Add%2A> オブジェクトへの参照を保持するため、通常は、の直後に解放し <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager.Add%2A> ます。  
  
   クラスは、 `OleUndoManager` 単一の undo スタックインスタンスを表します。 このため、undo または redo の追跡対象となるデータエンティティごとに1つの undo manager オブジェクトがあります。  
  
> [!NOTE]
> 元に戻すマネージャーオブジェクトはテキストエディターによって広く使用されていますが、テキストエディターを特定の方法でサポートしていない一般的なコンポーネントです。 複数レベルの元に戻すまたはやり直しをサポートする場合は、このオブジェクトを使用できます。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLifetimeControlledObject>   
 [方法: 元に戻すスタックをクリアする](../extensibility/how-to-clear-the-undo-stack.md)

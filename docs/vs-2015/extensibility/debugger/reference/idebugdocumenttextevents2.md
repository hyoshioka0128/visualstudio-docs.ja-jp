---
title: IDebugDocumentTextEvents2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugDocumentTextEvents2
helpviewer_keywords:
- IDebugDocumentTextEvents2 interface
ms.assetid: a10cbb6b-11a8-4056-b42a-2ecebf0e690d
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b574ae45dafed11ed28047859676524054951512
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65678965"
---
# <a name="idebugdocumenttextevents2"></a>IDebugDocumentTextEvents2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、デバッグエンジンによって提供されるソースドキュメントへの変更について Visual Studio に通知するために使用されます。  
  
## <a name="syntax"></a>構文  
  
```  
IDebugDocumentTextEvents2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 DE は、このインターフェイスを実装して、ソースコードに変更を加えることをサポートします。 このインターフェイスは、通常、 [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) インターフェイスを実装するのと同じオブジェクトに実装されます。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] メソッドの呼び出しによって、このインターフェイスを取得 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint.Advise%2A> します。 インターフェイスは、 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> メソッドの呼び出しから取得され <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer.EnumConnectionPoints%2A> ます。 インターフェイスは、 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)インターフェイスの[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)メソッドを呼び出すことによって取得されます。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IDebugDocumentTextEvents2` ます。  
  
|Method|説明|  
|------------|-----------------|  
|[onDestroy](../../../extensibility/debugger/reference/idebugdocumenttextevents2-ondestroy.md)|ドキュメント全体が破棄されたことを示します。|  
|[onInsertText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-oninserttext.md)|ドキュメントにテキストが挿入されたことをデバッグパッケージに通知します。|  
|[onRemoveText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onremovetext.md)|ドキュメントからテキストが削除されたことをデバッグパッケージに通知します。|  
|[onReplaceText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onreplacetext.md)|ドキュメント内でテキストが置換されたことをデバッグパッケージに通知します。|  
|[onUpdateTextAttributes](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onupdatetextattributes.md)|ドキュメントでテキスト属性が更新されたことをデバッグパッケージに通知します。|  
|[onUpdateDocumentAttributes](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onupdatedocumentattributes.md)|ドキュメント属性が更新されたことをイベントの受信者に通知します。|  
  
## <a name="remarks"></a>解説  
 独自のドキュメントを提供するデバッグエンジンのみがインターフェイスを利用 `IDebugDocumentTextEvent2` できます。 この例として、スクリプトデバッグエンジンが挙げられます。 スクリプトを解釈するプロセスでは、新しいソースコードを生成できます。これは、ディスクファイルには存在せず、DE にのみ知られています。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)   
 [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)

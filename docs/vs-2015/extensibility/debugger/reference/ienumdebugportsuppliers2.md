---
title: IEnumDebugPortSuppliers2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugPortSuppliers2
helpviewer_keywords:
- IEnumDebugPortSuppliers2
ms.assetid: cd0a73dc-dd25-46fd-8c4f-5b011501afeb
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f8ed12c0ba9c6263968c51a7e8cfcdfe2fe47011
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68179148"
---
# <a name="ienumdebugportsuppliers2"></a>IEnumDebugPortSuppliers2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、ポートサプライヤーを列挙します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IEnumDebugPortSuppliers2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 Visual Studio は、このインターフェイスを実装して、ポートサプライヤーのリストを表します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 [Enumportsuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)を呼び出して、ポートサプライヤーの一覧を取得します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IEnumDebugPortSuppliers2` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[次へ](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-next.md)|列挙シーケンス内の指定された数のポート供給元を取得します。|  
|[Skip](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-skip.md)|列挙シーケンス内の指定された数のポートサプライヤーをスキップします。|  
|[リセット](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-reset.md)|列挙シーケンスを先頭にリセットします。|  
|[複製](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|  
|[GetCount](../../../extensibility/debugger/reference/ienumdebugportsuppliers2-getcount.md)|列挙子内のポートサプライヤーの数を取得します。|  
  
## <a name="remarks"></a>注釈  
 通常、デバッグエンジンでは、このインターフェイスを取得する必要はありません。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [EnumPortSuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)

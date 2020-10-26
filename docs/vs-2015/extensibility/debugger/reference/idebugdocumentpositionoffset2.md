---
title: IDebugDocumentPositionOffset2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentPositionOffset2 interface
ms.assetid: f1b05db3-50d8-453f-a72f-e68b239236a4
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c1f30c3a465d4803e5c91f14ee45ad582e76d986
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68200214"
---
# <a name="idebugdocumentpositionoffset2"></a>IDebugDocumentPositionOffset2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ソースファイル内の文字オフセットとしての位置を表します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IDebugDocumentPositionOffset2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 IDE によって実装され、デバッグエンジンによって使用されます。  
  
## <a name="methods"></a>メソッド  
 次の表に、のメソッドを示し `IDebugDocumentPositionOffset2` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetRange](../../../extensibility/debugger/reference/idebugdocumentpositionoffset2-getrange.md)|現在のドキュメントの位置の範囲を取得します。|  
  
## <a name="remarks"></a>注釈  
 これは、 [GetRange](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md) と同じ情報を返し `char` ますが、ドキュメントの先頭からのオフセットで返されます。 これにより、通常返される行と列の情報ではなく、ディスク上に存在するようなドキュメント、つまり1次元の文字配列が示されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: Msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)

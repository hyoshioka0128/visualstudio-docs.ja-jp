---
title: 'IEnumDebugBoundBreakpoints2:: Next |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugBoundBreakpoints2::Next
helpviewer_keywords:
- IEnumDebugBoundBreakpoints2::Next
ms.assetid: cb3a249f-2282-4bdc-b6d8-a4ee4bfb8365
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b7080ab3749b3b89d249a07e209cfc123e8914a5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62551998"
---
# <a name="ienumdebugboundbreakpoints2next"></a>IEnumDebugBoundBreakpoints2::Next
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

列挙体から次の要素のセットを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Next(  
   ULONG                    celt,  
   IDebugBoundBreakpoint2** rgelt,  
   ULONG*                   pceltFetched  
);  
```  
  
```csharp  
int Next(  
   uint                     celt,  
   IDebugBoundBreakpoint2[] rgelt,  
   ref uint                 pceltFetched  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `celt`  
 から取得する要素の数。 配列の最大サイズも指定し `rgelt` ます。  
  
 `rgelt`  
 [入力、出力]入力する [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md) 要素の配列。  
  
 `pceltFetched`  
 入出力で実際に返された要素の数を返し `rgelt` ます。  
  
## <a name="return-value"></a>戻り値  
 正常に終了した場合は、`S_OK` を返します。 要求された `S_FALSE` 数の要素を返すことができなかった場合は、を返します。それ以外の場合は、エラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)   
 [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)

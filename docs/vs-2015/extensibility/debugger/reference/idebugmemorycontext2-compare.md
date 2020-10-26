---
title: 'IDebugMemoryContext2:: Compare |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2::Compare
helpviewer_keywords:
- IDebugMemoryContext2::Compare method
- Compare method
ms.assetid: c51b5128-848e-4d8e-b2e9-1161339763c3
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3eb48c324b5a1a918ab864c5eb4c4ca39eae41ac
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68163439"
---
# <a name="idebugmemorycontext2compare"></a>IDebugMemoryContext2::Compare
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

比較フラグによって示される方法で、指定された配列内の各コンテキストとメモリコンテキストを比較し、に一致する最初のコンテキストのインデックスを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Compare(   
   CONTEXT_COMPARE        compare,  
   IDebugMemoryContext2** rgpMemoryContextSet,  
   DWORD                  dwMemoryContextSetLen,  
   DWORD*                 pdwMemoryContext  
);  
```  
  
```csharp  
int Compare(  
   enum_CONTEXT_COMPARE   compare,   
   IDebugMemoryContext2[] rgpMemoryContextSet,   
   uint                   dwMemoryContextSetLen,   
   out uint               pdwMemoryContext  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `compare`  
 から比較の種類を決定する [CONTEXT_COMPARE](../../../extensibility/debugger/reference/context-compare.md) 列挙の値。  
  
 `rgpMemoryContextSet`  
 から比較する [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) オブジェクトへの参照の配列。  
  
 `dwMemoryContextSetLen`  
 から配列内のコンテキストの数 `rgpMemoryContextSet` 。  
  
 `pdwMemoryContext`  
 入出力比較を満たす最初のメモリコンテキストのインデックスを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 `E_COMPARE_CANNOT_COMPARE`2 つのコンテキストを比較できない場合はを返します。  
  
## <a name="remarks"></a>注釈  
 デバッグエンジン (DE) は、すべての種類の比較をサポートする必要はありませんが、少なくとも、、およびをサポートする必要があり `CONTEXT_EQUAL` `CONTEXT_LESS_THAN` `CONTEXT_GREATER_THAN` `CONTEXT_SAME_SCOPE` ます。  
  
## <a name="see-also"></a>参照  
 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)   
 [CONTEXT_COMPARE](../../../extensibility/debugger/reference/context-compare.md)

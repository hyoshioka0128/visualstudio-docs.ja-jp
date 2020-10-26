---
title: CONTEXT_COMPARE |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- CONTEXT_COMPARE
helpviewer_keywords:
- CONTEXT_COMPARE enumeration
ms.assetid: 701ed61c-a320-4c20-a335-0b840024abc0
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a9cf283cf7239b5ed74e38ca534538a286a477c2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68179966"
---
# <a name="context_compare"></a>CONTEXT_COMPARE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

2つのメモリコンテキストを比較するための条件を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_CONTEXT_COMPARE {   
   CONTEXT_EQUAL                 = 0x0001,  
   CONTEXT_LESS_THAN             = 0x0002,  
   CONTEXT_GREATER_THAN          = 0x0003,  
   CONTEXT_LESS_THAN_OR_EQUAL    = 0x0004,  
   CONTEXT_GREATER_THAN_OR_EQUAL = 0x0005,  
   CONTEXT_SAME_SCOPE            = 0x0006,  
   CONTEXT_SAME_FUNCTION         = 0x0007,  
   CONTEXT_SAME_MODULE           = 0x0008,  
   CONTEXT_SAME_PROCESS          = 0x0009  
};  
typedef DWORD CONTEXT_COMPARE;  
```  
  
```csharp  
public enum enum_CONTEXT_COMPARE {   
   CONTEXT_EQUAL                 = 0x0001,  
   CONTEXT_LESS_THAN             = 0x0002,  
   CONTEXT_GREATER_THAN          = 0x0003,  
   CONTEXT_LESS_THAN_OR_EQUAL    = 0x0004,  
   CONTEXT_GREATER_THAN_OR_EQUAL = 0x0005,  
   CONTEXT_SAME_SCOPE            = 0x0006,  
   CONTEXT_SAME_FUNCTION         = 0x0007,  
   CONTEXT_SAME_MODULE           = 0x0008,  
   CONTEXT_SAME_PROCESS          = 0x0009  
};  
```  
  
## <a name="members"></a>メンバー  
 CONTEXT_EQUAL  
 リスト内でターゲットメモリコンテキストと同じ最初のメモリコンテキストを検索します。  
  
 CONTEXT_LESS_THAN  
 リスト内でターゲットメモリコンテキストよりも小さい最初のメモリコンテキストを検索します。  
  
 CONTEXT_GREATER_THAN  
 リスト内でターゲットメモリコンテキストよりも大きい最初のメモリコンテキストを検索します。  
  
 CONTEXT_LESS_THAN_OR_EQUAL  
 リスト内でターゲットメモリコンテキスト以下の最初のメモリコンテキストを検索します。  
  
 CONTEXT_GREATER_THAN_OR_EQUAL  
 リスト内でターゲットメモリコンテキスト以上の最初のメモリコンテキストを検索します。  
  
 CONTEXT_SAME_SCOPE  
 一覧で、ターゲットメモリコンテキストと同じスコープ内にある最初のメモリコンテキストを検索します。  
  
 CONTEXT_SAME_FUNCTION  
 リスト内で、ターゲットメモリスコープと同じ関数内にある最初のメモリコンテキストを検索します。  
  
 CONTEXT_SAME_MODULE  
 ターゲットメモリコンテキストと同じモジュール内にある、リスト内の最初のメモリコンテキストを検索します。  
  
 CONTEXT_SAME_PROCESS  
 ターゲットメモリコンテキストと同じプロセスにある、一覧内の最初のメモリコンテキストを検索します。  
  
## <a name="remarks"></a>注釈  
 [Compare](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md)メソッドに引数として渡されます。  
  
 これらの値は、指定された比較条件を満たすリスト内の最初のメモリコンテキストを検索するために使用されます。 メモリコンテキストには、メソッドを通じて比較するメモリコンテキストのリストが与えられ `IDebugMemoryContext2::Compare` ます。 次に、比較演算子があるリスト内の最初のメモリコンテキスト `true` が返されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [比較](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md)

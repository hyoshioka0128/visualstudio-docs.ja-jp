---
title: DOCCONTEXT_COMPARE |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- DOCCONTEXT_COMPARE
helpviewer_keywords:
- DOCCONTEXT_COMPARE enumeration
ms.assetid: ed947c34-b07e-4b69-8381-b6e7cb842862
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6d0fd8cff2f352c8ede674be64062a738c1f3d02
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198801"
---
# <a name="doccontext_compare"></a>DOCCONTEXT_COMPARE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

2つのドキュメントコンテキストを比較するための条件を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_DOCCONTEXT_COMPARE {   
   DOCCONTEXT_EQUAL         = 0x0001,  
   DOCCONTEXT_LESS_THAN     = 0x0002,  
   DOCCONTEXT_GREATER_THAN  = 0x0003,  
   DOCCONTEXT_SAME_DOCUMENT = 0x0004  
};  
typedef DWORD DOCCONTEXT_COMPARE;  
```  
  
```csharp  
enum enum_DOCCONTEXT_COMPARE {   
   DOCCONTEXT_EQUAL         = 0x0001,  
   DOCCONTEXT_LESS_THAN     = 0x0002,  
   DOCCONTEXT_GREATER_THAN  = 0x0003,  
   DOCCONTEXT_SAME_DOCUMENT = 0x0004  
};  
```  
  
## <a name="members"></a>メンバー  
 DOCCONTEXT_EQUAL  
 リスト内でターゲットドキュメントコンテキストと同じ最初のドキュメントコンテキストを検索します。  
  
 DOCCONTEXT_LESS_THAN  
 リスト内でターゲットドキュメントコンテキストより小さい最初のドキュメントコンテキストを検索します。  
  
 DOCCONTEXT_GREATER_THAN  
 リスト内でターゲットドキュメントコンテキストよりも大きい最初のドキュメントコンテキストを検索します。  
  
 DOCCONTEXT_SAME_DOCUMENT  
 リスト内で、ターゲットドキュメントコンテキストと同じドキュメント内にある最初のドキュメントコンテキストを検索します。  
  
## <a name="remarks"></a>注釈  
 [Compare](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md)メソッドに引数として渡されます。  
  
 これらの値は、リスト内の最初のドキュメントコンテキストを検索するための比較条件を指定するために使用されます。 ドキュメントコンテキストには、メソッドを通じて比較するドキュメントコンテキストのリストが与えられ `IDebugDocumentContext2::Compare` ます。 次に、比較演算子があるリスト内の最初のドキュメントコンテキスト `true` が返されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [比較](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md)

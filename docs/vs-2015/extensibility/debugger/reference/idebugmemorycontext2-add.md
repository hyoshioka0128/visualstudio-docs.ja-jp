---
title: 'IDebugMemoryContext2:: Add |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2::Add
helpviewer_keywords:
- IDebugMemoryContext2::Add method
- Add method
ms.assetid: 3c47e646-ce9e-4dd3-8f1a-6dbd3827d407
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2b1b4b236b438d5ff94120c00952d5cd3adfd590
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68164081"
---
# <a name="idebugmemorycontext2add"></a>IDebugMemoryContext2::Add
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定した値を現在のコンテキストに追加し、新しいコンテキストを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Add(   
   UINT64                 dwCount,  
   IDebugMemoryContext2** ppMemCxt  
);  
```  
  
```csharp  
int Add(  
   ulong                    dwCount,   
   out IDebugMemoryContext2 ppMemCxt  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dwCount`  
 から現在のコンテキストに追加する値。  
  
 `ppMemCxt`  
 入出力新しい [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) オブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 メモリコンテキストはアドレスであるため、アドレスに値を追加すると、新しいコンテキストインターフェイスを必要とする新しいアドレスが生成されます。  
  
 生成されたアドレスがこのコンテキストに関連付けられているメモリ空間の範囲外であっても、このメソッドは常に新しいコンテキストを生成する必要があります。 唯一の例外は、新しいコンテキストにメモリを割り当てることができない場合、または `ppMemCxt` が null 値 (エラーの場合) である場合です。  
  
## <a name="see-also"></a>参照  
 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)

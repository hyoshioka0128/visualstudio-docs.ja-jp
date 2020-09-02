---
title: 'IDebugMemoryContext2:: 減算 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2::Subtract
helpviewer_keywords:
- Subtract method
- IDebugMemoryContext2::Subtract method
ms.assetid: 63df14c7-8d7e-47c1-afa7-5a1ab5d8eaba
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2efe4e15c5489ef07741a0d267b9c1b870d07aa8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68146369"
---
# <a name="idebugmemorycontext2subtract"></a>IDebugMemoryContext2::Subtract
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

現在のコンテキストから指定された値を減算し、新しいコンテキストを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Subtract(   
   UINT64                 dwCount,  
   IDebugMemoryContext2** ppMemCxt  
);  
```  
  
```csharp  
int Subtract(  
   ulong                    dwCount,   
   out IDebugMemoryContext2 ppMemCxt  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dwCount`  
 からデクリメントするメモリのバイト数。  
  
 `ppMemCxt`  
 入出力新しい [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) オブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 メモリコンテキストはアドレスであるため、アドレスから値を減算すると、新しいコンテキストインターフェイスを必要とする新しいアドレスが生成されます。  
  
 生成されたアドレスがこのコンテキストに関連付けられているメモリ空間の範囲外であっても、このメソッドは常に新しいコンテキストを生成する必要があります。 唯一の例外は、新しいコンテキストにメモリを割り当てることができない場合、または `ppMemCxt` が null 値 (エラーの場合) である場合です。  
  
## <a name="see-also"></a>参照  
 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)

---
title: 'IDebugBinder3:: FindAlias |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugBinder3::FindAlias
helpviewer_keywords:
- IDebugBinder3::FindAlias method
ms.assetid: b8333701-2718-4983-8513-0875fb7cb730
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 47aaaec73d2c364e974b7430335404bf8caf406c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68142962"
---
# <a name="idebugbinder3findalias"></a>IDebugBinder3::FindAlias
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドは、名前を指定してエイリアスを検索します。 これにより、プログラム内のすべてのエイリアスが検索されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT FindAlias(  
   LPCOLESTR     pcstrName,  
   IDebugAlias** ppAlias  
);  
```  
  
```csharp  
int FindAlias(  
   string          pcstrName,  
   out IDebugAlias ppAlias  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pcstrName`  
 から検索するエイリアスの名前。  
  
 `ppAlias`  
 入出力 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md) インターフェイスによって表されるエイリアス (存在する場合) が見つかりました。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返し `S_OK` ます。それ以外の場合はを返します `S_FALSE` 。エイリアスが見つからない場合は、エラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドは、を呼び出す前に、対象のオブジェクトを null に初期化します。次に、エイリアスが見つかったかどうかを判断するために、後で null 値をテストします。  
  
## <a name="see-also"></a>参照  
 [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)   
 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)

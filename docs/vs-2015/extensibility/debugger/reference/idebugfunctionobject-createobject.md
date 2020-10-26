---
title: 'IDebugFunctionObject:: CreateObject |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreateObject
helpviewer_keywords:
- IDebugFunctionObject::CreateObject method
ms.assetid: c4c99dd5-609a-4e7c-8f29-eb728f57e995
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 08483d5f015af7088eb5968a5bf6358ce5065579
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68179467"
---
# <a name="idebugfunctionobjectcreateobject"></a>IDebugFunctionObject::CreateObject
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

コンストラクターを使用してオブジェクトを作成します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT CreateObject(   
   IDebugFunctionObject* pConstructor,  
   DWORD                 dwArgs,  
   IDebugObject*         pArgs[],  
   IDebugObject**        ppObject  
);  
```  
  
```csharp  
int CreateObject(  
   IDebugFunctionObject pConstructor,   
   uint                 dwArgs,   
   IDebugObject[]       pArgs,   
   out IDebugObject     ppObject  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pConstructor`  
 から作成されるオブジェクトのコンストラクターを表す [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) オブジェクト。  
  
 `dwArgs`  
 から配列内のパラメーターの数 `pArg` 。 コンストラクターに渡されるパラメーターの数を表します。  
  
 `pArg`  
 からコンストラクターに渡されたパラメーターを表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトの配列。  
  
 `ppObject`  
 入出力 `IDebugObject` 新しく作成されたオブジェクトを表すを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドを呼び出して、 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) インターフェイスによって表される関数のパラメーターであるクラス (または、コンストラクターを必要とする他の複合型) のインスタンスを表すオブジェクトを作成します。  
  
 オブジェクトパラメーターがコンストラクターを必要としない場合は、 [Createobjectnoconstructor](../../../extensibility/debugger/reference/idebugfunctionobject-createobjectnoconstructor.md) メソッドを呼び出します。  
  
## <a name="see-also"></a>参照  
 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)   
 [CreateObjectNoConstructor](../../../extensibility/debugger/reference/idebugfunctionobject-createobjectnoconstructor.md)

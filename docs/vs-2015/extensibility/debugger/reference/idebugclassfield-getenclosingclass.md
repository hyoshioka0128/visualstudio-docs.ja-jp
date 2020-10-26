---
title: 'IDebugClassField:: GetEnclosingClass |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugClassField::GetEnclosingClass
helpviewer_keywords:
- IDebugClassField::GetEnclosingClass method
ms.assetid: a0c12e3c-9ea0-4dfb-9e45-8cea18725022
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 896d3ecd5202bf85e6b9e86af31796c662a6eef1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68191000"
---
# <a name="idebugclassfieldgetenclosingclass"></a>IDebugClassField::GetEnclosingClass
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このクラスを囲むクラスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetEnclosingClass(   
   IDebugClassField** ppClassField  
);  
```  
  
```csharp  
int GetEnclosingClass(  
   out IDebugClassField ppClassField  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppClassField`  
 入出力外側のクラスを表す [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) オブジェクトを返します。 外側のクラスがない場合は、null 値を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 この [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) オブジェクトによって表されるクラスが入れ子になったクラスである場合、パラメーターは、 `ppClassField` `IDebugClassField` 外側のクラスを表すオブジェクトを返します。 たとえば、次のクラス定義があるとします。  
  
```  
class RootClass {  
   class NestedClass { }  
};  
```  
  
 クラスを表すオブジェクトのメソッドを呼び出すと `GetEnclosingClass` `IDebugClassField` `NestedClass` `IDebugClassField` 、クラスを表すオブジェクトが返さ `RootClass` れます。  
  
## <a name="see-also"></a>参照  
 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)

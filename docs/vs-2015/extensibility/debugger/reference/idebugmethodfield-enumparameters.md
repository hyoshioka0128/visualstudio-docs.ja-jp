---
title: 'IDebugMethodField:: EnumParameters |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumParameters
helpviewer_keywords:
- IDebugMethodField::EnumParameters method
ms.assetid: d77b1197-deb6-4144-8d1b-8b09949ccfac
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8ebdd604ba97fda8751cf037e7494b59e7bb77ff
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68162595"
---
# <a name="idebugmethodfieldenumparameters"></a>IDebugMethodField::EnumParameters
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

メソッドのパラメーターの列挙子を作成します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT EnumParameters(   
   IEnumDebugFields** ppParams  
);  
```  
  
```csharp  
int EnumParameters(  
   out IEnumDebugFields ppParams  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppParams`  
 入出力メソッドに対するパラメーターのリストを表す [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) オブジェクトを返します。それ以外の場合は、パラメーターがない場合は null 値を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は S_OK を返します。パラメーターがない場合は S_FALSE を返します。 それ以外の場合はエラー コードを返します。  
  
## <a name="remarks"></a>注釈  
 各要素は、さまざまな種類のパラメーターを表す [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトです。 各オブジェクトの [Getkind](../../../extensibility/debugger/reference/idebugfield-getkind.md) メソッドを呼び出して、オブジェクトが表すパラメーターの種類を正確に特定します。  
  
 パラメーターには、変数名とその型の両方が含まれます。 クラスメソッドの最初のパラメーターは、通常、"this" ポインターです。  
  
 パラメーターの型のみが必要な場合は、 [Enumarguments](../../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md) メソッドを呼び出します。  
  
## <a name="see-also"></a>参照  
 [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)   
 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)   
 [EnumArguments](../../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)

---
title: 'IDebugBinder:: ResolveRuntimeType |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugBinder::ResolveRuntimeType
helpviewer_keywords:
- IDebugBinder::ResolveRuntimeType method
ms.assetid: 6456ab3e-1c03-4f3c-91f9-16797ab7f5e7
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 69b1418c76e01b87bcd6d992a82ce58287e79ceb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68192294"
---
# <a name="idebugbinderresolveruntimetype"></a>IDebugBinder::ResolveRuntimeType
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドは、オブジェクトの実行時の型を決定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT ResolveRuntimeType(   
   IDebugObject* pObject,  
   IDebugField** ppResolved  
);  
```  
  
```csharp  
int ResolveRuntimeType(  
   IDebugObject     pObject,   
   out IDebugField  ppResolved  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pObject`  
 から解決する [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 。  
  
 `ppResolved`  
 入出力オブジェクトの型を [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)として返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 オブジェクトのランタイム型は、コンパイル時には常にわからないということです。 たとえば、ポリモーフィズムを使用すると、引数は、ボタンクラスなどの基本クラスとして関数に渡すことができます。 実際の引数は、オプションボタンクラスなどの派生クラスである場合があります。  
  
## <a name="see-also"></a>参照  
 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)   
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)

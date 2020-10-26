---
title: 'IDebugReference2:: GetDerivedMostReference |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugReference2::GetDerivedMostReference
helpviewer_keywords:
- IDebugReference2::GetDerivedMostReference
ms.assetid: 07253b74-7d39-48e0-8e85-ac8dfd919f6e
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 44413531cf3a91c6677d9ce3d56e10646307ffd6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68155850"
---
# <a name="idebugreference2getderivedmostreference"></a>IDebugReference2::GetDerivedMostReference
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

参照の最も派生した参照を取得します。 将来使用するために予約されています。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetDerivedMostReference(   
   IDebugReference2** ppDerivedMost  
);  
```  
  
```csharp  
int GetDerivedMostReference(   
   out IDebugReference2 ppDerivedMost  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppDerivedMost`  
 入出力最派生のプロパティを表す [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) オブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 常に `E_NOTIMPL` を返します。  
  
## <a name="remarks"></a>注釈  
 たとえば、このプロパティがを実装するオブジェクトを表し、 `ClassRoot` 実際にから派生したのインスタンス化である場合、 `ClassDerived` このメソッドは、 `ClassRoot` オブジェクトへの参照を表す [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) オブジェクトを返し `ClassDerived` ます。  
  
## <a name="see-also"></a>参照  
 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)

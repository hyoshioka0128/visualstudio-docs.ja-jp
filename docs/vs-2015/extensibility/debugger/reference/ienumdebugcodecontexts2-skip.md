---
title: 'IEnumDebugCodeContexts2:: Skip |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugCodeContexts2::Skip
helpviewer_keywords:
- IEnumDebugCodeContexts2::Skip
ms.assetid: 3451a3eb-bf5b-4ec5-acc9-aa5a24363801
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: abf8ea0b14f1afdda3d950127ca814993c29eea1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62551606"
---
# <a name="ienumdebugcodecontexts2skip"></a>IEnumDebugCodeContexts2::Skip
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定した数の要素をスキップします。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Skip(  
   ULONG celt  
);  
```  
  
```csharp  
int Skip(  
   uint celt  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `celt`  
 からスキップする要素の数。  
  
## <a name="return-value"></a>戻り値  
 正常に終了した場合は、`S_OK` を返します。 `S_FALSE` `celt` が残りの要素の数より大きい場合はを返します。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 が、 `celt` 残りの要素の数よりも大きい値を指定した場合、列挙は終了に設定され、 `S_FALSE` が返されます。  
  
## <a name="see-also"></a>参照  
 [IEnumDebugCodeContexts2](../../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)

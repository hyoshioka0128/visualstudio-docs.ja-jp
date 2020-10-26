---
title: 'IDebugGenericFieldDefinition:: GetFormalTypeParams |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- GetFormalTypeParams
- IDebugGenericFieldDefinition::GetFormalTypeParams
ms.assetid: cadbd6a1-bc7c-4aff-8777-5396b7a23c3e
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2e4595cd8a93c266d0eb70e91b8ab8ca8aeb8cb5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68180839"
---
# <a name="idebuggenericfielddefinitiongetformaltypeparams"></a>IDebugGenericFieldDefinition::GetFormalTypeParams
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

パラメーターの数を指定して、型パラメーターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetFormalTypeParams(  
   ULONG32                   cParams,  
   IDebugGenericParamField** ppParams,  
   ULONG32*                  pcParams  
);  
```  
  
```csharp  
int GetFormalTypeParams(  
   uint                          cParams,  
   out IDebugGenericParamField[] ppParams,  
   ref uint                      pcParams  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `cParams`  
 からパラメーターの数。  
  
 `ppParams`  
 入出力型パラメーターの配列。  
  
 `pcParams`  
 [入力、出力]配列内のパラメーターの数 `ppParams` 。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 型パラメーターを左から右へ順に返します。 たとえば、Dictionary は \<K,V> IDebugFormalGenericParameters {K, V} を返します。  
  
## <a name="see-also"></a>参照  
 [IDebugGenericFieldDefinition](../../../extensibility/debugger/reference/idebuggenericfielddefinition.md)

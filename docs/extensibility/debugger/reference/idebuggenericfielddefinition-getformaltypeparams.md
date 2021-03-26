---
description: パラメーターの数を指定して、型パラメーターを取得します。
title: 'IDebugGenericFieldDefinition:: GetFormalTypeParams |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetFormalTypeParams
- IDebugGenericFieldDefinition::GetFormalTypeParams
ms.assetid: cadbd6a1-bc7c-4aff-8777-5396b7a23c3e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3aba284bab3299bf6ef300f9493c20e9c0d230ee
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063449"
---
# <a name="idebuggenericfielddefinitiongetformaltypeparams"></a>IDebugGenericFieldDefinition::GetFormalTypeParams
パラメーターの数を指定して、型パラメーターを取得します。

## <a name="syntax"></a>構文

```cpp
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

## <a name="parameters"></a>パラメーター
`cParams`\
からパラメーターの数。

`ppParams`\
入出力型パラメーターの配列。

`pcParams`\
[入力、出力]配列内のパラメーターの数 `ppParams` 。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 型パラメーターを左から右へ順に返します。 たとえば、Dictionary は \<K,V> IDebugFormalGenericParameters {K, V} を返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugGenericFieldDefinition](../../../extensibility/debugger/reference/idebuggenericfielddefinition.md)

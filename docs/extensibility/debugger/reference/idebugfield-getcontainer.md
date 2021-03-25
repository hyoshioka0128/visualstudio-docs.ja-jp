---
description: このメソッドは、フィールドのコンテナーを取得します。
title: 'IDebugField:: GetContainer |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetContainer
helpviewer_keywords:
- IDebugField::GetContainer method
ms.assetid: 6d6c8213-6181-4adf-9584-3e4cac163dd8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c5e5f474a55291245cc1811e8f063f80e651b3a5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077084"
---
# <a name="idebugfieldgetcontainer"></a>IDebugField::GetContainer
このメソッドは、フィールドのコンテナーを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetContainer( 
   IDebugContainerField** ppContainerField
);
```

```csharp
int GetContainer(
   out IDebugContainerField ppContainerField
);
```

## <a name="parameters"></a>パラメーター
`ppContainerField`\
入出力 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) インターフェイスによって表されるコンテナーを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このフィールドにコンテナーがない場合、返されるは `ppContainerField` null 値になります。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)

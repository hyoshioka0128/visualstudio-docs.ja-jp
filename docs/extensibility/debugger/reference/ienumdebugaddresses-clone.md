---
description: このメソッドは、現在の addresses 列挙体のコピーを別のオブジェクトとして返します。
title: 'IEnumDebugAddresses:: Clone |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugAddresses::Clone
helpviewer_keywords:
- IEnumDebugAddresses::Clone method
ms.assetid: 71189a00-34eb-4c71-b96e-8bd6e70c6966
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4f26eb76ff9126d1aa4f490488513a3d22113b4f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083207"
---
# <a name="ienumdebugaddressesclone"></a>IEnumDebugAddresses::Clone
このメソッドは、現在の列挙体のコピーを別のオブジェクトとして返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Clone(
   IEnumDebugAddresses** ppEnum
);
```

```csharp
int Clone(
   out IEnumDebugAddresses ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\
入出力この列挙体のコピーを別のオブジェクトとして返します。

## <a name="property-valuereturn-value"></a>プロパティ値/戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 列挙体のコピーは、このメソッドが呼び出されたときの元の状態と同じ状態になります。 ただし、コピーと元の状態は別々であり、個別に変更できます。

## <a name="see-also"></a>こちらもご覧ください
- [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)

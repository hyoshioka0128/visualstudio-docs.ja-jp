---
description: 現在のコードコンテキスト列挙体のコピーを別のオブジェクトとして返します。
title: 'IEnumDebugCodeContexts2:: Clone |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugCodeContexts2::Clone
helpviewer_keywords:
- IEnumDebugCodeContexts2::Clone
ms.assetid: 22c98975-4294-4fbd-a345-16f65fe1200d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d26f6b96d4ea73fecd7446625a049b5ac7755f97
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080152"
---
# <a name="ienumdebugcodecontexts2clone"></a>IEnumDebugCodeContexts2::Clone
現在の列挙体のコピーを別のオブジェクトとして返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Clone(
   IEnumDebugCodeContexts2** ppEnum
);
```

```csharp
int Clone(
   out IEnumDebugCodeContexts2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\
入出力この列挙体のコピーを別のオブジェクトとして返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 列挙体のコピーは、このメソッドが呼び出されたときの元の状態と同じ状態になります。 ただし、コピーと元の状態は別々であり、個別に変更できます。

## <a name="see-also"></a>こちらもご覧ください
- [IEnumDebugCodeContexts2](../../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)

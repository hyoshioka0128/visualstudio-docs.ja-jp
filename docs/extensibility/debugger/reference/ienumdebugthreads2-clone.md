---
description: 現在の threads 列挙体のコピーを別のオブジェクトとして返します。
title: 'IEnumDebugThreads2:: Clone |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugThreads2::Clone
helpviewer_keywords:
- IEnumDebugThreads2::Clone
ms.assetid: d774322c-e72d-4df3-b317-928da39dadc5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 82b0895cfabc63fc61c85fd626f8811796532e19
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082726"
---
# <a name="ienumdebugthreads2clone"></a>IEnumDebugThreads2::Clone
現在の列挙体のコピーを別のオブジェクトとして返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Clone(
   IEnumDebugThreads2** ppEnum
);
```

```csharp
int Clone(
   out IEnumDebugThreads2 ppEnum
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
- [IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)

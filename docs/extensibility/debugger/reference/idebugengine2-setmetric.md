---
description: このメソッドは、メトリックと呼ばれるレジストリ値を設定します。
title: 'IDebugEngine2:: SetMetric |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2:::SetMetric
helpviewer_keywords:
- IDebugEngine2:::SetMetric
ms.assetid: dcda4972-c32e-4693-a0e1-25d5c58b9782
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ec947a97506283b6d26f0e4cb26b06afb183dd57
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087887"
---
# <a name="idebugengine2setmetric"></a>IDebugEngine2::SetMetric
このメソッドは、メトリックと呼ばれるレジストリ値を設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetMetric(
   LPCOLESTR pszMetric,
   VARIANT   varValue
);
```

```csharp
int SetMetric(
   string pszMetric,
   object varValue
);
```

## <a name="parameters"></a>パラメーター
`pszMetric`\
からメトリックの名前。

`varValue`\
からメトリック値を指定します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 メトリックは、デバッグエンジンの動作を変更したり、サポートされている機能を提供したりするために使用されるレジストリ値です。 このメソッドは、デバッグ機能を実行するために、適切な形式の [SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) に呼び出しを転送でき `SetMetric` ます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [デバッグ用の SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)

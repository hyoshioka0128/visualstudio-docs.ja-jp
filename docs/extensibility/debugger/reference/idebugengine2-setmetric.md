---
title: 'IDebugEngine2:: SetMetric |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2:::SetMetric
helpviewer_keywords:
- IDebugEngine2:::SetMetric
ms.assetid: dcda4972-c32e-4693-a0e1-25d5c58b9782
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: caada8db1791d94e7a9632394cd4659bf8cec3a0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80730901"
---
# <a name="idebugengine2setmetric"></a>IDebugEngine2::SetMetric
このメソッドは、メトリックと呼ばれるレジストリ値を設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetMetric(
   LPCOLESTR pszMetric,
   VARIANT   varValue
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

## <a name="remarks"></a>解説
 メトリックは、デバッグエンジンの動作を変更したり、サポートされている機能を提供したりするために使用されるレジストリ値です。 このメソッドは、デバッグ機能を実行するために、適切な形式の [SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) に呼び出しを転送でき `SetMetric` ます。

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [デバッグ用の SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)

---
title: Iデバッグエンジン2::セットメトリック |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
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
[in]メトリック名。

`varValue`\
[in]メトリック値を指定します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 メトリックは、デバッグ エンジンの動作を変更したり、サポートされている機能をアドバタイズするために使用されるレジストリ値です。 このメソッドは、[デバッグ用 SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)関数の適切な形式に呼び出`SetMetric`しを転送できます。

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [デバッグ用の SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)

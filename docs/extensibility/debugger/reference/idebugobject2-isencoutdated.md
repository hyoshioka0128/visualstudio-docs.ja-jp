---
title: 'IDebugObject2:: IsEncOutdated |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::IsEncOutdated
helpviewer_keywords:
- IDebugObject2::IsEncOutdated method
ms.assetid: d3a8c02d-895b-478c-9957-d663130f308e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 94f861e6a45b05c8db1b7e7e76815579f6568c69
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99953384"
---
# <a name="idebugobject2isencoutdated"></a>IDebugObject2::IsEncOutdated
このメソッドは、このオブジェクトまたは親コンテナーのエディットコンティニュの状態が古いかどうかを判断します。 カスタム式エバリュエーターでは、このメソッドは実装されず、常にを返し `E_NOTIMPL` ます。

## <a name="syntax"></a>構文

```cpp
HRESULT IsEncOutdated(
   BOOL* pfEncOutdated
);
```

```csharp
int IsEncOutdated(
   out int pfEncOutdated
);
```

## <a name="parameters"></a>パラメーター
`pfEncOutdated`\
入出力`TRUE`エディットコンティニュの状態が古い場合は0以外 ()。それ以外の場合は 0 ( `FALSE` )。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

> [!NOTE]
> カスタム式エバリュエーターは常にを返す必要があり `E_NOTIMPL` ます。

## <a name="see-also"></a>関連項目
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)

---
description: このメソッドは、このポートの IDebugPortNotify2 インターフェイスを取得します。
title: 'IDebugDefaultPort2:: GetPortNotify |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2::GetPortNotify
helpviewer_keywords:
- IDebugDefaultPort2::GetPortNotify
ms.assetid: 3ae715ee-9886-4694-a52b-59bb3b27467a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cd0d49275188eed1cebb7b1af3ee4dfcbb79cbe4
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102150654"
---
# <a name="idebugdefaultport2getportnotify"></a>IDebugDefaultPort2::GetPortNotify
このメソッドは、このポートの [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) インターフェイスを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetPortNotify(
   IDebugPortNotify2** ppPortNotify
);
```

```csharp
int GetPortNotify(
   out IDebugPortNotify2 ppPortNotify
);
```

## <a name="parameters"></a>パラメーター
`ppPortNotify`\
入出力 [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) オブジェクトです。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 通常、 `QueryInterface` メソッドは、 [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md)インターフェイスを取得するために、 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)インターフェイスを実装するオブジェクトで呼び出されます。 ただし、必要なインターフェイスが別のオブジェクトに実装されている場合もあります。 このメソッドは、これらの状況を隠し、 `IDebugPortNotify2` 最も適切なオブジェクトからインターフェイスを返します。

## <a name="see-also"></a>関連項目
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md)

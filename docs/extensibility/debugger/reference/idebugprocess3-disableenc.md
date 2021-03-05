---
description: このメソッドは、このプロセス (およびそれに含まれるすべてのプログラム) のエディットコンティニュを明示的に無効にします。
title: IDebugProcess3::D isableENC |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::DisableENC
helpviewer_keywords:
- IDebugProcess3::DisableENC
ms.assetid: cffdbdac-4d76-4aeb-aa55-5d0410db99f1
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ffedebd14f720e006c0bec2044afe80901762b52
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158489"
---
# <a name="idebugprocess3disableenc"></a>IDebugProcess3::DisableENC
このメソッドは、このプロセス (およびそれに含まれるすべてのプログラム) のエディットコンティニュを明示的に無効にします。 カスタムポート供給業者は常にを返す必要があり `E_NOTIMPL` ます。

## <a name="syntax"></a>構文

```cpp
HRESULT DisableENC(
   EncUnavailableReason reason
);
```

```csharp
   EncUnavailableReason reason
);
```

## <a name="parameters"></a>パラメーター
`reason`\
から [EncUnavailableReason](../../../extensibility/debugger/reference/encunavailablereason.md) 列挙の値です。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

> [!NOTE]
> カスタムポート供給業者は常にを返す必要があり `E_NOTIMPL` ます。

## <a name="remarks"></a>解説
 プロセスのエディットコンティニュを無効にすると、プロセスを再起動することによってのみ再度有効にすることができます。

## <a name="see-also"></a>関連項目
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [EncUnavailableReason](../../../extensibility/debugger/reference/encunavailablereason.md)

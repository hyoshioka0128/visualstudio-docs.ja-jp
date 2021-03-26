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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7f9c4a1e05cf7d4a98489daf0c2ee3377d54f417
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081621"
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

## <a name="remarks"></a>注釈
 プロセスのエディットコンティニュを無効にすると、プロセスを再起動することによってのみ再度有効にすることができます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [EncUnavailableReason](../../../extensibility/debugger/reference/encunavailablereason.md)

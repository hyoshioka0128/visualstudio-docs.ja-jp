---
description: ブレークポイントがバインド解除された理由を示します。
title: BP_UNBOUND_REASON |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_UNBOUND_REASON
helpviewer_keywords:
- BP_UNBOUND_REASON enumeration
ms.assetid: 939b6f9c-113b-471d-9f30-b03871af6285
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 857f07e70809200567b6c2f79c5a22aff78b4af8
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102162551"
---
# <a name="bp_unbound_reason"></a>BP_UNBOUND_REASON
ブレークポイントがバインド解除された理由を示します。

## <a name="syntax"></a>構文

```cpp
enum enum_BP_UNBOUND_REASON {
    BPUR_UNKNOWN           = 0x0000,
    BPUR_CODE_UNLOADED     = 0x0002,
    BPUR_BREAKPOINT_REBIND = 0x0003,
    BPUR_BREAKPOINT_ERROR  = 0x0004
};
typedef DWORD BP_UNBOUND_REASON;
```

```csharp
public enum enum_BP_UNBOUND_REASON {
    BPUR_UNKNOWN           = 0x0000,
    BPUR_CODE_UNLOADED     = 0x0002,
    BPUR_BREAKPOINT_REBIND = 0x0003,
    BPUR_BREAKPOINT_ERROR  = 0x0004
};
```

## <a name="fields"></a>フィールド
`BPUR_UNKNOWN`\
理由は不明です。

`BPUR_CODE_UNLOADED`\
ブレークポイントを含むコードはアンロードされました。

`BPUR_BREAKPOINT_REBIND`\
ブレークポイントは別の場所に再バインドされています。 これは、ブレークポイントが移動したとき、または無効になったパスを持つファイルにブレークポイントがバインドされたときに発生する可能性があります。

`BPUR_ BREAKPOINT_ERROR`\
ブレークポイントは、バインド後にエラーが発生していると判断されます。 これは、条件が有効でなくなったマネージブレークポイントに発生します。

## <a name="remarks"></a>解説
[Getreason](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getreason.md)メソッドによって返されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetReason](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getreason.md)

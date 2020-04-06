---
title: BP_UNBOUND_REASON |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_UNBOUND_REASON
helpviewer_keywords:
- BP_UNBOUND_REASON enumeration
ms.assetid: 939b6f9c-113b-471d-9f30-b03871af6285
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b0ee695e1108bf9f1c6069084a0826ee23bf37d4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737777"
---
# <a name="bp_unbound_reason"></a>BP_UNBOUND_REASON
ブレークポイントがバインドされなかった理由を示します。

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
その理由は不明です。

`BPUR_CODE_UNLOADED`\
ブレークポイントを含むコードがアンロードされました。

`BPUR_BREAKPOINT_REBIND`\
ブレークポイントが別の場所に再バインドされました。 これは、ブレークポイントが移動したとき、または無効になったパスを持つファイルにブレークポイントがバインドされているときに、エディット コンティニュ操作の後に発生します。

`BPUR_ BREAKPOINT_ERROR`\
ブレークポイントは、バインド後にエラーと判断されます。 これは、条件が無効になったマネージ ブレークポイントに発生します。

## <a name="remarks"></a>Remarks
[メソッドによって](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getreason.md)返されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetReason](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2-getreason.md)

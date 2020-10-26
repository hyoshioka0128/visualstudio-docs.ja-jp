---
title: BP_PASSCOUNT_STYLE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_PASSCOUNT_STYLE
helpviewer_keywords:
- BP_PASSCOUNT_STYLE structure
ms.assetid: 0a647047-e2d5-4724-a0b8-68108425ecad
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1633c5e9aa6ff251fedce83a0243664cd9e0e0a7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80737922"
---
# <a name="bp_passcount_style"></a>BP_PASSCOUNT_STYLE
ブレークポイントが発生する原因となる、ブレークポイントのパス数に関連付けられた条件を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_BP_PASSCOUNT_STYLE {
    BP_PASSCOUNT_NONE             = 0x0000,
    BP_PASSCOUNT_EQUAL            = 0x0001,
    BP_PASSCOUNT_EQUAL_OR_GREATER = 0x0002,
    BP_PASSCOUNT_MOD              = 0x0003
};
typedef DWORD BP_PASSCOUNT_STYLE;
```

```csharp
public enum enum_BP_PASSCOUNT_STYLE {
    BP_PASSCOUNT_NONE             = 0x0000,
    BP_PASSCOUNT_EQUAL            = 0x0001,
    BP_PASSCOUNT_EQUAL_OR_GREATER = 0x0002,
    BP_PASSCOUNT_MOD              = 0x0003
};
```

## <a name="fields"></a>フィールド
`BP_PASSCOUNT_NONE`\
ブレークポイントのパス数のスタイルを指定しません。

`BP_PASSCOUNT_EQUAL`\
ブレークポイントのパスカウントのスタイルを等しくなるように設定します。 ブレークポイントがヒットした回数がパス数と等しいときに、ブレークポイントが発生します。

`BP_PASSCOUNT_EQUAL_OR_GREATER`\
ブレークポイントのパスカウントのスタイルを等しいかそれ以上に設定します。 ブレークポイントがヒットした回数が、パスの数以上になると、ブレークポイントが発生します。

`BP_PASSCOUNT_MOD`\
剰余パスカウントを指定します。 たとえば、パスカウントが型で、 `BP_PASSCOUNT_MOD` pass count 値が4の場合、ヒットカウントが4の倍数になるたびにブレークポイントが起動します。

## <a name="remarks"></a>解説
`stylePassCount` [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)と[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)構造体のメンバーである[BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)構造体のメンバーに使用されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)

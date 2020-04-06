---
title: BP_PASSCOUNT_STYLE |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737922"
---
# <a name="bp_passcount_style"></a>BP_PASSCOUNT_STYLE
ブレークポイントのパスカウントに関連付けられている条件を指定します。

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
ブレークポイントパスカウントスタイルを指定しません。

`BP_PASSCOUNT_EQUAL`\
ブレークポイントのパスカウント スタイルを等に設定します。 ブレークポイントは、ブレークポイントがヒットした回数がパスカウントと等しいときに起動します。

`BP_PASSCOUNT_EQUAL_OR_GREATER`\
ブレークポイントのパスカウント スタイルを等しい以上に設定します。 ブレークポイントは、ブレークポイントがヒットした回数がパスカウント以上の場合に発生します。

`BP_PASSCOUNT_MOD`\
モジュロ パス数を指定します。 たとえば、パスカウントがタイプ`BP_PASSCOUNT_MOD`で、パスカウント値が4の場合、ブレークポイントはヒットカウントが4の倍数であるたびに起動します。

## <a name="remarks"></a>Remarks
BP_REQUEST_INFO構造体と`stylePassCount`[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)構造体のメンバである[BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)構造体のメンバに使用されます。 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)

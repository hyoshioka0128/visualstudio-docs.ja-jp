---
title: BP_COND_STYLE |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_COND_STYLE
helpviewer_keywords:
- BP_COND_STYLE enumeration
ms.assetid: a93b1412-f447-48a1-af9d-38f3dbb3092f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ca704ca186308ea9e44c4fa7edc6617cbac806eb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738115"
---
# <a name="bp_cond_style"></a>BP_COND_STYLE
保留中のブレークポイントとバインドされたブレークポイントのブレークポイント条件スタイルを指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_BP_COND_STYLE {
    BP_COND_NONE         = 0x0000,
    BP_COND_WHEN_TRUE    = 0x0001,
    BP_COND_WHEN_CHANGED = 0x0002
};
typedef DWORD BP_COND_STYLE;
```

```csharp
public enum enum_BP_COND_STYLE {
    BP_COND_NONE         = 0x0000,
    BP_COND_WHEN_TRUE    = 0x0001,
    BP_COND_WHEN_CHANGED = 0x0002
};
```

## <a name="fields"></a>フィールド
`BP_COND_NONE`\
ブレークポイントの位置に達すると、ブレークポイントを起動します。 ブレークポイントの条件が指定されていません。

`BP_COND_WHEN_TRUE`\
ブレークポイントに関連付けられた条件式が に評価された場合にのみ、`true`ブレークポイントを起動します。

`BP_COND_WHEN_CHANGED`\
ブレークポイントを起動するのは、ブレークポイントに関連付けられている条件式の値が前回の評価から変更された場合だけです。

## <a name="remarks"></a>Remarks
BP_CONDITION構造体の`styleCondition`メンバーに使用[BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)

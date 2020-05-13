---
title: CONTEXT_COMPARE |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONTEXT_COMPARE
helpviewer_keywords:
- CONTEXT_COMPARE enumeration
ms.assetid: 701ed61c-a320-4c20-a335-0b840024abc0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1c88b50644d1adda2dd0eaa3b74a828f9739d70b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737607"
---
# <a name="context_compare"></a>CONTEXT_COMPARE
2 つのメモリ コンテキストを比較するための条件を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_CONTEXT_COMPARE {
    CONTEXT_EQUAL                 = 0x0001,
    CONTEXT_LESS_THAN             = 0x0002,
    CONTEXT_GREATER_THAN          = 0x0003,
    CONTEXT_LESS_THAN_OR_EQUAL    = 0x0004,
    CONTEXT_GREATER_THAN_OR_EQUAL = 0x0005,
    CONTEXT_SAME_SCOPE            = 0x0006,
    CONTEXT_SAME_FUNCTION         = 0x0007,
    CONTEXT_SAME_MODULE           = 0x0008,
    CONTEXT_SAME_PROCESS          = 0x0009
};
typedef DWORD CONTEXT_COMPARE;
```

```csharp
public enum enum_CONTEXT_COMPARE {
    CONTEXT_EQUAL                 = 0x0001,
    CONTEXT_LESS_THAN             = 0x0002,
    CONTEXT_GREATER_THAN          = 0x0003,
    CONTEXT_LESS_THAN_OR_EQUAL    = 0x0004,
    CONTEXT_GREATER_THAN_OR_EQUAL = 0x0005,
    CONTEXT_SAME_SCOPE            = 0x0006,
    CONTEXT_SAME_FUNCTION         = 0x0007,
    CONTEXT_SAME_MODULE           = 0x0008,
    CONTEXT_SAME_PROCESS          = 0x0009
};
```

## <a name="fields"></a>フィールド
`CONTEXT_EQUAL`\
ターゲット のメモリ コンテキストと等しいメモリ コンテキストを一覧から探します。

`CONTEXT_LESS_THAN`\
ターゲット のメモリ コンテキストより小さいメモリ コンテキストを一覧から探します。

`CONTEXT_GREATER_THAN`\
ターゲット のメモリ コンテキストより大きいメモリ コンテキストを一覧から探します。

`CONTEXT_LESS_THAN_OR_EQUAL`\
ターゲット のメモリ コンテキスト以下のメモリ コンテキストを一覧から探します。

`CONTEXT_GREATER_THAN_OR_EQUAL`\
ターゲット メモリ コンテキスト以上のメモリ コンテキストを一覧から探します。

`CONTEXT_SAME_SCOPE`\
ターゲット のメモリ コンテキストと同じスコープ内にある最初のメモリ コンテキストをリストから探します。

`CONTEXT_SAME_FUNCTION`\
ターゲット のメモリ スコープと同じ関数内にある一覧の最初のメモリ コンテキストを検索します。

`CONTEXT_SAME_MODULE`\
ターゲットのメモリ コンテキストと同じモジュール内にある最初のメモリ コンテキストをリストで検索します。

`CONTEXT_SAME_PROCESS`\
ターゲット のメモリ コンテキストと同じプロセス内にある最初のメモリ コンテキストをリストから探します。

## <a name="remarks"></a>Remarks
[引数として引数](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md)として渡されます、 Compare メソッド。

これらの値は、指定された比較基準を満たすリスト内の最初のメモリ コンテキストを検索するために使用されます。 メモリ コンテキストには、メソッドを通じて自身を比較するメモリ コンテキストの`IDebugMemoryContext2::Compare`一覧が与えられます。 次に、比較演算子`true`が返される、リスト内の最初のメモリ コンテキスト。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [比較](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md)

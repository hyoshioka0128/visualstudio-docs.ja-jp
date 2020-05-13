---
title: DOCCONTEXT_COMPARE |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DOCCONTEXT_COMPARE
helpviewer_keywords:
- DOCCONTEXT_COMPARE enumeration
ms.assetid: ed947c34-b07e-4b69-8381-b6e7cb842862
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 75e4453cae63f484961cb2d0f3385a703709f83b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737231"
---
# <a name="doccontext_compare"></a>DOCCONTEXT_COMPARE
2 つのドキュメント コンテキストを比較するための基準を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_DOCCONTEXT_COMPARE {
    DOCCONTEXT_EQUAL         = 0x0001,
    DOCCONTEXT_LESS_THAN     = 0x0002,
    DOCCONTEXT_GREATER_THAN  = 0x0003,
    DOCCONTEXT_SAME_DOCUMENT = 0x0004
};
typedef DWORD DOCCONTEXT_COMPARE;
```

```csharp
enum enum_DOCCONTEXT_COMPARE {
    DOCCONTEXT_EQUAL         = 0x0001,
    DOCCONTEXT_LESS_THAN     = 0x0002,
    DOCCONTEXT_GREATER_THAN  = 0x0003,
    DOCCONTEXT_SAME_DOCUMENT = 0x0004
};
```

## <a name="fields"></a>フィールド
`DOCCONTEXT_EQUAL`\
リスト内の、ターゲットドキュメントコンテキストと等しい最初のドキュメントコンテキストを検索します。

`DOCCONTEXT_LESS_THAN`\
リスト内の、対象のドキュメント コンテキストよりも小さい最初のドキュメント コンテキストを検索します。

`DOCCONTEXT_GREATER_THAN`\
ターゲットドキュメントのコンテキストよりも大きいリスト内の最初のドキュメントコンテキストを検索します。

`DOCCONTEXT_SAME_DOCUMENT`\
ターゲットドキュメントコンテキストと同じドキュメント内にあるリスト内の最初のドキュメントコンテキストを検索します。

## <a name="remarks"></a>Remarks
[引数として引数](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md)として渡されます、 Compare メソッド。

これらの値は、リスト内の最初のドキュメント コンテキストを検索するための比較基準を指定するために使用されます。 ドキュメントコンテキストには、メソッドを通じてそれ自体を比較するドキュメントコンテキストのリスト`IDebugDocumentContext2::Compare`が与えられます。 次に、比較演算子が返されるリスト内の最初の`true`ドキュメント コンテキスト。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [比較](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md)

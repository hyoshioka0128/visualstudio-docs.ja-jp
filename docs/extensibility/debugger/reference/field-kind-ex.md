---
title: FIELD_KIND_EX |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- FIELD_KIND_EX enumeration
ms.assetid: 922c3208-1e94-485f-b70a-3bc96affeff8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f0c13d83f80b311838eca32945462c1f17ca23f4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736880"
---
# <a name="field_kind_ex"></a>FIELD_KIND_EX
[オブジェクト](../../../extensibility/debugger/reference/idebugfield.md)に含めることができる追加の種類のフィールドを列挙します。 この列挙体は[、FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)列挙体を拡張します。

## <a name="syntax"></a>構文

```cpp
enum enum_FIELD_KIND_EX
{
    FIELD_KIND_EX_NONE = 0,
    FIELD_TYPE_EX_METHODVAR = 0x1,
    FIELD_TYPE_EX_CLASSVAR = 0x2
};
typedef DWORD FIELD_KIND_EX;
```

```csharp
public enum enum_FIELD_KIND_EX
{
    FIELD_KIND_EX_NONE = 0,
    FIELD_TYPE_EX_METHODVAR = 0x1,
    FIELD_TYPE_EX_CLASSVAR = 0x2
};
```

## <a name="fields"></a>フィールド
`FIELD_KIND_EX_NONE`\
フィールドに拡張型が含まれていません。

`FIELD_TYPE_EX_METHODVAR`\
フィールドにはメソッド変数が含まれています。

`FIELD_TYPE_EX_CLASSVAR`\
フィールドにはクラス変数が含まれています。

## <a name="requirements"></a>必要条件
ヘッダー: Sh.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetExtendedKind](../../../extensibility/debugger/reference/idebugextendedfield-getextendedkind.md)

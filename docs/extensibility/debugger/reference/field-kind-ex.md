---
title: FIELD_KIND_EX |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80736880"
---
# <a name="field_kind_ex"></a>FIELD_KIND_EX
[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)オブジェクトに格納できるその他の種類のフィールドを列挙します。 この列挙体は [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md) 列挙体を拡張します。

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
フィールドにメソッド変数が含まれています。

`FIELD_TYPE_EX_CLASSVAR`\
フィールドにクラス変数が含まれています。

## <a name="requirements"></a>必要条件
ヘッダー: Sh. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetExtendedKind](../../../extensibility/debugger/reference/idebugextendedfield-getextendedkind.md)

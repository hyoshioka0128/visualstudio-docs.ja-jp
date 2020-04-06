---
title: BP_ERROR_TYPE |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_ERROR_TYPE
helpviewer_keywords:
- BP_ERROR_TYPE enumeration
ms.assetid: c483eaab-db29-46de-bfdb-5c2a9a9cfb68
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e777e1f8cb67187a81f8f3bb4f79299939bfa31c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738072"
---
# <a name="bp_error_type"></a>BP_ERROR_TYPE
ブレークポイントのエラーの種類を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_BP_ERROR_TYPE {
    BPET_NONE            = 0x00000000,
    BPET_TYPE_WARNING    = 0x00000001,
    BPET_TYPE_ERROR      = 0x00000002,
    BPET_SEV_HIGH        = 0x0F000000,
    BPET_SEV_GENERAL     = 0x07000000,
    BPET_SEV_LOW         = 0x01000000,
    BPET_TYPE_MASK       = 0x0000ffff,
    BPET_SEV_MASK        = 0xffff0000,
    BPET_GENERAL_WARNING = BPET_SEV_GENERAL | BPET_TYPE_WARNING,
    BPET_GENERAL_ERROR   = BPET_SEV_GENERAL | BPET_TYPE_ERROR,
    BPET_ALL             = 0xffffffff
};
typedef DWORD BP_ERROR_TYPE;
```

```csharp
public enum enum_BP_ERROR_TYPE {
    BPET_NONE            = 0x00000000,
    BPET_TYPE_WARNING    = 0x00000001,
    BPET_TYPE_ERROR      = 0x00000002,
    BPET_SEV_HIGH        = 0x0F000000,
    BPET_SEV_GENERAL     = 0x07000000,
    BPET_SEV_LOW         = 0x01000000,
    BPET_TYPE_MASK       = 0x0000ffff,
    BPET_SEV_MASK        = 0xffff0000,
    BPET_GENERAL_WARNING = BPET_SEV_GENERAL | BPET_TYPE_WARNING,
    BPET_GENERAL_ERROR   = BPET_SEV_GENERAL | BPET_TYPE_ERROR,
    BPET_ALL             = 0xffffffff
};
```

## <a name="fields"></a>フィールド
`BPET_NONE`\
ブレークポイント エラーを指定しません。

`BPET_TYPE_WARNING`\
警告スタイルのブレークポイント エラーを指定します。

`BPET_TYPE_ERROR`\
エラー スタイルのブレークポイント エラーを指定します。

`BPET_SEV_HIGH`\
重大度の高いブレークポイント エラーを指定します。

`BPET_SEV_GENERAL`\
重大度中のブレークポイント エラーを指定します。

`BPET_SEV_LOW`\
重大度低のブレークポイント エラーを指定します。

`BPET_TYPE_MASK`\
マスク スタイルのブレークポイント エラーを指定します。

`BPET_SEV_MASK`\
重大度マスク形式のブレークポイント エラーを指定します。

`BPET_GENERAL_WARNING`\
一般的な警告スタイルのブレークポイント エラーを指定します。

`BPET_GENERAL_ERROR`\
一般的なエラースタイルのブレークポイント エラーを指定します。

`BPET_ALL`\
すべてのブレークポイント エラーの種類を指定します。

## <a name="remarks"></a>Remarks
これらの値はビット単位`OR`で組み合わせ[、BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)構造体の`dwType`メンバーに使用できます。 パラメーターとして渡されます、[列挙エラーブレークポイントメソッド](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)です。

ブレークポイント エラーの種類は、型と重大度で構成されます。 つまり、ブレークポイント エラーの種類は、`BPET_TYPE_ERROR`単独では、型 (、たとえば、、 など) または重大`BPET_SEV_GENERAL`度 (たとえば) ではありません。 `BPET_GENERAL_WARNING`一`BPET_GENERAL_ERROR`般的な警告およびエラーブレークポイントの定義済みの値を提供します。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
- [EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)

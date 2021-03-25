---
description: ブレークポイントのエラーの種類を指定します。
title: BP_ERROR_TYPE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_ERROR_TYPE
helpviewer_keywords:
- BP_ERROR_TYPE enumeration
ms.assetid: c483eaab-db29-46de-bfdb-5c2a9a9cfb68
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ddff439aba67248bd2eb706a85c5f91b4bf1628d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085287"
---
# <a name="bp_error_type"></a>BP_ERROR_TYPE
ブレークポイントのエラーの種類を指定します。

## <a name="syntax"></a>Syntax

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
ブレークポイントエラーを指定しません。

`BPET_TYPE_WARNING`\
警告スタイルのブレークポイントエラーを指定します。

`BPET_TYPE_ERROR`\
エラースタイルのブレークポイントエラーを指定します。

`BPET_SEV_HIGH`\
重大度の高いブレークポイントエラーを指定します。

`BPET_SEV_GENERAL`\
中レベルのブレークポイントエラーを指定します。

`BPET_SEV_LOW`\
重大度の低いブレークポイントエラーを指定します。

`BPET_TYPE_MASK`\
マスクスタイルのブレークポイントエラーを指定します。

`BPET_SEV_MASK`\
重要度マスクスタイルのブレークポイントエラーを指定します。

`BPET_GENERAL_WARNING`\
一般警告スタイルのブレークポイントエラーを指定します。

`BPET_GENERAL_ERROR`\
一般的な-エラースタイルのブレークポイントエラーを指定します。

`BPET_ALL`\
すべてのブレークポイントエラーの種類を指定します。

## <a name="remarks"></a>注釈
これらの値は、ビットごとの `OR` and で結合し、 `dwType` [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md) 構造体のメンバーに使用することができます。 [Enumerrorbreakpoints ブレークポイント](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)メソッドにパラメーターとして渡されます。

ブレークポイントのエラーの種類は、型と重大度で構成されています。 つまり、ブレークポイントのエラーの種類は、単独では型 (たとえば、 `BPET_TYPE_ERROR` ) または重大度 (など) にすぎません `BPET_SEV_GENERAL` 。 `BPET_GENERAL_WARNING` と `BPET_GENERAL_ERROR` には、一般的な警告とエラーのブレークポイントの定義済みの値が用意されています。

## <a name="requirements"></a>要件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
- [EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)

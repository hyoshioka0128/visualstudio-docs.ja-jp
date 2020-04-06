---
title: BP_TYPE |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_TYPE
helpviewer_keywords:
- BP_TYPE enumeration
ms.assetid: ef07191e-7966-43ab-96fb-1a0b1db3115d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 02550141fb1857214d5bfd80d5dd86969bec9fba
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737792"
---
# <a name="bp_type"></a>BP_TYPE
ブレークポイントがコードの場所にあるか、データの場所であるか、または別の種類のブレークポイントであるかを指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_BP_TYPE {
    BPT_NONE    = 0x0000,
    BPT_CODE    = 0x0001,
    BPT_DATA    = 0x0002,
    BPT_SPECIAL = 0x0003
};
typedef DWORD BP_TYPE;
```

```csharp
public enum enum_BP_TYPE {
    BPT_NONE    = 0x0000,
    BPT_CODE    = 0x0001,
    BPT_DATA    = 0x0002,
    BPT_SPECIAL = 0x0003
};
```

## <a name="fields"></a>フィールド
`BPT_NONE`\
ブレークポイントの種類を指定しません。

`BPT_CODE`\
コード ブレークポイントを指定します。

`BPT_DATA`\
データ ブレークポイントを指定します。

`BPT_SPECIAL`\
コードでもデータ型でもないブレークポイントを指定します。 この型は非推奨であるため、使用しないでください。

## <a name="remarks"></a>Remarks
パラメーターとして渡されます、[ブレークポイントの種類](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getbreakpointtype.md)と[ブレークポイントの種類の取得します](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getbreakpointtype.md)。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetBreakpointType](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getbreakpointtype.md)
- [GetBreakpointType](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getbreakpointtype.md)

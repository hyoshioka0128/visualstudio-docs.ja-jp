---
description: ブレークポイントがコードの場所にあるか、データの場所であるか、または別の種類のブレークポイントであるかを指定します。
title: BP_TYPE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_TYPE
helpviewer_keywords:
- BP_TYPE enumeration
ms.assetid: ef07191e-7966-43ab-96fb-1a0b1db3115d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3e310154bc62cdea1fb9069cc868cf9e20335d06
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102151106"
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
コードのブレークポイントを指定します。

`BPT_DATA`\
データブレークポイントを指定します。

`BPT_SPECIAL`\
コードでもデータ型でもないブレークポイントを指定します。 この型は非推奨とされているため、使用しないでください。

## <a name="remarks"></a>解説
[Getbreakpointtype](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getbreakpointtype.md)メソッドおよび[getbreakpointtype](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getbreakpointtype.md)メソッドにパラメーターとして渡されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetBreakpointType](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getbreakpointtype.md)
- [GetBreakpointType](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getbreakpointtype.md)

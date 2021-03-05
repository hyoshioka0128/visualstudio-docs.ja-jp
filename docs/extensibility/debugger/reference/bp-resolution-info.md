---
description: コードのブレークポイントまたはデータブレークポイントのバインドされたブレークポイント情報について説明します。
title: BP_RESOLUTION_INFO |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_RESOLUTION_INFO
helpviewer_keywords:
- BP_RESOLUTION_INFO structure
ms.assetid: ba0c162a-61e8-4a0b-811f-4c1d8a5d82f0
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9acdc85cd7ea3e8da239395e5db8c921936a98bd
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102162590"
---
# <a name="bp_resolution_info"></a>BP_RESOLUTION_INFO
コードのブレークポイントまたはデータブレークポイントのバインドされたブレークポイント情報について説明します。

## <a name="syntax"></a>構文

```cpp
typedef struct _BP_RESOLUTION_INFO {
    BPRESI_FIELDS          dwFields;
    BP_RESOLUTION_LOCATION bpResLocation;
    IDebugProgram2*        pProgram;
    IDebugThread2*         pThread;
} BP_RESOLUTION_INFO;
```

```csharp
public struct BP_RESOLUTION_INFO {
    public uint                   dwFields;
    public BP_RESOLUTION_LOCATION bpResLocation;
    public IDebugProgram2         pProgram;
    public IDebugThread2          pThread;
};
```

## <a name="members"></a>メンバー
`dwFields`\
入力するフィールドを指定する [BPRESI_FIELDS](../../../extensibility/debugger/reference/bpresi-fields.md) 列挙体のフラグのコレクション。

`bpResLocation`\
コードまたはデータ内のブレークポイントの位置を指定する [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md) 構造体。

`pProgram`\
ブレークポイントエラーが発生したアプリケーションを表す [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) オブジェクト。

`pThread`\
ブレークポイントエラーを含むアプリケーションが実行されているスレッドを表す [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) オブジェクト。

## <a name="remarks"></a>解説
この構造体は、 [Get解像度情報](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)によって返されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)
- [BPRESI_FIELDS](../../../extensibility/debugger/reference/bpresi-fields.md)
- [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)

---
title: BP_CONDITION |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_CONDITION
helpviewer_keywords:
- BP_CONDITION structure
ms.assetid: 407f87a3-2878-429b-8c65-b68feb36622a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 88ed6b6468c5765c8f987c1f15f3e4e8ade9c8c6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738103"
---
# <a name="bp_condition"></a>BP_CONDITION
ブレークポイントが発生する条件を記述します。

## <a name="syntax"></a>構文

```cpp
typedef struct _BP_CONDITION {
    IDebugThread2* pThread;
    BP_COND_STYLE  styleCondition;
    BSTR           bstrContext;
    BSTR           bstrCondition;
    UINT           nRadix;
} BP_CONDITION;
```

```csharp
public struct BP_CONDITION {
    public IDebugThread2 pThread;
    public uint          styleCondition;
    public string        bstrContext;
    public string        bstrCondition;
    public uint          nRadix;
};
```

## <a name="members"></a>メンバー
`pThread`\
ブレークポイントを含むアプリケーションのアクティブなスレッドを表す[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)オブジェクト。

`styleCondition`\
このブレークポイント条件のスタイルを記述する[BP_COND_STYLE](../../../extensibility/debugger/reference/bp-cond-style.md)列挙体の値。

`bstrContext`\
ブレークポイントの位置。

`bstrCondition`\
ブレークポイントの実行条件。

`nRadix`\
数値情報の評価に使用する基数。

## <a name="remarks"></a>Remarks
この構造体は[、BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)および[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)構造のメンバーです。

この構造体は、パラメーターとして[SetCondition](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setcondition.md)メソッドと[SetCondition](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setcondition.md)メソッドにも渡されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
- [SetCondition](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setcondition.md)
- [SetCondition](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setcondition.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [BP_COND_STYLE](../../../extensibility/debugger/reference/bp-cond-style.md)

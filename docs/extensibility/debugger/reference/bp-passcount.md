---
title: BP_PASSCOUNT |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_PASSCOUNT
helpviewer_keywords:
- BP_PASSCOUNT structure
ms.assetid: 791ac175-b897-4c70-873e-240da7e0ac89
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0e3177ff093aea9a6f52465bd606b22883249d6b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80737904"
---
# <a name="bp_passcount"></a>BP_PASSCOUNT
条件付きブレークポイントが発生する回数と条件について説明します。

## <a name="syntax"></a>構文

```cpp
typedef struct _BP_PASSCOUNT {
    DWORD              dwPassCount;
    BP_PASSCOUNT_STYLE stylePassCount;
} BP_PASSCOUNT;
```

```csharp
public struct BP_PASSCOUNT {
    public uint dwPassCount;
    public uint stylePassCount;
};
```

## <a name="members"></a>メンバー
`dwPassCount`\
ブレークポイントを実行する前に、そのブレークポイントを通過する回数。

`stylePassCount`\
ブレークポイントのパスカウントのスタイルを指定する [BP_PASSCOUNT_STYLE](../../../extensibility/debugger/reference/bp-passcount-style.md) 列挙の値です。

## <a name="remarks"></a>解説
この構造体は、 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) 構造体のメンバーです。

この構造体は、パラメーターとして[Setpass count](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setpasscount.md) および[setpass count](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md) メソッドにも渡されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg. h

名前空間: VisualStudio。

アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [SetPassCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-setpasscount.md)
- [SetPassCount](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-setpasscount.md)
- [BP_PASSCOUNT_STYLE](../../../extensibility/debugger/reference/bp-passcount-style.md)

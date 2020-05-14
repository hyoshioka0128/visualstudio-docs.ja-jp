---
title: BP_STATE |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_STATE
helpviewer_keywords:
- BP_STATE enumeration
ms.assetid: 08aa6a3f-3e5f-4c83-8eca-7b7b5f8e208d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2721028c0635af274174574e4a264546c1909778
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737803"
---
# <a name="bp_state"></a>BP_STATE
バインドされたブレークポイントの存在を指定し、有効にするかどうかを指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_BP_STATE {
    BPS_NONE     = 0x0000,
    BPS_DELETED  = 0x0001,
    BPS_DISABLED = 0x0002,
    BPS_ENABLED  = 0x0003
};
typedef DWORD BP_STATE;
```

```csharp
public enum enum_BP_STATE {
    BPS_NONE     = 0x0000,
    BPS_DELETED  = 0x0001,
    BPS_DISABLED = 0x0002,
    BPS_ENABLED  = 0x0003
};
```

## <a name="fields"></a>フィールド
`BPS_NONE`\
ブレークポイントが存在しない場合に指定します。

`BPS_DELETED`\
ブレークポイントが削除されたことを示します。

`BPS_DISABLED`\
ブレークポイントが無効であることを指定します。

`BPS_ENABLED`\
ブレークポイントが有効であることを指定します。

## <a name="remarks"></a>Remarks
[メソッド](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)から返されます。

## <a name="requirements"></a>必要条件
ヘッダー: msdbg.h

名前空間: を使用します。

アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [Getstate](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getstate.md)

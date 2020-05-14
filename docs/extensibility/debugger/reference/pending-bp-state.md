---
title: PENDING_BP_STATE |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PENDING_BP_STATE
helpviewer_keywords:
- PENDING_BP_STATE enumeration
ms.assetid: ac04ad72-fa92-4a15-ade2-0d0bbbadfc7f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 69c8dbe1022ee0b1b2ff034d2b83b947c8fb3df6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713996"
---
# <a name="pending_bp_state"></a>PENDING_BP_STATE
保留中のブレークポイント (まだバインドされていないブレークポイント) の状態を指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_PENDING_BP_STATE { 
   PBPS_NONE     = 0x0000,
   PBPS_DELETED  = 0x0001,
   PBPS_DISABLED = 0x0002,
   PBPS_ENABLED  = 0x0003
};
typedef DWORD PENDING_BP_STATE;
```

```csharp
public enum enum_PENDING_BP_STATE { 
   PBPS_NONE     = 0x0000,
   PBPS_DELETED  = 0x0001,
   PBPS_DISABLED = 0x0002,
   PBPS_ENABLED  = 0x0003
};
```

## <a name="fields"></a>フィールド
 `PBPS_NONE`\
 ゼロのプレースホルダー。 この値は返されません。

 `PBPS_DELETED`\
 保留中のブレークポイントが削除されたことを示します。

 `PBPS_DISABLED`\
 保留中のブレークポイントが無効であることを示します。

 `PBPS_ENABLED`\
 保留中のブレークポイントが有効であることを示します。

## <a name="remarks"></a>Remarks
 PENDING_BP_STATE_INFO構造体の`state`メンバーとして使用[PENDING_BP_STATE_INFO](../../../extensibility/debugger/reference/pending-bp-state-info.md)します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PENDING_BP_STATE_INFO](../../../extensibility/debugger/reference/pending-bp-state-info.md)

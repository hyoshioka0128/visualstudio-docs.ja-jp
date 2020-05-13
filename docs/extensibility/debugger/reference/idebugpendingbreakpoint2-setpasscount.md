---
title: を待ってブレークポイント2:::セットパスカウント |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2::SetPassCount
helpviewer_keywords:
- SetPassCount method
- IDebugPendingBreakpoint2::SetPassCount method
ms.assetid: 08ddd328-57eb-42e0-baa9-8424dcd1bf04
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 732eadc955b9a6c9bdded3d52f038ff58ed9c217
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725681"
---
# <a name="idebugpendingbreakpoint2setpasscount"></a>IDebugPendingBreakpoint2::SetPassCount
保留中のブレークポイントに関連付けられているパス数を設定または変更します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetPassCount( 
   BP_PASSCOUNT bpPassCount
);
```

```csharp
int SetPassCount( 
   BP_PASSCOUNT bpPassCount
);
```

## <a name="parameters"></a>パラメーター
`bpPassCount`\
[in]パスカウントを含む[BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)構造体。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。 ブレークポイント`E_BP_DELETED`が削除されたかどうかを返します。

## <a name="remarks"></a>Remarks
 以前に保留中のブレークポイントに関連付けられていたパスカウントは失われます。 この保留中のブレークポイントからバインドされたすべてのブレークポイントが呼び出され、パスカウントが`bpPassCount`パラメーターに設定されます。

## <a name="see-also"></a>関連項目
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)

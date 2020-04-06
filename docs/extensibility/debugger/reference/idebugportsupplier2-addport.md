---
title: IDebugポートサプライヤー2::AddPort |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::AddPort
helpviewer_keywords:
- IDebugPortSupplier2::AddPort
ms.assetid: df491161-6bf3-4fcc-b478-b9ec88ec995f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 00954ceaa0ddd750a3d08e372d1edaa1905f01c1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724739"
---
# <a name="idebugportsupplier2addport"></a>IDebugPortSupplier2::AddPort
ポートを追加します。

## <a name="syntax"></a>構文

```cpp
HRESULT AddPort( 
   IDebugPortRequest2* pRequest,
   IDebugPort2**       ppPort
);
```

```csharp
int AddPort( 
   IDebugPortRequest2 pRequest,
   out IDebugPort2    ppPort
);
```

## <a name="parameters"></a>パラメーター
`pRequest`\
[in]追加するポートを記述する[IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)オブジェクト。

`ppPort`\
[アウト]ポートを表す[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、実際には、要求されたポートを作成するだけでなく、アクティブなポートのポートサプライヤーの内部リストに追加します。 時間のかかる遅延を回避するために[、CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)メソッドを最初に呼び出すことができます。

## <a name="see-also"></a>関連項目
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)

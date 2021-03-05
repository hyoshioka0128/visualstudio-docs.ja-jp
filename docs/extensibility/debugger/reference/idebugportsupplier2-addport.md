---
description: ポートを追加します。
title: 'IDebugPortSupplier2:: AddPort |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::AddPort
helpviewer_keywords:
- IDebugPortSupplier2::AddPort
ms.assetid: df491161-6bf3-4fcc-b478-b9ec88ec995f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 14232ac49b3862c635a41c25e79c7ab166fa24ef
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102169237"
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
から追加するポートを記述する [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) オブジェクト。

`ppPort`\
入出力ポートを表す [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドは、要求されたポートを実際に作成するだけでなく、ポート供給元のアクティブなポートの内部リストに追加します。 [Canaddport](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)メソッドは、時間がかかる可能性のある遅延を回避するために最初に呼び出すことができます。

## <a name="see-also"></a>関連項目
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)

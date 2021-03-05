---
description: 別の参照から参照の値を設定します。
title: 'IDebugReference2:: SetValueAsReference |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::SetValueAsReference
helpviewer_keywords:
- IDebugReference2::SetValueAsReference
ms.assetid: 94a545d2-16b9-45e9-b2e7-4e49ff90aad0
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 84117f4a9eb925b442be86a73736479a05818ca1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102165944"
---
# <a name="idebugreference2setvalueasreference"></a>IDebugReference2::SetValueAsReference
別の参照から参照の値を設定します。 将来使用するために予約されています。

## <a name="syntax"></a>構文

```cpp
HRESULT SetValueAsReference ( 
   IDebugReference2** rgpArgs,
   DWORD              dwArgCount,
   IDebugReference2*  pValue,
   DWORD              dwTimeout
);
```

```cpp
int SetValueAsReference ( 
   IDebugReference2[] rgpArgs,
   uint               dwArgCount,
   IDebugReference2   pValue,
   uint               dwTimeout
);
```

## <a name="parameters"></a>パラメーター
`rgpArgs`\
から参照値の設定方法を決定するために使用される [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) オブジェクトの配列。

`dwArgCount`\
から配列内の参照の数。

`pValue`\
からプロパティ値の設定元の [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) オブジェクト。

`dwTimeout`\
からこのメソッドから戻る前に待機する最大時間 (ミリ秒単位)。 `INFINITE`無期限に待機するには、を使用します。

## <a name="return-value"></a>戻り値
 常に `E_NOTIMPL` を返します。

## <a name="see-also"></a>関連項目
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)

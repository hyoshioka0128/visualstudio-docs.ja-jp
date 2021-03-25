---
description: 参照を記述する DEBUG_REFERENCE_INFO 構造体を取得します。
title: 'IDebugReference2:: GetReferenceInfo |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::GetReferenceInfo
helpviewer_keywords:
- IDebugReference2::GetReferenceInfo
ms.assetid: ae611714-f114-4cf2-b5bb-37461e6ff289
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 01a36cbf7d1ca9ec56d7785c06d16e0071abc177
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087224"
---
# <a name="idebugreference2getreferenceinfo"></a>IDebugReference2::GetReferenceInfo
参照を記述する [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 構造体を取得します。 将来使用するために予約されています。

## <a name="syntax"></a>構文

```cpp
HRESULT GetReferenceInfo ( 
   DEBUGREF_INFO_FLAGS   dwFields,
   DWORD                 nRadix,
   DWORD                 dwTimeout,
   IDebugReference2**    rgpArgs,
   DWORD                 dwArgCount,
   DEBUG_REFERENCE_INFO* pReferenceInfo
);
```

```csharp
int GetReferenceInfo ( 
   enum_DEBUGREF_INFO_FLAGS  dwFields,
   uint                      nRadix,
   uint                      dwTimeout,
   IDebugReference2[]        rgpArgs,
   uint                      dwArgCount,
   DEBUG_REFERENCE_INFO[]    pReferenceInfo
);
```

## <a name="parameters"></a>パラメーター
`dwFields`\
から[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)構造体に入力するフィールドを決定する、 [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)列挙のフラグの組み合わせ。

`nRadix`\
から数値情報の書式設定に使用される基数。

`dwTimeout`\
からこのメソッドから戻る前に待機する最大時間 (ミリ秒単位)。 `INFINITE`無期限に待機するには、を使用します。

`rgpArgs`\
から [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) オブジェクトの配列。 将来使用するために予約されています。を null 値に設定します。

`dwArgCount`\
から配列内の参照引数の数 `rgpArgs` 。 将来使用するために予約されています。を0に設定します。

`pReferenceInfo`\
入出力プロパティの説明が入力されている [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 構造体。

## <a name="return-value"></a>戻り値
 常に `E_NOTIMPL` を返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)

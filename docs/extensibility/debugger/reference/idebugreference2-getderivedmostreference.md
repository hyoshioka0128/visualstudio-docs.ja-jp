---
title: 参照2::ほとんどの参照を取得する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::GetDerivedMostReference
helpviewer_keywords:
- IDebugReference2::GetDerivedMostReference
ms.assetid: 07253b74-7d39-48e0-8e85-ac8dfd919f6e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 15e98884d040cfb2ebf1b33a56c7edea331fbff0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80720617"
---
# <a name="idebugreference2getderivedmostreference"></a>IDebugReference2::GetDerivedMostReference
参照の派生最も参照を取得します。 将来利用するために予約されています。

## <a name="syntax"></a>構文

```cpp
HRESULT GetDerivedMostReference( 
   IDebugReference2** ppDerivedMost
);
```

```csharp
int GetDerivedMostReference( 
   out IDebugReference2 ppDerivedMost
);
```

## <a name="parameters"></a>パラメーター
`ppDerivedMost`\
[アウト]最派生プロパティを表す[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)オブジェクトを返します。

## <a name="return-value"></a>戻り値
 常に `E_NOTIMPL` を返します。

## <a name="remarks"></a>Remarks
 たとえば、このプロパティが実装する`ClassRoot`オブジェクトを記述するが、実際に`ClassDerived`のインスタンス化がから`ClassRoot`派生している場合、このメソッドは、オブジェクトへの参照を表す[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)オブジェクトを`ClassDerived`返します。

## <a name="see-also"></a>関連項目
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)

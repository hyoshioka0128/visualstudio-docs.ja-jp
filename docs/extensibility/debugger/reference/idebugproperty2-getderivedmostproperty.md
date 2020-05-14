---
title: プロパティ 2::ほとんどのプロパティを取得します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetDerivedMostProperty
helpviewer_keywords:
- IDebugProperty2::GetDerivedMostProperty
ms.assetid: cc86b461-62d1-4340-8209-c65037fd8b02
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2086aded4361049d722ec36ba1d470ed8f7ac6e5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721506"
---
# <a name="idebugproperty2getderivedmostproperty"></a>IDebugProperty2::GetDerivedMostProperty
プロパティの派生プロパティを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetDerivedMostProperty ( 
   IDebugProperty2** ppDerivedMost
);
```

```csharp
int GetDerivedMostProperty ( 
   out IDebugProperty2 ppDerivedMost
);
```

## <a name="parameters"></a>パラメーター
`ppDerivedMost`\
[アウト]最派生プロパティを表す[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。 取得`S_GETDERIVEDMOST_NO_DERIVED_MOST`する最も派生したプロパティがない場合に返します。

## <a name="remarks"></a>Remarks
 たとえば、このプロパティが実装する`ClassRoot`オブジェクトを記述するが、実際に`ClassDerived`のインスタンス化がから`ClassRoot`派生している場合、このメソッドは、オブジェクトを記述する[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)オブジェクトを`ClassDerived`返します。

## <a name="see-also"></a>関連項目
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)

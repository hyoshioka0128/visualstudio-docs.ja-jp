---
title: 'IDebugReference2:: GetDerivedMostReference |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::GetDerivedMostReference
helpviewer_keywords:
- IDebugReference2::GetDerivedMostReference
ms.assetid: 07253b74-7d39-48e0-8e85-ac8dfd919f6e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ac8321bc571264d050f5f3559e840c3d169096d7
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99909684"
---
# <a name="idebugreference2getderivedmostreference"></a>IDebugReference2::GetDerivedMostReference
参照の最も派生した参照を取得します。 将来使用するために予約されています。

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
入出力最派生のプロパティを表す [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 常に `E_NOTIMPL` を返します。

## <a name="remarks"></a>解説
 たとえば、このプロパティがを実装するオブジェクトを表し、 `ClassRoot` 実際にから派生したのインスタンス化である場合、 `ClassDerived` このメソッドは、 `ClassRoot` オブジェクトへの参照を表す [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) オブジェクトを返し `ClassDerived` ます。

## <a name="see-also"></a>関連項目
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)

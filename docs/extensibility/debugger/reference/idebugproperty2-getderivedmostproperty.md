---
title: 'IDebugProperty2:: GetDerivedMostProperty |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetDerivedMostProperty
helpviewer_keywords:
- IDebugProperty2::GetDerivedMostProperty
ms.assetid: cc86b461-62d1-4340-8209-c65037fd8b02
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2f91b00d2f448aea2f187e37813782ce568ad859
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99916047"
---
# <a name="idebugproperty2getderivedmostproperty"></a>IDebugProperty2::GetDerivedMostProperty
プロパティの最も派生したプロパティを取得します。

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
入出力最派生のプロパティを表す [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、を返します。それ以外の場合は `S_OK` エラーコードを返します。 `S_GETDERIVEDMOST_NO_DERIVED_MOST`取得するプロパティが派生していない場合は、を返します。

## <a name="remarks"></a>解説
 たとえば、このプロパティがを実装するオブジェクトを表し、 `ClassRoot` 実際にはから派生したのインスタンス化である場合、 `ClassDerived` `ClassRoot` このメソッドは、オブジェクトを記述する [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) オブジェクトを返し `ClassDerived` ます。

## <a name="see-also"></a>関連項目
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)

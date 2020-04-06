---
title: バインダーの作成方法 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder::ResolveRuntimeType
helpviewer_keywords:
- IDebugBinder::ResolveRuntimeType method
ms.assetid: 6456ab3e-1c03-4f3c-91f9-16797ab7f5e7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4bdbff651618365f3b68a142a6cb1e76836876a3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735958"
---
# <a name="idebugbinderresolveruntimetype"></a>IDebugBinder::ResolveRuntimeType
このメソッドは、オブジェクトの実行時の型を決定します。

## <a name="syntax"></a>構文

```cpp
HRESULT ResolveRuntimeType( 
   IDebugObject* pObject,
   IDebugField** ppResolved
);
```

```csharp
int ResolveRuntimeType(
   IDebugObject     pObject,
   out IDebugField  ppResolved
);
```

## <a name="parameters"></a>パラメーター
`pObject`\
[in]解決する[IDebug オブジェクト](../../../extensibility/debugger/reference/idebugobject.md)。

`ppResolved`\
[アウト]オブジェクトの型を[返](../../../extensibility/debugger/reference/idebugfield.md)します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 オブジェクトの実行時の型は、コンパイル時に常に認識されるとは限りません。 たとえば、ポリモーフィズムを使用すると、引数をボタン クラスなどの基本クラスとして関数に渡すことができます。 実際の引数は、ラジオ ボタン クラスなどの派生クラスである場合があります。

## <a name="see-also"></a>関連項目
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)

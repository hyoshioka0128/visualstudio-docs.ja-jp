---
title: Iデバッグオブジェクト2::ゲットエイリアス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::GetAlias
helpviewer_keywords:
- IDebugObject2::GetAlias method
ms.assetid: aa6824d5-c932-42ba-8713-950e7d1fb42f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 53c72182b497e2b24d41a784c405d169c3db195f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726289"
---
# <a name="idebugobject2getalias"></a>IDebugObject2::GetAlias
このオブジェクトに関連付けられているエイリアス (存在する場合) を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetAlias(
   IDebugAlias** ppAlias
);
```

```csharp
int GetAlias(
   out IDebugAlias ppAlias
);
```

## <a name="parameters"></a>パラメーター
`ppAlias`\
[アウト]このオブジェクトのエイリアスを表す[IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)オブジェクトを返します。それ以外の場合は、null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 オブジェクトのエイリアスは[、CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)メソッドの呼び出しで作成されます。

## <a name="see-also"></a>関連項目
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)

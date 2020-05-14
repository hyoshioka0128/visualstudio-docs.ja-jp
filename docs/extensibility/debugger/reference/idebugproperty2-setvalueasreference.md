---
title: プロパティ 2::セットバリューアスリファレンス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::SetValueAsReference
helpviewer_keywords:
- IDebugProperty2::SetValueAsReference method
ms.assetid: 341b1b89-4ab8-4e1c-abe2-fb955df5c6b0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 73d00ccedc6985061448170735e9ebcaac42f530
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721258"
---
# <a name="idebugproperty2setvalueasreference"></a>IDebugProperty2::SetValueAsReference
このプロパティの値を、指定した参照の値に設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetValueAsReference(
   IDebugReference2** rgpArgs,
   DWORD              dwArgCount,
   IDebugReference2*  pValue,
   DWORD              dwTimeout
);
```

```csharp
int SetValueAsReference(
   IDebugReference2[] rgpArgs,
   uint               dwArgCount,
   IDebugReference2   pValue,
   uint               dwTimeout
);
```

## <a name="parameters"></a>パラメーター
`rgpArgs`\
[in]マネージ コード プロパティの setter に渡す引数の配列。 プロパティセッターが引数を受け取らない場合、またはこの[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)オブジェクトがそのようなプロパティセッターを参照`rgpArgs`していない場合は、null 値にする必要があります。 このパラメータは通常、NULL 値です。

`dwArgCount`\
[in]配列内の引数の`rgpArgs`数。

`pValue`\
[in]このプロパティを設定するために使用する値への参照を[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)オブジェクトの形式で指定します。

`dwTimeout`\
[in]値の設定にかかる時間 (ミリ秒単位)。 一般的な値`INFINITE`は です。 これは、可能な評価にかかる時間の長さに影響します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コード (通常は次のいずれか) を返します。

|エラー|説明|
|-----------|-----------------|
|`E_SETVALUEASREFERENCE_NOTSUPPORTED`|参照からの値の設定はサポートされていません。|
|`E_SETVALUE_VALUE_CANNOT_BE_SET`|このプロパティはメソッドを参照するので、値を設定できません。|
|`E_SETVALUE_VALUE_IS_READONLY`|値は読み取り専用であり、設定できません。|
|`E_NOTIMPL`|このメソッドは実装されていません。|

## <a name="see-also"></a>関連項目
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)

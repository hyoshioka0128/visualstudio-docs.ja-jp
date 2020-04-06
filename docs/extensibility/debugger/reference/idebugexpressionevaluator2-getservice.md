---
title: 検証評価器2::ゲットサービス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugExpressionEvaluator2::GetService
- GetService
ms.assetid: f8988a9e-9d18-42af-84a7-55f41e9adf63
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c5428606ad54c7938037c3ffecf04f1cfe41787c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729355"
---
# <a name="idebugexpressionevaluator2getservice"></a>IDebugExpressionEvaluator2::GetService
一意の識別子を指定してサービス オブジェクトを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetService (
   GUID        uid,
   IUnknown ** ppService
);
```

```csharp
int GetService (
   Guid       uid,
   out object ppService
);
```

## <a name="parameters"></a>パラメーター
`uid`\
[in]取得するサービスを表す一意の識別子です。

`ppService`\
[アウト]サービスを表すオブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 これは、他の式エバリュエーターからサービスを取得するために、サードパーティの式エバリュエーターによって使用できます。 たとえば、このメソッドを使用して、ビジュアライザー サービスのインターフェイスを既定の式エバリュエーターから取得できます。 サードパーティ式エバリュエーターは、このインターフェイスを実装する必要はほとんどありません。

## <a name="see-also"></a>関連項目
- [IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md)

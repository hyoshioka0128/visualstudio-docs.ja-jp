---
title: Iデバッグバインダー3::検索エイリアス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::FindAlias
helpviewer_keywords:
- IDebugBinder3::FindAlias method
ms.assetid: b8333701-2718-4983-8513-0875fb7cb730
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f0a697e39d21b1c25a98c09ad6cc4837cca7a293
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735867"
---
# <a name="idebugbinder3findalias"></a>IDebugBinder3::FindAlias
このメソッドは、名前を指定してエイリアスを検索します。 これにより、プログラム内のすべてのエイリアスが検索されます。

## <a name="syntax"></a>構文

```cpp
HRESULT FindAlias(
   LPCOLESTR     pcstrName,
   IDebugAlias** ppAlias
);
```

```csharp
int FindAlias(
   string          pcstrName,
   out IDebugAlias ppAlias
);
```

## <a name="parameters"></a>パラメーター
`pcstrName`\
[in]検索するエイリアスの名前。

`ppAlias`\
[アウト][IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)インターフェイスによって表されるエイリアスが見つかりました (存在する場合)。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の`S_FALSE`場合は、(エイリアスが見つからない場合)、またはエラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、呼び出し前に宛先オブジェクトを null に初期化します。その後、その後、ヌル値を調べて、別名が見つかったかどうかを判別します。

## <a name="see-also"></a>関連項目
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)

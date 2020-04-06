---
title: ポートサプライヤー3::列挙永続ポート |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier3::EnumPersistedPorts
helpviewer_keywords:
- IDebugPortSupplier3::EnumPersistedPorts
ms.assetid: 1c3dead3-5d6c-4067-8418-4015f0b0dd07
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 92b31a6b6898b0031e4a01d5a6433d0ce77e64f4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724454"
---
# <a name="idebugportsupplier3enumpersistedports"></a>IDebugPortSupplier3::EnumPersistedPorts
このメソッドは、永続化されたポートの一覧の列挙を許可するオブジェクトを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumPersistedPorts(
   BSTR_ARRAY         PortNames,
   IEnumDebugPorts2** ppEnum
);
```

```csharp
int EnumPersistedPorts(
   BSTR_ARRAY           PortNames,
   out IEnumDebugPorts2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`PortNames`\
[in]永続化されたポート間で検索および返すポート名のリストを含む[BSTR_ARRAY](../../../extensibility/debugger/reference/bstr-array.md)構造体。 これらの名前を持つ永続化されたポートのみが返されます。

`ppEnum`\
[アウト][インターフェイスを](../../../extensibility/debugger/reference/ienumdebugports2.md)実装するオブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 永続化されたポートは、ポート サプライヤーがインスタンス化されるときに読み込まれ、ポート サプライヤーが破棄されたときに保存されます。

## <a name="see-also"></a>関連項目
- [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)
- [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md)
- [BSTR_ARRAY](../../../extensibility/debugger/reference/bstr-array.md)

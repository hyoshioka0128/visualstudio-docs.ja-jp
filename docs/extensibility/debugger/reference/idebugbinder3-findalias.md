---
description: このメソッドは、名前を指定してエイリアスを検索します。
title: 'IDebugBinder3:: FindAlias |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::FindAlias
helpviewer_keywords:
- IDebugBinder3::FindAlias method
ms.assetid: b8333701-2718-4983-8513-0875fb7cb730
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: db4d5cad6d0c2990141e0dd3a824425b8b53145b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167725"
---
# <a name="idebugbinder3findalias"></a>IDebugBinder3::FindAlias
このメソッドは、名前を指定してエイリアスを検索します。 これにより、プログラム内のすべてのエイリアスが検索されます。

## <a name="syntax"></a>構文

```cpp
HRESULT FindAlias(
   LPCOLESTR     pcstrName,
   IDebugAlias** ppAlias
);
```

```csharp
int FindAlias(
   string          pcstrName,
   out IDebugAlias ppAlias
);
```

## <a name="parameters"></a>パラメーター
`pcstrName`\
から検索するエイリアスの名前。

`ppAlias`\
入出力 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md) インターフェイスによって表されるエイリアス (存在する場合) が見つかりました。

## <a name="return-value"></a>戻り値
 成功した場合は、を返し `S_OK` ます。それ以外の場合はを返します `S_FALSE` 。エイリアスが見つからない場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドは、を呼び出す前に、対象のオブジェクトを null に初期化します。次に、エイリアスが見つかったかどうかを判断するために、後で null 値をテストします。

## <a name="see-also"></a>関連項目
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)

---
title: I列挙型フィールド::スキップ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFields::Skip
helpviewer_keywords:
- IEnumDebugFields::Skip method
ms.assetid: b3bc51c4-21ae-4913-800c-c2ca9dc18443
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b4c08e9291d6aad2801ada8d427adc198d6bc5e5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80716805"
---
# <a name="ienumdebugfieldsskip"></a>IEnumDebugFields::Skip
このメソッドは、指定された数の要素をスキップします。

## <a name="syntax"></a>構文

```cpp
HRESULT Skip(
   ULONG celt
);
```

```csharp
int Skip(
   uint celt
);
```

## <a name="parameters"></a>パラメーター
`celt`\
[in]スキップする要素の数。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 残`S_FALSE`りの`celt`要素の数よりも大きい場合は返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 残`celt`りの要素数より大きい値を指定した場合、列挙型は末尾に設定され`S_FALSE`、返されます。

## <a name="see-also"></a>関連項目
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)

---
title: IEnumデバッグプログラム2::次 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPrograms2::Next
helpviewer_keywords:
- IEnumDebugPrograms2::Next
ms.assetid: 9120e263-e97c-4a40-ab2c-e9264ce3d6c4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 035af638b9504318a39e01f34ed32719d957896e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80715618"
---
# <a name="ienumdebugprograms2next"></a>IEnumDebugPrograms2::Next
列挙体から次の要素セットを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Next(
   ULONG            celt,
   IDebugProgram2** rgelt,
   ULONG*           pceltFetched
);
```

```csharp
int Next(
   uint             celt,
   IDebugProgram2[] rgelt,
   ref uint         pceltFetched
);
```

## <a name="parameters"></a>パラメーター
`celt`\
[in]取得する要素の数。 また、配列の最大サイズも`rgelt`指定します。

`rgelt`\
[イン、アウト]入力する[要素](../../../extensibility/debugger/reference/idebugprogram2.md)の配列。

`pceltFetched`\
[アウト]で実際に返される要素の数`rgelt`を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 返`S_FALSE`される要素の要求数より少ない場合は返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)

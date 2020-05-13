---
title: 2::次 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFrameInfo2::Next
helpviewer_keywords:
- IEnumDebugFrameInfo2::Next
ms.assetid: 64a64eeb-5dea-4119-8a22-03771015d1e5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a5fe15c46066fdbc94b0b7f005ef7a06e1f10cc0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80716705"
---
# <a name="ienumdebugframeinfo2next"></a>IEnumDebugFrameInfo2::Next
列挙体から次の要素セットを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Next(
   ULONG       celt,
   FRAMEINFO** rgelt,
   ULONG*      pceltFetched
);
```

```csharp
int Next(
   uint        celt,
   FRAMEINFO[] rgelt,
   ref uint    pceltFetched
);
```

## <a name="parameters"></a>パラメーター
`celt`\
[in]取得する要素の数。 また、配列の最大サイズも`rgelt`指定します。

`rgelt`\
[イン、アウト]入力する[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)要素の配列。

`pceltFetched`\
[アウト]で実際に返される要素の数`rgelt`を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 返`S_FALSE`される要素の要求数より少ない場合は返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)

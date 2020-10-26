---
title: 'IEnumDebugFrameInfo2:: Next |Microsoft Docs'
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80716705"
---
# <a name="ienumdebugframeinfo2next"></a>IEnumDebugFrameInfo2::Next
列挙体から次の要素のセットを返します。

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
から取得する要素の数。 配列の最大サイズも指定し `rgelt` ます。

`rgelt`\
[入力、出力]入力する [フレーム情報](../../../extensibility/debugger/reference/frameinfo.md) 要素の配列。

`pceltFetched`\
入出力で実際に返された要素の数を返し `rgelt` ます。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 要求された `S_FALSE` 数の要素を返すことができなかった場合は、を返します。それ以外の場合は、エラーコードを返します。

## <a name="see-also"></a>関連項目
- [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)

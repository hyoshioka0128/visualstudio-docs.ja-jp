---
title: イデバッグモドオプト::ゲットモドオプト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugModOpt::GetModOpts
- GetModOpts
ms.assetid: cb513fa9-d521-4a65-b968-f55f53a368df
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5ab870db3ae3517b60bebd4815e4530f6035b327
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727052"
---
# <a name="idebugmodoptgetmodopts"></a>IDebugModOpt::GetModOpts
省略可能な修飾子の一覧を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetModOpts(
   ULONG  celt,
   BSTR*  rgelt,
   ULONG* pceltFetched
);
```

```csharp
int GetModOpts(
   uint         celt,
   out string[] rgelt,
   ref uint     pceltFetched
);
```

## <a name="parameters"></a>パラメーター
`celt`\
[in]返される要素の数。

`rgelt`\
[アウト]オプションを含む配列を返します。

`pceltFetched`\
[イン、アウト]配列に返される要素の`rgelt`数。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugModOpt](../../../extensibility/debugger/reference/idebugmodopt.md)

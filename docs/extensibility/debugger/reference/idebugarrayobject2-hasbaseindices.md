---
title: を返す2::ハスベースインデックス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- HasBaseIndices
- IDebugArrayObject2::HasBaseIndices
ms.assetid: 51a5d145-ea53-422c-b5cf-c800cf64b8e6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 48250b3328310c3f1cb1c84c8fe1a9c61c534cad
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736148"
---
# <a name="idebugarrayobject2hasbaseindices"></a>IDebugArrayObject2::HasBaseIndices
配列に基本インデックス (下限) が定義されているかどうかを判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT HasBaseIndices (
   BOOL* pfHasBaseIndices
);
```

```csharp
int HasBaseIndices (
   out bool pfHasBaseIndices
);
```

## <a name="parameters"></a>パラメーター
`pfHasBaseIndices`\
[アウト]配列に基本インデックス (下限) があることを指定する場合は TRUE。それ以外の場合は FALSE。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

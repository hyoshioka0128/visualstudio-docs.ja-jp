---
title: ドキュメント コンテキスト2::シーク |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::Seek
helpviewer_keywords:
- IDebugDocumentContext2::Seek
ms.assetid: 71501356-8a82-4d36-b354-6625bdd2baa0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 435bb2d5402be06a5fcb3ff9fc99a5c5cb8cb3ab
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731752"
---
# <a name="idebugdocumentcontext2seek"></a>IDebugDocumentContext2::Seek
指定された数のステートメントまたは行でドキュメント コンテキストを移動します。

## <a name="syntax"></a>構文

```cpp
HRESULT Seek( 
   int                      nCount,
   IDebugDocumentContext2** ppDocContext
);
```

```cpp
int Seek( 
   int                        nCount,
   out IDebugDocumentContext2 ppDocContext
);
```

## <a name="parameters"></a>パラメーター
`nCount`\
[in]ドキュメントのコンテキストに応じて、先に進むステートメントまたは行の数。

`ppDocContext`\
[アウト]新しい位置を持つ新しい[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)

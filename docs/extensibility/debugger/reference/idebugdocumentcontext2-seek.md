---
title: 'IDebugDocumentContext2:: Seek |Microsoft Docs'
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80731752"
---
# <a name="idebugdocumentcontext2seek"></a>IDebugDocumentContext2::Seek
指定された数のステートメントまたは行によってドキュメントコンテキストを移動します。

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
からドキュメントコンテキストに応じて、前に移動するステートメントまたは行の数。

`ppDocContext`\
入出力新しい位置を持つ新しい [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)

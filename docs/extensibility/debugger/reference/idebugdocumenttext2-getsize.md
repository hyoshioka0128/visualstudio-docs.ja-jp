---
title: ドキュメント テキスト2::GetSize |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentText2::GetSize
helpviewer_keywords:
- IDebugDocumentText2::GetSize
ms.assetid: bf515a8f-dcee-4004-8f81-543d547ceaae
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: edc4a209537ca4bd54d3f6d9343d1496ab7c0e90
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731595"
---
# <a name="idebugdocumenttext2getsize"></a>IDebugDocumentText2::GetSize
文書内のこの位置にあるテキストのサイズを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetSize( 
   ULONG* pcNumLines,
   ULONG* pcNumChars
);
```

```csharp
int GetSize( 
   ref uint pcNumLines,
   ref uint pcNumChars
);
```

## <a name="parameters"></a>パラメーター
`pcNumLines`\
[アウト]テキストの行数を返します。

`pcNumChars`\
[アウト]テキストの文字数を返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks

 [C++のみ]特定の値が必要ない場合は、パラメータに NULL を渡します。

 [C#のみ]両方のパラメーターを指定する必要があります。

## <a name="see-also"></a>関連項目
- [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)

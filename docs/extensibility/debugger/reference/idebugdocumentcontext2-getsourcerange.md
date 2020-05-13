---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::GetSourceRange
helpviewer_keywords:
- IDebugDocumentContext2::GetSourceRange
ms.assetid: 5903c75e-5390-4d13-9314-1ee276255313
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 782cf230c38af77da09b49f69c093e2e95bf7199
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731790"
---
# <a name="idebugdocumentcontext2getsourcerange"></a>IDebugDocumentContext2::GetSourceRange
このドキュメント コンテキストのソース コード範囲を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetSourceRange( 
   TEXT_POSITION* pBegPosition,
   TEXT_POSITION* pEndPosition
);
```

```csharp
int GetSourceRange( 
   TEXT_POSITION[] pBegPosition,
   TEXT_POSITION[] pEndPosition
);
```

## <a name="parameters"></a>パラメーター
`pBegPosition`\
[イン、アウト]開始位置で埋め込まれる[TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)構造体。 この情報が必要ない場合は、この引数を null 値に設定します。

`pEndPosition`\
[イン、アウト]終了位置で埋め込まれる[TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)構造体。 この情報が必要ない場合は、この引数を null 値に設定します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 ソース範囲は、ソース コードの範囲全体で、現在のステートメントから、コードを提供した直前のステートメントの直後までさかのぼります。 ソース範囲は通常、ソースステートメント (コメントを含む) と逆アセンブリウィンドウのコードを混在させる場合に使用されます。

 このドキュメント コンテキストに含まれるコード ステートメントの範囲だけを取得するには[、GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)

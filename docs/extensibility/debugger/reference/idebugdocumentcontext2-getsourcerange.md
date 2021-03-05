---
description: このドキュメントコンテキストのソースコードの範囲を取得します。
title: 'IDebugDocumentContext2:: GetSourceRange |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::GetSourceRange
helpviewer_keywords:
- IDebugDocumentContext2::GetSourceRange
ms.assetid: 5903c75e-5390-4d13-9314-1ee276255313
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6d02dfbd93002bedadd4c82168d498f89050ddc0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102162902"
---
# <a name="idebugdocumentcontext2getsourcerange"></a>IDebugDocumentContext2::GetSourceRange
このドキュメントコンテキストのソースコードの範囲を取得します。

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
[入力、出力]開始位置を格納する [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 構造体。 この情報が不要な場合は、この引数を null 値に設定します。

`pEndPosition`\
[入力、出力]終了位置を格納する [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 構造体。 この情報が不要な場合は、この引数を null 値に設定します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 ソース範囲は、ソースコードの範囲全体であり、現在のステートメントから、コードを提供した前のステートメントの直後に戻ります。 ソース範囲は、通常、コメントなどのソースステートメントと、[逆アセンブル] ウィンドウのコードを組み合わせるために使用されます。

 このドキュメントコンテキスト内に含まれるコードステートメントの範囲だけを取得するには、 [GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md) メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)

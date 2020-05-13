---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::GetStatementRange
helpviewer_keywords:
- IDebugDocumentContext2::GetStatementRange
ms.assetid: bc94851a-0ec4-47ea-99c7-0a585e54e726
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 50e521d98f10477d56dfece30e20fd000b87b632
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731771"
---
# <a name="idebugdocumentcontext2getstatementrange"></a>IDebugDocumentContext2::GetStatementRange
ドキュメント コンテキストのファイル ステートメント範囲を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetStatementRange(
    TEXT_POSITION* pBegPosition,
    TEXT_POSITION* pEndPosition
);
```

```csharp
int GetStatementRange(
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
ステートメント範囲は、このドキュメントコンテキストが参照するコードを提供した行の範囲です。

このドキュメント コンテキスト内のソース コード (コメントを含む) の範囲を取得するには[、GetSourceRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getsourcerange.md)メソッドを呼び出します。

## <a name="example"></a>例
次の例は[、IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)インターフェイス`CDebugContext`を公開する単純なオブジェクトに対してこのメソッドを実装する方法を示しています。 次の使用例は、開始位置が NULL 値でない場合にのみ、終了位置に値を設定します。

```cpp
HRESULT CDebugContext::GetStatementRange(TEXT_POSITION* pBegPosition,
                                         TEXT_POSITION* pEndPosition)
{
    HRESULT hr;

    // Check for a valid beginning position argument pointer.
    if (pBegPosition)
    {
        // Copy the member TEXT_POSITION into the local pBegPosition.
        memcpy(pBegPosition, &m_pos, sizeof (TEXT_POSITION));

        // Check for a valid ending position argument pointer.
        if (pEndPosition)
        {
            // Copy the member TEXT_POSITION into the local pEndPosition.
            memcpy(pEndPosition, &m_pos, sizeof (TEXT_POSITION));
        }
        hr = S_OK;
    }
    else
    {
        hr = E_INVALIDARG;
    }

    return hr;
}
```

## <a name="see-also"></a>関連項目
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [GetSourceRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getsourcerange.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)

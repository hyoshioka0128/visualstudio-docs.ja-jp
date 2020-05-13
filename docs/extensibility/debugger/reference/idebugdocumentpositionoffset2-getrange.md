---
title: 位置オフセット2::ゲットレンジ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentPositionOffset2::GetRange
ms.assetid: 27da7130-0932-4f97-abde-05e6fb018606
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fd305b6506471a40de90fbd954e54461d2a139d0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731625"
---
# <a name="idebugdocumentpositionoffset2getrange"></a>IDebugDocumentPositionOffset2::GetRange
現在のドキュメントの位置の範囲を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetRange(
   DWORD* pdwBegOffset,
   DWORD* pdwEndOffset
);
```

```csharp
public int GetRange(
   ref uint pdwBegOffset,
   ref uint pdwEndOffset
);
```

## <a name="parameters"></a>パラメーター
`pdwBegOffset`\
[イン、アウト]範囲の開始位置のオフセット。 この情報が必要ない場合は、このパラメーターを NULL 値に設定します。

`pdwEndOffset`\
[イン、アウト]範囲の終了位置のオフセット。 この情報が必要ない場合は、このパラメーターを NULL 値に設定します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 場所ブレークポイントのドキュメント位置で指定された範囲は、実際にコードを提供するステートメントを検索するために、デバッグ エンジン (DE) によって使用されます。 次に例を示します。

```
Line 5: // comment
Line 6: x = 1;
```

 5 行目は、デバッグ中のプログラムにコードを提供しません。 5 行目にブレークポイントを設定するデバッガーが、コードに含まれる最初の行について、デが一定量前方を検索することを望む場合、デバッガーはブレークポイントが正しく配置される可能性がある追加候補行を含む範囲を指定します。 DE は、ブレークポイントを受け入れることができる行が見つかるまで、それらの行を前方に検索します。

## <a name="see-also"></a>関連項目
- [IDebugDocumentPositionOffset2](../../../extensibility/debugger/reference/idebugdocumentpositionoffset2.md)
- [GetRange](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md)

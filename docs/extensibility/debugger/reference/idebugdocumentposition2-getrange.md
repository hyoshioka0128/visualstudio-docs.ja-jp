---
title: ドキュメント位置2::ゲットレンジ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentPosition2::GetRange
helpviewer_keywords:
- IDebugDocumentPosition2::GetRange
ms.assetid: 91a06ee7-253a-4215-be22-04bf57305aa8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a923691afdfe145931ab31d0e9bbc6142e7c8d1c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731667"
---
# <a name="idebugdocumentposition2getrange"></a>IDebugDocumentPosition2::GetRange
このドキュメントの位置の範囲を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetRange( 
   TEXT_POSITION* pBegPosition,
   TEXT_POSITION* pEndPosition
);
```

```csharp
int GetRange( 
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
 場所ブレークポイントのドキュメント位置で指定された範囲は、実際にコードを提供するステートメントを検索するために、デバッグ エンジン (DE) によって使用されます。 次に例を示します。

```
Line 5: // comment
Line 6: x = 1;
```

 5 行目は、デバッグ中のプログラムにコードを提供しません。 5 行目にブレークポイントを設定するデバッガーが、コードに含まれる最初の行について、デが一定量前方を検索することを望む場合、デバッガーはブレークポイントが適切に配置される可能性がある追加候補行を含む範囲を指定します。 DE は、ブレークポイントを受け入れることができる行が見つかるまで、それらの行を前方に検索します。

## <a name="see-also"></a>関連項目
- [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)

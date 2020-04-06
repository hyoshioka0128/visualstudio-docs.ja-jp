---
title: Iデバッグモジュール2::ReloadSymbols_Deprecated |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule2::ReloadSymbols
helpviewer_keywords:
- IDebugModule2::ReloadSymbols method
ms.assetid: 0f9f0133-7d58-4cd9-a6ca-1141e095749d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e776434e17d90cd2c61c926bbf0100a44ecc524b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726918"
---
# <a name="idebugmodule2reloadsymbols_deprecated"></a>IDebugModule2::ReloadSymbols_Deprecated
廃止。 使用しないでください。 このモジュールのシンボルを再ロードします。

## <a name="syntax"></a>構文

```cpp
HRESULT ReloadSymbols( 
   LPCOLESTR pszUrlToSymbols,
   BSTR*     pbstrDebugMessage
);
```

```csharp
int ReloadSymbols( 
   string     pszUrlToSymbols,
   out string pbstrDebugMessage
);
```

## <a name="parameters"></a>パラメーター
`pszUrlToSymbols`\
[in]シンボル ストアへのパス。

`pbstrDebugMessage`\
[アウト]モジュール名の右側に表示されるステータス やエラー メッセージなどの情報メッセージを [モジュール] ウィンドウに返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。 デバッグ エンジンは常に`E_FAIL`を返す必要があります。

## <a name="remarks"></a>Remarks
 このメソッドはサポートされなくなりました。 代わりに[、メソッドを](../../../extensibility/debugger/reference/idebugmodule3-loadsymbols.md)実装します。

## <a name="see-also"></a>関連項目
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
- [LoadSymbols](../../../extensibility/debugger/reference/idebugmodule3-loadsymbols.md)

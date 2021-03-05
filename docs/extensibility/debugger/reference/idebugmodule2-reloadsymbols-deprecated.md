---
description: 互換性のために残されています。 このモジュールのシンボルを再読み込みします。
title: 'IDebugModule2:: ReloadSymbols_Deprecated |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule2::ReloadSymbols
helpviewer_keywords:
- IDebugModule2::ReloadSymbols method
ms.assetid: 0f9f0133-7d58-4cd9-a6ca-1141e095749d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d07f80a3dccef666c0608d79505816f73ff52013
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102150524"
---
# <a name="idebugmodule2reloadsymbols_deprecated"></a>IDebugModule2::ReloadSymbols_Deprecated
互換性のために残されています。 使用しないでください。 このモジュールのシンボルを再読み込みします。

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
からシンボルストアへのパス。

`pbstrDebugMessage`\
入出力[モジュール] ウィンドウのモジュール名の右側に表示される情報メッセージ (状態やエラーメッセージなど) を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。 デバッグエンジンは常にを返す必要があり `E_FAIL` ます。

## <a name="remarks"></a>解説
 このメソッドはサポートされなくなりました。 代わりに、 [Loadsymbols](../../../extensibility/debugger/reference/idebugmodule3-loadsymbols.md) メソッドを実装してください。

## <a name="see-also"></a>関連項目
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
- [LoadSymbols](../../../extensibility/debugger/reference/idebugmodule3-loadsymbols.md)

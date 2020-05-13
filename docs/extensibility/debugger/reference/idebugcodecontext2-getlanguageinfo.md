---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCodeContext2::GetLanguageInfo
helpviewer_keywords:
- IDebugCodeContext2::GetLanguageInfo
ms.assetid: 03002ef1-9fe6-44b6-b23b-ef7b86b2b21b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 465cc07b3ca75835afe0737fb22ba403acc4098b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734242"
---
# <a name="idebugcodecontext2getlanguageinfo"></a>IDebugCodeContext2::GetLanguageInfo
このコード コンテキストの言語情報を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetLanguageInfo( 
   BSTR* pbstrLanguage,
   GUID* pguidLanguage
);
```

```csharp
int GetLanguageInfo( 
   ref string pbstrLanguage,
   ref Guid pguidLanguage
);
```

## <a name="parameters"></a>パラメーター
`pbstrLanguage`\
[イン、アウト]言語の名前を含む文字列を返します。

`pguidLanguage`\
[イン、アウト]コード コンテキストの言語の GUID`guidCPPLang`を返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 少なくとも 1 つのパラメーターは、null 以外の値を返す必要があります。

## <a name="see-also"></a>関連項目
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)

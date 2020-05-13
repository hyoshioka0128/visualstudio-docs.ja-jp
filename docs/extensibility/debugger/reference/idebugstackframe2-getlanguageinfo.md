---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetLanguageInfo
helpviewer_keywords:
- IDebugStackFrame2::GetLanguageInfo
ms.assetid: 0e12fd92-f155-46a7-8272-cda279388cfb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cefb4bdd9d0c85311c63e6a988956301a6c2cc14
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719701"
---
# <a name="idebugstackframe2getlanguageinfo"></a>IDebugStackFrame2::GetLanguageInfo

このスタック フレームに関連付けられている言語を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetLanguageInfo ( 
   BSTR* pbstrLanguage,
   GUID* pguidLanguage
);
```

```csharp
int GetLanguageInfo ( 
   ref string pbstrLanguage,
   ref Guid   pguidLanguage
);
```

## <a name="parameters"></a>パラメーター

`pbstrLanguage`\
[アウト]このスタック フレームに関連付けられているメソッドを実装する言語の名前を返します。

`pguidLanguage`\
[アウト]言語の`GUID`を返します。 たとえば、[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]言語の場合は、次の値を返すことができます。

- `guidVBScriptLang`\

- `guidJScriptLang`\

- `guidCPPLang`\

- `guidVBLang`\

- `guidSQLLang`\

- `guidScriptLang`\

## <a name="return-value"></a>戻り値

 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目

- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)

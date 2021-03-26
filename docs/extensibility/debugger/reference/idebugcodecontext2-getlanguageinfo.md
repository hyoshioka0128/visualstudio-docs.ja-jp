---
description: このコードコンテキストの言語情報を取得します。
title: 'IDebugCodeContext2:: Get言語 Info |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCodeContext2::GetLanguageInfo
helpviewer_keywords:
- IDebugCodeContext2::GetLanguageInfo
ms.assetid: 03002ef1-9fe6-44b6-b23b-ef7b86b2b21b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 62d076a2780ab8d49f79379111eaeef9dd1cdc88
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088381"
---
# <a name="idebugcodecontext2getlanguageinfo"></a>IDebugCodeContext2::GetLanguageInfo
このコードコンテキストの言語情報を取得します。

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
[入力、出力]"C++" など、言語の名前を含む文字列を返します。

`pguidLanguage`\
[入力、出力]コードコンテキストの言語の GUID を返します。たとえば、のように `guidCPPLang` なります。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 少なくとも1つのパラメーターが null 以外の値を返す必要があります。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)

---
description: このメソッドは、SetHostingProcessLanguage の呼び出しによって設定された、このプロセスの言語を表す GUID を返します。
title: 'IDebugProcess3:: GetHostingProcessLanguage |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::GetHostingProcessLanguage
helpviewer_keywords:
- IDebugProcess3::GetHostingProcessLanguage
ms.assetid: 52fca002-a9ef-43b1-9192-afbe7bb59ad4
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 303f0e5dcd4cc87bbc13e55fcc9b95bc870213d5
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158437"
---
# <a name="idebugprocess3gethostingprocesslanguage"></a>IDebugProcess3::GetHostingProcessLanguage
このメソッドは、 `GUID` [Sethostingprocesslanguage](../../../extensibility/debugger/reference/idebugprocess3-sethostingprocesslanguage.md)の呼び出しによって設定された、このプロセスの言語を表すを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetHostingProcessLanguage(
   GUID* pguidLang
);
```

```csharp
int GetHostingProcessLanguage(
   out Guid pguidLang
);
```

## <a name="parameters"></a>パラメーター
`pguidLang`\
入出力 `GUID` このプロセスの言語の。 `GUID_NULL` (C++) または `Guid.Empty` (C#) は、言語が設定されていないことを意味します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [SetHostingProcessLanguage](../../../extensibility/debugger/reference/idebugprocess3-sethostingprocesslanguage.md)

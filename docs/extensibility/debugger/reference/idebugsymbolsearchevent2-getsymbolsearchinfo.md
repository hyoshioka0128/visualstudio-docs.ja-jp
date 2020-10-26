---
title: 'IDebugSymbolSearchEvent2:: Getシンボル Searchinfo |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolSearchEvent2::GetSymbolSearchInfo
helpviewer_keywords:
- IDebugSymbolSearchEvent2::GetSymbolSearchInfo
ms.assetid: ae9eb72b-f2aa-43b8-87ca-da19d2e78d17
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: be498154a8141c61f114682893d0aaf8b841cf95
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80718885"
---
# <a name="idebugsymbolsearchevent2getsymbolsearchinfo"></a>IDebugSymbolSearchEvent2::GetSymbolSearchInfo
シンボルの読み込みプロセスに関する結果を取得するために、イベントハンドラーによって呼び出されます。

## <a name="syntax"></a>構文

```cpp
HRESULT GetSymbolSearchInfo(
   IDebugModule3**    pModule,
   BSTR*              pbstrDebugMessage,
   MODULE_INFO_FLAGS* pdwModuleInfoFlags
);
```

```csharp
int GetSymbolSearchInfo(
   IDebugModule3              pModule,
   ref string                 pbstrDebugMessage,
   out enum_MODULE_INFO_FLAGS pdwModuleInfoFlags
);
```

## <a name="parameters"></a>パラメーター
`pModule`\
入出力シンボルが読み込まれたモジュールを表す IDebugModule3 オブジェクト。

`pbstrDebugMessage`\
[入力、出力]モジュールからのエラーメッセージを含む文字列を返します。 エラーがない場合、この文字列にはモジュールの名前だけが含まれますが、空になることはありません。

> [!NOTE]
> [C++] `pbstrDebugMessage` をにすることはできません `NULL` 。また、で解放する必要があり `SysFreeString` ます。

`pdwModuleInfoFlags`\
入出力シンボルが読み込まれたかどうかを示す、 [MODULE_INFO_FLAGS](../../../extensibility/debugger/reference/module-info-flags.md) 列挙のフラグの組み合わせ。

## <a name="return-value"></a>戻り値
 成功した場合は、を返します。それ以外の場合は `S_OK` エラーコードを返します。

## <a name="remarks"></a>注釈
 モジュールのデバッグシンボルの読み込みが試行された後にハンドラーが [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md) イベントを受け取ると、ハンドラーは thismethod を呼び出してその読み込みの結果を確認できます。

## <a name="see-also"></a>関連項目
- [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)
- [MODULE_INFO_FLAGS](../../../extensibility/debugger/reference/module-info-flags.md)
- [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)

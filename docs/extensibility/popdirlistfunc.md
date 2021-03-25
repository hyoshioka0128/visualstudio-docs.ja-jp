---
title: POPDIRLISTFUNC |Microsoft Docs
description: ソース管理下にあることを確認するために更新ディレクトリに渡される POPDIRLISTFUNC callback 関数について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- POPLISTFUNC
helpviewer_keywords:
- POPDIRLISTFUNC callback function
ms.assetid: 0ee90fd2-5467-4154-ab4c-7eb02ac3a14c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0f8cde3e6835a7d3262bbb89fed13e0dbc8e540e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090253"
---
# <a name="popdirlistfunc"></a>POPDIRLISTFUNC
これは、 [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md) 関数に与えられたコールバック関数であり、ディレクトリのコレクションと (必要に応じて) ファイル名を更新して、ソース管理下にある場所を検索します。

 `POPDIRLISTFUNC`コールバックは、実際にソース管理下にあるディレクトリとファイル名 (関数に指定されたリスト内) に対してのみ呼び出す必要があり `SccPopulateDirList` ます。

## <a name="signature"></a>署名

```cpp
typedef BOOL (*POPDIRLISTFUNC)(
   LPVOID pvCallerData,
   BOOL bFolder,
   LPCSTR lpDirectoryOrFileName
);
```

## <a name="parameters"></a>パラメーター
 pvCallerData

から [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)に指定されたユーザー値。

 bFolder

[入力] `TRUE` 内の名前がディレクトリである場合は `lpDirectoryOrFileName` 。それ以外の場合はファイル名。

 lpDirectoryOrFileName

からソースコード管理下にあるディレクトリまたはファイル名への完全なローカルパス。

## <a name="return-value"></a>戻り値
 IDE から適切なエラーコードが返されます。

|値|説明|
|-----------|-----------------|
|SCC_OK|処理し続けます。|
|SCC_I_OPERATIONCANCELED|処理を停止します。|
|SCC_E_xxx|適切なソース管理エラーが発生すると、処理が停止します。|

## <a name="remarks"></a>注釈
 関数のパラメーターにフラグが含まれている場合、 `fOptions` `SccPopulateDirList` `SCC_PDL_INCLUDEFILES` リストにはファイル名とディレクトリ名が含まれている可能性があります。

## <a name="see-also"></a>こちらもご覧ください
- [IDE によって実装されるコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)
- [エラー コード](../extensibility/error-codes.md)

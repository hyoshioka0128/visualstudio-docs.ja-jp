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
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 805d7a5c9250bc511692c497bc9083852dad2301
ms.sourcegitcommit: dd96a95d87a039525aac86abe689c30e2073ae87
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2021
ms.locfileid: "97863447"
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

## <a name="remarks"></a>解説
 関数のパラメーターにフラグが含まれている場合、 `fOptions` `SccPopulateDirList` `SCC_PDL_INCLUDEFILES` リストにはファイル名とディレクトリ名が含まれている可能性があります。

## <a name="see-also"></a>関連項目
- [IDE によって実装されるコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)
- [エラー コード](../extensibility/error-codes.md)

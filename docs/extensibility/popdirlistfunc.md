---
title: ポプディリストファンク |マイクロソフトドキュメント
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
ms.openlocfilehash: 52a0c16af0e142bda8527c5244a22e0830ced9e0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702078"
---
# <a name="popdirlistfunc"></a>POPDIRLISTFUNC
これは、ディレクトリのコレクションを更新するために[SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)関数に与えられたコールバック関数であり、(オプションで) ソース管理下にあるファイル名を調べるためにします。

 コールバック`POPDIRLISTFUNC`は、実際にソース管理下にあるディレクトリとファイル名 (`SccPopulateDirList`関数に与えられたリスト内) に対してのみ呼び出す必要があります。

## <a name="signature"></a>署名

```cpp
typedef BOOL (*POPDIRLISTFUNC)(
   LPVOID pvCallerData,
   BOOL bFolder,
   LPCSTR lpDirectoryOrFileName
);
```

## <a name="parameters"></a>パラメーター
 呼び出し元データ

[in]に与えられたユーザー値[。](../extensibility/sccpopulatedirlist-function.md)

 bフォルダ

[in]`TRUE`の`lpDirectoryOrFileName`名前がディレクトリの場合。それ以外の場合、名前はファイル名です。

 ファイル名

[in]ソース コード管理下にあるディレクトリまたはファイル名への完全なローカル パス。

## <a name="return-value"></a>戻り値
 IDE は、適切なエラー コードを返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|処理し続けます。|
|SCC_I_OPERATIONCANCELED|処理を停止します。|
|SCC_E_xxx|適切なソース管理エラーは処理を停止する必要があります。|

## <a name="remarks"></a>Remarks
 関数の`fOptions`パラメータにフラグ`SccPopulateDirList`が`SCC_PDL_INCLUDEFILES`含まれている場合、リストにはファイル名とディレクトリ名が含まれる可能性があります。

## <a name="see-also"></a>関連項目
- [IDE によって実装されるコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)
- [エラー コード](../extensibility/error-codes.md)

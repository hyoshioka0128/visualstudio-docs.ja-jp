---
title: SccRemove 関数 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccRemove
helpviewer_keywords:
- SccRemove function
ms.assetid: 20830fdc-c0e9-4a5f-bf60-33f28874442f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 17889d50dbdcf68dd4cca161d6703b8b6d69ad47
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700454"
---
# <a name="sccremove-function"></a>SccRemove 関数
この関数は、ソース管理システムからファイルを削除します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccRemove(
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LPCSTR    lpComment,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

#### <a name="parameters"></a>パラメーター
 を行う

[in]ソース管理プラグインのコンテキスト構造。

 hWnd

[in]ソース管理プラグインが提供するダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 nファイル

[in]配列に指定されたファイルの`lpFileNames`数。

 ファイル名

[in]削除するファイルの完全修飾ローカル パス名の配列。

 ル・コメント

[in]削除する各ファイルに適用するコメント。

 f オプション

[in]コマンド フラグ (未使用)。

 オプション

[in]ソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|削除に成功しました。|
|SCC_E_FILENOTCONTROLLED|選択したファイルはソース管理下にありません。|
|SCC_E_OPNOTSUPPORTED|ソース管理システムはこの操作をサポートしていません。|
|SCC_E_ISCHECKEDOUT|ユーザーが現在チェックアウトしているため、ファイルを削除できません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセスに問題が発生しました。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_E_NONSPECIFICERROR|非特異的な障害;ファイルは削除されませんでした。|
|SCC_I_OPERATIONCANCELED|操作は完了前に取り消されました。|

## <a name="remarks"></a>Remarks
 この関数は、ソース管理システムからファイルを削除しますが、ユーザーのローカルハード ドライブからは削除しません。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)

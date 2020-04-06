---
title: SccCheckin 関数 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccCheckin
helpviewer_keywords:
- SccCheckin function
ms.assetid: e3f26ac2-6163-42e1-a764-22cfea5a3bc6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a5ba512642e1a63d9d39856f96194d717583d44f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701183"
---
# <a name="scccheckin-function"></a>SccCheckin 関数
この関数は、以前チェックアウトされたファイルをソース管理システムにチェックインし、変更を保存して新しいバージョンを作成します。 この関数は、チェックインするファイルの名前の数と配列を使用して呼び出されます。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccCheckin (
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPSTR*    lpFileNames,
   LPCSTR    lpComment,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>パラメーター
 を行う

[in]ソース管理プラグインのコンテキスト構造。

 hWnd

[in]SCC プラグインが提供するダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 nファイル

[in]チェックインするファイルの数を指定します。

 ファイル名

[in]チェックインするファイルの完全修飾ローカル パス名の配列。

 ル・コメント

[in]チェックインされる選択した各ファイルに適用するコメント。 このパラメーターは`NULL`、ソース管理プラグインがコメントを求める必要がある場合です。

 f オプション

[in]コマンド フラグは 0`SCC_KEEP_CHECKEDOUT`または .

 オプション

[in]SCC プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|ファイルは正常にチェックインされました。|
|SCC_E_FILENOTCONTROLLED|選択したファイルはソース コード管理の対象ではありません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセスに問題が発生しました。 再試行することをお勧めします。|
|SCC_E_NONSPECIFICERROR|非特異的なエラー。 ファイルはチェックインされませんでした。|
|SCC_E_NOTCHECKEDOUT|ユーザーはファイルをチェックアウトしていないので、チェックインできません。|
|SCC_E_CHECKINCONFLICT|次の理由により、チェックインを実行できませんでした。<br /><br /> - 別のユーザーが事前に`bAutoReconcile`チェックインし、偽でした。<br /><br /> \- または -<br /><br /> - 自動マージは実行できません (ファイルがバイナリの場合など)。|
|SCC_E_VERIFYMERGE|ファイルは自動マージされましたが、保留中のユーザー検証でチェックインされていません。|
|SCC_E_FIXMERGE|ファイルは自動マージされましたが、手動で解決する必要があるマージの競合のためチェックインされていません。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_I_OPERATIONCANCELED|操作は完了前に取り消されました。|
|SCC_I_RELOADFILE|ファイルまたはプロジェクトを再ロードする必要があります。|
|SCC_E_FILENOTEXIST|ローカル ファイルが見つかりませんでした。|

## <a name="remarks"></a>Remarks
 コメントはチェックインされるすべてのファイルに適用されます。 comment 引数には文字列を`null`指定できます。

 引数`fOptions`には、ファイルを`SCC_KEEP_CHECKEDOUT`チェックインして再度チェックアウトするユーザーの意図を示すフラグの値を指定できます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)

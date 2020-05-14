---
title: SccCheckout 関数 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccCheckout
helpviewer_keywords:
- SccCheckout function
ms.assetid: 06e9ecd7-fc09-40c1-9dd1-2b56c622c80b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6ed809e33a80bf2903c88550e97b28b1e0178bcd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701103"
---
# <a name="scccheckout-function"></a>SccCheckout 関数
この関数は、完全修飾ファイル名のリストを指定して、ローカル ドライブにファイル名をチェックアウトします。 コメントは、チェックアウトされているすべてのファイルに適用されます。comment 引数には文字列を`null`指定できます。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccCheckout (
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LPCSTR    lpComment,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>パラメーター
 を行う

[in]ソース管理プラグインのコンテキスト構造。

 hWnd

[in]ソース管理プラグインが提供するダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 nファイル

[in]チェックアウトするファイルの数。

 ファイル名

[in]チェックアウトするファイルの完全修飾ローカル パス名の配列。

 ル・コメント

[in]チェックアウトされている選択した各ファイルに適用するコメント。

 f オプション

[in]コマンド フラグ ([特定のコマンドで使用されるビットフラグを](../extensibility/bitflags-used-by-specific-commands.md)参照)。

 オプション

[in]ソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|チェックアウトが成功しました。|
|SCC_E_FILENOTCONTROLLED|選択したファイルはソース コード管理の対象ではありません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセスに問題が発生しました。 再試行することをお勧めします。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_E_NONSPECIFICERROR|非特異的なエラー。 ファイルはチェックアウトされませんでした。|
|SCC_E_ALREADYCHECKEDOUT|ユーザーは既にファイルをチェックアウトしています。|
|SCC_E_FILEISLOCKED|ファイルがロックされ、新しいバージョンの作成が禁止されています。|
|SCC_E_FILEOUTEXCLUSIVE|別のユーザーがこのファイルに対して排他的チェックアウトを行いました。|
|SCC_I_OPERATIONCANCELED|操作は完了前に取り消されました。|

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)

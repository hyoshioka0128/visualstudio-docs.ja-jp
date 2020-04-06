---
title: SccUncheckout機能 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccUncheckout
helpviewer_keywords:
- SccUncheckout function
ms.assetid: 6d498b70-29c7-44b7-ae1c-7e99e488bb09
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4317133b2f215e0f9af447e5c042785561231f63
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700247"
---
# <a name="sccuncheckout-function"></a>SccUncheckout 関数
この関数は、以前のチェックアウト操作を元に戻し、選択したファイルの内容をチェックアウト前の状態に復元します。 チェックアウト後にファイルに加えられたすべての変更は失われます。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccUncheckout (
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
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

[in]チェックアウトを取り消すファイルの完全修飾ローカル パス名の配列。

 f オプション

[in]コマンド フラグ (使用されていません)。

 オプション

[in]ソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|チェックアウトの取り消しが正常に行われました。|
|SCC_E_FILENOTCONTROLLED|選択したファイルはソース コード管理の対象ではありません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセスに問題が発生しました。 再試行することをお勧めします。|
|SCC_E_NONSPECIFICERROR|非特異的なエラー。 チェックアウトを元に戻せませんでした。|
|SCC_E_NOTCHECKEDOUT|ユーザーはファイルをチェックアウトしていません。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_E_PROJNOTOPEN|プロジェクトはソース管理から開かれていない。|
|SCC_I_OPERATIONCANCELED|操作は完了前に取り消されました。|

## <a name="remarks"></a>Remarks
 この操作の`SCC_STATUS_CHECKEDOUT`後、および`SCC_STATUS_MODIFIED`両方のフラグは、チェックアウトを元に戻すが実行されたファイルに対してクリアされます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)

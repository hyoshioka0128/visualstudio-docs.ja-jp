---
description: この関数は、ソース管理システムからファイルを削除します。
title: SccRemove 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccRemove
helpviewer_keywords:
- SccRemove function
ms.assetid: 20830fdc-c0e9-4a5f-bf60-33f28874442f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d80daf83458c9e05ef0a081348080579e7fafef4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073873"
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
 pvContext

からソース管理プラグインのコンテキスト構造。

 hWnd

からソース管理プラグインが提供するすべてのダイアログボックスの親として使用できる IDE ウィンドウへのハンドル。

 nFiles

から配列に指定されたファイルの数 `lpFileNames` 。

 lpFileNames 名

から削除するファイルの完全修飾ローカルパス名の配列。

 lpComment

から削除する各ファイルに適用されるコメント。

 限ら

からコマンドフラグ (未使用)。

 pvOptions

からソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|削除に成功しました。|
|SCC_E_FILENOTCONTROLLED|選択されたファイルはソース管理下にありません。|
|SCC_E_OPNOTSUPPORTED|ソース管理システムでは、この操作はサポートされていません。|
|SCC_E_ISCHECKEDOUT|現在、ユーザーがチェックアウトしているため、ファイルを削除できません。|
|SCC_E_ACCESSFAILURE|ネットワークまたは競合の問題が原因で、ソース管理システムへのアクセスで問題が発生しました。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。ファイルは削除されませんでした。|
|SCC_I_OPERATIONCANCELED|操作は完了前に取り消されました。|

## <a name="remarks"></a>注釈
 この関数は、ソース管理システムからファイルを削除しますが、ユーザーのローカルハードドライブからは削除しません。

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)

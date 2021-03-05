---
description: この関数は、以前にチェックアウトされたファイルをソース管理システムにチェックインし、変更を保存し、新しいバージョンを作成します。
title: SccCheckin 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccCheckin
helpviewer_keywords:
- SccCheckin function
ms.assetid: e3f26ac2-6163-42e1-a764-22cfea5a3bc6
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a835ead5fb0404b78d9e9c9ecc92ee0c73eaf252
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102220860"
---
# <a name="scccheckin-function"></a>SccCheckin 関数
この関数は、以前にチェックアウトされたファイルをソース管理システムにチェックインし、変更を保存し、新しいバージョンを作成します。 この関数は、カウントと、チェックインするファイルの名前の配列を使用して呼び出されます。

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
 pvContext

からソース管理プラグインのコンテキスト構造。

 hWnd

からSCC プラグインが提供するすべてのダイアログボックスの親として使用できる IDE ウィンドウへのハンドル。

 nFiles

からチェックインするように選択されたファイルの数。

 lpFileNames 名

からチェックインするファイルの完全修飾ローカルパス名の配列。

 lpComment

からチェックインする選択された各ファイルに適用されるコメント。 `NULL`ソース管理プラグインがコメントの入力を求められる場合、このパラメーターはになります。

 限ら

からコマンドフラグ (0 またはのいずれか) `SCC_KEEP_CHECKEDOUT` 。

 pvOptions

からSCC プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|ファイルは正常にチェックインされました。|
|SCC_E_FILENOTCONTROLLED|選択したファイルはソースコード管理されていません。|
|SCC_E_ACCESSFAILURE|ネットワークまたは競合の問題が原因で、ソース管理システムへのアクセスで問題が発生しました。 再試行することをお勧めします。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。 ファイルがチェックインされませんでした。|
|SCC_E_NOTCHECKEDOUT|ユーザーはファイルをチェックアウトしていないので、チェックインできません。|
|SCC_E_CHECKINCONFLICT|次の理由により、チェックインを実行できませんでした:<br /><br /> -別のユーザーが事前にチェックインし、 `bAutoReconcile` が false でした。<br /><br /> - または -<br /><br /> -自動マージは実行できません (たとえば、ファイルがバイナリの場合)。|
|SCC_E_VERIFYMERGE|ファイルは自動マージされていますが、保留中のユーザーの検証がチェックインされていません。|
|SCC_E_FIXMERGE|ファイルは自動マージされていますが、マージの競合が原因でチェックインされていないため、手動で解決する必要があります。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_I_OPERATIONCANCELED|操作が完了前に取り消されました。|
|SCC_I_RELOADFILE|ファイルまたはプロジェクトを再度読み込む必要があります。|
|SCC_E_FILENOTEXIST|ローカルファイルが見つかりませんでした。|

## <a name="remarks"></a>解説
 コメントは、チェックインされているすべてのファイルに適用されます。 Comment 引数には文字列を指定できます `null` 。この場合、ソース管理プラグインは、ファイルごとにコメント文字列の入力をユーザーに求めることができます。

 `fOptions`引数にフラグの値を指定 `SCC_KEEP_CHECKEDOUT` すると、ユーザーがファイルをチェックインする目的を示すことができます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)

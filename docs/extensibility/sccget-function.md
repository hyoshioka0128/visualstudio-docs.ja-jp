---
title: 関数の機能 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGet
helpviewer_keywords:
- SccGet function
ms.assetid: 09a18bd2-b788-411a-9da6-067d806e46f6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c2d69308d2f569fc2e0d72dcf64c762687955d4d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700899"
---
# <a name="sccget-function"></a>関数を実行する
この関数は、表示およびコンパイル用の 1 つ以上のファイルのコピーを取得しますが、編集用ではありません。 ほとんどのシステムでは、ファイルは読み取り専用としてタグ付けされます。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccGet(
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
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

[in]配列に指定されたファイルの`lpFileNames`数。

 ファイル名

[in]取得するファイルの完全修飾名の配列。

 f オプション

[in]コマンド フラグ`SCC_GET_ALL` `SCC_GET_RECURSIVE`( , )

 オプション

[in]ソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|取得操作の成功。|
|SCC_E_FILENOTCONTROLLED|ファイルはソース管理下にありません。|
|SCC_E_OPNOTSUPPORTED|ソース管理システムはこの操作をサポートしていません。|
|SCC_E_FILEISCHECKEDOUT|ユーザーが現在チェックアウトしているファイルを取得できません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセスに問題が発生しました。 再試行することをお勧めします。|
|SCC_E_NOSPECIFIEDVERSION|無効なバージョンまたは日付/時刻を指定しました。|
|SCC_E_NONSPECIFICERROR|非特異的な障害;ファイルが同期されていません。|
|SCC_I_OPERATIONCANCELED|操作は完了前にキャンセルされました。|
|SCC_E_NOTAUTHORIZED|ユーザーにはこの操作を実行する権限がありません。|

## <a name="remarks"></a>Remarks
 この関数は、取得するファイルの名前の数と配列を使用して呼び出されます。 IDE が フラグ`SCC_GET_ALL`を渡す場合、この場合、`lpFileNames`の項目はファイルではなくディレクトリであり、指定されたディレクトリ内のソース管理下にあるすべてのファイルが取得されます。

 `SCC_GET_ALL`フラグとフラグを`SCC_GET_RECURSIVE`組み合わせて、指定されたディレクトリとすべてのサブディレクトリにあるすべてのファイルを取得できます。

> [!NOTE]
> `SCC_GET_RECURSIVE`なしで`SCC_GET_ALL`渡されるべきではありません。 また、*ディレクトリ C:\A*と*C:\A\B*の両方が再帰的な取得で渡される場合 *、C:\A\B*とそのサブディレクトリはすべて実際には 2 回取得されることに注意してください。 このような重複が配列から除外されるようにするのは、ソース管理プラグインではなく IDE の責任です。

 最後に、ソース管理プラグインが初期化時に`SCC_CAP_GET_NOUI`Get コマンドのユーザー インターフェイスを持たないというフラグを指定した場合でも、この関数は IDE から呼び出され、ファイルを取得できます。 このフラグは、IDE が Get メニュー項目を表示せず、プラグインが UI を提供しないことを示しています。

## <a name="rename-files-and-sccget"></a>ファイルの名前を変更し、SccGet
 状況: ユーザーがファイルをチェックアウトし、たとえば*a.txt*を変更します。 *a.txt を*チェックインする前に、2 人目のユーザーがソース管理データベースの*a.txt*を*b.txt*に変更し *、b.txt*をチェックアウトして、ファイルを変更してファイルをチェックインします。 最初のユーザーは、2 番目のユーザーが行った変更を必要とするため、最初のユーザーはローカル バージョンの*a.txt*ファイルを*b.txt*に変更し、ファイルを取得します。 ただし、バージョン番号を追跡するローカル キャッシュは *、a.txt*の最初のバージョンがローカルに格納されているので、ソース管理では相違点を解決できないと考えています。

 ソース管理バージョンのローカル キャッシュがソース管理データベースと同期しなくなる場合、この状況を解決するには 2 つの方法があります。

1. 現在チェックアウトされているソース管理データベースのファイル名を変更することはできません。

2. 「古い削除」の後に「新規追加」と同等の操作を行います。 次のアルゴリズムは、これを実現する 1 つの方法です。

    1. ソース管理データベース内の*a.txt*から*b.txt*への名前変更について学習するには[、SccQueryChanges](../extensibility/sccquerychanges-function.md)関数を呼び出します。

    2. ローカル*a.txt*の名前を*b.txt に*変更します。

    3. a.txt と`SccGet`*b.txt*の両方の関数を呼び出*します*。

    4. *a.txt*はソース管理データベースに存在しないため、ローカル バージョン キャッシュは欠落している*a.txt*バージョン情報を削除します。

    5. チェックアウト中の*b.txt*ファイルは、ローカル*b.txt*ファイルの内容とマージされます。

    6. 更新された*b.txt*ファイルをチェックインできるようになりました。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)

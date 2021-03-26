---
description: この関数は、表示とコンパイルのために1つ以上のファイルのコピーを取得しますが、編集することはできません。
title: SccGet 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGet
helpviewer_keywords:
- SccGet function
ms.assetid: 09a18bd2-b788-411a-9da6-067d806e46f6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 172e0ec5fdba4b91c3cf86ea964b4a98a23a5fa8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060342"
---
# <a name="sccget-function"></a>SccGet 関数
この関数は、表示とコンパイルのために1つ以上のファイルのコピーを取得しますが、編集することはできません。 ほとんどのシステムでは、ファイルは読み取り専用としてタグ付けされています。

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
 pvContext

からソース管理プラグインのコンテキスト構造。

 hWnd

からソース管理プラグインが提供するすべてのダイアログボックスの親として使用できる IDE ウィンドウへのハンドル。

 nFiles

から配列に指定されたファイルの数 `lpFileNames` 。

 lpFileNames 名

から取得するファイルの完全修飾名の配列。

 限ら

からコマンドフラグ ( `SCC_GET_ALL` 、 `SCC_GET_RECURSIVE` )。

 pvOptions

からソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|Get 操作が成功しました。|
|SCC_E_FILENOTCONTROLLED|ファイルがソース管理下にありません。|
|SCC_E_OPNOTSUPPORTED|ソース管理システムでは、この操作はサポートされていません。|
|SCC_E_FILEISCHECKEDOUT|ユーザーが現在チェックアウトしているファイルを取得できません。|
|SCC_E_ACCESSFAILURE|ネットワークまたは競合の問題が原因で、ソース管理システムへのアクセスで問題が発生しました。 再試行することをお勧めします。|
|SCC_E_NOSPECIFIEDVERSION|無効なバージョンまたは日付/時刻が指定されました。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。ファイルは同期されませんでした。|
|SCC_I_OPERATIONCANCELED|操作は完了前に取り消されました。|
|SCC_E_NOTAUTHORIZED|ユーザーにはこの操作を実行する権限がありません。|

## <a name="remarks"></a>注釈
 この関数は、カウントと、取得するファイルの名前の配列を使用して呼び出されます。 IDE がフラグを渡す `SCC_GET_ALL` と、内の項目はファイルでは `lpFileNames` なくディレクトリであり、特定のディレクトリ内のソース管理下にあるすべてのファイルが取得されることを意味します。

 `SCC_GET_ALL`フラグをフラグと組み合わせて、 `SCC_GET_RECURSIVE` 指定したディレクトリとすべてのサブディレクトリ内のすべてのファイルを取得することもできます。

> [!NOTE]
> `SCC_GET_RECURSIVE` を指定せずにを渡すことはできません `SCC_GET_ALL` 。 また、ディレクトリ *c:\* と *c:\* の両方が再帰的 get で渡される場合、 *c:\ a\b* とそのすべてのサブディレクトリは、実際に2回取得されることに注意してください。 これは、ソース管理プラグインではなく、IDE の責任であり、このような重複が配列から確実に保持されるようにします。

 最後に、ソース管理プラグインで初期化時にフラグが指定されていても、 `SCC_CAP_GET_NOUI` Get コマンドのユーザーインターフェイスがないことを示す場合でも、ファイルを取得するために IDE によってこの関数が呼び出されることがあります。 フラグは、IDE に [取得] メニュー項目が表示されず、プラグインが UI を提供しないことを意味します。

## <a name="rename-files-and-sccget"></a>ファイル名の変更と SccGet
 状況: ユーザーがファイル ( *a.txt* など) をチェックアウトし、変更します。 *a.txt* をチェックインする前に、2番目のユーザーが *a.txt* の名前をソース管理データベースの *b.txt* に変更し、 *b.txt* をチェックアウトして、ファイルに何らかの変更を加え、ファイルをチェックインします。 最初のユーザーは、2番目のユーザーによって行われた変更を必要とします。そのため、最初のユーザーが *a.txt* ファイルのローカルバージョンの名前を *b.txt* に変更し、ファイルに対して get を実行します。 ただし、バージョン番号を追跡するローカルキャッシュでは、 *a.txt* の最初のバージョンがローカルに格納されていると判断されるため、ソース管理では相違点を解決できません。

 ソース管理のバージョンのローカルキャッシュがソース管理データベースと同期しなくなる状況を解決するには、次の2つの方法があります。

1. 現在チェックアウトされているソース管理データベース内のファイルの名前を変更することはできません。

2. "古いものを削除" の後に "add new" を続けて実行します。 次のアルゴリズムは、これを実現するための1つの方法です。

    1. [Sccquerychanges](../extensibility/sccquerychanges-function.md)関数を呼び出して、ソース管理データベース内で *b.txt* する *a.txt* の名前変更について学習します。

    2. ローカル *a.txt* の名前を *b.txt* に変更します。

    3. `SccGet` *a.txt* と *b.txt* の両方に対して関数を呼び出します。

    4. ソース管理データベースには *a.txt* が存在しないため、ローカルバージョンのキャッシュは、不足している *a.txt* バージョン情報を削除します。

    5. チェックアウトされている *b.txt* ファイルは、ローカル *b.txt* ファイルの内容とマージされます。

    6. 更新された *b.txt* ファイルをチェックインできるようになりました。

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)

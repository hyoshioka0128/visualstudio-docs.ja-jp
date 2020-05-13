---
title: 関数の追加 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccAdd
helpviewer_keywords:
- SccAdd function
ms.assetid: 545268f3-8e83-446a-a398-1a9db9e866e8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 23a6226b0d3cc2441a509c16b2e4672a766f3329
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701314"
---
# <a name="sccadd-function"></a>SccAdd 関数
この関数は、ソース管理システムに新しいファイルを追加します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccAdd(
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LPCSTR    lpComment,
   LONG*     pfOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>パラメーター
 を行う

[in]ソース管理プラグインのコンテキスト構造。

 hWnd

[in]ソース管理プラグインが提供するダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 nファイル

[in]配列に指定されている現在のプロジェクトに追加するファイルの数。 `lpFileNames`

 ファイル名

[in]追加するファイルの完全修飾ローカル名の配列。

 ル・コメント

[in]追加されるすべてのファイルに適用されるコメント。

 オプション

[in]ファイル単位で指定されるコマンド フラグの配列。

 オプション

[in]ソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|追加操作は正常に実行されました。|
|SCC_E_FILEALREADYEXISTS|選択したファイルは既にソース管理下にあります。|
|SCC_E_TYPENOTSUPPORTED|ファイルの種類 (バイナリなど) は、ソース管理システムではサポートされていません。|
|SCC_E_OPNOTSUPPORTED|ソース管理システムはこの操作をサポートしていません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセスに問題が発生しました。 再試行することをお勧めします。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_E_NONSPECIFICERROR|非特異的な障害;追加は実行されません。|
|SCC_I_OPERATIONCANCELED|操作は完了前に取り消されました。|
|SCC_I_RELOADFILE|ファイルまたはプロジェクトを再ロードする必要があります。|
|SCC_E_FILENOTEXIST|ローカル ファイルが見つかりませんでした。|

## <a name="remarks"></a>Remarks
 通常`fOptions`は、ファイルごとに 1 つの`pfOptions``LONG`オプション指定を使用して、配列で置き換えられます。 これは、ファイルの種類がファイルごとに異なる可能性があるためです。

> [!NOTE]
> 同じファイルに対して`SCC_FILETYPE_TEXT`両方`SCC_FILETYPE_BINARY`のオプションとオプションを指定することは無効ですが、どちらも指定しないのは有効です。 どちらの設定も設定`SCC_FILETYPE_AUTO`と同じではありません。

 配列で使用されるフラグのリストを次`pfOptions`に示します。

|オプション|[値]|意味|
|------------|-----------|-------------|
|SCC_FILETYPE_AUTO|0x00|ソース管理プラグインは、ファイルの種類を検出する必要があります。|
|SCC_FILETYPE_TEXT|0x01|ASCII テキスト ファイルを示します。|
|SCC_FILETYPE_BINARY|0x02|ASCII テキスト以外のファイルの種類を示します。|
|SCC_ADD_STORELATEST|0x04|ファイルの最新のコピーのみを格納し、デルタは保存しません。|
|SCC_FILETYPE_TEXT_ANSI|0x08|ファイルを ANSI テキストとして扱います。|
|SCC_FILETYPE_UTF8|0x10|ファイルを UTF8 形式の Unicode テキストとして扱います。|
|SCC_FILETYPE_UTF16LE|0x20|ファイルを UTF16 リトル エンディアン形式の Unicode テキストとして扱います。|
|SCC_FILETYPE_UTF16BE|0x40|ファイルを UTF16 ビッグ エンディアン形式の Unicode テキストとして扱います。|

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)

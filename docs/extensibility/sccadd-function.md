---
title: SccAdd 関数 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
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
 pvContext

からソース管理プラグインのコンテキスト構造。

 hWnd

からソース管理プラグインが提供するすべてのダイアログボックスの親として使用できる IDE ウィンドウへのハンドル。

 nFiles

から配列に指定されている現在のプロジェクトに追加されるように選択されたファイルの数 `lpFileNames` 。

 lpFileNames 名

から追加するファイルの完全修飾ローカル名の配列。

 lpComment

から追加されるすべてのファイルに適用されるコメント。

 pfOptions

からファイルごとに提供されるコマンドフラグの配列。

 pvOptions

からソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|追加操作が正常に完了しました。|
|SCC_E_FILEALREADYEXISTS|選択されたファイルは既にソース管理下にあります。|
|SCC_E_TYPENOTSUPPORTED|ファイルの種類 (バイナリなど) は、ソース管理システムではサポートされていません。|
|SCC_E_OPNOTSUPPORTED|ソース管理システムでは、この操作はサポートされていません。|
|SCC_E_ACCESSFAILURE|ネットワークまたは競合の問題が原因で、ソース管理システムへのアクセスで問題が発生しました。 再試行することをお勧めします。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。追加は実行されません。|
|SCC_I_OPERATIONCANCELED|操作は完了前に取り消されました。|
|SCC_I_RELOADFILE|ファイルまたはプロジェクトを再度読み込む必要があります。|
|SCC_E_FILENOTEXIST|ローカルファイルが見つかりませんでした。|

## <a name="remarks"></a>注釈
 通常は、 `fOptions` ここでは配列で置き換えられ、 `pfOptions` ファイルごとに1つのオプションが指定され `LONG` ます。 これは、ファイルの種類がファイルによって異なる場合があるためです。

> [!NOTE]
> `SCC_FILETYPE_TEXT`同じファイルに対してオプションとオプションの両方を指定することはできません `SCC_FILETYPE_BINARY` が、どちらも指定することはできません。 どちらの設定も設定と同じです `SCC_FILETYPE_AUTO` 。この場合、ソース管理プラグインによってファイルの種類が自動検出されます。

 配列で使用されるフラグの一覧を次に示し `pfOptions` ます。

|オプション|値|説明|
|------------|-----------|-------------|
|SCC_FILETYPE_AUTO|0x00|ソース管理プラグインは、ファイルの種類を検出する必要があります。|
|SCC_FILETYPE_TEXT|0x01|ASCII テキストファイルを示します。|
|SCC_FILETYPE_BINARY|0x02|ASCII テキスト以外のファイルの種類を示します。|
|SCC_ADD_STORELATEST|0x04|ファイルの最新のコピーのみを格納し、デルタは格納しません。|
|SCC_FILETYPE_TEXT_ANSI|0x08|ファイルを ANSI テキストとして扱います。|
|SCC_FILETYPE_UTF8|0x10|ファイルを UTF8 形式の Unicode テキストとして扱います。|
|SCC_FILETYPE_UTF16LE|0x20|ファイルを、UTF16 リトルエンディアン形式で Unicode テキストとして扱います。|
|SCC_FILETYPE_UTF16BE|0x40|は、ファイルを UTF16 ビッグエンディアン形式の Unicode テキストとして扱います。|

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)

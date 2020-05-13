---
title: SccDiff 関数 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccDiff
helpviewer_keywords:
- SccDiff function
ms.assetid: d49bc8c5-f631-4153-9d3c-feb3564da305
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9b68df68ce7fa4ad5cbc98db256204ddf8623d2c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701023"
---
# <a name="sccdiff-function"></a>SccDiff 関数
この関数は、現在のファイル (ローカル ディスク上) とソース管理システムの最後にチェックインされたバージョンとの違いを表示します (または、オプションでチェックするだけです)。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccDiff(
   LPVOID    pvContext,
   HWND      hWnd,
   LPCSTR    lpFileName,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>パラメーター
 を行う

[in]ソース管理プラグインのコンテキスト構造。

 hWnd

[in]ソース管理プラグインが提供するダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 ファイル名

[in]差分が要求されるファイル名。

 f オプション

[in]コマンド フラグ。 詳細については、「解説」を参照してください。

 オプション

[in]ソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|作業コピーとサーバーのバージョンは同じです。|
|SCC_I_FILESDIFFERS|作業コピーは、ソース管理下のバージョンとは異なります。|
|SCC_I_RELOADFILE|ファイルまたはプロジェクトを再ロードする必要があります。|
|SCC_E_FILENOTCONTROLLED|ファイルはソース管理下にありません。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセスに問題が発生しました。 再試行することをお勧めします。|
|SCC_E_NONSPECIFICERROR|非特異的な障害;ファイルの差分は得られない。|
|SCC_E_FILENOTEXIST|ローカル ファイルが見つかりませんでした。|

## <a name="remarks"></a>Remarks
 この関数は、2 つの異なる目的を果たします。 既定では、ファイルに対する変更の一覧が表示されます。 ソース管理プラグインは、選択した形式で独自のウィンドウを開き、ディスク上のユーザーのファイルとソース管理下の最新バージョンのファイルの違いを表示します。

 または、IDE はファイルが変更されたかどうかを判断する必要がある場合もあります。 たとえば、IDE は、ユーザーに通知せずにファイルをチェックアウトしても安全かどうかを判断する必要があります。 その場合、IDE はフラグを`SCC_DIFF_CONTENTS`渡します。 ソース管理プラグインは、ソース管理されたファイルに対して、ディスク上のファイルをバイト単位でチェックし、ユーザーに何も表示せずに 2 つのファイルが異なるかどうかを示す値を返す必要があります。

 パフォーマンスの最適化として、ソース管理プラグインは、チェックサムまたはタイムスタンプに基づく代替を使用する可能性があります`SCC_DIFF_CONTENTS`。 すべてのソース管理システムがこれらの代替比較方法をサポートしているわけではないので、プラグインはコンテンツ比較にフォールバックする必要があります。 すべてのソース管理プラグインは、少なくともコンテンツ比較をサポートする必要があります。

> [!NOTE]
> クイック差分フラグは相互に排他的です。 フラグを渡さないことは有効ですが、同時に複数のフラグを渡しても無効です。 `SCC_DIFF_QUICK_DIFF`これは、すべてのフラグを結合するマスクで、テストに使用できますが、パラメーターとして渡す必要は決してありません。

|`fOption`|意味|
|---------------|-------------|
|SCC_DIFF_IGNORECASE|大文字と小文字を区別しない比較 (クイックまたは視覚的な違いのために使用できます)。|
|SCC_DIFF_IGNORESPACE|空白を無視します (クイックまたは視覚的な違いのために使用できます)。|
|SCC_DIFF_QD_CONTENTS|ファイルをバイト単位で暗黙的に比較します。|
|SCC_DIFF_QD_CHECKSUM|サポートされている場合は、チェックサムを使用してファイルを暗黙的に比較します。 サポートされていない場合は、内容の比較にフォールバックします。|
|SCC_DIFF_QD_TIME|サポートされている場合は、タイムスタンプを使用してファイルを暗黙的に比較します。 サポートされていない場合は、内容の比較にフォールバックします。|

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)

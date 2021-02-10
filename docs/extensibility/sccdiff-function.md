---
title: SccDiff 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccDiff
helpviewer_keywords:
- SccDiff function
ms.assetid: d49bc8c5-f631-4153-9d3c-feb3564da305
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8ff2b2d5e5a0043cde17fecd2d59c084d2958e32
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99943115"
---
# <a name="sccdiff-function"></a>SccDiff 関数
この関数は、ソース管理システムで現在のファイル (ローカルディスク上) と最後にチェックインされたバージョンとの相違点を表示します (または、必要に応じて確認するだけです)。

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
 pvContext

からソース管理プラグインのコンテキスト構造。

 hWnd

からソース管理プラグインが提供するすべてのダイアログボックスの親として使用できる IDE ウィンドウへのハンドル。

 lpFileName

から差分が要求されるファイルの名前。

 限ら

からコマンドフラグ。 詳細については、「解説」を参照してください。

 pvOptions

からソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|作業コピーとサーバーのバージョンが同じです。|
|SCC_I_FILESDIFFERS|作業コピーは、ソース管理下のバージョンとは異なります。|
|SCC_I_RELOADFILE|ファイルまたはプロジェクトを再度読み込む必要があります。|
|SCC_E_FILENOTCONTROLLED|ファイルがソース管理下にありません。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_E_ACCESSFAILURE|ネットワークまたは競合の問題が原因で、ソース管理システムへのアクセスで問題が発生しました。 再試行することをお勧めします。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。ファイルの差は取得されませんでした。|
|SCC_E_FILENOTEXIST|ローカルファイルが見つかりませんでした。|

## <a name="remarks"></a>解説
 この関数は、2つの異なる目的で機能します。 既定では、ファイルに対する変更の一覧が表示されます。 ソース管理プラグインは、選択した形式で独自のウィンドウを開き、ユーザーのディスク上のファイルと、ソース管理下の最新バージョンのファイルとの違いを表示します。

 また、IDE では、ファイルが変更されたかどうかを判断するだけで済む場合もあります。 たとえば、IDE では、ユーザーに通知することなくファイルをチェックアウトしても安全かどうかを判断する必要がある場合があります。 その場合は、IDE によってフラグが渡され `SCC_DIFF_CONTENTS` ます。 ソース管理プラグインは、ソース管理されたファイルに対して、ディスク上のファイルをバイト単位でチェックし、ユーザーに何も表示しないで2つのファイルが異なっているかどうかを示す値を返す必要があります。

 パフォーマンスを最適化するため、ソース管理プラグインは、チェックサムまたはタイムスタンプに基づく別のを使用することがあります。これは、によって呼び出されるバイト単位の比較ではなく、 `SCC_DIFF_CONTENTS` 明らかに高速ですが、信頼性は低くなります。 すべてのソース管理システムでこれらの代替の比較方法がサポートされるとは限りません。また、プラグインがコンテンツの比較にフォールバックする必要がある場合があります。 すべてのソース管理プラグインは、少なくともコンテンツの比較をサポートしている必要があります。

> [!NOTE]
> クイック差分フラグは相互に排他的です。 フラグを渡すことは有効ですが、複数のを同時に渡すことはできません。 `SCC_DIFF_QUICK_DIFF`は、すべてのフラグを組み合わせたマスクであり、テストに使用できますが、パラメーターとして渡すことはできません。

|`fOption`|意味|
|---------------|-------------|
|SCC_DIFF_IGNORECASE|大文字と小文字を区別しない比較 (クイックまたはビジュアルの違いに使用できます)。|
|SCC_DIFF_IGNORESPACE|空白は無視されます (クイックまたはビジュアルの違いに使用される場合があります)。|
|SCC_DIFF_QD_CONTENTS|ファイルをバイト単位で自動的に比較します。|
|SCC_DIFF_QD_CHECKSUM|サポートされている場合は、チェックサムを使用してファイルをサイレントに比較します。 サポートされていない場合は、内容の比較にフォールバックします。|
|SCC_DIFF_QD_TIME|サポートされている場合は、タイムスタンプを使用してファイルを自動的に比較します。 サポートされていない場合は、内容の比較にフォールバックします。|

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)

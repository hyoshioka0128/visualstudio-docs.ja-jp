---
title: SccHistory 関数 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccHistory
helpviewer_keywords:
- SccHistory function
ms.assetid: a636d9d3-47c1-4b48-ac6b-bcfde19d6cf9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 734afefd97e61867076d487acbcf67f10f54e672
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700658"
---
# <a name="scchistory-function"></a>SccHistory 関数
この関数は、指定したファイルの履歴を表示します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccHistory(
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

#### <a name="parameters"></a>パラメーター
 `pvContext`

[in]ソース管理プラグインのコンテキスト構造。

 `hWnd`

[in]ソース管理プラグインが提供するダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 `nFiles`

[in]配列に指定されたファイルの`lpFileName`数。

 `lpFileName`

[in]ファイルの完全修飾名の配列。

 `fOptions`

[in]コマンド フラグ (現在は使用されていません)。

 `pvOptions`

[in]ソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|バージョン履歴が正常に取得されました。|
|SCC_I_RELOADFILE|ソース管理システムは、履歴を取得する際にディスク上のファイルを実際に変更するため (古いバージョンを取得するなど)、IDE はこのファイルを再読み込みする必要があります。|
|SCC_E_FILENOTCONTROLLED|ファイルはソース管理下にありません。|
|SCC_E_OPNOTSUPPORTED|ソース管理システムはこの操作をサポートしていません。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセスに問題が発生しました。 再試行することをお勧めします。|
|SCC_E_PROJNOTOPEN|プロジェクトは開かれていない。|
|SCC_E_NONSPECIFICERROR|非特異的なエラー。 ファイル履歴を取得できませんでした。|

## <a name="remarks"></a>Remarks
 ソース管理プラグインは、親ウィンドウとして使用`hWnd`して、各ファイルの履歴を表示する独自のダイアログ ボックスを表示できます。 または[、SccOpenProject](../extensibility/sccopenproject-function.md)に提供されるオプションのテキスト出力コールバック関数を使用することもできます (サポートされている場合)。

 特定の状況下では、この呼び出しの実行中に、検査中のファイルが変更される可能性があることに注意してください。 たとえば、history[!INCLUDE[vsvss](../extensibility/includes/vsvss_md.md)]コマンドを使用すると、古いバージョンのファイルを取得できます。 このような場合、ソース管理プラグインは、ファイルを再読`SCC_I_RELOAD`み込みする必要があることを IDE に警告するために戻ります。

> [!NOTE]
> ソース管理プラグインがファイルの配列に対してこの機能をサポートしていない場合は、最初のファイルのファイル履歴のみを表示できます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)

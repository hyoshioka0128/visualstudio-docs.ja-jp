---
title: SccDirDiff 関数 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccDirDiff
helpviewer_keywords:
- SccDirDiff function
ms.assetid: 26c9ba92-e3b9-4dd2-bd5e-76b17745e308
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1bb592a1174a91480ed76ef818733c288c5273c0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701012"
---
# <a name="sccdirdiff-function"></a>関数
この関数は、クライアント ディスク上の現在のローカル ディレクトリと、ソース管理下の対応するプロジェクトとの相違点を表示します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccDirDiff(
   LPVOID    pContext,
   HWND      hWnd,
   LPCSTR    lpDirName,
   LONG      dwFlags,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>パラメーター
 pContext

[in]ソース管理プラグインのコンテキスト構造。

 hWnd

[in]ソース管理プラグインが提供するダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 名前

[in]視覚的な違いを示すローカル ディレクトリへの完全修飾パス。

 dwFlags

[in]コマンド フラグ (解説セクションを参照)。

 オプション

[in]ソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|ディスク上のディレクトリは、ソース コード管理のプロジェクトと同じです。|
|SCC_I_FILESDIFFER|ディスク上のディレクトリがソース コード管理のプロジェクトと異なります。|
|SCC_I_RELOADFILE|ファイルまたはプロジェクトを再ロードする必要があります。|
|SCC_E_FILENOTCONTROLLED|ディレクトリがソース コード管理下にありません。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセスに問題が発生しました。 再試行することをお勧めします。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特異的なエラー。|
|SCC_E_FILENOTEXIST|ローカル ディレクトリが見つかりませんでした。|

## <a name="remarks"></a>Remarks
 この関数は、ソース管理プラグインに対して、指定したディレクトリに対する変更の一覧をユーザーに表示するように指示するために使用します。 プラグインは、ディスク上のユーザーのディレクトリとバージョン管理下の対応するプロジェクトの違いを表示するために、独自のウィンドウを選択した形式で開きます。

 プラグインがディレクトリの比較をまったくサポートしている場合、"quick-diff" オプションがサポートされていない場合でも、ファイル名ベースでのディレクトリ比較をサポートする必要があります。

|`dwFlags`|解釈|
|---------------|--------------------|
|SCC_DIFF_IGNORECASE|大文字と小文字を区別しない比較 (クイック差分またはビジュアルのどちらにも使用できます)。|
|SCC_DIFF_IGNORESPACE|空白を無視します (クイック差分またはビジュアルに使用できます)。|
|SCC_DIFF_QD_CONTENTS|ソース管理プラグインでサポートされている場合は、ディレクトリをバイト単位で暗黙的に比較します。|
|SCC_DIFF_QD_CHECKSUM|プラグインでサポートされている場合は、チェックサムを使用してディレクトリを暗黙的に比較するか、サポートされていない場合はSCC_DIFF_QD_CONTENTSにフォールバックします。|
|SCC_DIFF_QD_TIME|プラグインでサポートされている場合は、タイムスタンプを使用してディレクトリを暗黙的に比較するか、またはサポートされていない場合は、SCC_DIFF_QD_CHECKSUMまたはSCC_DIFF_QD_CONTENTSにフォールバックします。|

> [!NOTE]
> この関数は[、SccDiff](../extensibility/sccdiff-function.md)と同じコマンド フラグを使用します。 ただし、ソース管理プラグインは、ディレクトリの"クイック差分"操作をサポートしないことを選択する場合があります。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)

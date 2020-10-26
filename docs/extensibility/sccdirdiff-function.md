---
title: SccDirDiff 関数 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80701012"
---
# <a name="sccdirdiff-function"></a>SccDirDiff 関数
この関数は、クライアントディスク上の現在のローカルディレクトリと、ソース管理下にある対応するプロジェクトの相違点を表示します。

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

からソース管理プラグインのコンテキスト構造。

 hWnd

からソース管理プラグインが提供するすべてのダイアログボックスの親として使用できる IDE ウィンドウへのハンドル。

 lpDirName

から視覚的な相違点を表示するローカルディレクトリへの完全修飾パス。

 dwFlags

からコマンドフラグ (「解説」を参照してください)。

 pvOptions

からソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|ディスク上のディレクトリは、ソースコード管理のプロジェクトと同じです。|
|SCC_I_FILESDIFFER|ディスク上のディレクトリが、ソースコード管理のプロジェクトと異なります。|
|SCC_I_RELOADFILE|ファイルまたはプロジェクトを再度読み込む必要があります。|
|SCC_E_FILENOTCONTROLLED|ディレクトリがソースコード管理下にありません。|
|SCC_E_NOTAUTHORIZED|ユーザーはこの操作を実行できません。|
|SCC_E_ACCESSFAILURE|ネットワークまたは競合の問題が原因で、ソース管理システムへのアクセスで問題が発生しました。 再試行することをお勧めします。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|不特定のエラーです。|
|SCC_E_FILENOTEXIST|ローカルディレクトリが見つかりませんでした。|

## <a name="remarks"></a>注釈
 この関数は、指定されたディレクトリに対する変更の一覧をユーザーに表示するようにソース管理プラグインに指示するために使用されます。 プラグインによって、独自のウィンドウが選択された形式で開き、ディスク上のユーザーのディレクトリとバージョン管理下の対応するプロジェクトの違いが表示されます。

 プラグインがディレクトリの比較をサポートしている場合は、[クイック差分] オプションがサポートされていない場合でも、ファイル名に基づいたディレクトリの比較をサポートする必要があります。

|`dwFlags`|解釈|
|---------------|--------------------|
|SCC_DIFF_IGNORECASE|大文字と小文字を区別しない比較 (クイック diff またはビジュアルのいずれかに使用できます)。|
|SCC_DIFF_IGNORESPACE|空白文字は無視されます (クイック diff またはビジュアルに使用できます)。|
|SCC_DIFF_QD_CONTENTS|ソース管理プラグインによってサポートされている場合は、ディレクトリをバイト単位で自動的に比較します。|
|SCC_DIFF_QD_CHECKSUM|プラグインでサポートされている場合、チェックサムを使用してディレクトリをサイレントに比較します。サポートされていない場合は、SCC_DIFF_QD_CONTENTS にフォールバックします。|
|SCC_DIFF_QD_TIME|プラグインによってサポートされている場合、は、そのタイムスタンプを使用してディレクトリをサイレントに比較します。サポートされていない場合は、SCC_DIFF_QD_CHECKSUM または SCC_DIFF_QD_CONTENTS にフォールバックします。|

> [!NOTE]
> この関数では、 [Sccdiff](../extensibility/sccdiff-function.md)と同じコマンドフラグが使用されます。 ただし、ソース管理プラグインは、ディレクトリの "クイック差分" 操作をサポートしないことを選択する場合があります。

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)

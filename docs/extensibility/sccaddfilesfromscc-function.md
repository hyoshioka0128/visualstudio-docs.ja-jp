---
title: 関数の中 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccAddFilesFromSCC
helpviewer_keywords:
- SccAddFilesFromSCC function
ms.assetid: f21a3500-ade8-4dd8-8647-10e2179be9c1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1d22527644edbf1697112f5cf8b73b8a3f72b774
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701284"
---
# <a name="sccaddfilesfromscc-function"></a>関数の一覧
この関数は、ソース管理から現在開いているプロジェクトにファイルのリストを追加します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccAddFilesFromSCC(
   LPVOID  pContext,
   HWND    hWnd,
   LPSTR   lpUser,
   LPSTR   lpAuxProjPath,
   LONG    cFiles,
   LPCSTR* lpFilePaths,
   LPCSTR  lpDestination,
   LPCSTR  lpComment,
   LPBOOL  pbResults
);
```

### <a name="parameters"></a>パラメーター
 pContext

[in]ソース管理プラグイン のコンテキスト ポインター。

 hWnd

[in]ソース管理プラグインが提供するダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 ユーザー数を指定します。

[イン、アウト]ユーザー名 (null 終端文字を含むSCC_USER_SIZEまで)。

 プロウプロイパス

[イン、アウト]プロジェクトを識別する補助文字列`SCC_PRJPATH_`(NULL 終端文字を含む SIZE まで)。

 ファイル

[in]によって`lpFilePaths`与えられたファイルの数。

 パス

[イン、アウト]現在のプロジェクトに追加するファイル名の配列。

 lpデスティネーション

[in]ファイルが書き込まれる宛先パス。

 ル・コメント

[in]追加する各ファイルに適用するコメント。

 結果

[イン、アウト]各ファイルの成功 (ゼロまたは TRUE 以外) または失敗 (ゼロまたは FALSE) を示すように設定されているフラグの配列 (`cFiles`配列のサイズは少なくとも長くなければなりません)。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返します。

|[値]|説明|
|-----------|-----------------|
|SCC_E_PROJNOTOPEN|プロジェクトが開かれていない。|
|SCC_E_OPNOTPERFORMED|次の指定と同じプロジェクトへの接続ではありません。`lpAuxProjPath.`|
|SCC_E_NOTAUTHORIZED|ユーザーはデータベースの更新を許可されていません。|
|SCC_E_NONSPECIFICERROR|不明なエラー。|
|SCC_I_RELOADFILE|ファイルまたはプロジェクトを再ロードする必要があります。|

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)

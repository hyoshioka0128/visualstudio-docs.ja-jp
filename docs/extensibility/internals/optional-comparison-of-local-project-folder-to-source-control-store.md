---
title: プロジェクト フォルダとソース管理ストアの比較 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, comparing versions
- source control plug-ins, local project folders
ms.assetid: 65217e8b-15a6-4446-92b0-4cff1c6220f5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: facb3b656e0ac50b50fdb0291307aa2fe98b1df4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706866"
---
# <a name="optional-comparison-of-local-project-folder-to-source-control-store"></a>ソース管理ストアとローカルのプロジェクト フォルダーとの比較 (オプション)
ソース管理プラグイン API 1.2 では、ローカル プロジェクト フォルダーとソース管理の比較は、関数[SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)と[SccDirDiff](../../extensibility/sccdirdiff-function.md)を使用して行われます。

 **ソリューション エクスプローラー**内で、個々のファイルではなくフォルダーが選択されている場合 **、ソース管理**プラグインの新しい[SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)と[SccDirDiff](../../extensibility/sccdirdiff-function.md)のショートカット メニューが呼び出されます。

## <a name="new-capability-flags"></a>新しい機能フラグ
 `SCC_CAP_DIRECTORYDIFF`

 `SCC_CAP_DIRECTORYCHECKOUT`

## <a name="new-functions"></a>新しい関数
- [SccDirDiff](../../extensibility/sccdirdiff-function.md)

- [SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)

 この`SccDirQueryInfo`関数は、作業`SccDirDiff`ディレクトリがソース管理されているかどうかを判断するために前に呼び出されます。 この`SccDirDiff`関数は、現在のローカル ディレクトリと対応するソース管理フォルダの違いを表示します。 このコマンドは、ソース管理プラグインにディレクトリへの変更の一覧を表示するように要求します。 ソース管理プラグインは、相違点を表示する独自の UI を提供します。

> [!NOTE]
> この関数は[、SccDiff](../../extensibility/sccdiff-function.md)と同じコマンド フラグを使用します。 ソース管理プラグイン プロバイダーとして、ディレクトリの "簡易差分" 操作をサポートしないように選択できます。

## <a name="see-also"></a>関連項目
- [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)

---
title: プロジェクトフォルダーをソース管理ストアに比較する |Microsoft Docs
description: ソース管理プラグイン API では、ローカルのプロジェクトフォルダーとソース管理の比較は SccDirQueryInfo と SccDirDiff を使用して実現されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, comparing versions
- source control plug-ins, local project folders
ms.assetid: 65217e8b-15a6-4446-92b0-4cff1c6220f5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f7b334bb6e1b73dd31060020378e91b74e5af102
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063046"
---
# <a name="optional-comparison-of-local-project-folder-to-source-control-store"></a>ソース管理ストアとローカルのプロジェクト フォルダーとの比較 (オプション)
ソース管理プラグイン API 1.2 では、ローカルのプロジェクトフォルダーとソース管理を比較するには、関数 [Sccdirqueryinfo](../../extensibility/sccdirqueryinfo-function.md) と [Sccdirdiff](../../extensibility/sccdirdiff-function.md)を使用します。

 **ソリューションエクスプローラー** 内では、個々のファイルではなくフォルダーを選択すると、[**バージョンの比較**] ショートカットメニューによって、ソース管理プラグインの新しい [sccdirqueryinfo](../../extensibility/sccdirqueryinfo-function.md)と [sccdirdiff](../../extensibility/sccdirdiff-function.md)が呼び出されます。

## <a name="new-capability-flags"></a>新しい機能フラグ
 `SCC_CAP_DIRECTORYDIFF`

 `SCC_CAP_DIRECTORYCHECKOUT`

## <a name="new-functions"></a>新しい関数
- [SccDirDiff](../../extensibility/sccdirdiff-function.md)

- [SccDirQueryInfo](../../extensibility/sccdirqueryinfo-function.md)

 関数は、 `SccDirQueryInfo` `SccDirDiff` 作業ディレクトリがソース管理されているかどうかを判断する前に呼び出されます。 関数は、 `SccDirDiff` 現在のローカルディレクトリとそれに対応するソース管理フォルダーとの違いを表示します。 このコマンドは、ソース管理プラグインに対して、ディレクトリへの変更の一覧を表示するように要求します。 ソース管理プラグインには、違いを表示するための独自の UI が用意されています。

> [!NOTE]
> この関数は、 [Sccdiff](../../extensibility/sccdiff-function.md)と同じコマンドフラグを使用します。 ソース管理プラグインプロバイダーは、ディレクトリの "クイック diff" 操作をサポートしないことを選択できます。

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグイン API バージョン 1.2 の新機能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)

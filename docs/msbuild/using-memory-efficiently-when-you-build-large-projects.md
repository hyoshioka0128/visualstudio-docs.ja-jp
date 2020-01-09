---
title: 大規模なプロジェクトのビルドにおけるメモリの効率的な使用 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- memory use (MSBuild)
- msbuild, efficient memory use building large trees
- caching (MSBuild)
ms.assetid: 853a21ed-69f7-4817-af00-57f73e2c74b5
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: af61c15c8ef65c062c1aab6eba079c613f99b5f8
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75595230"
---
# <a name="use-memory-efficiently-when-you-build-large-projects"></a>大規模なプロジェクトのビルドにおけるメモリの効率的な使用
大規模プロジェクトには、多くの場合、サブプロジェクトやその他の依存関係が含まれています。それらがビルド時に大量のシステム メモリを使うことがあります。 利用できるシステム メモリが少なくなると、システム パフォーマンスが落ちることもあります。 古いバージョンの [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] プロジェクトはメモリに残っていました。 バージョン 3.5 では、古いバージョンのプロジェクトは削除されましたが、ビルド結果は後で取得するためにキャッシュ内に保持されていました。

 バージョン 4.0 では、このメモリ管理が自動的に処理されます。`UnloadProjectsOnCompletion` や `UseResultsCache` のようなプロパティをプロジェクトで使用する必要がありません。

### <a name="see-also"></a>関連項目
- [複数プロジェクトの並行ビルド](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)

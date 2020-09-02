---
title: 大規模なプロジェクトのビルドにおけるメモリの効率的な使用 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- memory use (MSBuild)
- msbuild, efficient memory use building large trees
- caching (MSBuild)
ms.assetid: 853a21ed-69f7-4817-af00-57f73e2c74b5
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 28d9f3d43faa53731b101dfdf58fe1e68a0920c5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68178294"
---
# <a name="using-memory-efficiently-when-you-build-large-projects"></a>大規模なプロジェクトのビルドにおけるメモリの効率的な使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

大規模プロジェクトには、多くの場合、サブプロジェクトやその他の依存関係が含まれています。それらがビルド時に大量のシステム メモリを使うことがあります。 利用できるシステム メモリが少なくなると、システム パフォーマンスが落ちることもあります。 旧バージョンの [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクトがメモリに残ったか、バージョン 3.5 でプロジェクトが削除されましたが、後の取得のためにキャッシュにビルド結果が維持されました。  
  
 バージョン 4.0 では、このメモリ管理が自動的に処理されます。`UnloadProjectsOnCompletion` や `UseResultsCache` のようなプロパティをプロジェクトで使用する必要がありません。  
  
## <a name="see-also"></a>参照  
 [複数のプロジェクトの並行ビルド](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)

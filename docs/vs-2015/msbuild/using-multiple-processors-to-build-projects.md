---
title: 複数のプロセッサを使用したプロジェクトのビルド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- multiple processors
- MSBuild, multiple processor systems
ms.assetid: 49fa36c9-8e14-44f5-8a2b-34146cf6807b
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3a590d3dc3053c5b857917dc358e32a2c7d5247c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68192856"
---
# <a name="using-multiple-processors-to-build-projects"></a>複数のプロセッサを使用したプロジェクトのビルド
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

MSBuild では、複数のプロセッサまたはマルチコア プロセッサを搭載したシステムを使用できます。 プロセッサごとに個別のビルド プロセスが作成されます。 たとえば、4 つのプロセッサを搭載したシステムでは、4 つのビルド プロセスが作成されます。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] では、これらのビルドを同時に処理できるため、全体的なビルド時間が短縮されます。 ただし、並行ビルドでは、ビルド処理が行われる方法がいくつかの点で通常とは異なります。 このトピックでは、それらの相違点について説明します。  
  
## <a name="project-to-project-references"></a>プロジェクト間参照  
 [!INCLUDE[vstecmsbuildengine](../includes/vstecmsbuildengine-md.md)] が並行ビルドによってプロジェクトをビルドしているときにプロジェクト間 (P2P) 参照を検出した場合は、その参照を 1 回のみビルドします。 2 つのプロジェクトに同じ P2P 参照がある場合、その参照はプロジェクトごとに再ビルドされません。 ビルド エンジンが同じ P2P 参照をそれに依存する両方のプロジェクトに返します。 それ以降にセッション内で同じターゲットが要求された場合は、同じ P2P 参照が返されます。  
  
## <a name="cycle-detection"></a>サイクルの検出  
 サイクルの検出は [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 2.0 の場合と同じように機能します。ただし、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] には現在、サイクルの検出を別の時点またはビルド時に報告する機能が追加されています。  
  
## <a name="errors-and-exceptions-during-parallel-builds"></a>並行ビルド中のエラーと例外  
 並行ビルドでは、通常のビルドとは異なる時点でエラーや例外が発生することがあり、あるプロジェクトのビルドが失敗した場合でも他のプロジェクトのビルドは続行されます。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] では、同時に実行されているプロジェクトのビルドのいずれかが失敗しても、他のビルドが停止されることはありません。 他のプロジェクトのビルドは、成功または失敗するまで続行されます。 ただし、<xref:Microsoft.Build.Framework.IBuildEngine.ContinueOnError%2A> が有効である場合は、エラーが発生したビルドも停止しません。  
  
## <a name="visual-c-project-vcproj-and-solution-sln-files"></a>Visual C++ のプロジェクト ファイル (.vcproj) とソリューション ファイル (.sln)  
 [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] のプロジェクト ファイル (.vcproj) とソリューション ファイル (.sln) は、どちらも [MSBuild タスク](../msbuild/msbuild-task.md)に渡すことができます。 [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] プロジェクトでは、VCWrapperProject が呼び出され、内部 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクトが作成されます。 [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] ソリューションについては、SolutionWrapperProject が作成され、次に内部 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクトが作成されます。 いずれの場合も、生成されるプロジェクトは他の [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクトと同じように扱われます。  
  
## <a name="multi-process-execution"></a>マルチプロセス実行  
 ビルドに関連するほとんどの操作では、パス関連のエラーを回避するために、ビルド プロセスの全体をとおして現在のディレクトリが変わらないことが必要です。 そのため、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] では、スレッドごとにディレクトリが作成される可能性があるため、複数のスレッドでプロジェクトを実行することはできません。  
  
 この問題を回避し、マルチプロセッサによるビルドを可能にするために、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] では "プロセス分離" が使用されます。 プロセス分離によって、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] は最大 `n` のプロセスを作成できます。`n` はシステムで利用可能なプロセッサの数です。 たとえば、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] が 2 つのプロセッサを搭載したシステムでソリューションをビルドする場合は、2 つのビルド プロセスのみ作成されます。 これらのプロセスは、ソリューションに含まれるすべてのプロジェクトのビルドに再利用されます。  
  
## <a name="see-also"></a>参照  
 [複数のプロジェクトの並行ビルド](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)   
 [タスク](../msbuild/msbuild-tasks.md)

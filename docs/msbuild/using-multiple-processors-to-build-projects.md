---
title: 複数のプロセッサを使用したプロジェクトのビルド | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- multiple processors
- MSBuild, multiple processor systems
ms.assetid: 49fa36c9-8e14-44f5-8a2b-34146cf6807b
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bd377318d92989f7e1341d166b2ca3d3978a148d
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75595242"
---
# <a name="use-multiple-processors-to-build-projects"></a>複数のプロセッサを使用したプロジェクトのビルド
MSBuild では、複数のプロセッサまたはマルチコア プロセッサを搭載したシステムを使用できます。 プロセッサごとに個別のビルド プロセスが作成されます。 たとえば、4 つのプロセッサを搭載したシステムでは、4 つのビルド プロセスが作成されます。 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] では、これらのビルドを同時に処理できるため、全体的なビルド時間が短縮されます。 ただし、並行ビルドでは、ビルド処理が行われる方法がいくつかの点で通常とは異なります。 このトピックでは、それらの相違点について説明します。

## <a name="project-to-project-references"></a>プロジェクト間参照
 [!INCLUDE[vstecmsbuildengine](../msbuild/includes/vstecmsbuildengine_md.md)] が並行ビルドによってプロジェクトをビルドしているときにプロジェクト間 (P2P) 参照を検出した場合は、その参照を 1 回のみビルドします。 2 つのプロジェクトに同じ P2P 参照がある場合、その参照はプロジェクトごとに再ビルドされません。 ビルド エンジンが同じ P2P 参照をそれに依存する両方のプロジェクトに返します。 それ以降にセッション内で同じターゲットが要求された場合は、同じ P2P 参照が返されます。

## <a name="cycle-detection"></a>サイクルの検出
 サイクルの検出は [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 2.0 の場合と同じように機能します。ただし、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] には現在、サイクルの検出を別の時点またはビルド時に報告する機能が追加されています。

## <a name="errors-and-exceptions-during-parallel-builds"></a>並行ビルド中のエラーと例外
 並行ビルドでは、通常のビルドとは異なる時点でエラーや例外が発生することがあり、あるプロジェクトのビルドが失敗した場合でも他のプロジェクトのビルドは続行されます。 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] では、同時に実行されているプロジェクトのビルドのいずれかが失敗しても、他のビルドが停止されることはありません。 他のプロジェクトのビルドは、成功または失敗するまで続行されます。 ただし、<xref:Microsoft.Build.Framework.IBuildEngine.ContinueOnError%2A> が有効である場合は、エラーが発生したビルドも停止しません。

## <a name="c-project-vcxproj-and-solution-sln-files"></a>C++ のプロジェクト ファイル (.vcxproj) とソリューション ファイル (.sln)
 [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] のプロジェクト ファイル ( *.vcxproj*) とソリューション ファイル ( *.sln*) は、どちらも [MSBuild タスク](../msbuild/msbuild-task.md)に渡すことができます。 [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] プロジェクトでは、VCWrapperProject が呼び出され、内部 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] プロジェクトが作成されます。 [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] ソリューションについては、SolutionWrapperProject が作成され、次に内部 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] プロジェクトが作成されます。 いずれの場合も、生成されるプロジェクトは他の [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] プロジェクトと同じように扱われます。

## <a name="multi-process-execution"></a>マルチプロセス実行
 ビルドに関連するほとんどの操作では、パス関連のエラーを回避するために、ビルド プロセスの全体をとおして現在のディレクトリが変わらないことが必要です。 そのため、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] では、スレッドごとにディレクトリが作成される可能性があるため、複数のスレッドでプロジェクトを実行することはできません。

 この問題を回避し、マルチプロセッサによるビルドを可能にするために、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] では "プロセス分離" が使用されます。 プロセス分離によって、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] は最大 `n` のプロセスを作成できます。`n` はシステムで利用可能なプロセッサの数です。 たとえば、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] が 2 つのプロセッサを搭載したシステムでソリューションをビルドする場合は、2 つのビルド プロセスのみ作成されます。 これらのプロセスは、ソリューションに含まれるすべてのプロジェクトのビルドに再利用されます。

## <a name="see-also"></a>関連項目
- [複数プロジェクトの並行ビルド](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)
- [タスク](../msbuild/msbuild-tasks.md)

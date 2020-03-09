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
ms.openlocfilehash: f5dc62112324f7ad19c47b346ac8c1e3f86570b0
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/26/2020
ms.locfileid: "77631303"
---
# <a name="use-multiple-processors-to-build-projects"></a>複数のプロセッサを使用したプロジェクトのビルド

MSBuild では、複数のプロセッサまたはマルチコア プロセッサを搭載したシステムを使用できます。 プロセッサごとに個別のビルド プロセスが作成されます。 たとえば、4 つのプロセッサを搭載したシステムでは、4 つのビルド プロセスが作成されます。 MSBuild では、これらのビルドを同時に処理できるため、全体的なビルド時間が短縮されます。 ただし、並行ビルドでは、ビルド処理が行われる方法がいくつかの点で通常とは異なります。 このトピックでは、それらの相違点について説明します。

## <a name="project-to-project-references"></a>プロジェクト間参照

 Microsoft Build Engine で、並行ビルドを使用してプロジェクトをビルドしているときにプロジェクト間 (P2P) 参照が検出された場合、その参照は一度だけビルドされます。 2 つのプロジェクトに同じ P2P 参照がある場合、その参照はプロジェクトごとに再ビルドされません。 ビルド エンジンが同じ P2P 参照をそれに依存する両方のプロジェクトに返します。 それ以降にセッション内で同じターゲットが要求された場合は、同じ P2P 参照が返されます。

## <a name="cycle-detection"></a>サイクルの検出

 サイクルの検出は MSBuild 2.0 の場合と同じように機能します。ただし、現在の MSBuild では、別の時点またはビルド時にサイクルの検出を報告できます。

## <a name="errors-and-exceptions-during-parallel-builds"></a>並行ビルド中のエラーと例外

 並行ビルドでは、通常のビルドとは異なる時点でエラーや例外が発生することがあり、あるプロジェクトのビルドが失敗した場合でも他のプロジェクトのビルドは続行されます。 MSBuild では、失敗したプロジェクトのビルドと並行して実行されているビルドが停止されることはありません。 他のプロジェクトのビルドは、成功または失敗するまで続行されます。 ただし、<xref:Microsoft.Build.Framework.IBuildEngine.ContinueOnError%2A> が有効である場合は、エラーが発生したビルドも停止しません。

## <a name="c-project-vcxproj-and-solution-sln-files"></a>C++ のプロジェクト ファイル (.vcxproj) とソリューション ファイル (.sln)

 C++ のプロジェクト ファイル ( *.vcxproj*) とソリューション ファイル ( *.sln*) は、どちらも [MSBuild タスク](../msbuild/msbuild-task.md)に渡すことができます。 C++ プロジェクトでは、VCWrapperProject が呼び出された後、内部 MSBuild プロジェクトが作成されます。 C++ ソリューションについては、SolutionWrapperProject が作成された後、内部 MSBuild プロジェクトが作成されます。 いずれの場合も、生成されるプロジェクトは他の MSBuild プロジェクトと同じように扱われます。

## <a name="multi-process-execution"></a>マルチプロセス実行

 ビルドに関連するほとんどの操作では、パス関連のエラーを回避するために、ビルド プロセスの全体をとおして現在のディレクトリが変わらないことが必要です。 そのため、MSBuild では、異なるスレッドでプロジェクトを実行することはできません。それによって複数のディレクトリが作成される可能性があるためです。

 この問題を回避しつつマルチプロセッサによるビルドを可能にするために、MSBuild では "プロセス分離" が使用されます。 プロセス分離によって、MSBuild では最大 `n` 個のプロセスを作成できます。`n` はシステムで利用可能なプロセッサの数です。 たとえば、2 つのプロセッサを搭載したシステム上で MSBuild によってソリューションがビルドされる場合、2 つのビルド プロセスだけが作成されます。 これらのプロセスは、ソリューションに含まれるすべてのプロジェクトのビルドに再利用されます。

## <a name="see-also"></a>関連項目

- [複数プロジェクトの並行ビルド](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)
- [タスク](../msbuild/msbuild-tasks.md)

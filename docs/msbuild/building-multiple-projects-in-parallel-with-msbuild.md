---
title: MSBuild での複数のプロジェクトの並行ビルド | Microsoft Docs
description: 複数のプロジェクトのビルドを並列に実行することによって高速化するために使用できる MSBuild 設定について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- parallel project builds
- building multiple projects in parallel
- msbuild, building projects in parallel
ms.assetid: c8c9aadc-33ad-4aa1-b07d-b879e9eabda0
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b91bca1fb1e8866e4f0c9b5a68140f7a7ae892f2
ms.sourcegitcommit: d3bca34f82de03fa34ecdd72233676c17fb3cb14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92353240"
---
# <a name="build-multiple-projects-in-parallel-with-msbuild"></a>MSBuild で複数のプロジェクトを並行ビルドする

MSBuild では、複数のプロジェクトを並列に実行することによって、これらのプロジェクトをより速くビルドすることができます。 ビルドを並列で実行するには、マルチコア コンピューターまたはマルチプロセッサ コンピューターで次の設定を使用します。

- `-maxcpucount` スイッチをコマンド プロンプトで使用します。

- <xref:Microsoft.Build.Tasks.MSBuild.BuildInParallel%2A> タスク パラメーターを MSBuild タスクで使用します。

> [!NOTE]
> コマンド ラインで **-verbosity** ( **-v** ) スイッチを使うと、ビルドのパフォーマンスが影響を受ける場合があります。 ビルド ログ情報の詳細レベルが、トラブルシューティングで使用するために "詳細" または "診断" に設定されている場合、ビルドのパフォーマンスが低下する可能性があります。 詳しくは、「[ビルド ログの取得](../msbuild/obtaining-build-logs-with-msbuild.md)」と「[コマンド ライン リファレンス](../msbuild/msbuild-command-line-reference.md)」をご覧ください。

## <a name="-maxcpucount-switch"></a>-maxcpucount スイッチ

`-maxcpucount` スイッチ (省略形は `-m`) を使用すると、MSBuild では、並列実行される可能性がある *MSBuild.exe* プロセスを指定された数だけ作成できます。 これらのプロセスは、"ワーカー プロセス" とも呼ばれます。 各ワーカー プロセスがそれぞれ別のコアまたはプロセッサを使用してプロジェクトをビルドするため、プロセッサごとに異なるプロジェクトを同時にビルドできます。 たとえば、このスイッチを "4" に設定すると、MSBuild では 4 つのワーカー プロセスを作成してプロジェクトをビルドします。

値を指定せずに `-maxcpucount` スイッチを追加すると、MSBuild では、コンピューター上のプロセッサの数まで使用します。

MSBuild 3.5 で導入されたこのスイッチについて詳しくは、「[コマンド ライン リファレンス](../msbuild/msbuild-command-line-reference.md)」をご覧ください。

次の例は、MSBuild で 3 つのワーカー プロセスを使用する方法を示しています。 この構成を使用すると、MSBuild では同時に 3 つのプロジェクトをビルドできます。

```cmd
msbuild.exe myproj.proj -maxcpucount:3
```

## <a name="buildinparallel-task-parameter"></a>BuildInParallel タスク パラメーター

`BuildInParallel` は、MSBuild タスクに対する省略可能なブール値パラメーターです。 `BuildInParallel` を `true` (既定値は `true`) に設定すると、複数のワーカー プロセスが生成され、それと同じ数のプロジェクトを同時にビルドすることができます。 このようなビルドを行うためには、`-maxcpucount` スイッチが 1 より大きい値に設定され、システムが最低でもデュアルコアであるか 2 つ以上のプロセッサを搭載している必要があります。

次の例で、 *microsoft.common.targets`BuildInParallel` の一部であり、* パラメーターの設定方法を示しています。

```xml
<PropertyGroup>
    <BuildInParallel Condition="'$(BuildInParallel)' ==
        ''">true</BuildInParallel>
</PropertyGroup>
<MSBuild
    Projects="@(_MSBuildProjectReferenceExistent)"
    Targets="GetTargetPath"
    BuildInParallel="$(BuildInParallel)"
    Properties="%(_MSBuildProjectReferenceExistent.SetConfiguration);
        %(_MSBuildProjectReferenceExistent.SetPlatform)"
    Condition="'@(NonVCProjectReference)'!='' and
        ('$(BuildingSolutionFile)' == 'true' or
        '$(BuildingInsideVisualStudio)' == 'true' or
        '$(BuildProjectReferences)' != 'true') and
        '@(_MSBuildProjectReferenceExistent)' != ''"
    ContinueOnError="!$(BuildingProject)">
    <Output TaskParameter="TargetOutputs"
        ItemName="_ResolvedProjectReferencePaths"/>
</MSBuild>
```

## <a name="see-also"></a>関連項目

- [複数のプロセッサを使用したプロジェクトのビルド](../msbuild/using-multiple-processors-to-build-projects.md)
- [マルチプロセッサ対応のロガーの記述](../msbuild/writing-multi-processor-aware-loggers.md)
- [C++ での並列ビルドの調整に関するブログ](https://devblogs.microsoft.com/visualstudio/tuning-c-build-parallelism-in-vs2010/)

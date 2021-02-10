---
title: MSBuild タスク | Microsoft Docs
description: MSBuild でビルド プロセス中にタスクまたはアトミック ビルド操作を実行する実行可能コードのユニットを使用する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- tasks
- MSBuild, tasks
ms.assetid: 5d3cc4a7-e5db-4f73-b707-8b6882fddcf8
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6b3bb4c1a17cd5d1481be2fa942686bce3861bb2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99918920"
---
# <a name="msbuild-tasks"></a>MSBuild タスク

ビルド プラットフォームでは、ビルドの処理中に、いくつかのアクションを実行する権限が必要です。 MSBuild では、これらのアクションを実行するために "*タスク*" が使用されます。 タスクとは、分割不可能なビルド操作を実行するために MSBuild で使用される実行可能コードの単位です。

## <a name="task-logic"></a>タスクのロジック

 MSBuild XML プロジェクト ファイル形式は、それ自体でビルド操作を完全に実行することができないため、プロジェクト ファイルの外部でタスクのロジックを実装する必要があります。

 タスクの実行ロジックは、<xref:Microsoft.Build.Framework> 名前空間で定義されている <xref:Microsoft.Build.Framework.ITask> インターフェイスを実装する .NET クラスとして実装されます。

 タスク クラスは、プロジェクト ファイル内のタスクで使用可能な入力パラメーターと出力パラメーターも定義します。 タスク クラスによって公開されている、パブリックに設定可能な非静的かつ非抽象のプロパティは、すべてプロジェクト ファイル内で値を設定できます。それには、[Task](../msbuild/task-element-msbuild.md) 要素上に、対応する属性を同じ名前で配置し、この記事の後半の例で示すようにその値を設定します。

 <xref:Microsoft.Build.Framework.ITask> インターフェイスを実装するマネージド クラスを記述することにより、独自のタスクを作成できます。 詳細については、「[タスクの作成](../msbuild/task-writing.md)」を参照してください。

## <a name="execute-a-task-from-a-project-file"></a>プロジェクト ファイルからタスクを実行する

 プロジェクト ファイルでタスクを実行する前に、まずタスクを実装するアセンブリ内の型を、[UsingTask](../msbuild/usingtask-element-msbuild.md) 要素でタスク名にマップする必要があります。 これにより、MSBuild が、プロジェクト ファイルでタスクを見つけた場合にどこでその実行ロジックを探せばよいかを把握できます。

 MSBuild プロジェクト ファイルでタスクを実行するには、要素を、そのタスクの名前で、`Target` 要素の子として作成します。 タスクがパラメーターを受け取る場合、パラメーターは要素の属性として渡されます。

 MSBuild の項目一覧とプロパティは、パラメーターとして使用できます。 たとえば、次のコードでは、`MakeDir` タスクを呼び出し、`MakeDir` オブジェクトの `Directories` プロパティの値を `BuildDir` プロパティの値と等しくなるよう設定します。

```xml
<Target Name="MakeBuildDirectory">
    <MakeDir
        Directories="$(BuildDir)" />
</Target>
```

 また、タスクはプロジェクト ファイルに情報を返すこともできます。この情報は、後で使用するために項目またはプロパティに格納できます。 たとえば、次のコードは `Copy` タスクを呼び出して、`SuccessfullyCopiedFiles` 項目一覧に `CopiedFiles` 出力プロパティからの情報を格納します。

```xml
<Target Name="CopyFiles">
    <Copy
        SourceFiles="@(MySourceFiles)"
        DestinationFolder="@(MyDestFolder)">
        <Output
            TaskParameter="CopiedFiles"
            ItemName="SuccessfullyCopiedFiles"/>
     </Copy>
</Target>
```

## <a name="included-tasks"></a>含まれているタスク

 MSBuild には、ファイルをコピーする [Copy](../msbuild/copy-task.md)、ディレクトリを作成する [MakeDir](../msbuild/makedir-task.md)、C# ソース コード ファイルをコンパイルする [Csc](../msbuild/csc-task.md) など、多数のタスクが装備されています。 使用可能なすべてのタスクと使用法については、「[タスク リファレンス](../msbuild/msbuild-task-reference.md)」をご覧ください。

## <a name="overridden-tasks"></a>オーバーライドされたタスク

 MSBuild では、いくつかの場所にあるタスクが検索されます。 最初の検索場所は、.NET Framework ディレクトリに格納されている拡張子が *.OverrideTasks* であるファイル内です。 これらのファイル内のタスクは、プロジェクト ファイル内のタスクも含め、同じ名前を持つ他のタスクをオーバーライドします。 2 番目の検索場所は、.NET Framework ディレクトリ内の拡張子が *.Tasks* であるファイル内です。 タスクがこれらの場所のいずれにも見つからない場合は、プロジェクト ファイル内のタスクが使用されます。

## <a name="see-also"></a>関連項目

- [MSBuild の概念](../msbuild/msbuild-concepts.md)
- [MSBuild](../msbuild/msbuild.md)
- [タスクの作成](../msbuild/task-writing.md)
- [インライン タスク](../msbuild/msbuild-inline-tasks.md)

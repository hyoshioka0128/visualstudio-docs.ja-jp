---
title: MSBuild バッチ | Microsoft Docs
description: MSBuild で項目のメタデータに基づいて項目一覧が異なるカテゴリまたはバッチに分割され、バッチごとにターゲットまたはタスクが 1 回実行される方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 06/09/2020
ms.topic: conceptual
helpviewer_keywords:
- batching [MSBuild]
- MSBuild, batching
ms.assetid: d35c085b-27b8-49d7-b6f8-8f2f3a0eec38
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5c4d91e95d080b93c8bcdc4486593b4c94bcb501
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93047698"
---
# <a name="msbuild-batching"></a>MSBuild バッチ

MSBuild では、項目のメタデータに基づいて項目一覧が異なるカテゴリまたはバッチに分割され、バッチごとにターゲットまたはタスクが 1 回実行されます。

## <a name="task-batching"></a>タスクのバッチ処理

タスクのバッチ処理を利用すると、項目一覧をさまざまバッチに分割し、各バッチをタスクに個別に渡すことができます。プロジェクト ファイルが扱いやすくなります。 つまり、プロジェクト ファイルは複数回実行できますが、タスクとその属性は一回宣言すれば十分です。

タスク属性の 1 つで `%(ItemMetaDataName)` という表記を使用して、MSBuild でタスクのバッチ処理を実行することを指定します。 次の例では、`Example` 項目一覧が `Color` 項目メタデータ値に基づいてバッチに分割し、各バッチを `MyTask` タスクに個別に渡します。

> [!NOTE]
> タスク属性の他の場所で項目一覧を参照していない場合、またはメタデータ名があいまいな場合は、%(<ItemCollection.ItemMetaDataName>) という表記を使用して、バッチ処理に使用する項目のメタデータの値を完全に修飾できます。

```xml
<Project
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <Example Include="Item1">
            <Color>Blue</Color>
        </Example>
        <Example Include="Item2">
            <Color>Red</Color>
        </Example>
    </ItemGroup>

    <Target Name="RunMyTask">
        <MyTask
            Sources = "@(Example)"
            Output = "%(Color)\MyFile.txt"/>
    </Target>

</Project>
```

特定のバッチ処理の例については、「[タスクのバッチの項目メタデータ](../msbuild/item-metadata-in-task-batching.md)」を参照してください。

## <a name="target-batching"></a>ターゲットのバッチ処理

MSBuild では、ターゲットを実行する前に、ターゲットの入力と出力が最新かどうかが確認されます。 入力と出力がどちらも最新である場合、ターゲットはスキップされます。 ターゲット内のタスクでバッチ処理が使用される場合、MSBuild では、項目の各バッチの入力と出力が最新かどうかを判断する必要があります。 そうでない場合、ターゲットはヒットするたびに実行されます。

次の例では、`%(ItemMetadataName)` 表記のある `Outputs` 属性が含まれる `Target` 要素を示します。 MSBuild は、`Color` メタデータに基づいて `Example` 項目一覧をバッチに分割し、バッチごとに出力ファイルのタイムスタンプを分析します。 バッチからの出力が最新の状態でない場合は、ターゲットが実行されます。 最新の状態であれば、ターゲットはスキップされます。

```xml
<Project
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <Example Include="Item1">
            <Color>Blue</Color>
        </Example>
        <Example Include="Item2">
            <Color>Red</Color>
        </Example>
    </ItemGroup>

    <Target Name="RunMyTask"
        Inputs="@(Example)"
        Outputs="%(Color)\MyFile.txt">
        <MyTask
            Sources = "@(Example)"
            Output = "%(Color)\MyFile.txt"/>
    </Target>

</Project>
```

ターゲットのバッチ処理のもう 1 つの例については、「[ターゲットのバッチの項目メタデータ](../msbuild/item-metadata-in-target-batching.md)」を参照してください。

## <a name="item-and-property-mutations"></a>項目とプロパティの変更

ここでは、ターゲットのバッチ処理またはタスクのバッチ処理を使用しているときに、プロパティや項目メタデータを変更した場合の影響を理解する方法について説明します。

ターゲットのバッチ処理とタスクのバッチ処理は 2 つの異なる MSBuild 操作であるため、ケースごとに MSBuild でどの形式のバッチ処理が使用されているかを正確に理解することが重要です。 ターゲットのタスクにはバッチ処理構文 `%(ItemMetadataName)` が含まれ、ターゲットの属性には含まれない場合、MSBuild ではタスク バッチ処理が使用されています。 ターゲットのバッチ処理を指定する唯一の方法は、ターゲットの属性 (通常は `Outputs` 属性) でバッチ処理構文を使用することです。

ターゲットのバッチ処理とタスクのバッチ処理のどちらでも、バッチは独立して実行されると考えることができます。 すべてのバッチは、プロパティと項目メタデータの値の同じ初期状態のコピーで開始されます。 バッチ実行の間にプロパティ値が変更されても、他のバッチからはわかりません。 次に例を示します。

```xml
  <ItemGroup>
    <Thing Include="2" Color="blue" />
    <Thing Include="1" Color="red" />
  </ItemGroup>

  <Target Name="DemoIndependentBatches">
    <ItemGroup>
      <Thing Condition=" '%(Color)' == 'blue' ">
        <Color>red</Color>
        <NeededColorChange>true</NeededColorChange>
      </Thing>
    </ItemGroup>
    <Message Importance="high"
             Text="Things: @(Thing->'%(Identity) is %(Color); needed change=%(NeededColorChange)')"/>
  </Target>
```

出力は次のようになります。

```output
Target DemoIndependentBatches:
  Things: 2 is red; needed change=true;1 is red; needed change=
```

ターゲットの `ItemGroup` は暗黙的にタスクであり、`Condition` 属性で `%(Color)` が使用されているので、タスクのバッチ処理が実行されます。 2 つのバッチがあります (red に対して 1 つと、blue に対して 1 つ)。 プロパティ `%(NeededColorChange)` は `%(Color)` メタデータが blue の場合にのみ設定され、その設定は、blue のバッチが実行されたときに条件が一致した個々の項目にのみ影響します。 `%(ItemMetadataName)` 構文が指定されていても、`Message` タスクの `Text` 属性ではバッチ処理はトリガーされません。これは、それが項目変換の内側で使用されているためです。

バッチは個別に実行されますが、並列では実行されません。 それにより、バッチ実行で変更されるメタデータ値にアクセスするときに違いがあります。 バッチ実行の一部のメタデータに基づいてプロパティを設定する場合、プロパティは " *最後* " に設定された値になります。

```xml
   <PropertyGroup>
       <SomeProperty>%(SomeItem.MetadataValue)</SomeProperty>
   </PropertyGroup>
```

バッチ実行の後、プロパティでは `%(MetadataValue)` の最終的な値が保持されます。

バッチは個別に実行されますが、ターゲットのバッチ処理とタスクのバッチ処理の違いを考慮し、自分の状況にはどちらの種類が当てはまるかを理解することが重要です。 この区別の重要性を理解するために、次の例を考えてみます。

タスクは明示的ではなく暗黙的な場合があり、タスクのバッチ処理が暗黙的なタスクで発生した場合、混乱を招く可能性があります。 `PropertyGroup` 要素または `ItemGroup` 要素が `Target` に含まれる場合、グループ内の各プロパティ宣言は、個別の [CreateProperty](createproperty-task.md) タスクまたは [CreateItem](createitem-task.md) タスクと同様に、暗黙的に処理されます。 つまり、ターゲットがバッチ処理されるときと、ターゲットがバッチ処理されないとき (つまり、`Outputs` 属性に `%(ItemMetadataName)` 構文がない場合) では、動作が異なります。 ターゲットがバッチ処理されるときは、ターゲットごとに `ItemGroup` が 1 回実行されます。一方、ターゲットがバッチ処理されないときは、`CreateItem` タスクまたは `CreateProperty` タスクと暗黙的に同等のものがタスク バッチ処理を使用してバッチ処理されるため、ターゲットは 1 回だけ実行され、グループ内の各項目または各プロパティは、タスク バッチ処理を使用して個別にバッチ処理されます。

次の例では、メタデータが変更される場合のターゲット バッチ処理とタスク バッチ処理の違いを示します。 いくつかのファイルが含まれるフォルダー A と B がある状況について考えます。

```
A\1.stub
B\2.stub
B\3.stub
```

これら 2 つの似たプロジェクトの出力を見てみます。

```xml
    <ItemGroup>
      <StubFiles Include="$(MSBuildThisFileDirectory)**\*.stub"/>

      <StubDirs Include="@(StubFiles->'%(RecursiveDir)')"/>
    </ItemGroup>

    <Target Name="Test1" AfterTargets="Build" Outputs="%(StubDirs.Identity)">
      <PropertyGroup>
        <ComponentDir>%(StubDirs.Identity)</ComponentDir>
        <ComponentName>$(ComponentDir.TrimEnd('\'))</ComponentName>
      </PropertyGroup>

      <Message Text=">> %(StubDirs.Identity) '$(ComponentDir)' '$(ComponentName)'"/>
    </Target>
```

出力は次のようになります。

```output
Test1:
  >> A\ 'A\' 'A'
Test1:
  >> B\ 'B\' 'B'
```

ここで、ターゲットのバッチ処理を指定した `Outputs` 属性を削除します。

```xml
    <ItemGroup>
      <StubFiles Include="$(MSBuildThisFileDirectory)**\*.stub"/>

      <StubDirs Include="@(StubFiles->'%(RecursiveDir)')"/>
    </ItemGroup>

    <Target Name="Test1" AfterTargets="Build">
      <PropertyGroup>
        <ComponentDir>%(StubDirs.Identity)</ComponentDir>
        <ComponentName>$(ComponentDir.TrimEnd('\'))</ComponentName>
      </PropertyGroup>

      <Message Text=">> %(StubDirs.Identity) '$(ComponentDir)' '$(ComponentName)'"/>
    </Target>
```

出力は次のようになります。

```output
Test1:
  >> A\ 'B\' 'B'
  >> B\ 'B\' 'B'
```

見出し `Test1` は 1 回だけ出力されますが、前の例では 2 回出力されたことに注意してください。 つまり、ターゲットはバッチ処理されません。  その結果、出力は紛らわしいほど異なります。

これは、ターゲットのバッチ処理を使用した場合は、各ターゲットのバッチで、ターゲット内のすべてのものが、すべてのプロパティと項目の独自の独立したコピーを使用して実行されますが、`Outputs` 属性を省略すると、プロパティ グループの個々の行が個別のタスクとして扱われ、バッチ処理される可能性があるためです。 この場合、`ComponentName` 行が実行されるときまでに、`ComponentDir` 行の両方のバッチが完了し、実行された 2 番目のものによって 2 行目で示される値が決定されているように、`ComponentDir` タスクはバッチ処理されます (`%(ItemMetadataName)` 構文が使用されます)。

## <a name="property-functions-using-metadata"></a>メタデータを利用するプロパティ関数

バッチ処理は、メタデータを含むプロパティ関数で制御できます。 たとえば、オブジェクトに適用された

`$([System.IO.Path]::Combine($(RootPath),%(Compile.Identity)))`

このプロパティ関数は、<xref:System.IO.Path.Combine%2A> を使用し、ルート フォルダーパスとコンパイル項目パスを結合します。

プロパティ関数はメタデータ値内に表示されない場合があります。 たとえば、オブジェクトに適用された

`%(Compile.FullPath.Substring(0,3))`

これは許可されません。

プロパティ関数の詳細については、「[プロパティ関数](../msbuild/property-functions.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [ItemMetadata 要素 (MSBuild)](../msbuild/itemmetadata-element-msbuild.md)
- [MSBuild の概念](../msbuild/msbuild-concepts.md)
- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
- [詳細な概念](../msbuild/msbuild-advanced-concepts.md)

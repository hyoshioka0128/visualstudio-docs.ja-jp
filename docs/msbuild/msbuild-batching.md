---
title: MSBuild バッチ | Microsoft Docs
ms.date: 11/04/2016
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
ms.openlocfilehash: 78aeef8ea651aac1fe2a780207474399f4bbcf09
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/26/2020
ms.locfileid: "77633435"
---
# <a name="msbuild-batching"></a>MSBuild バッチ

MSBuild には、項目メタデータに基づき、項目一覧をさまざまなカテゴリまたはバッチに分割し、各バッチで一度に 1 つのターゲットまたはタスクを実行する機能があります。

## <a name="task-batching"></a>タスクのバッチ処理

タスクのバッチ処理を利用すると、項目一覧をさまざまバッチに分割し、各バッチをタスクに個別に渡すことができます。プロジェクト ファイルが扱いやすくなります。 つまり、プロジェクト ファイルは複数回実行できますが、タスクとその属性は一回宣言すれば十分です。

タスク属性の 1 つで %(\<ItemMetaDataName>) という表記を利用し、MSBuild でタスクのバッチ処理を実行するように指定します。 次の例では、`Example` 項目一覧が `Color` 項目メタデータ値に基づいてバッチに分割し、各バッチを `MyTask` タスクに個別に渡します。

> [!NOTE]
> タスク属性の他の場所で項目一覧を参照しない場合、あるいはメタデータ名があいまいな場合、%(\<ItemCollection.ItemMetaDataName>) という表記を利用し、バッチ処理に使用する項目メタデータ値を完全修飾できます。

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

MSBuild は、ターゲットを実行する前に、ターゲットの入力と出力が最新の状態になっているかを確認します。 入力と出力の両方が最新の状態になっている場合、ターゲットはスキップされます。 ターゲット内のタスクがバッチ処理を利用する場合、MSBuild では、項目の各バッチの入力と出力が最新の状態になっているかを判断する必要があります。 最新の状態ではない場合、ターゲットにヒットするたびにターゲットが実行されます。

次の例では、%(\<ItemMetaDataName>) 表記がある `Outputs` 属性を含む `Target` 要素を確認できます。 MSBuild は、`Color` メタデータに基づいて `Example` 項目一覧をバッチに分割し、バッチごとに出力ファイルのタイムスタンプを分析します。 バッチからの出力が最新の状態ではない場合、ターゲットが実行されます。 最新の状態であれば、ターゲットはスキップされます。

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

---
title: ビルド処理を拡張する
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, overriding predefined targets
- MSBuild, overriding DependsOn properties
- MSBuild, extending Visual Studio builds
- MSBuild, DependsOn properties
ms.assetid: cb077613-4a59-41b7-96ec-d8516689163c
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cca0c55951d4928347528814d043bb8a7c55be9a
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/26/2020
ms.locfileid: "77633851"
---
# <a name="how-to-extend-the-visual-studio-build-process"></a>方法: Visual Studio ビルド処理を拡張する

Visual Studio のビルド処理は、プロジェクト ファイルにインポートされる一連の MSBuild *.targets* ファイルによって定義されます。 このインポートされるファイルの 1 つである *Microsoft.Common.targets* を拡張することで、ビルド処理の複数のポイントでカスタム タスクを実行できます。 この記事では、Visual Studio のビルド処理を拡張するために使用できる 2 つの方法について説明します。

- 共通のターゲット (*Microsoft.Common.targets* またはインポートされるファイル) で定義されている特定の定義済みターゲットをオーバーライドする。

- 共通のターゲットで定義されている "DependsOn" プロパティをオーバーライドする。
## <a name="override-predefined-targets"></a>事前定義されているターゲットをオーバーライドする

## <a name="override-predefined-targets"></a>事前定義されているターゲットをオーバーライドする

共通のターゲットには、事前定義されている空のターゲットのセットが含まれています。これは、ビルド処理の一部の主要ターゲットの前後で呼び出されます。 たとえば、MSBuild では、メインの `CoreBuild` ターゲットの前に `BeforeBuild` ターゲットが呼び出され、`CoreBuild` ターゲットの後に `AfterBuild` ターゲットが呼び出されます。 既定では、共通のターゲットの空のターゲットでは何も行われませんが、共通のターゲットをインポートするプロジェクト ファイルでターゲットを定義することで、その既定の動作をオーバーライドできます。 事前定義されているターゲットをオーバーライドすることで、MSBuild タスクを利用し、ビルド処理をさらに細かく制御できます。
共通のターゲットには、事前定義されている空のターゲットのセットが含まれています。これは、ビルド処理の一部の主要ターゲットの前後で呼び出されます。 たとえば、MSBuild では、メインの `CoreBuild` ターゲットの前に `BeforeBuild` ターゲットが呼び出され、`CoreBuild` ターゲットの後に `AfterBuild` ターゲットが呼び出されます。 既定では、共通のターゲットの空のターゲットでは何も行われませんが、共通のターゲットをインポートするプロジェクト ファイルでターゲットを定義することで、その既定の動作をオーバーライドできます。 事前定義されているターゲットをオーバーライドすることで、MSBuild タスクを利用し、ビルド処理をさらに細かく制御できます。

> [!NOTE]
> SDK スタイルのプロジェクトでは、*プロジェクト ファイルの最後の行の後に*、ターゲットが暗黙的にインポートされます。 つまり、インポートを手動で指定しない限り、既定のターゲットをオーバーライドすることはできないということです。詳しくは、「[方法: MSBuild プロジェクト SDK の使用](how-to-use-project-sdk.md)」で説明されています。

#### <a name="to-override-a-predefined-target"></a>事前定義されているターゲットをオーバーライドするには

1. オーバーライドする共通のターゲットで事前定義済みターゲットを特定します。 下の表をご覧ください。これは安全にオーバーライドできるターゲットの完全一覧です。

2. プロジェクト ファイルの最後で、`</Project>` タグの直前で、ターゲットを定義します。 次に例を示します。

    ```xml
    <Project>
        ...
        <Target Name="BeforeBuild">
            <!-- Insert tasks to run before build here -->
        </Target>
        <Target Name="AfterBuild">
            <!-- Insert tasks to run after build here -->
        </Target>
    </Project>
    ```

3. プロジェクト ファイルをビルドします。

次の表では、共通のターゲットで安全にオーバーライドできるすべてのターゲットを示しています。

|ターゲット名|説明|
|-----------------|-----------------|
|`BeforeCompile`、`AfterCompile`|これらのターゲットのいずれかに挿入されているタスクは、コア コンパイル完了の前または後に実行されます。 ほとんどのカスタマイズはこれら 2 つのターゲットのいずれかで行われます。|
|`BeforeBuild`、`AfterBuild`|これらのターゲットのいずれかに挿入されているタスクは、ビルド内の他のすべての前または後に実行されます。 **注:** `BeforeBuild` ターゲットと `AfterBuild` ターゲットは、ほとんどのプロジェクト ファイルの終わりにあるコメントで既に定義されており、ビルド前イベントとビルド後イベントをプロジェクト ファイルに簡単に追加できます。|
|`BeforeRebuild`、`AfterRebuild`|これらのターゲットのいずれかに挿入されているタスクは、コア再ビルド機能の呼び出しの前または後に実行されます。 *Microsoft.Common.targets* のターゲット実行順序は `BeforeRebuild`、`Clean`、`Build`、`AfterRebuild` です。|
|`BeforeClean`、`AfterClean`|これらのターゲットのいずれかに挿入されているタスクは、コア クリーン機能の呼び出しの前または後に実行されます。|
|`BeforePublish`、`AfterPublish`|これらのターゲットのいずれかに挿入されているタスクは、コア公開機能の呼び出しの前または後に実行されます。|
|`BeforeResolveReferences`、`AfterResolveReferences`|これらのターゲットのいずれかに挿入されているタスクは、アセンブリ参照解決の前または後に実行されます。|
|`BeforeResGen`、`AfterResGen`|これらのターゲットのいずれかに挿入されているタスクは、リソース生成の前または後に実行されます。|

## <a name="override-dependson-properties"></a>DependsOn プロパティをオーバーライドする

事前定義済みターゲットのオーバーライドはビルド処理を拡張する簡単な方法ですが、MSBuild ではターゲットの定義が順番に評価されるため、プロジェクトをインポートする別のプロジェクトが、既にオーバーライドしているターゲットをオーバーライドすることを防ぐことはできません。 そのため、たとえば、プロジェクト ファイルに定義されている最後の `AfterBuild` ターゲットが、その他すべてのプロジェクトがインポートされた後に、ビルド中に使用されるターゲットになります。

共通のターゲット全体で `DependsOnTargets` 属性で使用される DependsOn プロパティをオーバーライドすることで、ターゲットの意図しないオーバーライドを防ぐことができます。 たとえば、`Build` ターゲットには、`DependsOnTargets` 属性値 `"$(BuildDependsOn)"` が含まれています。 次の例を考えてみましょう。

```xml
<Target Name="Build" DependsOnTargets="$(BuildDependsOn)"/>
```

XML のこの部分は、`Build` ターゲットを実行するには、`BuildDependsOn` プロパティに指定されているすべてのターゲットを先に実行する必要があります。 `BuildDependsOn` プロパティは次のように定義されています。

```xml
<PropertyGroup>
    <BuildDependsOn>
        BeforeBuild;
        CoreBuild;
        AfterBuild
    </BuildDependsOn>
</PropertyGroup>
```

プロジェクト ファイルの終わりで `BuildDependsOn` という名前の別のプロパティを宣言することでこのプロパティ値をオーバーライドできます。 新しいプロパティに前の `BuildDependsOn` プロパティを含めることで、ターゲット一覧の最初と最後に新しいターゲットを追加できます。 次に例を示します。

```xml
<PropertyGroup>
    <BuildDependsOn>
        MyCustomTarget1;
        $(BuildDependsOn);
        MyCustomTarget2
    </BuildDependsOn>
</PropertyGroup>

<Target Name="MyCustomTarget1">
    <Message Text="Running MyCustomTarget1..."/>
</Target>
<Target Name="MyCustomTarget2">
    <Message Text="Running MyCustomTarget2..."/>
</Target>
```

プロジェクト ファイルをインポートするプロジェクトは、既に行っているカスタマイズを上書きすることなく、これらのプロパティをオーバーライドできます。

#### <a name="to-override-a-dependson-property"></a>DependsOn プロパティをオーバーライドするには

1. オーバーライドする共通のターゲットで事前定義済み DependsOn プロパティを特定します。 下の表をご覧ください。一般的にオーバーライドされる DependsOn プロパティの一覧です。

2. プロパティ ファイルの終わりにプロパティの別のインスタンスを定義します。 新しいプロパティに元のプロパティ (たとえば、`$(BuildDependsOn)`) を含めます。

3. プロパティ定義の前または後にカスタム ターゲットを定義します。

4. プロジェクト ファイルをビルドします。

### <a name="commonly-overridden-dependson-properties"></a>一般的にオーバーライドされる DependsOn プロパティ

|プロパティ名|説明|
|-------------------|-----------------|
|`BuildDependsOn`|ビルド処理全体の前または後にカスタム ターゲットを挿入する場合にオーバーライドするプロパティ。|
|`CleanDependsOn`|カスタム ビルド処理からの出力をクリーンアップする場合にオーバーライドするプロパティ。|
|`CompileDependsOn`|コンパイル手順の前または後にカスタム プロセスを挿入する場合にオーバーライドするプロパティ。|

## <a name="see-also"></a>関連項目

- [Visual Studio の統合](../msbuild/visual-studio-integration-msbuild.md)
- [MSBuild の概念](../msbuild/msbuild-concepts.md)
- [.targets ファイル](../msbuild/msbuild-dot-targets-files.md)

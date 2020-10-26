---
title: '方法: ビルド処理を拡張する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, overriding predefined targets
- MSBuild, overriding DependsOn properties
- MSBuild, extending Visual Studio builds
- MSBuild, DependsOn properties
ms.assetid: cb077613-4a59-41b7-96ec-d8516689163c
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 789c60da5be841721ab3a999120e2fe560ffd588
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68156601"
---
# <a name="how-to-extend-the-visual-studio-build-process"></a>方法 : Visual Studio ビルド処理を拡張する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ビルド処理は、プロジェクト ファイルにインポートされる一連の [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] .targets ファイルによって定義されます。 このインポートされるファイルの 1 つである Microsoft.Common.targets を拡張することで、ビルド処理の複数のポイントでカスタム タスクを実行できます。 このトピックでは、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ビルド処理を拡張するための 2 つの方法について説明します。

- Microsoft.Common.targets で事前定義されている特定のターゲットをオーバーライドする。

- Microsoft.Common.targets で定義されている "DependsOn" プロパティをオーバーライドする。

## <a name="overriding-predefined-targets"></a>事前定義されているターゲットをオーバーライドする
 Microsoft.Common.targets ファイルには、事前定義されている空のファイルが含まれています。この一連のファイルは、ビルド処理の一部の主要ターゲットの前後で呼び出されます。 たとえば、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] は、メインの `CoreBuild` ターゲットの前に `BeforeBuild` ターゲットを、`CoreBuild` ターゲットの後に `AfterBuild` ターゲットを呼び出します。 既定では、Microsoft.Common.targets の空のターゲットは何も行いませんが、その既定の動作をオーバーライドできます。その方法としては、Microsoft.Common.targets をインポートするプロジェクト ファイルでターゲットを定義します。 これを行うことで、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] タスクを利用し、ビルド処理をさらに細かく制御できます。

#### <a name="to-override-a-predefined-target"></a>事前定義されているターゲットをオーバーライドするには

1. オーバーライドする Microsoft.Common.targets で事前定義済みターゲットを見つけます。 下の表をご覧ください。これは安全にオーバーライドできるターゲットの完全一覧です。

2. プロジェクト ファイルの最後で、`</Project>` タグの直前で、ターゲットを定義します。 次に例を示します。

   ```
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

   次の表は、Microsoft.Common.targets で安全にオーバーライドできるすべてのターゲットをまとめたものです。

|ターゲット名|説明|
|-----------------|-----------------|
|`BeforeCompile`, `AfterCompile`|これらのターゲットのいずれかに挿入されているタスクは、コア コンパイル完了の前または後に実行されます。 ほとんどのカスタマイズはこれら 2 つのターゲットのいずれかで行われます。|
|`BeforeBuild`, `AfterBuild`|これらのターゲットのいずれかに挿入されているタスクは、ビルド内の他のすべての前または後に実行されます。 **注:**`BeforeBuild` ターゲットと `AfterBuild` ターゲットは、ほとんどのプロジェクト ファイルの終わりにあるコメントで既に定義されています。 これにより、ビルド前イベントとビルド後イベントをプロジェクト ファイルに簡単に追加できます。|
|`BeforeRebuild`, `AfterRebuild`|これらのターゲットのいずれかに挿入されているタスクは、コア再ビルド機能の呼び出しの前または後に実行されます。 Microsoft.Common.targets のターゲット実行順序は `BeforeRebuild`、`Clean`、`Build`、`AfterRebuild` です。|
|`BeforeClean`, `AfterClean`|これらのターゲットのいずれかに挿入されているタスクは、コア クリーン機能の呼び出しの前または後に実行されます。|
|`BeforePublish`, `AfterPublish`|これらのターゲットのいずれかに挿入されているタスクは、コア公開機能の呼び出しの前または後に実行されます。|
|`BeforeResolveReference`, `AfterResolveReferences`|これらのターゲットのいずれかに挿入されているタスクは、アセンブリ参照解決の前または後に実行されます。|
|`BeforeResGen`, `AfterResGen`|これらのターゲットのいずれかに挿入されているタスクは、リソース生成の前または後に実行されます。|

## <a name="overriding-dependson-properties"></a>"DependsOn" プロパティをオーバーライドする
 事前定義済みターゲットのオーバーライドはビルド処理を拡張する簡単な方法ですが、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] はターゲットの定義を順次評価するため、プロジェクトをインポートする別のプロジェクトが既にオーバーライドしているターゲットをオーバーライドすることを阻止できません。 そのため、たとえば、プロジェクト ファイルに定義されている最後の `AfterBuild` ターゲットが、その他すべてのプロジェクトがインポートされた後に、ビルド中に使用されるターゲットになります。

 ターゲットの意図しないオーバーライドを防ぐ方法があります。Microsoft.Common.targets ファイル全体で `DependsOnTargets` 属性で利用される "DependsOn" プロパティをオーバーライドします。 たとえば、`Build` ターゲットには、`DependsOnTargets` 属性値 `"$(BuildDependsOn)"` が含まれています。 次の点を考慮してください。

```
<Target Name="Build" DependsOnTargets="$(BuildDependsOn)"/>
```

 XML のこの部分は、`Build` ターゲットを実行するには、`BuildDependsOn` プロパティに指定されているすべてのターゲットを先に実行する必要があります。 `BuildDependsOn` プロパティは次のように定義されています。

```
<PropertyGroup>
    <BuildDependsOn>
        BeforeBuild;
        CoreBuild;
        AfterBuild
    </BuildDependsOn>
</PropertyGroup>
```

 プロジェクト ファイルの終わりで `BuildDependsOn` という名前の別のプロパティを宣言することでこのプロパティ値をオーバーライドできます。 新しいプロパティに前の `BuildDependsOn` プロパティを含めることで、ターゲット一覧の最初と最後に新しいターゲットを追加できます。 次に例を示します。

```
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

#### <a name="to-override-a-dependson-property"></a>"DependsOn" プロパティをオーバーライドするには

1. オーバーライドする Microsoft.Common.targets で事前定義済み "DependsOn" プロパティを見つけます。 下の表をご覧ください。一般的にオーバーライドされる "DependsOn" プロパティの一覧です。

2. プロパティ ファイルの終わりにプロパティの別のインスタンスを定義します。 新しいプロパティに元のプロパティ (たとえば、`$(BuildDependsOn)`) を含めます。

3. プロパティ定義の前または後にカスタム ターゲットを定義します。

4. プロジェクト ファイルをビルドします。

### <a name="commonly-overridden-dependson-properties"></a>一般的にオーバーライドされる "DependsOn" プロパティ

|プロパティ名|説明|
|-------------------|-----------------|
|`BuildDependsOn`|ビルド処理全体の前または後にカスタム ターゲットを挿入する場合にオーバーライドするプロパティ。|
|`CleanDependsOn`|カスタム ビルド処理からの出力をクリーンアップする場合にオーバーライドするプロパティ。|
|`CompileDependsOn`|コンパイル手順の前または後にカスタム プロセスを挿入する場合にオーバーライドするプロパティ。|

## <a name="see-also"></a>参照
 [Visual Studio の統合](../msbuild/visual-studio-integration-msbuild.md) [MSBuild の概念](../msbuild/msbuild-concepts.md) [.targets ファイル](../msbuild/msbuild-dot-targets-files.md)

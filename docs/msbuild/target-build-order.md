---
title: ターゲットのビルド順序 | Microsoft Docs
ms.date: 05/02/2019
ms.topic: conceptual
helpviewer_keywords:
- msbuild, build order
ms.assetid: f4a26339-9f9a-497a-9aa6-0797183d450d
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 607584b4b41bdfde224bdb35d30eec1c6c8a4197
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75585458"
---
# <a name="target-build-order"></a>ターゲットのビルド順序

あるターゲットへの入力が別のターゲットの出力に依存する場合、ターゲットの順序を指定する必要があります。 以下の属性を使用して、ターゲットを実行する順序を指定できます。

- `InitialTargets` で初期化します。 この `Project` 属性は、ターゲットがコマンド ラインまたは `DefaultTargets` 属性に指定されている場合でも最初に実行されるターゲットを指定します。

- `DefaultTargets` で初期化します。 この `Project` 属性を使うと、ターゲットがコマンドラインで明示的に指定されていない場合に実行されるターゲットを指定できます。

- `DependsOnTargets` で初期化します。 この `Target` 属性は、このターゲットを実行する前に実行する必要があるターゲットを指定します。

- `BeforeTargets` および `AfterTargets`。 これらの `Target` 属性は、このターゲットを、指定されたターゲットの前または後に実行するように指定します (MSBuild 4.0)。

ビルド内の後続のターゲットがそのターゲットに依存している場合でも、ビルド中に 1 つのターゲットが 2 回実行されることはありません。 ターゲットは一度実行されると、それ以上ビルドに影響しません。

ターゲットには `Condition` 属性を指定することができます。 指定した条件が `false` と評価された場合、ターゲットは実行されず、ビルドには影響しません。 条件の詳細については、「[条件](../msbuild/msbuild-conditions.md)」を参照してください。

## <a name="initial-targets"></a>初期ターゲット

`InitialTargets`Project[ 要素の ](../msbuild/project-element-msbuild.md) 属性は、ターゲットがコマンド ラインまたは `DefaultTargets` 属性に指定されている場合でも最初に実行されるターゲットを指定します。 通常、初期ターゲットはエラー チェックに使用されます。

`InitialTargets` 属性の値は、ターゲットをセミコロンで区切った、順序指定された一覧です。 次の例では、`Warm` ターゲットを実行してから `Eject` ターゲットを実行するように指定しています。

```xml
<Project InitialTargets="Warm;Eject" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
```

インポートされたプロジェクトには、独自の `InitialTargets` 属性が含まれている場合があります。 それらのすべての初期ターゲットが集約されて順番に実行されます。

詳細については、「[方法: 最初にビルドするターゲットを指定する](../msbuild/how-to-specify-which-target-to-build-first.md)」を参照してください。

## <a name="default-targets"></a>既定のターゲット

`DefaultTargets`Project[ 要素の ](../msbuild/project-element-msbuild.md) 属性は、ターゲットがコマンド ラインで明示的に指定されていない場合にビルドするターゲット (複数可) を指定します。

`DefaultTargets` 属性の値は、既定のターゲットをセミコロンで区切った、順序指定された一覧です。 次の例では、`Clean` ターゲットを実行してから `Build` ターゲットを実行するように指定しています。

```xml
<Project DefaultTargets="Clean;Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
```

コマンド ラインで **-target** スイッチを使用して、既定のターゲットをオーバーライドすることができます。 次の例では、`Build` ターゲットを実行してから `Report` ターゲットを実行するように指定しています。 この方法でターゲットを指定する場合、既定のターゲットは無視されます。

 `msbuild -target:Build;Report`

初期ターゲットと既定のターゲットの両方が指定されており、コマンド ライン ターゲットが指定されていない場合、MSBuild はまず初期ターゲットを実行してから、既定のターゲットを実行します。

インポートされたプロジェクトには、独自の `DefaultTargets` 属性が含まれている場合があります。 検出された最初の `DefaultTargets` 属性によって、実行する既定のターゲットが決定されます。

詳細については、「[方法: 最初にビルドするターゲットを指定する](../msbuild/how-to-specify-which-target-to-build-first.md)」を参照してください。

## <a name="first-target"></a>最初のターゲット

初期ターゲット、既定のターゲット、またはコマンド ラインのターゲットがいずれも指定されていない場合、MSBuild はプロジェクト ファイル内またはインポートされたプロジェクト ファイル内で検出された最初のターゲットを実行します。

## <a name="target-dependencies"></a>ターゲットの依存関係

ターゲット同士は相互に依存関係を記述できます。 `DependsOnTargets` 属性は、ターゲットが他のターゲットに依存していることを示します。 次に例を示します。

```xml
<Target Name="Serve" DependsOnTargets="Chop;Cook" />
```

`Serve` ターゲットが `Chop` ターゲットと `Cook` ターゲットに依存することを MSBuild に指示します。 MSBuild は `Chop` ターゲット、`Cook` ターゲットの順に実行してから、`Serve` ターゲットを実行します。

## <a name="beforetargets-and-aftertargets"></a>BeforeTargets と AfterTargets

MSBuild 4.0 では、`BeforeTargets` 属性と `AfterTargets` 属性を使用して、ターゲットの順序を指定できます。

次のスクリプトがあるとします。

```xml
<Project DefaultTargets="Compile;Link" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Target Name="Compile">
        <Message Text="Compiling" />
    </Target>
    <Target Name="Link">
        <Message Text="Linking" />
    </Target>
</Project>
```

`Optimize` ターゲットの後、`Compile` ターゲットの前に実行される中間ターゲット `Link` を作成するには、`Project` 要素内の任意の場所に次のターゲットを追加します。

```xml
<Target Name="Optimize"
    AfterTargets="Compile" BeforeTargets="Link">
    <Message Text="Optimizing" />
</Target>
```

## <a name="determine-the-target-build-order"></a>ターゲットのビルド順序の決定

MSBuild では、ターゲットのビルド順序を次のように決定します。

1. `InitialTargets` ターゲットが実行されます。

2. **-target** スイッチによってコマンドラインで指定されたターゲットが実行されます。 コマンド ラインでターゲットが指定されていない場合、`DefaultTargets` ターゲットが実行されます。 どちらも存在しない場合は、検出された最初のターゲットが実行されます。

3. ターゲットの `Condition` 属性が評価されます。 `Condition` 属性が存在し、`false` と評価された場合、ターゲットは実行されず、ビルドにはそれ以上影響しません。

   `BeforeTargets` または `AfterTargets` の条件付きターゲットをリストしている他のターゲットは、やはり決められた順序で実行します。

4. `DependsOnTargets` 属性がターゲットに適用されており、評価の結果、`Condition` にならない限り、ターゲットが実行されるか、スキップされる前に、その `false` ターゲットが実行されます。

   > [!NOTE]
   > 実行されていない場合、ターゲットはスキップされたものと見なされます。その出力項目が最新の状態になっているためです (「[インクリメンタル ビルド](../msbuild/incremental-builds.md)」を参照してください)。 このチェックはターゲット内のタスクが実行される直前に行われ、ターゲットの実行順序には影響を与えません。

5. ターゲットが実行されるか、スキップされる前に、`BeforeTargets` 属性でターゲットをリストする他のターゲットが実行されます。

6. ターゲットが実行される前に、その `Inputs` 属性と `Outputs` 属性が比較されます。 対応する入力ファイルに対して最新ではない出力ファイルがあると MSBuild が判断した場合、MSBuild はターゲットを実行します。 それ以外の場合は、MSBuild はターゲットをスキップします。

7. ターゲットが実行されるか、スキップされると、`AfterTargets` 属性でそれをリストする他のターゲットが実行されます。

## <a name="see-also"></a>参照

- [ターゲット](../msbuild/msbuild-targets.md)

---
title: Target 要素 (MSBuild) | Microsoft Docs
ms.date: 06/13/2019
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Target
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Target element [MSBuild]
- <Target> element [MSBuild]
ms.assetid: 350f6fc2-86b3-45f2-a31e-ece0e6bd4dca
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 472d4c9c4c44176048a1bfd8c0791a1a406b95bd
ms.sourcegitcommit: 8ff6c6975148ce43bdac21c8995fbab910c312fe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2020
ms.locfileid: "80375548"
---
# <a name="target-element-msbuild"></a>Target 要素 (MSBuild)

MSBuild によって順次実行されるタスクのセットを格納します。

 \<Project> \<Target>

## <a name="syntax"></a>構文

```xml
<Target Name="Target Name"
        Inputs="Inputs"
        Outputs="Outputs"
        Returns="Returns"
        KeepDuplicateOutputs="true/false"
        BeforeTargets="Targets"
        AfterTargets="Targets"
        DependsOnTargets="DependentTarget"
        Condition="'String A' == 'String B'"
        Label="Label">
    <Task>... </Task>
    <PropertyGroup>... </PropertyGroup>
    <ItemGroup>... </ItemGroup>
    <OnError... />
</Target>
```

## <a name="attributes-and-elements"></a>属性と要素

 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`Name`|必須の属性です。<br /><br /> ターゲットの名前。 ターゲットの名前に使用できるのは `$@()%*?.` 以外の文字です。|
|`Condition`|省略可能な属性です。<br /><br /> 評価する条件です。 条件が `false` と評価された場合、ターゲットの本体も、`DependsOnTargets` 属性で設定されたいずれのターゲットも実行されません。 条件の詳細については、「[条件](../msbuild/msbuild-conditions.md)」を参照してください。|
|`Inputs`|省略可能な属性です。<br /><br /> このターゲットの入力を形成するファイル。 複数のファイルを指定するときは、セミコロン (;) で区切ります。 ファイルのタイムスタンプは、`Outputs` のファイルのタイムスタンプと比較され、`Target` が最新かどうか判断されます。 詳細については、「[インクリメンタル ビルド](../msbuild/incremental-builds.md)」、「[方法:インクリメンタル ビルドを実行する](../msbuild/how-to-build-incrementally.md)」、および[変換](../msbuild/msbuild-transforms.md)に関するページを参照してください。|
|`Outputs`|省略可能な属性です。<br /><br /> このターゲットの出力を形成するファイル。 複数のファイルを指定するときは、セミコロン (;) で区切ります。 ファイルのタイムスタンプは、`Inputs` のファイルのタイムスタンプと比較され、`Target` が最新かどうか判断されます。 詳細については、「[インクリメンタル ビルド](../msbuild/incremental-builds.md)」、「[方法:インクリメンタル ビルドを実行する](../msbuild/how-to-build-incrementally.md)」、および[変換](../msbuild/msbuild-transforms.md)に関するページを参照してください。|
|`Returns`|省略可能な属性です。<br /><br /> このターゲットを呼び出すタスク (MSBuild タスクなど) で使用可能になる項目のセットです。 複数のターゲットを指定するときは、セミコロン (;) で区切ります。 ファイル内のターゲットに `Returns` 属性がない場合、代わりに Outputs 属性がこの目的で使用されます。|
|`KeepDuplicateOutputs`|省略可能な Boolean 属性です。<br /><br /> `true` の場合、ターゲットの Returns の同じ項目への参照が複数記録されます。  既定では、この属性は `false` です。|
|`BeforeTargets`|省略可能な属性です。<br /><br /> ターゲット名のセミコロン区切りのリストです。  指定した場合、指定したターゲットの前にこのターゲットが実行されます。 これにより、プロジェクト作成者は、これらを直接変更せずに、既存のターゲット セットを拡張できます。 詳細については、「[ターゲットのビルド順序](../msbuild/target-build-order.md)」を参照してください。|
|`AfterTargets`|省略可能な属性です。<br /><br /> ターゲット名のセミコロン区切りのリストです。 指定した場合、指定したターゲットの後でこのターゲットが実行されます。 これにより、プロジェクト作成者は、これらを直接変更せずに、既存のターゲット セットを拡張できます。 詳細については、「[ターゲットのビルド順序](../msbuild/target-build-order.md)」を参照してください。|
|`DependsOnTargets`|省略可能な属性です。<br /><br /> このターゲットを実行する前、またはトップレベルの依存関係分析を実行する前に、実行する必要のあるターゲットです。 複数のターゲットを指定するときは、セミコロン (;) で区切ります。|
|`Label`|省略可能な属性です。<br /><br /> システム要素およびユーザー要素を識別するため、または順序付けるための識別子です。|

### <a name="child-elements"></a>子要素

| 要素 | 説明 |
| - | - |
| [Task](../msbuild/task-element-msbuild.md) | MSBuild タスクのインスタンスを作成して、実行します。 1 つのターゲットに 0 個以上のタスクを指定できます。 |
| [PropertyGroup](../msbuild/propertygroup-element-msbuild.md) | ユーザー定義の `Property` 要素のセットを格納します。 .NET Framework 3.5 以降では、`Target` 要素に `PropertyGroup` 要素を格納できます。 |
| [ItemGroup](../msbuild/itemgroup-element-msbuild.md) | ユーザー定義の `Item` 要素のセットを格納します。 .NET Framework 3.5 以降では、`Target` 要素に `ItemGroup` 要素を格納できます。 詳細については、「[項目](../msbuild/msbuild-items.md)」を参照してください。 |
| [OnError](../msbuild/onerror-element-msbuild.md) | 失敗したタスクの `ContinueOnError` 属性が ErrorAndStop (または `false`) の場合、1 つ以上のターゲットが実行されます。 1 つのターゲットに 0 個以上の `OnError` 要素を指定できます。 `OnError` 要素がある場合は、`Target` 要素内で最後の要素である必要があります。<br /><br /> `ContinueOnError` 属性の詳細は、「[Task 要素 (MSBuild)](../msbuild/task-element-msbuild.md)」を参照してください。 |

### <a name="parent-elements"></a>親要素

| 要素 | 説明 |
| - | - |
| [プロジェクト](../msbuild/project-element-msbuild.md) | MSBuild プロジェクト ファイルの必須のルート要素です。 |

## <a name="remarks"></a>Remarks

 実行する最初のターゲットは実行時に指定されます。 各ターゲットは他のターゲットとの依存関係を持つ場合があります。 たとえば、展開用のターゲットはコンパイル用のターゲットに依存します。 MSBuild エンジンでは依存関係が、`DependsOnTargets` 属性に出現する順序で、左から右に実行されます。 詳細については、[ターゲット](../msbuild/msbuild-targets.md) を参照してください。

 MSBuild はインポートの順序に依存するので、特定の `Name` 属性を持つ最後のターゲットの定義が使われます。

 あるターゲットに複数のターゲットが依存関係を持つ場合でも、ターゲットは 1 回のビルド中に 1 回だけ実行されます。

 `Condition` 属性が `false` と評価されたためにターゲットがスキップされた場合でも、そのターゲットがその後ビルドで呼び出され、`Condition` 属性がその時点で `true` と評価された場合には、そのターゲットを実行できます。

 MSBuild 4 より前のバージョンでは、`Target` によって `Outputs` 属性で指定されていたすべての項目を返していました。  このために、MSBuild では、後でビルドのタスクによって要求された場合に備えて、これらの項目を記録しておく必要がありました。 どのターゲットが呼び出し元を必要とする出力を持つかを指定する手段がなかったため、MSBuild は呼び出されたすべての `Target` のすべての `Outputs` からのすべての項目を蓄積していました。 このため、出力項目の多いビルドについては、スケーリングの問題が発生していました。

 ユーザーがプロジェクト内の任意の `Target` 要素で `Returns` を指定した場合、`Returns` 属性を持つ `Target` だけがその項目を記録します。

 `Target` には `Outputs` 属性と `Returns` 属性の両方を含めることができます。  `Outputs` と `Inputs` を組み合わせて使用して、ターゲットが最新かどうかを確認します。 `Returns` がある場合、`Outputs` の値がオーバーライドされ、どの項目が呼び出し元に返されるかを判断できます。  `Returns` がない場合、前述のケースを除き、呼び出し元が `Outputs` を使用できるようになります。

 MSBuild 4 より前のバージョンでは、`Target` の `Outputs` に同じ項目に対する参照が複数ある場合は、常にそれらの重複項目が記録されていました。 出力数が多く、プロジェクトの相互依存関係が多数ある非常に大規模なビルドでは、無用な重複項目が原因で大量のメモリが無駄に使用されていました。 `KeepDuplicateOutputs` 属性が `true` に設定されている場合、この重複が記録されます。

## <a name="example"></a>例

 次のコード例では、`Csc` タスクを実行する `Target` 要素を示しています。

```xml
<Target Name="Compile" DependsOnTargets="Resources" Returns="$(TargetPath)">
    <Csc Sources="@(CSFile)"
          TargetType="library"
          Resources="@(CompiledResources)"
          EmitDebugInformation="$(includeDebugInformation)"
          References="@(Reference)"
          DebugType="$(debuggingType)" >
        <Output TaskParameter="OutputAssembly"
                  ItemName="FinalAssemblyName" />
    </Csc>
</Target>
```

## <a name="see-also"></a>関連項目

- [ターゲット](../msbuild/msbuild-targets.md)
- [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)

---
title: Task 要素の使用 (MSBuild) | Microsoft Docs
ms.date: 03/13/2017
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#UsingTask
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- UsingTask element [MSBuild]
- <UsingTask> element [MSBuild]
ms.assetid: 20247902-9446-4a1f-8253-5c7a17e4fe43
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 22d61fe30e9eb68697f073ca0bcfbcc515e513dd
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79431450"
---
# <a name="usingtask-element-msbuild"></a>UsingTask 要素 (MSBuild)

[Task](../msbuild/task-element-msbuild.md) 要素で参照されているタスクを、タスクの実装が含まれているアセンブリにマップします。

 \<Project> \<UsingTask>

## <a name="syntax"></a>構文

```xml
<UsingTask TaskName="TaskName"
    AssemblyName = "AssemblyName"
    TaskFactory = "ClassName"
    Condition="'String A'=='String B'" />
```

> [!NOTE]
> プロパティと項目とは異なり、`TaskName` に適用される "*最初*" の `UsingTask` 要素が使用されます。タスクをオーバーライドするには、新しい `UsingTask` を既存のものの "*前*" に定義する必要があります。

## <a name="attributes-and-elements"></a>属性と要素

 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`AssemblyName`|`AssemblyName` 属性と `AssemblyFile` 属性のどちらかが必要です。<br /><br /> 読み込むアセンブリの名前。 `AssemblyName` 属性は厳密な名前付きのアセンブリを受け取りますが、厳密な名前は必須ではありません。 この属性を使用すると、.NET の <xref:System.Reflection.Assembly.Load%2A> メソッドを使用してアセンブリを読み込む場合と同じ結果が得られます。<br /><br /> `AssemblyFile` 属性が使用されている場合、この属性は使用できません。|
|`AssemblyFile`|`AssemblyName` と `AssemblyFile` 属性のどちらかが必要です。<br /><br /> アセンブリのファイル パス。 この属性は、完全パスまたは相対パスを受け取ります。 相対パスは、`UsingTask` 要素が宣言されているプロジェクト ファイルまたはターゲット ファイルのディレクトリに対して相対的なパスです。 この属性を使用すると、.NET の <xref:System.Reflection.Assembly.LoadFrom%2A> メソッドを使用してアセンブリを読み込む場合と同じ結果が得られます。<br /><br /> `AssemblyName` 属性が使用されている場合、この属性は使用できません。|
|`TaskFactory`|省略可能な属性です。<br /><br /> 指定された `Task` 名のインスタンスの生成を担うアセンブリ内のクラスを指定します。  ユーザーは、タスク ファクトリが受信してタスクの生成に使用する子要素として、`Task` を指定することもできます。 `Task` の内容は、タスク ファクトリに固有のものです。|
|`TaskName`|必須の属性です。<br /><br /> アセンブリから参照するタスクの名前。 あいまいになる可能性がある場合、この属性は常に完全な名前空間を指定する必要があります。 あいまいさが存在する場合、MSBuild によって任意の一致が選択され、予期しない結果につながる可能性があります。|
|`Condition`|省略可能な属性です。<br /><br /> 評価する条件です。 詳細については、「[条件](../msbuild/msbuild-conditions.md)」を参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[ParameterGroup](../msbuild/parametergroup-element.md)|指定された `TaskFactory` によって生成されるタスクに表示されるパラメーターのセットです。|
|[Task](../msbuild/task-element-msbuild.md)|タスクのインスタンスを生成するために `TaskFactory` に渡されるデータです。|

### <a name="parent-elements"></a>親要素

| 要素 | 説明 |
| - | - |
| [プロジェクト](../msbuild/project-element-msbuild.md) | MSBuild プロジェクト ファイルの必須のルート要素です。 |

## <a name="remarks"></a>Remarks

 環境変数、コマンド ライン プロパティ、プロジェクト レベル プロパティ、およびプロジェクト レベル項目は、直接、またはインポートされたプロジェクト ファイルを通じて、プロジェクト ファイルに含まれる `UsingTask` 要素内で参照できます。 詳細については、[タスク](../msbuild/msbuild-tasks.md)に関する記事を参照してください。

> [!NOTE]
> MSBuild エンジンを使用してグローバルに登録された *.tasks* ファイルの 1 つから `UsingTask` 要素が使用されている場合、プロジェクトレベル プロパティおよび項目は意味を持ちません。 プロジェクト レベルの値は、MSBuild に対してグローバルなプロパティではありません。

 MSBuild 4.0 では、UsingTask を *.overridetask* ファイルから読み込むことができます。

カスタム タスクに含まれるアセンブリは、`Task` が最初に使用されたときに読み込まれます。

## <a name="example"></a>例

 次の例では、`AssemblyName` 属性で `UsingTask` 要素を使用する方法を示します。

```xml
<UsingTask TaskName="MyTask" AssemblyName="My.Assembly" TaskFactory="MyTaskFactory">
       <ParameterGroup>
              <Parameter1 ParameterType="System.String" Required="False" Output="False"/>
              <Parameter2 ParameterType="System.Int" Required="True" Output="False"/>
              ...
</ParameterGroup>
       <Task>
      ... Task factory-specific data ...
       </Task>
</UsingTask>
```

## <a name="example"></a>例

 次の例では、`AssemblyFile` 属性で `UsingTask` 要素を使用する方法を示します。

```xml
<UsingTask TaskName="Email"
              AssemblyFile="c:\myTasks\myTask.dll" />
```

## <a name="see-also"></a>関連項目

- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
- [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)

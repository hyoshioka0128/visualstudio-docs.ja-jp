---
title: Target の Task 要素 (MSBuild) | Microsoft Docs
description: MSBuild タスクのインスタンスを作成して実行する、MSBuild Target の Task 要素について説明します。
ms.custom: SEO-VS-2020
ms.date: 03/13/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Task element [MSBuild]
- <Task> element [MSBuild]
ms.assetid: d82e2485-e5f0-4936-a357-745bacccc299
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a4b8e3cb3acccc2e7ae4c6c2d93353bec79a3690
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99966046"
---
# <a name="task-element-of-target-msbuild"></a>Target の Task 要素 (MSBuild)

MSBuild タスクのインスタンスを作成して、実行します。 要素名は、作成されるタスクの名前によって決まります。

 \<Project> \<Target>

## <a name="syntax"></a>構文

```xml
<Task Parameter1="Value1"... ParameterN="ValueN"
    ContinueOnError="WarnAndContinue/true/ErrorAndContinue/ErrorAndStop/false"
    Condition="'String A' == 'String B'" >
    <Output... />
</Task>
```

## <a name="attributes-and-elements"></a>属性と要素

 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`Condition`|省略可能な属性です。 評価する条件です。 詳細については、「[条件](../msbuild/msbuild-conditions.md)」を参照してください。|
|`ContinueOnError`|省略可能な属性です。 次の値のいずれかを含めることができます。<br /><br /> -   **WarnAndContinue** または **true**。 タスクが失敗すると、[Target](../msbuild/target-element-msbuild.md) 要素の後続のタスクとビルドの実行が継続し、タスクのすべてのエラーが警告として扱われます。<br />-   **ErrorAndContinue**。 タスクが失敗すると、`Target` 要素の後続のタスクとビルドの実行が継続し、タスクのすべてのエラーがエラーとして扱われます。<br />-   **ErrorAndStop** または **false** (既定)。 タスクが失敗すると、`Target` 要素の残りのタスクとビルドは実行されず、`Target` 要素全体とビルドは失敗したと見なされます。<br /><br /> バージョン 4.5 より前の .NET Framework では、`true` 値と `false` 値のみがサポートされます。<br /><br /> 詳細については、「[方法:タスクで発生したエラーを無視する](../msbuild/how-to-ignore-errors-in-tasks.md)」を参照してください。|
|`Parameter`|タスク クラスに `[Required]` 属性のラベルが付けられた 1 つ以上のプロパティが含まれる場合は必須です。<br /><br /> パラメーター値とその値を含むユーザー定義のタスク パラメーターです。 `Task` 要素には任意の数のパラメーターを指定でき、各属性はタスク クラスの .NET プロパティにマップされます。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[出力](../msbuild/output-element-msbuild.md)|タスクからの出力をプロジェクト ファイルに格納します。 1 つのタスクに 0 個以上の `Output` 要素を指定できます。|

### <a name="parent-elements"></a>親要素

| 要素 | 説明 |
| - | - |
| [移行先](../msbuild/target-element-msbuild.md) | MSBuild タスクのコンテナー要素。 |

## <a name="remarks"></a>注釈

 MSBuild プロジェクト ファイル内の `Task` 要素では、タスクのインスタンスを作成し、そこにプロパティを設定して実行します。 `Output` 要素は、プロジェクト ファイル内の別の場所で使用するプロパティまたは項目に出力パラメーターを格納します。

 タスクの親 `Target` 要素に [OnError](../msbuild/onerror-element-msbuild.md) 要素がある場合は、タスクが失敗して `ContinueOnError` の値が `false` の場合も評価されます。 タスクについて詳しくは、「[MSBuild タスク](../msbuild/msbuild-tasks.md)」をご覧ください。

## <a name="example"></a>例

 次のコード例は、[Csc タスク](../msbuild/csc-task.md) クラスのインスタンスを作成し、6 つのプロパティを設定し、タスクを実行します。 実行後に、オブジェクトの `OutputAssembly` プロパティの値は `FinalAssemblyName` という項目一覧に配置されます。

```xml
<Target Name="Compile" DependsOnTarget="Resources" >
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

- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
- [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)

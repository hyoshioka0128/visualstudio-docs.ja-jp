---
title: タスクの作成 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, writing tasks
- tasks, creating for MSBuild
- MSBuild, creating tasks
ms.assetid: 3ebc5f87-8f00-46fc-82a1-228f35a6823b
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8cbcf47ec83e1b900ba94ab3842c2cfa63fdcc5d
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77631838"
---
# <a name="task-writing"></a>タスクの作成

タスクでは、ビルド プロセスの間に実行するコードを指定します。 タスクはターゲットに含まれます。 一般的なタスクのライブラリは MSBuild に付属します。また、独自のタスクを作成することもできます。 MSBuild に付属するタスクのライブラリの詳細については、[タスク リファレンス](../msbuild/msbuild-task-reference.md)を参照してください。

## <a name="tasks"></a>タスク

 タスクの例としては、1 つまたは複数のファイルをコピーする [Copy](../msbuild/copy-task.md)、ディレクトリを作成する [MakeDir](../msbuild/makedir-task.md)、C# ソース コード ファイルをコンパイルする [Csc](../msbuild/csc-task.md) などがあります。 各タスクは、*Microsoft.Build.Framework.dll* アセンブリで定義されている <xref:Microsoft.Build.Framework.ITask> インターフェイスを実装する .NET クラスとして実装されます。

 タスクを実装するには 2 つの方法があります。

- <xref:Microsoft.Build.Framework.ITask> インターフェイスを直接実装します。

- *Microsoft.Build.Utilities.dll* アセンブリで定義されているヘルパー クラス <xref:Microsoft.Build.Utilities.Task> からクラスを継承します。 Task は ITask を実装し、一部の ITask メンバーの既定の実装を提供します。 また、ログは簡単に記録できます。

いずれの場合でも、クラスを `Execute` という名前のメソッドに追加する必要があります。これは、タスクの実行時に呼び出されるメソッドです。 このメソッドはパラメーターを取らず、`Boolean` 値を返します。タスクが成功した場合は `true` を、失敗した場合は `false` を返します。 次は、何のアクションも実行せず、`true` を返すタスクの例です。

```csharp
using System;
using Microsoft.Build.Framework;
using Microsoft.Build.Utilities;

namespace MyTasks
{
    public class SimpleTask : Task
    {
        public override bool Execute()
        {
            return true;
        }
    }
}
```

 次のプロジェクト ファイルはこのタスクを実行します。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Target Name="MyTarget">
        <SimpleTask />
    </Target>
</Project>
```

 タスクが実行されるとき、タスク クラスで .NET プロパティを作成する場合、プロジェクト ファイルからも入力を受け取ります。 MSBuild により、タスクの `Execute` メソッドを呼び出す直前にこれらのプロパティが設定されます。 文字列プロパティを作成するには、次のようなタスク コードを使用します。

```csharp
using System;
using Microsoft.Build.Framework;
using Microsoft.Build.Utilities;

namespace MyTasks
{
    public class SimpleTask : Task
    {
        public override bool Execute()
        {
            return true;
        }

        public string MyProperty { get; set; }
    }
}
```

 次のプロジェクト ファイルはこのタスクを実行し、与えられた値に `MyProperty` を設定します。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
   <Target Name="MyTarget">
      <SimpleTask MyProperty="Value for MyProperty" />
   </Target>
</Project>
```

## <a name="register-tasks"></a>登録タスク

 プロジェクトでタスクを実行する場合、そのタスク クラスが含まれているアセンブリを見つける方法が MSBuild によって認識されている必要があります。 タスクは [UsingTask 要素 (MSBuild)](../msbuild/usingtask-element-msbuild.md) で登録されます。

 MSBuild ファイルの *Microsoft.Common.Tasks* は、MSBuild に付属するすべてのタスクを登録する `UsingTask` 要素の一覧が含まれるプロジェクト ファイルです。 このファイルは、あらゆるプロジェクトのビルド時に自動的に追加されます。 *Microsoft.Common.Tasks* に登録されているタスクが現在のプロジェクト ファイルにも登録されている場合、現在のプロジェクト ファイルに優先権が与えられます。つまり、既定のタスクが、同じ名前を持つ独自のタスクでオーバーライドされます。

> [!TIP]
> *Microsoft.Common.Tasks* のコンテンツを表示することで、MSBuild に付属するタスクの一覧を確認できます。

## <a name="raise-events-from-a-task"></a>タスクからイベントを生成する

 タスクが <xref:Microsoft.Build.Utilities.Task> ヘルパー クラスから派生する場合、<xref:Microsoft.Build.Utilities.Task> クラスで次のいずれかのヘルパー メソッドを利用して生成したイベントは、登録されているあらゆるロガーで記録され、表示されます。

```csharp
public override bool Execute()
{
    Log.LogError("messageResource1", "1", "2", "3");
    Log.LogWarning("messageResource2");
    Log.LogMessage(MessageImportance.High, "messageResource3");
    ...
}
```

 このようなイベントは、タスクが <xref:Microsoft.Build.Framework.ITask> を直接実装する場合でも生成できますが、IBuildEngine インターフェイスを利用する必要があります。 次は、ITask を実装し、カスタム イベントを生成するタスクの例です。

```csharp
public class SimpleTask : ITask
{
    public IBuildEngine BuildEngine { get; set; }

    public override bool Execute()
    {
        TaskEventArgs taskEvent =
            new TaskEventArgs(BuildEventCategory.Custom,
            BuildEventImportance.High, "Important Message",
           "SimpleTask");
        BuildEngine.LogBuildEvent(taskEvent);
        return true;
    }
}
```

## <a name="require-task-parameters-to-be-set"></a>タスク パラメーターの設定を要求する

 特定のタスク プロパティを "必須" に設定できます。必須にすると、タスクを実行するプロジェクト ファイルで、必須のプロパティに値を設定する必要があります。設定しないと、ビルドに失敗します。 次のように、タスクの .NET プロパティに `[Required]` 属性を適用します。

```csharp
[Required]
public string RequiredProperty { get; set; }
```

 `[Required]` 属性は <xref:Microsoft.Build.Framework> 名前空間の <xref:Microsoft.Build.Framework.RequiredAttribute> によって定義されます。

## <a name="how-msbuild-invokes-a-task"></a>MSBuild によるタスクの呼び出し方法

タスクを呼び出すと、まず MSBuild によってタスク クラスがインスタンス化され、次にプロジェクト ファイルのタスク要素内に設定されているタスク パラメーター用のオブジェクトのプロパティ セッターが呼び出されます。 タスク要素によってパラメーターが指定されていない場合、または要素内で指定された式によって空の文字列であると評価された場合、プロパティ セッターは呼び出されません。

たとえば、プロジェクトでは次のようになります

```xml
<Project>
 <Target Name="InvokeCustomTask">
  <CustomTask Input1=""
              Input2="$(PropertyThatIsNotDefined)"
              Input3="value3" />
 </Target>
</Project>
```

`Input3` のセッターのみが呼び出されます。

タスクは、パラメータープロパティ セッター呼び出しの相対順序に依存しないようにする必要があります。

### <a name="task-parameter-types"></a>タスク パラメーターの型

MSBuild では、`string`、`bool`、`ITaskItem`、`ITaskItem[]` 型のプロパティがネイティブに処理されます。 タスクが別の型のパラメーターを受け入れる場合、MSBuild によって <xref:System.Convert.ChangeType%2A> が呼び出され、`string` から (すべてのプロパティと項目の参照が展開された状態で) 変換先の型に変換されます。 入力パラメーターの変換に失敗した場合、MSBuild によってエラーが出力されます。タスクの `Execute()` メソッドは呼び出されません。

## <a name="example"></a>例

### <a name="description"></a>説明

次の C# クラスは、<xref:Microsoft.Build.Utilities.Task> ヘルパー クラスから派生したタスクを示しています。 このタスクは成功を示す `true` を返します。

### <a name="code"></a>コード

```csharp
using System;
using Microsoft.Build.Utilities;

namespace SimpleTask1
{
    public class SimpleTask1: Task
    {
        public override bool Execute()
        {
            // This is where the task would presumably do its work.
            return true;
        }
    }
}
```

## <a name="example"></a>例

### <a name="description"></a>説明

次の C# クラスは、<xref:Microsoft.Build.Framework.ITask> インターフェイスを実装するタスクを示しています。 このタスクは成功を示す `true` を返します。

### <a name="code"></a>コード

```csharp
using System;
using Microsoft.Build.Framework;

namespace SimpleTask2
{
    public class SimpleTask2: ITask
    {
        //When implementing the ITask interface, it is necessary to
        //implement a BuildEngine property of type
        //Microsoft.Build.Framework.IBuildEngine. This is done for
        //you if you derive from the Task class.
        public IBuildEngine BuildEngine { get; set; }

        // When implementing the ITask interface, it is necessary to
        // implement a HostObject property of type object.
        // This is done for you if you derive from the Task class.
        public object HostObject { get; set; }

        public bool Execute()
        {
            // This is where the task would presumably do its work.
            return true;
        }
    }
}
```

## <a name="example"></a>例

### <a name="description"></a>説明

この C# クラスは、<xref:Microsoft.Build.Utilities.Task> ヘルパー クラスから派生したタスクを示しています。 必須の文字列プロパティがあり、登録されているすべてのロガーで表示されるイベントを生成します。

### <a name="code"></a>コード

[!code-csharp[msbuild_SimpleTask3#1](../msbuild/codesnippet/CSharp/task-writing_1.cs)]

## <a name="example"></a>例

### <a name="description"></a>説明

次は、前のサンプル タスク SimpleTask3 を呼び出すプロジェクト ファイルの例です。

### <a name="code"></a>コード

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <UsingTask TaskName="SimpleTask3.SimpleTask3"
        AssemblyFile="SimpleTask3\bin\debug\simpletask3.dll"/>

    <Target Name="MyTarget">
        <SimpleTask3 MyProperty="Hello!"/>
    </Target>
</Project>
```

## <a name="see-also"></a>関連項目

- [タスク リファレンス](../msbuild/msbuild-task-reference.md)

---
title: Copy タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Copy
- MSBuild.Copy.SourceFileNotFound
- MSBuild.Copy.Retrying
- MSBuild.Copy.ExceededRetries
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, Copy task
- Copy task [MSBuild]
ms.assetid: a46ba9da-3e4e-4890-b4ea-09a099b6bc40
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 28fd0033f5ef6f83ca29432f95d6b635fcd36116
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77634371"
---
# <a name="copy-task"></a>Copy タスク

ファイルをファイル システム上の新しい場所にコピーします。

## <a name="parameters"></a>パラメーター

`Copy` タスクのパラメーターの説明を次の表に示します。

|パラメーター|[説明]|
|---------------|-----------------|
|`CopiedFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> 正常にコピーされた項目が含まれます。これには、実際にはコピーされていないけれども、既に最新の状態であり、`SkipUnchangedFiles` が `true` であったためにスキップされたものも*含まれます*。|
|`DestinationFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> ソース ファイルのコピー先ファイルの一覧を指定します。 この一覧のファイルは、`SourceFiles` パラメーターに指定した一覧の内容と 1 対 1 で対応している必要があります。 つまり、`SourceFiles` の最初のファイルは、`DestinationFiles` の最初の場所にコピーされ、2 番目以降のファイルも同様に処理されます。|
|`DestinationFolder`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> ファイルのコピー先ディレクトリを指定します。 ファイルではなく、ディレクトリである必要があります。 ディレクトリが存在しない場合は、自動的に作成されます。|
|`OverwriteReadOnlyFiles`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> ファイルが読み取り専用としてマークされている場合でも、ファイルを上書きします。|
|`Retries`|省略可能な `Int32` 型のパラメーターです。<br /><br /> コピーに失敗した場合の再試行回数を指定します。 既定値はゼロです。<br /><br /> **メモ:** 再試行を行った場合、ビルド処理で同期の問題が生じる可能性があるので注意してください。|
|`RetryDelayMilliseconds`|省略可能な `Int32` 型のパラメーターです。<br /><br /> 再試行の間隔を指定します。 既定値は RetryDelayMillisecondsDefault 引数であり、これが CopyTask コンストラクターに渡されます。|
|`SkipUnchangedFiles`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` に設定すると、コピー元のファイルとコピー先のファイルで変更がない場合、コピー処理がスキップされます。 `Copy` タスクでは、ファイルのサイズが等しく、最終更新時刻が等しい場合、ファイルは変更されていないと見なされます。 <br /><br /> **メモ:** このパラメーターに `true` を設定した場合は、コピー先のファイルに対して依存関係分析を行わないでください。この設定を行った場合には、ソース ファイルの最終更新時刻が、コピー先のファイルの最終更新時刻よりも新しい場合にだけ、タスクが実行されるためです。|
|`SourceFiles`|必須の <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> コピー元となるファイルを指定します。|
|`UseHardlinksIfPossible`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、ファイルがコピーされるのではなく、コピーされたファイルのハード リンクが作成されます。|

## <a name="warnings"></a>警告

次のような警告が記録されます。

- `Copy.DestinationIsDirectory`

- `Copy.SourceIsDirectory`

- `Copy.SourceFileNotFound`

- `Copy.CreatesDirectory`

- `Copy.HardLinkComment`

- `Copy.RetryingAsFileCopy`

- `Copy.FileComment`

- `Copy.RemovingReadOnlyAttribute`

## <a name="remarks"></a>解説

`DestinationFolder` パラメーターか `DestinationFiles` パラメーターのいずれかを指定する必要がありますが、両方は指定できません。 両方を指定した場合、タスクは失敗し、エラーがログに記録されます。

上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="example"></a>例

`MySourceFiles` アイテム コレクション内のアイテムを *C:\MyProject\Destination* にコピーする例を次に示します。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <MySourceFiles Include="a.cs;b.cs;c.cs"/>
    </ItemGroup>

    <Target Name="CopyFiles">
        <Copy
            SourceFiles="@(MySourceFiles)"
            DestinationFolder="c:\MyProject\Destination"
        />
    </Target>

</Project>
```

## <a name="example"></a>例

再帰的なコピーを行う方法を次の例に示します。 このプロジェクトでは、*C:\MySourceTree* から *C:\MyDestinationTree* に、ディレクトリ構造を維持しながら、すべてのファイルが再帰的にコピーされます。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <MySourceFiles Include="c:\MySourceTree\**\*.*"/>
    </ItemGroup>

    <Target Name="CopyFiles">
        <Copy
            SourceFiles="@(MySourceFiles)"
            DestinationFiles="@(MySourceFiles->'c:\MyDestinationTree\%(RecursiveDir)%(Filename)%(Extension)')"
        />
    </Target>

</Project>
```

## <a name="see-also"></a>参照

- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)

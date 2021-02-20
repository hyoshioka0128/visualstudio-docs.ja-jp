---
title: '方法 : ビルドをクリーンする | Microsoft Docs'
description: MSBuild を使用してビルドをクリーンする方法について説明します。すべての中間ファイルと出力ファイルが削除され、プロジェクト ファイルとコンポーネント ファイルだけが残ります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Exec task [MSBuild]
- MSBuild, cleaning a build
- directories [.NET Framework], for output items
- output, removing items
ms.assetid: 999ba473-b0c4-45c7-930a-63ea7a510509
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e6c0beb70379d8b79a3e1826ba74f34202eea19f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99914450"
---
# <a name="how-to-clean-a-build"></a>方法: ビルドをクリーンする

ビルドをクリーンするとき、すべての中間ファイルと出力ファイルが削除され、プロジェクト ファイルとコンポーネント ファイルが残ります。 プロジェクト ファイルとコンポーネント ファイルから、中間ファイルと出力ファイルの新しいインスタンスをビルドできます。 

## <a name="create-a-directory-for-output-items"></a>出力項目のディレクトリを作成するには

 既定では、プロジェクトのコンパイル時に作成される *.exe* ファイルは、プロジェクトおよびソース ファイルと同じディレクトリに置かされます。 ただし、一般的には、出力項目は別個のディレクトリに作成されます。

### <a name="to-create-a-directory-for-output-items"></a>出力項目のディレクトリを作成するには

1. `Property` 要素を利用し、ディレクトリの場所と名前を定義します。 たとえば、プロジェクトおよびソースファイルを含むディレクトリに *BuiltApp* という名前のディレクトリを作成します。

     `<builtdir>BuiltApp</builtdir>`

2. ディレクトリが存在しない場合、[MakeDir](../msbuild/makedir-task.md) タスクを理使用してディレクトリを作成します。 次に例を示します。

     ```xml
     <MakeDir Directories = "$(builtdir)"
      Condition = "!Exists('$(builtdir)')" />
     ```

## <a name="remove-the-output-items"></a>出力項目を削除する

 中間ファイルと出力ファイルの新しいインスタンスを作成する前に、以前のインスタンスをすべて消去しておくことをお勧めします。 [RemoveDir](../msbuild/removedir-task.md) タスクを利用し、ディレクトリとそれに含まれるすべてのファイルとディレクトリをディスクから削除します。

#### <a name="to-remove-a-directory-and-all-files-contained-in-the-directory"></a>ディレクトリとそのディレクトリに含まれるすべてのファイルを削除するには

- `RemoveDir` タスクを利用してディレクトリを削除します。 次に例を示します。

     `<RemoveDir Directories="$(builtdir)" />`

## <a name="example"></a>例

 次のコード例プロジェクトには、新しいターゲット、`Clean` が含まれています。このターゲットは `RemoveDir` タスクを使用し、ディレクトリとそのディレクトリに含まれるすべてのファイルを削除します。 この例ではまた、`Compile` ターゲットは、ビルドのクリーン時に削除される出力項目に対して別個のディレクトリを作成します。

 `Compile` は既定のターゲットとして定義されます。そのため、別のターゲットを指定しない限り、自動的に使用されます。 コマンド ライン スイッチ **-target** を使用し、別のターゲットを指定します。 次に例を示します。

 `msbuild <file name>.proj -target:Clean`

 **-target** スイッチは **-t** に短縮できます。また、複数のターゲットを指定できます。 たとえば、ターゲット `Clean` を使用し、次にターゲット `Compile` を使用するには、次のように入力します。

 `msbuild <file name>.proj -t:Clean;Compile`

```xml
<Project DefaultTargets = "Compile"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >

    <PropertyGroup>
        <!-- Set the application name as a property -->
        <name>HelloWorldCS</name>

        <!-- Set the output folder as a property -->
        <builtdir>BuiltApp</builtdir>
    </PropertyGroup>

    <ItemGroup>
        <!-- Specify the inputs by type and file name -->
        <CSFile Include = "consolehwcs1.cs"/>
    </ItemGroup>

    <Target Name = "Compile">
        <!-- Check whether an output folder exists and create
        one if necessary -->
        <MakeDir Directories = "$(builtdir)"
            Condition = "!Exists('$(builtdir)')" />

        <!-- Run the Visual C# compiler -->
        <CSC Sources = "@(CSFile)"
            OutputAssembly = "$(BuiltDir)\$(appname).exe">
            <Output TaskParameter = "OutputAssembly"
                ItemName = "EXEFile" />
        </CSC>

        <!-- Log the file name of the output file -->
        <Message Text="The output file is @(EXEFile)"/>
    </Target>

    <Target Name = "Clean">
        <RemoveDir Directories="$(builtdir)" />
    </Target>
</Project>
```

## <a name="see-also"></a>関連項目

- [MakeDir タスク](../msbuild/makedir-task.md)
- [RemoveDir タスク](../msbuild/removedir-task.md)
- [Csc タスク](../msbuild/csc-task.md)
- [ターゲット](../msbuild/msbuild-targets.md)

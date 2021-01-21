---
title: '方法: ビルドするファイルを選択する | Microsoft Docs'
description: 各ファイルを個別にリストするか、ワイルドカードを使用して、MSBuild プロジェクト ファイルでビルドするファイルを選択する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, wildcards
- MSBuild, including files
- Include attribute [MSBuild]
ms.assetid: f5ff182f-7b3a-46fb-9335-37df54cfb8eb
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4593fff50feb0176ea81f70dc297bc39d8dd1936
ms.sourcegitcommit: c4927ef8fe239005d7feff6c5a7707c594a7a05c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92436203"
---
# <a name="how-to-select-the-files-to-build"></a>方法: ビルドするファイルを選択する

複数のファイルを含むプロジェクトをビルドするときに、各ファイルを個別にプロジェクト ファイルにリストしたり、ワイルドカードを使用して、1 つのディレクトリまたは入れ子になった一連のディレクトリ内のすべてのファイルを含めたりすることができます。

## <a name="specify-inputs"></a>入力を指定する

項目は、ビルドの入力を表します。 項目の詳細については、「[MSBuild 項目](../msbuild/msbuild-items.md)」をご覧ください。

ビルドにファイルを含めるには、それらが MSBuild プロジェクト ファイルの項目一覧に含まれている必要があります。 複数のファイルを項目リストに追加するには、ファイルを個別に含めるか、ワイルドカードを使用して一度に複数のファイルを含めます。

#### <a name="to-declare-items-individually"></a>項目を個別に宣言するには

- 次のような `Include` 属性を使用します。

    `<CSFile Include="form1.cs"/>`

    or

    `<VBFile Include="form1.vb"/>`

    > [!NOTE]
    > 項目コレクション内の項目がプロジェクト ファイルと同じディレクトリにない場合は、その項目への完全パスまたは相対パスを指定する必要があります。 (例: `Include="..\..\form2.cs"`)。

#### <a name="to-declare-multiple-items"></a>複数の項目を宣言するには

- 次のような `Include` 属性を使用します。

    `<CSFile Include="form1.cs;form2.cs"/>`

    or

    `<VBFile Include="form1.vb;form2.vb"/>`

## <a name="specify-inputs-with-wildcards"></a>ワイルドカードを使用して入力を指定する

ワイルドカードを使用して、すべてのファイルまたはサブディレクトリから特定のファイルのみを再帰的に含めることができます。 ワイルドカードの詳細については、「[MSBuild 項目](../msbuild/msbuild-items.md)」をご覧ください。

次の例は、次のディレクトリとサブディレクトリ内のグラフィック ファイルを含むプロジェクトに基づいており、プロジェクト ファイルは *Project* ディレクトリに配置されています。

*Project\Images\BestJpgs*

*Project\Images\ImgJpgs*

*Project\Images\ImgJpgs\Img1*

#### <a name="to-include-all-jpg-files-in-the-images-directory-and-subdirectories"></a>*Images* ディレクトリとサブディレクトリ内のすべての *.jpg* ファイルを含めるには

- 次の `Include` 属性を使用します。

    `Include="Images\**\*.jpg"`

#### <a name="to-include-all-jpg-files-starting-with-img"></a>*img* で始まるすべての *.jpg* ファイルを含めるには

- 次の `Include` 属性を使用します。

    `Include="Images\**\img*.jpg"`

#### <a name="to-include-all-files-in-directories-with-names-ending-in-jpgs"></a>ディレクトリ内の *jpg* で終わる名前を持つすべてのファイルを含めるには

- 次のいずれかの `Include` 属性を使用します。

    `Include="Images\**\*jpgs\*.*"`

    or

    `Include="Images\**\*jpgs\*"`

## <a name="pass-items-to-a-task"></a>項目をタスクに渡す

プロジェクト ファイルでは、タスクで @() の表記を使用して、項目リスト全体をビルドの入力として指定できます。 この表記を使用して、すべてのファイルを個別にリストすることも、ワイルドカードを使用することもできます。

#### <a name="to-use-all-visual-c-or-visual-basic-files-as-inputs"></a>すべての Visual C# ファイルまたは Visual Basic ファイルを入力として使用するには

- 次のような `Include` 属性を使用します。

    `<CSC Sources="@(CSFile)">...</CSC>`

    or

    `<VBC Sources="@(VBFile)">...</VBC>`

> [!NOTE]
> ワイルドカードと項目を使用して、ビルドの入力を指定する必要があります。MSBuild タスクの `Sources` 属性 ([Csc](../msbuild/csc-task.md) や[Vbc](../msbuild/vbc-task.md) など) を使用して入力を指定することはできません。 次の例はプロジェクト ファイルでは無効です。
>
> `<CSC Sources="*.cs">...</CSC>`

## <a name="example-1"></a>例 1

次のコード例では、すべての入力ファイルを個別に含むプロジェクトを示します。

```xml
<Project DefaultTargets="Compile"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >
    <PropertyGroup>
        <Builtdir>built</Builtdir>
    </PropertyGroup>

    <ItemGroup>
        <CSFile Include="Form1.cs"/>
        <CSFile Include="AssemblyInfo.cs"/>

        <Reference Include="System.dll"/>
        <Reference Include="System.Data.dll"/>
        <Reference Include="System.Drawing.dll"/>
        <Reference Include="System.Windows.Forms.dll"/>
        <Reference Include="System.XML.dll"/>
    </ItemGroup>

    <Target Name="PreBuild">
        <Exec Command="if not exist $(builtdir) md $(builtdir)"/>
    </Target>

    <Target Name="Compile" DependsOnTargets="PreBuild">
        <Csc Sources="@(CSFile)"
            References="@(Reference)"
            OutputAssembly="$(builtdir)\$(MSBuildProjectName).exe"
            TargetType="exe" />
    </Target>
</Project>
```

## <a name="example-2"></a>例 2

次のコード例では、ワイルドカードを使用してすべての *.cs* ファイルを含めます。

```xml
<Project DefaultTargets="Compile"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >

    <PropertyGroup>
        <builtdir>built</builtdir>
    </PropertyGroup>

    <ItemGroup>
        <CSFile Include="*.cs"/>

        <Reference Include="System.dll"/>
        <Reference Include="System.Data.dll"/>
        <Reference Include="System.Drawing.dll"/>
        <Reference Include="System.Windows.Forms.dll"/>
        <Reference Include="System.XML.dll"/>
    </ItemGroup>

    <Target Name="PreBuild">
        <Exec Command="if not exist $(builtdir) md $(builtdir)"/>
    </Target>

    <Target Name="Compile" DependsOnTargets="PreBuild">
        <Csc Sources="@(CSFile)"
            References="@(Reference)"
            OutputAssembly="$(builtdir)\$(MSBuildProjectName).exe"
            TargetType="exe" />
    </Target>
</Project>
```

## <a name="see-also"></a>関連項目

- [方法: ビルドからファイルを除外する](../msbuild/how-to-exclude-files-from-the-build.md)
- [項目](../msbuild/msbuild-items.md)

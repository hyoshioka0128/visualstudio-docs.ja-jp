---
title: プロジェクト ファイルの名前または場所を参照する
description: MSBuild の予約済みプロパティを使用して、独自のプロパティを作成せずにプロジェクト ファイルの名前または場所を参照する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- locations, referencing
- locations
- MSBuildProjectName property
- MSBuild, referencing the project file
- names, referencing
- reserved properties
- project files, referencing
ms.assetid: c8fcc594-5d37-4e2e-b070-4d9c012043b5
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c6527a4f54abf147d54e73c8f887b57b70ff4243
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99914190"
---
# <a name="how-to-reference-the-name-or-location-of-the-project-file"></a>方法: プロジェクト ファイルの名前または場所を参照する

独自のプロパティを作成することなく、プロジェクト ファイル自体のプロジェクトの名前または場所を使用できます。 MSBuild には、プロジェクト ファイル名とプロジェクトに関連するその他のプロパティを参照する、予約済みのプロパティが用意されています。 予約済みのプロパティの詳細については、「[MSBuild の予約済みおよび既知のプロパティ](../msbuild/msbuild-reserved-and-well-known-properties.md)」を参照してください。

## <a name="use-the-project-properties"></a>プロジェクトのプロパティを使用する

 MSBuild には、毎回定義することなくプロジェクト ファイル内で使用できる、いくつかの予約済みプロパティが用意されています。 たとえば、予約済みプロパティ `MSBuildProjectName` はプロジェクト ファイル名への参照を提供します。 予約済みプロパティ `MSBuildProjectDirectory` はプロジェクト ファイルの場所への参照を提供します。

#### <a name="to-use-the-project-properties"></a>プロジェクトのプロパティを使用するには

- 他のすべてのプロパティの場合と同様に、$() 表記でプロジェクト ファイルのプロパティを参照します。 次に例を示します。

  ```xml
  <CSC Sources = "@(CSFile)"
      OutputAssembly = "$(MSBuildProjectName).exe"/>
  </CSC>
  ```

  予約済みのプロパティを使用する利点は、プロジェクト ファイル名への変更がすべて自動的に組み込まれることです。 次回プロジェクトをビルドするとき、出力ファイルに新しい名前が付けられ、追加の操作は必要ありません。

  ファイル参照またはプロジェクト参照での特殊文字の使用の詳細については、「[MSBuild の特殊文字](../msbuild/msbuild-special-characters.md)」を参照してください。

> [!NOTE]
> 予約済みのプロパティは、プロジェクト ファイルで再定義できません。

## <a name="example-1"></a>例 1

 次の例では、プロジェクト ファイルは出力の名前を指定する予約済みのプロパティとして、プロジェクト名を参照します。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003"
    DefaultTargets = "Compile">

    <!-- Specify the inputs -->
    <ItemGroup>
        <CSFile Include = "consolehwcs1.cs"/>
     </ItemGroup>
    <Target Name = "Compile">
        <!-- Run the Visual C# compilation using
        input files of type CSFile -->
        <CSC Sources = "@(CSFile)"
            OutputAssembly = "$(MSBuildProjectName).exe" >
            <!-- Set the OutputAssembly attribute of the CSC task
            to the name of the project -->
            <Output
                TaskParameter = "OutputAssembly"
                ItemName = "EXEFile" />
        </CSC>
        <!-- Log the file name of the output file -->
        <Message Text="The output file is @(EXEFile)"/>
    </Target>
</Project>
```

## <a name="example-2"></a>例 2

 次のプロジェクト ファイルの例では、`MSBuildProjectDirectory` 予約済みプロパティを使用して、プロジェクト ファイルの場所にあるファイルへの完全パスを作成します。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <!-- Build the path to a file in the root of the project -->
    <PropertyGroup>
        <NewFilePath>$([System.IO.Path]::Combine($(MSBuildProjectDirectory), `BuildInfo.txt`))</NewFilePath>
    </PropertyGroup>
</Project>
```

この例では、[プロパティ関数](property-functions.md)の構文を使用して、静的な .NET Framework メソッド <xref:System.IO.Path.Combine*?displayProperty=fullName> を呼び出しています。

## <a name="see-also"></a>関連項目

- [MSBuild](../msbuild/msbuild.md)
- [MSBuild の予約済みおよび既知のプロパティ](../msbuild/msbuild-reserved-and-well-known-properties.md)

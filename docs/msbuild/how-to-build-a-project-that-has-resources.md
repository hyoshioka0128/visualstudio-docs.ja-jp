---
title: '方法: リソースがあるプロジェクトをビルドする | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- resource files, compiling with MSBuild
- resources [Visual Studio], compiling with MSBuild
- projects [.NET Framework], building
- MSBuild, building a project with resources
ms.assetid: d07ac73f-2c2d-4e9a-812a-6dcb632bafe2
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a76246096eec8779ce331e93f01be5ab791d1cdb
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77633955"
---
# <a name="how-to-build-a-project-that-has-resources"></a>方法: リソースがあるプロジェクトをビルドする

プロジェクトのローカライズ版を作成する場合、すべてのユーザー インターフェイス要素を言語別のリソース ファイルに分ける必要があります。 プロジェクトが文字列だけを使用している場合、リソース ファイルとしてテキスト ファイルを使用できます。 あるいは、 *.resx* ファイルをリソース ファイルとして使用することもできます。

## <a name="compile-resources-with-msbuild"></a>MSBuild を使用してリソースをコンパイルする

MSBuild とともに提供されている一般的なタスクのライブラリには、 *.resx* ファイルまたはテキスト ファイルのリソースのコンパイルに利用できる `GenerateResource` タスクが含まれています。 このタスクには、どのリソース ファイルをコンパイルするかを指定する `Sources` パラメーターと、出力リソース ファイルの名前を指定する `OutputResources` パラメーターが含まれています。 `GenerateResource` タスクの詳細については、「[GenerateResource タスク](../msbuild/generateresource-task.md)」を参照してください。

#### <a name="to-compile-resources-with-msbuild"></a>MSBuild を使用してリソースをコンパイルするには

1. プロジェクトのリソース ファイルを識別し、項目一覧かファイル名として `GenerateResource` タスクに渡します。

2. `GenerateResource` タスクの `OutputResources` パラメーターを指定します。これによって、出力リソース ファイルに名前を設定できます。

3. `OutputResources` パラメーターの値を項目に保存するため、タスクの `Output` 要素を使用します。

4. `Output` 要素から作成された項目を別のタスクへの入力として使用します。

## <a name="example"></a>例

次のコード例では、コンパイルされたリソース ファイルである *alpha.resources* と *beta.resources* を `GenerateResource` タスクの `OutputResources` 属性に含めることと、これらの 2 ファイルを `Resources` 項目一覧に含めることを、`Output` 要素によってどのように指定するかを示します。 それらの *.resources* ファイルを同名の項目の集合として識別すれば、[Csc](../msbuild/csc-task.md) タスクのような別のタスクの入力として簡単に使用することができます。

このタスクは、[Resgen.exe](/dotnet/framework/tools/resgen-exe-resource-file-generator) の **/compile** スイッチを使用するのと同じことです。

`Resgen.exe /compile alpha.resx,alpha.resources /compile beta.txt,beta.resources`

```xml
<GenerateResource
    Sources="alpha.resx; beta.txt"
    OutputResources="alpha.resources; beta.resources">
    <Output TaskParameter="OutputResources"
        ItemName="Resources"/>
</GenerateResource>
```

## <a name="example"></a>例

次のプロジェクト例には、リソースをコンパイルする `GenerateResource` タスクと、ソース コード ファイルとコンパイルされたリソース ファイルの両方をコンパイルする `Csc` タスクの 2 つのタスクが含まれています。 `GenerateResource` タスクでコンパイルされたリソース ファイルは `Resources` 項目に保存され、`Csc` タスクに渡されます。

```xml
<Project DefaultTargets = "Build"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >

    <Target Name="Resources">
        <GenerateResource
            Sources="alpha.resx; beta.txt"
            OutputResources="alpha.resources; beta.resources">
            <Output TaskParameter="OutputResources"
                ItemName="Resources"/>
        </GenerateResource>
    </Target>

    <Target Name="Build" DependsOnTargets="Resources">
        <Csc Sources="hello.cs"
                Resources="@(Resources)"
                OutputAssembly="hello.exe"/>
    </Target>
</Project>
```

## <a name="see-also"></a>関連項目

- [MSBuild](../msbuild/msbuild.md)
- [GenerateResource タスク](../msbuild/generateresource-task.md)
- [Csc タスク](../msbuild/csc-task.md)
- [Resgen.exe (リソース ファイル ジェネレーター)](/dotnet/framework/tools/resgen-exe-resource-file-generator)

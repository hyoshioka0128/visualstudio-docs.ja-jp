---
title: T4 アセンブリディレクティブ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 44949749-ce3c-4fb5-8690-a17f1564ac2f
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: bc0e6e7e1530abb63beabc6fa4aedd4a0fa985af
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672334"
---
# <a name="t4-assembly-directive"></a>T4 アセンブリ ディレクティブ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のデザイン時テキスト テンプレートでは、テンプレート コードでアセンブリの型を使用できるように、`assembly` ディレクティブによってアセンブリが読み込まれます。 結果は、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクトでアセンブリ参照を追加した場合と同様です。

 テキストテンプレートの記述の概要については、「 [T4 テキストテンプレートの作成](../modeling/writing-a-t4-text-template.md)」を参照してください。

> [!NOTE]
> 実行時 (前処理された) テキスト テンプレートでは、`assembly` ディレクティブは不要です。 代わりに、必要なアセンブリをプロジェクトの **参照** に追加し [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。

## <a name="using-the-assembly-directive"></a>assembly ディレクティブの使用
 ディレクティブの構文は次のとおりです。

```
<#@ assembly name="[assembly strong name|assembly file name]" #>
```

 アセンブリ名は、次のいずれかであることが必要です。

- GAC のアセンブリの厳密な名前 (`System.Xml.dll` など)。 `name="System.Xml, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"` のような長い形式を使用することもできます。 詳細については、「<xref:System.Reflection.AssemblyName>」を参照してください。

- アセンブリの絶対パス。

  `$(variableName)` 構文を使用して、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の変数 (`$(SolutionDir)` など) を参照し、`%VariableName%` を使用して環境変数を参照できます。 次に例を示します。

```
<#@ assembly name="$(SolutionDir)\MyProject\bin\Debug\SomeLibrary.Dll" #>
```

 assembly ディレクティブは、前処理されたテキスト テンプレートでは無効です。 代わりに、必要な参照をプロジェクトの [ **参照** ] セクションに含め [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。 詳細については、「 [T4 テキストテンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)」を参照してください。

## <a name="standard-assemblies"></a>標準アセンブリ
 次のアセンブリは自動的に読み込まれるので、これらのアセンブリのアセンブリ ディレクティブを記述する必要はありません。

- `Microsoft.VisualStudio.TextTemplating.1*.dll`

- `System.dll`

- `WindowsBase.dll`

  カスタム ディレクティブを使用する場合は、ディレクティブ プロセッサによって追加のアセンブリが読み込まれます。 たとえば、ドメイン固有言語 (DSL) のテンプレートを作成した場合、次のアセンブリのアセンブリ ディレクティブを記述する必要はありません。

- `Microsoft.VisualStudio.Modeling.Sdk.1*.dll`

- `Microsoft.VisualStudio.Modeling.Sdk.Diagrams.1*.dsl`

- `Microsoft.VisualStudio.TextTemplating.Modeling.1*.dll`

- DSL を含むアセンブリ

## <a name="using-project-properties-in-both-msbuild-and-visual-studio"></a><a name="msbuild"></a> MSBuild と Visual Studio の両方でのプロジェクトプロパティの使用
 $(SolutionDir) などの Visual Studio のマクロは、MSBuild では動作しません。 ビルド コンピューターでテンプレートを変換する場合、代わりにプロジェクトのプロパティを使用する必要があります。

 .csproj ファイルまたは .vbproj ファイルを編集してプロジェクトのプロパティを定義します。 この例では、`myLibFolder` という名前のプロパティを定義します。

```xml
<!-- Define a project property, myLibFolder: -->
<PropertyGroup>
    <myLibFolder>$(MSBuildProjectDirectory)\..\libs</myLibFolder>
</PropertyGroup>

<!-- Tell the MSBuild T4 task to make the property available: -->
<ItemGroup>
    <T4ParameterValues Include="myLibFolder">
      <Value>$(myLibFolder)</Value>
    </T4ParameterValues>
  </ItemGroup>

```

 これで、Visual Studio および MSBuild の両方で正しく変換できるテキスト テンプレートでプロジェクトのプロパティを使用できます。

```
<#@ assembly name="$(myLibFolder)\MyLib.dll" #>
```

## <a name="see-also"></a>参照
 [T4 インクルード ディレクティブ](../modeling/t4-include-directive.md)

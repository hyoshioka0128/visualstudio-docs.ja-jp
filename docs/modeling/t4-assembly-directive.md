---
title: T4 アセンブリ ディレクティブ
description: Visual Studio のデザイン時テキストテンプレートでは、アセンブリディレクティブがアセンブリを読み込み、テンプレートコードがその型を使用できるようにすることを説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 41abd2b5a48f6e5e126747326e9815f3c2f46787
ms.sourcegitcommit: 4d394866b7817689411afee98e85da1653ec42f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2020
ms.locfileid: "97363706"
---
# <a name="t4-assembly-directive"></a>T4 アセンブリ ディレクティブ

Visual Studio のデザイン時テキストテンプレートでは、 `assembly` ディレクティブはアセンブリを読み込み、テンプレートコードがその型を使用できるようにします。 効果は、Visual Studio プロジェクトにアセンブリ参照を追加することに似ています。

 テキストテンプレートの記述の概要については、「 [T4 テキストテンプレートの作成](../modeling/writing-a-t4-text-template.md)」を参照してください。

> [!NOTE]
> 実行時 (前処理された) テキスト テンプレートでは、`assembly` ディレクティブは不要です。 代わりに、必要なアセンブリを Visual Studio プロジェクトの **参照** に追加します。

## <a name="using-the-assembly-directive"></a>assembly ディレクティブの使用
 ディレクティブの構文は次のとおりです。

```
<#@ assembly name="[assembly strong name|assembly file name]" #>
```

 アセンブリ名は、次のいずれかであることが必要です。

- GAC のアセンブリの厳密な名前 (`System.Xml.dll` など)。 `name="System.Xml, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"` のような長い形式を使用することもできます。 詳細については、「<xref:System.Reflection.AssemblyName>」を参照してください。

- アセンブリの絶対パス。

  構文を使用し `$(variableName)` て、などの Visual Studio 変数を参照 `$(SolutionDir)` したり、 `%VariableName%` 環境変数を参照したりすることができます。 次に例を示します。

```
<#@ assembly name="$(SolutionDir)\MyProject\bin\Debug\SomeLibrary.Dll" #>
```

 assembly ディレクティブは、前処理されたテキスト テンプレートでは無効です。 代わりに、必要な参照を Visual Studio プロジェクトの [ **参照** ] セクションに含めます。 詳細については、「[T4 テキスト テンプレートを使用した実行時テキスト生成](../modeling/run-time-text-generation-with-t4-text-templates.md)」を参照してください。

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
 $ (SolutionDir) などの Visual Studio マクロは、MSBuild では動作しません。 ビルド コンピューターでテンプレートを変換する場合、代わりにプロジェクトのプロパティを使用する必要があります。

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

## <a name="see-also"></a>関連項目

- [T4 インクルード ディレクティブ](../modeling/t4-include-directive.md)

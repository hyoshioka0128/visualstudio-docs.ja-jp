﻿---
title: '新しいプロジェクトの生成: 内部的には、パート 2 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio], new project dialog
- projects [Visual Studio], new project generation
ms.assetid: 73ce91d8-0ab1-4a1f-bf12-4d3c49c01e13
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8692f2012e5f2733982f04e35a7fed415e49c636
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707023"
---
# <a name="new-project-generation-under-the-hood-part-two"></a>新しいプロジェクトの生成: 内部、パート 2

[新規プロジェクトの生成：パート1](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md) で**新規プロジェク**トのダイアログボックスの表示方法について説明しました。 **Visual C# Windows アプリケーション** を選択し、**名前** と **場所** のテキストボックスに入力し、[OK]をクリックしたと仮定します。

## <a name="generating-the-solution-files"></a>ソリューション ファイルの生成
 アプリケーション テンプレートを選択すると、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]対応する .vstemplate ファイルを解凍して開き、このファイル内の XML コマンドを解釈するテンプレートを起動します。 これらのコマンドは、新規または既存のソリューションでプロジェクトとプロジェクト項目を作成します。

 テンプレートは、.vstemplate ファイルを保持する同じ .zip フォルダーから、項目テンプレートと呼ばれるソース ファイルをアンパックします。 テンプレートは、これらのファイルを新しいプロジェクトにコピーし、それに応じてカスタマイズします。

### <a name="template-parameter-replacement"></a>テンプレート パラメータの置換
 テンプレートは、項目テンプレートを新しいプロジェクトにコピーするときに、すべてのテンプレート パラメーターを文字列に置き換え、ファイルをカスタマイズします。 テンプレート パラメーターは、ドル記号 ($date$ など) の前に続く特殊なトークンです。

 一般的なプロジェクト項目テンプレートを見てみましょう。 プログラム ファイル\Microsoft Visual Studio 8\Common7\IDE\プロジェクトテンプレート\CSharp\Windows\1033\WindowsApplication.zip フォルダーでProgram.csを抽出して確認します。

```csharp
using System;
using System.Collections.Generic;
using System.Windows.Forms;

namespace $safeprojectname$
{
    static class Program
    {
        // source code deleted here for brevity
    }
}
```

Simple という名前の新しい Windows アプリケーション プロジェクトを作成すると`$safeprojectname$`、テンプレートによって、パラメータがプロジェクトの名前に置き換えられます。

```csharp
using System;
using System.Collections.Generic;
using System.Windows.Forms;

namespace Simple
{
    static class Program
    {
        // source code deleted here for brevity
    }
}
```

 テンプレート パラメーターの完全な一覧については、「[テンプレート パラメーター](../../ide/template-parameters.md)」を参照してください。

## <a name="a-look-inside-a-vstemplate-file"></a>内部を見る .VS テンプレート ファイル
 基本的な .vstemplate ファイルは、この形式です

```xml
<VSTemplate Version="2.0.0"     xmlns="http://schemas.microsoft.com/developer/vstemplate/2005"     Type="Project">
    <TemplateData>
    </TemplateData>
    <TemplateContent>
    </TemplateContent>
</VSTemplate>
```

 「[新しいプロジェクト生成](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md): フードの下で、パート 1」の\<TemplateData> セクションを見ました。 このセクションのタグは、[**新しいプロジェクト**] ダイアログ ボックスの外観を制御するために使用します。

 \<TemplateContent> セクションのタグは、新しいプロジェクトとプロジェクト項目の生成を制御します。 次の\<テンプレートコンテンツ> セクションです。

```xml
<TemplateContent>
  <Project File="WindowsApplication.csproj" ReplaceParameters="true">
    <ProjectItem ReplaceParameters="true"
      TargetFileName="Properties\AssemblyInfo.cs">
      AssemblyInfo.cs
    </ProjectItem>
    <ProjectItem TargetFileName="Properties\Resources.resx">
      Resources.resx
    </ProjectItem>
    <ProjectItem ReplaceParameters="true"       TargetFileName="Properties\Resources.Designer.cs">
      Resources.Designer.cs
    </ProjectItem>
    <ProjectItem TargetFileName="Properties\Settings.settings">
      Settings.settings
    </ProjectItem>
    <ProjectItem ReplaceParameters="true"       TargetFileName="Properties\Settings.Designer.cs">
      Settings.Designer.cs
    </ProjectItem>
    <ProjectItem ReplaceParameters="true" OpenInEditor="true">
      Form1.cs
    </ProjectItem>
    <ProjectItem ReplaceParameters="true">
      Form1.Designer.cs
    </ProjectItem>
    <ProjectItem ReplaceParameters="true">
      Program.cs
    </ProjectItem>
  </Project>
</TemplateContent>
```

 プロジェクト\<> タグはプロジェクトの生成を制御し、\<プロジェクト項目の生成をコントロールする ProjectItem> タグ。 パラメーター ReplaceParameters が true の場合、テンプレートはプロジェクト ファイルまたはプロジェクト項目内のすべてのテンプレート パラメーターをカスタマイズします。 この場合、設定設定を除くすべてのプロジェクト項目がカスタマイズされます。

 TargetFileName パラメーターは、作成されるプロジェクト ファイルまたは項目の名前と相対パスを指定します。 これにより、プロジェクトのフォルダ構造を作成できます。 この引数を指定しない場合、プロジェクト項目の名前はプロジェクト項目テンプレートと同じになります。

 結果として得られる Windows アプリケーション フォルダの構造は次のようになります。

 ![SimpleSolution](../../extensibility/internals/media/simplesolution.png "SimpleSolution")

 テンプレートの最初の\<唯一の Project> タグは、次のようになります。

```xml
<Project File="WindowsApplication.csproj" ReplaceParameters="true">
```

 これにより、新しいプロジェクト テンプレートに、テンプレート項目の windowsapplication.csproj をコピーしてカスタマイズすることによって Simple.csproj プロジェクト ファイルを作成するように指示します。

### <a name="designers-and-references"></a>デザイナーと参照
 ソリューション エクスプローラーで、[プロパティ] フォルダーが存在し、必要なファイルが含まれていることを確認できます。 しかし、Resources.resx へのResources.Designer.csやForm1.csへのForm1.Designer.csなど、プロジェクト参照やデザイナー ファイルの依存関係はどうでしょうか。  これらは、生成時に Simple.csproj ファイルで設定されます。

 プロジェクト参照を作成\<する Simple.csproj のアイテム グループ>を次に示します。

```xml
<ItemGroup>
    <Reference Include="System" />
    <Reference Include="System.Data" />
    <Reference Include="System.Deployment" />
    <Reference Include="System.Drawing" />
    <Reference Include="System.Windows.Forms" />
    <Reference Include="System.Xml" />
</ItemGroup>
```

 これらは、ソリューション エクスプローラーに表示される 6 つのプロジェクト参照であることがわかります。 別\<のアイテム グループ>のセクションを次に示します。 わかりやすくするために、コードの多くの行が削除されました。 このセクションでは、設定設定Settings.Designer.cs依存します。

```xml
<ItemGroup>
    <Compile Include="Properties\Settings.Designer.cs">
        <DependentUpon>Settings.settings</DependentUpon>
    </Compile>
</ItemGroup>
```

## <a name="see-also"></a>関連項目

- [新しいプロジェクトの生成: 内部的な処理、パート 1](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)
- [MSBuild](../../msbuild/msbuild.md)

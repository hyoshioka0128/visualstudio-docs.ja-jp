---
title: '新しいプロジェクトの生成: 内部的には、パート 2 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio], new project dialog
- projects [Visual Studio], new project generation
ms.assetid: 73ce91d8-0ab1-4a1f-bf12-4d3c49c01e13
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4ea614be39456f5d6a31ea6c9c12221b4db09bbd
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66311019"
---
# <a name="new-project-generation-under-the-hood-part-two"></a>新しいプロジェクトの生成: 内部的な処理、パート 2


## <a name="generating-the-solution-files"></a>ソリューション ファイルを生成します。
 アプリケーション テンプレートを選択するように指示[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を解凍して、対応する .vstemplate ファイルを開くと、このファイル内の XML コマンドを解釈するためのテンプレートを起動します。 これらのコマンドは、新規または既存のソリューションでプロジェクトとプロジェクト項目を作成します。

 テンプレートは、.vstemplate ファイルを保持する同じ .zip フォルダーから項目のテンプレートと呼ばれる、ソース ファイルをアンパックします。 テンプレートは、それに応じてカスタマイズして、新しいプロジェクトにこれらのファイルをコピーします。

### <a name="template-parameter-replacement"></a>テンプレート パラメーターの置換
 テンプレートは、新しいプロジェクトに項目テンプレートをコピー、ファイルをカスタマイズする文字列を含むテンプレートのパラメーターが置き換えられます。 テンプレート パラメーターは特殊なトークンを前後にドル記号では、たとえばは、$date$ です。

 一般的なプロジェクト項目テンプレートを見てみましょう。 抽出し、Program files \microsoft Visual Studio 8\Common7\IDE\ProjectTemplates\CSharp\Windows\1033\WindowsApplication.zip フォルダー内の Program.cs を確認します。

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

Simple という名前の新しい Windows アプリケーション プロジェクトを作成する場合、テンプレートに置き換えられます、`$safeprojectname$`プロジェクトの名前を持つパラメーター。

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

 テンプレート パラメーターの完全な一覧については、「[テンプレート パラメーター](../../ide/template-parameters.md)」をご覧ください。

## <a name="a-look-inside-a-vstemplate-file"></a>内でを参照してください。VSTemplate ファイル
 基本的な .vstemplate ファイルが次の形式

```xml
<VSTemplate Version="2.0.0"     xmlns="http://schemas.microsoft.com/developer/vstemplate/2005"     Type="Project">
    <TemplateData>
    </TemplateData>
    <TemplateContent>
    </TemplateContent>
</VSTemplate>
```

 これまで見てきた、 \<TemplateData > セクションで、[新しいプロジェクトの生成。内部的には、パート 1](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)します。 このセクションでは、タグの外観を制御するため、**新しいプロジェクト** ダイアログ ボックス。

 内のタグ、 \<TemplateContent > コントロールに新しいプロジェクトとプロジェクト項目の生成をセクションします。 ここでは、 \<TemplateContent > \Program Files\Microsoft Visual Studio の 8\Common7\IDE\ProjectTemplates\CSharp\Windows\1033\WindowsApplication.zip フォルダー cswindowsapplication.vstemplate ファイルからセクション。

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

 \<プロジェクト > タグは、プロジェクトの生成を制御し、 \<ProjectItem > タグは、プロジェクト項目の生成を制御します。 ReplaceParameters パラメーターが true の場合、テンプレートはプロジェクト ファイルまたは項目内のすべてのテンプレート パラメーターをカスタマイズします。 この場合、すべてのプロジェクト項目をカスタマイズ Settings.settings を除く。

 TargetFileName パラメーターは、作成されたプロジェクト ファイルまたは項目の相対パスと名前を指定します。 これにより、プロジェクトのフォルダー構造を作成できます。 この引数を指定しない場合、プロジェクト項目がプロジェクト項目テンプレートと同じ名前になります。

 結果として得られる Windows アプリケーションのフォルダー構造のようになります。

 ![SimpleSolution](../../extensibility/internals/media/simplesolution.png "SimpleSolution")

 最初で唯一\<プロジェクト > タグで、テンプレートの読み取り。

```xml
<Project File="WindowsApplication.csproj" ReplaceParameters="true">
```

 これには、新しいプロジェクト テンプレートをコピーしてカスタマイズするテンプレート アイテムの windowsapplication.csproj Simple.csproj プロジェクト ファイルを作成するように指示します。

### <a name="designers-and-references"></a>デザイナーと参照
 Properties フォルダーが存在し、必要なファイルが含まれています、ソリューション エクスプ ローラーで表示できます。 しかし、プロジェクトとは何を参照し、デザイナー ファイルには、Form1.cs、Form1.Designer.cs、Resources.resx に Resources.Designer.cs などの依存関係でしょうか。  生成されるときに、Simple.csproj ファイルで設定これらされます。

 ここでは、 \<ItemGroup > から Simple.csproj プロジェクト参照を作成します。

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

 これらは、ソリューション エクスプ ローラーに表示される 6 つのプロジェクト参照であることを確認できます。 別のセクションを次に示します\<ItemGroup >。 わかりやすくするため、多数のコード行が削除されました。 このセクションでは、Settings.Designer.cs を Settings.settings に依存します。

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

---
title: '新しいプロジェクトの生成: 内部的には、パート 2 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio], new project dialog
- projects [Visual Studio], new project generation
ms.assetid: 73ce91d8-0ab1-4a1f-bf12-4d3c49c01e13
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6643c52ff8e5801c562524e99c4e3f03c00f74b9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687477"
---
# <a name="new-project-generation-under-the-hood-part-two"></a>新しいプロジェクトの生成: 内部的な処理、パート 2
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[新しいプロジェクトの生成: 内部](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)では、[**新しいプロジェクト**] ダイアログボックスがどのように設定されているかを説明します。 ここでは、 **Visual C# Windows アプリケーション**を選択し、[ **名前** ] と [ **場所** ] のテキストボックスに入力して、[OK] をクリックしたとします。  
  
## <a name="generating-the-solution-files"></a>ソリューションファイルの生成  
 アプリケーションテンプレートを選択する [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] と、対応する .vstemplate ファイルを解凍して開き、このファイル内の XML コマンドを解釈するためのテンプレートを起動するように指示されます。 これらのコマンドは、新規または既存のソリューションにプロジェクトとプロジェクト項目を作成します。  
  
 このテンプレートは、.vstemplate ファイルを保持する同じ .zip フォルダーから、項目テンプレートと呼ばれるソースファイルをアンパックします。 テンプレートは、これらのファイルを新しいプロジェクトにコピーし、適宜カスタマイズします。 プロジェクトテンプレートと項目テンプレートの概要については、「 [NIB: Visual Studio templates](https://msdn.microsoft.com/141fccaa-d68f-4155-822b-27f35dd94041)」を参照してください。  
  
### <a name="template-parameter-replacement"></a>テンプレートパラメーターの置換  
 テンプレートが項目テンプレートを新しいプロジェクトにコピーすると、テンプレートパラメーターが文字列に置き換えられ、ファイルがカスタマイズされます。 テンプレートパラメーターは、$ 記号 ($date $ など) の前と後にある特別なトークンです。  
  
 一般的なプロジェクト項目テンプレートを見てみましょう。 プログラムの [Visual Studio 8\Common7\IDE\ProjectTemplates\CSharp\Windows\1033\WindowsApplication.zip フォルダー内の Program.cs を抽出して確認します。  
  
```  
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
  
 Simple という名前の新しい Windows アプリケーションプロジェクトを作成した場合、テンプレートは `$safeprojectname$` パラメーターをプロジェクトの名前に置き換えます。  
  
```  
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
  
 テンプレートパラメーターの完全な一覧については、「 [テンプレートパラメーター](../../ide/template-parameters.md)」を参照してください。  
  
## <a name="a-look-inside-a-vstemplate-file"></a>内を検索します。.Vstemplate ファイル  
 基本 .vstemplate ファイルの形式は次のようになります。  
  
```  
<VSTemplate Version="2.0.0"     xmlns="http://schemas.microsoft.com/developer/vstemplate/2005"     Type="Project">  
    <TemplateData>  
    </TemplateData>  
    <TemplateContent>  
    </TemplateContent>  
</VSTemplate>  
```  
  
 新しいプロジェクトの生成に関するセクションでは、内部的には \<TemplateData> [パート 1](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)が見られました。 このセクションのタグは、[ **新しいプロジェクト** ] ダイアログボックスの外観を制御するために使用されます。  
  
 セクションのタグは、 \<TemplateContent> 新しいプロジェクトとプロジェクト項目の生成を制御します。 次に示すのは、 \<TemplateContent> アプリケーションファイルの 8\Common7\IDE\ProjectTemplates\CSharp\Windows\1033\WindowsApplication.zip フォルダーにある cswindowsapplication .vstemplate ファイルのセクションです。  
  
```  
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
  
 タグは、 \<Project> プロジェクトの生成を制御し \<ProjectItem> ます。タグは、プロジェクト項目の生成を制御します。 パラメーター ReplaceParameters が true の場合、テンプレートはプロジェクトファイルまたは項目内のすべてのテンプレートパラメーターをカスタマイズします。 この場合、設定を除き、すべてのプロジェクト項目がカスタマイズされます。  
  
 TargetFileName パラメーターは、結果として得られるプロジェクトファイルまたは項目の名前と相対パスを指定します。 これにより、プロジェクトのフォルダー構造を作成できます。 この引数を指定しない場合、プロジェクト項目の名前はプロジェクト項目テンプレートと同じになります。  
  
 生成される Windows アプリケーションフォルダーの構造は次のようになります。  
  
 ![SimpleSolution](../../extensibility/internals/media/simplesolution.png "SimpleSolution")  
  
 テンプレートの最初のタグと唯一の \<Project> タグは次のようになります。  
  
```  
<Project File="WindowsApplication.csproj" ReplaceParameters="true">  
```  
  
 これにより、新しいプロジェクトテンプレートは、テンプレート項目 windowsapplication .csproj をコピーおよびカスタマイズすることによって、単純な .csproj プロジェクトファイルを作成するように指示します。  
  
### <a name="designers-and-references"></a>デザイナーと参照  
 ソリューションエクスプローラーに、Properties フォルダーが存在し、予想されるファイルが含まれていることを確認できます。 しかし、プロジェクト参照とデザイナーファイルの依存関係 (Resources.Designer.cs to Form1.cs、Form1.Designer.cs to など) はどうでしょうか。  これらは、単純な .csproj ファイルの生成時に設定されます。  
  
 \<ItemGroup>プロジェクト参照を作成する単純な .csproj のを次に示します。  
  
```  
<ItemGroup>  
    <Reference Include="System" />  
    <Reference Include="System.Data" />  
    <Reference Include="System.Deployment" />  
    <Reference Include="System.Drawing" />  
    <Reference Include="System.Windows.Forms" />  
    <Reference Include="System.Xml" />  
</ItemGroup>  
```  
  
 これらは、ソリューションエクスプローラーに表示される6つのプロジェクト参照であることがわかります。 もう1つのセクションを次に示し \<ItemGroup> ます。 わかりやすくするために、多くのコード行が削除されています。 このセクションでは、Settings.Designer.cs を設定に依存させます。設定:  
  
```  
<ItemGroup>  
    <Compile Include="Properties\Settings.Designer.cs">  
        <DependentUpon>Settings.settings</DependentUpon>  
    </Compile>  
</ItemGroup>  
```  
  
## <a name="see-also"></a>参照  
 [新しいプロジェクトの生成: 内部的な処理、パート 1](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)  
 [MSBuild](../../msbuild/msbuild.md)

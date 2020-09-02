---
title: Folder 要素 (Visual Studio プロジェクトテンプレート) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Folder
helpviewer_keywords:
- Folder element [Visual Studio project templates]
ms.assetid: 558e3d41-0db5-4c44-82bb-6bb87892b093
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 35448f4324213739cb2dc14a95598ac9a3d4432f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204361"
---
# <a name="folder-element-visual-studio-project-templates"></a>Folder 要素 (Visual Studio テンプレート)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

プロジェクトに追加されるフォルダーを指定します。  
  
 \<VSTemplate>  
 \<TemplateContent>  
 \<Project>  
 \<Folder>  
  
## <a name="syntax"></a>構文  
  
```  
<Folder Name="Project Folder">  
    <Folder> ... </Folder>  
    <ProjectItem> ... </ProjectItem>  
</Folder>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|`Name`|必須の属性です。<br /><br /> プロジェクトフォルダーの名前。|  
|`TargetFolderName`|省略可能な属性です。<br /><br /> プロジェクトがテンプレートから作成されるときにフォルダーに付ける名前を指定します。 この属性は、パラメーター置換を使用してフォルダー名を作成したり、.zip ファイルで直接使用できない国際文字列を使用してフォルダーに名前を付けたりする場合に便利です。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|`Folder`|プロジェクトに追加するフォルダーを指定します。 `Folder` 要素には子要素を含めることができ `Folder` ます。|  
|[ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md)|プロジェクトに追加するファイルを指定します。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[プロジェクト](../extensibility/project-element-visual-studio-templates.md)|[Templatecontent](../extensibility/templatecontent-element-visual-studio-templates.md)子要素 (省略可能)。|  
  
## <a name="remarks"></a>注釈  
 `Folder` は、の省略可能な子です `Project` 。  
  
 次のいずれかの方法を使用して、プロジェクト項目をテンプレート内のフォルダーに整理できます。  
  
- テンプレートの .zip ファイルにフォルダーを含めて、.vstemplate ファイル内のプロジェクトに追加します。これには、要素内のファイルへのパスを `ProjectItem` 要素を指定せずに指定します `Folder` 。 これが推奨される方法です。 次に例を示します。  
  
     `...`  
  
     `<ProjectItem>\Folder\item.cs</ProjectItem>`  
  
     `<ProjectItem>Form1.cs</ProjectItem>`  
  
     `...`  
  
- テンプレート .zip ファイルにフォルダーを含め、要素を含む .vstemplate ファイル内のプロジェクトに追加します。 `Folder` 次に例を示します。  
  
     `...`  
  
     `<Folder name="Folder">`  
  
     `<ProjectItem>item.cs</ProjectItem>`  
  
     `</Folder>`  
  
     `<ProjectItem>Form1.cs</ProjectItem>`  
  
     `...`  
  
- テンプレート .zip ファイルにはフォルダーを含めないでください。ただし、 `TargetFileName` 要素の属性を使用してフォルダーを追加してください `ProjectItem` 。 次に例を示します。  
  
     `...`  
  
     `<ProjectItem TargetFileName="\Folder\item.cs">item.cs</ProjectItem>`  
  
     `<ProjectItem>Form1.cs</ProjectItem>`  
  
     `...`  
  
## <a name="example"></a>例  
 次の例は、Windows アプリケーション用のプロジェクトテンプレートのメタデータを示してい [!INCLUDE[csprcs](../includes/csprcs-md.md)] ます。  
  
```  
<VSTemplate Type="Project" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>My template</Name>  
        <Description>A basic template</Description>  
        <Icon>TemplateIcon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
    </TemplateData>  
    <TemplateContent>  
        <Project File="MyTemplate.csproj">  
            <ProjectItem>Form1.cs<ProjectItem>  
            <ProjectItem>Form1.Designer.cs</ProjectItem>  
            <ProjectItem>Program.cs</ProjectItem>  
            <Folder Name="Properties">  
                <ProjectItem>AssemblyInfo.cs</ProjectItem>  
                <ProjectItem>Resources.resx</ProjectItem>  
                <ProjectItem>Resources.Designer.cs</ProjectItem>  
                <ProjectItem>Settings.settings</ProjectItem>  
                <ProjectItem>Settings.Designer.cs</ProjectItem>  
            </Folder>  
        </Project>  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>参照  
 [Visual Studio テンプレートスキーマリファレンス](../extensibility/visual-studio-template-schema-reference.md)   
 [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)   
 [ProjectItem 要素 (Visual Studio 項目テンプレート)](../extensibility/projectitem-element-visual-studio-item-templates.md)

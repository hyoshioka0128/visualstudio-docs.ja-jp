---
title: ProjectType 要素 (Visual Studio テンプレート) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectType
helpviewer_keywords:
- ProjectType element [Visual Studio project templates]
ms.assetid: ccf9d83f-c7f3-49c7-a31f-e1f22bec004c
caps.latest.revision: 20
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b01dd370fe5e3d7a5207363c5ab7ec4f2a0254c5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841412"
---
# <a name="projecttype-element-visual-studio-templates"></a>ProjectType 要素 (Visual Studio テンプレート)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[ **新しいプロジェクト** ] ダイアログボックスまたは [ **新しい項目の追加** ] ダイアログボックスで指定したグループの下に表示されるように、プロジェクトテンプレートを分類します。  
  
> [!WARNING]
> プロジェクト テンプレートは、Visual Studio 2012 以降の C++ でサポートされています。 これらは、Visual Studio 2010 以前のバージョンの C++ ではサポートされていません。  
  
 \<VSTemplate>  
 \<TemplateData>  
 \<ProjectType>  
  
## <a name="syntax"></a>構文  
  
```  
<ProjectType> CSharp/VisualBasic/VC/Web </ProjectType>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックス、または **[新しい項目の追加]** ダイアログ ボックスでどのように表示させるかを定義します。|  
  
## <a name="text-value"></a>テキスト値  
 テキスト値が必要です。  
  
 この値で、テンプレートから作成されるプロジェクトの種類を指定します。値には、次のいずれかの値を含める必要があります。  
  
- `CSharp` : テンプレートが [!INCLUDE[csprcs](../includes/csprcs-md.md)] のプロジェクトまたはアイテムを作成するよう指定します。  
  
- `VisualBasic` : テンプレートが [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] のプロジェクトまたはアイテムを作成するよう指定します。  
  
- `Web`: テンプレートが Web プロジェクトまたは項目を作成するように指定します。 要素に `ProjectType` この値が含まれている場合は、プロジェクトまたは項目の言語が [Projectsubtype 要素 (Visual Studio テンプレート)](../extensibility/projectsubtype-element-visual-studio-templates.md)で定義されます。  
  
## <a name="remarks"></a>注釈  
 `ProjectType` は `TemplateData` に必須の子要素です。  
  
 要素の値は、 `ProjectType` [ **新しいプロジェクト** ] ダイアログボックスまたは [ **新しい項目の追加** ] ダイアログボックスでテンプレートを配置する場所を指定します。 たとえば、値がのテンプレートは、 `ProjectType` `CSharp` [**新しいプロジェクト**] ダイアログボックスの [ **Visual C#** ] ノードの下に表示されます。  
  
 テンプレートのサブタイプは、 [Projectsubtype](../extensibility/projectsubtype-element-visual-studio-templates.md) 要素を使用して指定できます。  
  
## <a name="example"></a>例  
 [!INCLUDE[csprcs](../includes/csprcs-md.md)] アプリケーションでのプロジェクト テンプレートのメタデータの例を次に示します。  
  
```  
<VSTemplate Type="Project" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>My template</Name>  
        <Description>A basic starter kit</Description>  
        <Icon>TemplateIcon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
    </TemplateData>  
    <TemplateContent>  
        <Project File="MyStarterKit.csproj">  
            <ProjectItem>Form1.cs<ProjectItem>  
            <ProjectItem>Form1.Designer.cs</ProjectItem>  
            <ProjectItem>Program.cs</ProjectItem>  
            <ProjectItem>Properties\AssemblyInfo.cs</ProjectItem>  
            <ProjectItem>Properties\Resources.resx</ProjectItem>  
            <ProjectItem>Properties\Resources.Designer.cs</ProjectItem>  
            <ProjectItem>Properties\Settings.settings</ProjectItem>  
            <ProjectItem>Properties\Settings.Designer.cs</ProjectItem>  
        </Project>  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>参照  
 [Visual Studio テンプレートスキーマリファレンス](../extensibility/visual-studio-template-schema-reference.md)   
 [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)   
 [ProjectSubType 要素 (Visual Studio テンプレート)](../extensibility/projectsubtype-element-visual-studio-templates.md)

---
title: ProjectSubType 要素 (Visual Studio テンプレート) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectSubType
helpviewer_keywords:
- ProjectSubType element [Visual Studio Templates]
- <ProjectSubType> element [Visual Studio Templates]
ms.assetid: f6895cd4-3e95-4f0e-aa9e-8c7750f46ed4
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d07a62027b494242d3c25aba00fbd5f4d75df78b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68193907"
---
# <a name="projectsubtype-element-visual-studio-templates"></a>ProjectSubType 要素 (Visual Studio テンプレート)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テンプレートを、要素で指定された値のサブカテゴリに分類し `ProjectType` ます。  
  
 \<VSTemplate>  
 \<TemplateData>  
 \<ProjectSubType>  
  
## <a name="syntax"></a>構文  
  
```  
<ProjectSubType> SubType </ProjectSubType>  
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックス、または **[新しい項目の追加]** ダイアログ ボックスでどのように表示させるかを定義します。|  
  
## <a name="text-value"></a>テキスト値  
 テキスト値が必要です。  
  
 この値は、テンプレートのサブカテゴリを指定します。  
  
## <a name="remarks"></a>注釈  
 `ProjectSubType` は、`TemplateData` の子要素で、省略可能な要素です。  
  
 要素は、 `ProjectSubType` [ProjectType](../extensibility/projecttype-element-visual-studio-templates.md) 要素のサブカテゴリを提供します。 この値には次のものがあります。  
  
- `SmartDevice-NETCFv1`: テンプレートがバージョン1.0 を対象とすることを指定し [!INCLUDE[Compact](../includes/compact-md.md)] ます。  
  
- `SmartDevice-NETCFv2`: Temate がバージョン2.0 を対象とすることを指定します [!INCLUDE[Compact](../includes/compact-md.md)] 。  
  
  テンプレートに値がの要素が含まれている場合、 `ProjectType` `Web` `ProjectSubType` 要素はテンプレートのプログラミング言語を指定します。 この要素には、次の値を指定できます。  
  
- `CSharp`: テンプレートが [!INCLUDE[csprcs](../includes/csprcs-md.md)] Web プロジェクトまたは項目を作成するように指定します。  
  
- `VisualBasic`: テンプレートが [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] Web プロジェクトまたは項目を作成するように指定します。  
  
## <a name="example"></a>例  
 次の例は、バージョン2.0 を対象とするデバイスアプリケーションのプロジェクトテンプレートのメタデータを示して [!INCLUDE[csprcs](../includes/csprcs-md.md)] [!INCLUDE[Compact](../includes/compact-md.md)] います。  
  
```  
<VSTemplate Type="Project" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>My template</Name>  
        <Description>A basic device template</Description>  
        <Icon>TemplateIcon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
        <ProjectSubType>SmartDevice-NETCFv2</ProjectSubType>  
    </TemplateData>  
    <TemplateContent>  
        <Project File="MyTemplate.csproj">  
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
 [ProjectType 要素 (Visual Studio テンプレート)](../extensibility/projecttype-element-visual-studio-templates.md)

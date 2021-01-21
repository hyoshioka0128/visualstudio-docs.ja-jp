---
title: SolutionFolder 要素 (Visual Studio テンプレート) |Microsoft Docs
description: SolutionFolder 要素について、および複数プロジェクトのテンプレートでプロジェクトをグループ化する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#SolutionFolder
helpviewer_keywords:
- <SolutionFolder> element [Visual Studio Templates]
- SolutionFolder element [Visual Studio Templates]
ms.assetid: 963f0398-fb50-4d8e-879d-d48f8b7c6d80
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: be6cb773e2d822efe01f87b1102293898005cbc8
ms.sourcegitcommit: 86e98df462b574ade66392f8760da638fe455aa0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2020
ms.locfileid: "94903781"
---
# <a name="solutionfolder-element-visual-studio-templates"></a>SolutionFolder 要素 (Visual Studio テンプレート)
複数プロジェクトのテンプレートをグループ化します。

 \<VSTemplate> \<TemplateContent>
 \<ProjectCollection>
 \<SolutionFolder>

## <a name="syntax"></a>構文

```
<SolutionFolder Name="DirectoryName">
    ...
</SolutionFolder>
```

## <a name="attributes-and-elements"></a>属性および要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`Name`|必須の属性です。<br /><br /> ソリューション フォルダーの名前。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[ProjectTemplateLink](../extensibility/projecttemplatelink-element-visual-studio-templates.md)|省略可能な要素です。<br /><br /> 複数プロジェクトのテンプレートにある プロジェクトの .vstemplate ファイル パスを指定します。|
|`SolutionFolder`|省略可能な要素です。<br /><br /> 複数プロジェクトのテンプレートをグループ化します。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[ProjectCollection](../extensibility/projectcollection-element-visual-studio-templates.md)|複数プロジェクトのテンプレートの構成と内容を指定します。|
|`SolutionFolder`|複数プロジェクトのテンプレートをグループ化します。|

## <a name="remarks"></a>解説
 複数プロジェクトのテンプレートは、2 つ以上のプロジェクトのコンテナーとして機能します。 `SolutionFolder` 要素は、テンプレート内のプロジェクトをグループに編成するために使用されます。 `SolutionFolder` 要素で指定されたフォルダーは、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 内のプロジェクトのソリューション フォルダーとして作成されます。 複数プロジェクトのテンプレートの詳細については、「 [方法: 複数プロジェクトのテンプレートを作成する](../ide/how-to-create-multi-project-templates.md)」を参照してください。

## <a name="example"></a>例
 この例では、`SolutionFolder` 要素を使用して、複数のプロジェクトのテンプレートを 2 つのグループ、`Math Classes` と `Graphics Classes` に分割します。 テンプレートには 4 つのプロジェクトが含まれ、その 2 つは各ソリューション フォルダーに配置されます。

```
<VSTemplate Version="3.0.0" Type="ProjectGroup"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>Multi-Project Template Sample</Name>
        <Description>An example of a multi-project template</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>VisualBasic</ProjectType>
    </TemplateData>
    <TemplateContent>
        <ProjectCollection>
            <SolutionFolder Name="Math Classes">
                <ProjectTemplateLink ProjectName="MathClassLib1">
                    MathClassLib1\MyTemplate.vstemplate
                </ProjectTemplateLink>
                <ProjectTemplateLink ProjectName="MathClassLib2">
                    MathClassLib2\MyTemplate.vstemplate
                </ProjectTemplateLink>
            </SolutionFolder>
            <SolutionFolder Name="Graphics Classes">
                <ProjectTemplateLink ProjectName="GraphicsClassLib1">
                    GraphicsClassLib1\MyTemplate.vstemplate
                </ProjectTemplateLink>
                <ProjectTemplateLink ProjectName="GraphicsClassLib2">
                    GraphicsClassLib2\MyTemplate.vstemplate
                </ProjectTemplateLink>
            </SolutionFolder>
        </ProjectCollection>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレートスキーマリファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
- [方法: 複数プロジェクトのテンプレートを作成する](../ide/how-to-create-multi-project-templates.md)

---
title: プロジェクトコレクション要素 (Visual Studio テンプレート) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectCollection
helpviewer_keywords:
- <ProjectCollection> element [Visual Studio Templates]
- ProjectCollection element [Visual Studio Templates]
ms.assetid: deb27180-2035-49ed-b835-c47bb3cd2f8f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 12a22ca28c90ed1df69529ed3004b417b5e04276
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701973"
---
# <a name="projectcollection-element-visual-studio-templates"></a>プロジェクトコレクション要素
複数プロジェクトのテンプレートの構成と内容を指定します。

 \<VS テンプレート\<>\<テンプレートプロジェクトコレクション>>コンテンツ

## <a name="syntax"></a>構文

```xml
<ProjectCollection>
    <ProjectTemplateLink> ... </ProjectTemplateLink>
    <SolutionFolder> ... </SolutionFolder>
</ProjectCollection>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 [なし] :

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[ProjectTemplateLink](../extensibility/projecttemplatelink-element-visual-studio-templates.md)|省略可能な要素です。<br /><br /> 複数プロジェクト テンプレート内のプロジェクトを指定します。|
|[SolutionFolder](../extensibility/solutionfolder-element-visual-studio-templates.md)|省略可能な要素です。<br /><br /> 複数プロジェクトのテンプレートをグループ化します。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートの内容を指定します。|

## <a name="remarks"></a>Remarks
 複数プロジェクトのテンプレートは、2 つ以上のプロジェクトのコンテナーとして機能します。 要素`ProjectCollection`は、テンプレートに含めるプロジェクトを指定するために使用されます。 複数プロジェクトのテンプレートの詳細については、「[方法 : 複数プロジェクト テンプレートを作成する](../ide/how-to-create-multi-project-templates.md)」を参照してください。

## <a name="example"></a>例
 この例では、単純な複数プロジェクトのルート *.vstemplate*ファイルを示します。 この例では、テンプレートには `My Windows Application` と `My Class Library` の 2 つのプロジェクトが含まれています。 `ProjectName` 要素の `ProjectTemplateLink` 属性は、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] がこのプロジェクトに割り当てる名前を設定します。 属性が`ProjectName`存在しない場合は *、.vstemplate*ファイルの名前がプロジェクト名として使用されます。

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
            <ProjectTemplateLink ProjectName="My Windows Application">
                WindowsApp\MyTemplate.vstemplate
            </ProjectTemplateLink>
            <ProjectTemplateLink ProjectName="My Class Library">
                ClassLib\MyTemplate.vstemplate
            </ProjectTemplateLink>
        </ProjectCollection>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ リファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
- [方法: 複数プロジェクトテンプレートを作成する](../ide/how-to-create-multi-project-templates.md)

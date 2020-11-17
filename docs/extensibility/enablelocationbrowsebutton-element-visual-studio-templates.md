---
title: EnableLocationBrowseButton 要素 (Visual Studio テンプレート)
description: EnableLocationBrowseButton 要素について、および [新しいプロジェクト] ダイアログボックスで [参照] ボタンを使用できるかどうかをどのように指定するかについて説明します。
titleSuffix: ''
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#EnableLocationBrowseButton
helpviewer_keywords:
- EnableLocationBrowseButton [Visual Studio project templates]
ms.assetid: a12d10d8-af49-482a-af77-e084fd07a47d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 463219218994c9ec1e0f8a5be6e43a0bfd3f5d49
ms.sourcegitcommit: 3d96f7a8c9affab40358c3e81e3472db31d841b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2020
ms.locfileid: "94671260"
---
# <a name="enablelocationbrowsebutton-element-visual-studio-templates"></a>EnableLocationBrowseButton 要素 (Visual Studio テンプレート)
[**新しいプロジェクト**] ダイアログボックスで [**参照**] ボタンを使用できるようにするかどうかを指定します。これにより、新しいプロジェクトを保存する既定のディレクトリをユーザーが簡単に変更できるようになります。

 \<VSTemplate> \<TemplateData>
 \<EnableLocationBrowseButton>

## <a name="syntax"></a>構文

```xml
<EnableLocationBrowseButton> true/false </EnableLocationBrowseButton>
```

## <a name="attributes-and-elements"></a>属性と要素
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

 テキストは、[ `true` `false` **新しいプロジェクト**] ダイアログボックスに [**参照**] ボタンを表示するかどうかを示す、またはのいずれかである必要があります。

## <a name="remarks"></a>注釈
 `EnableLocationBrowseButton` は省略可能な要素です。 既定値はで、[ `true` **新しいプロジェクト**] ダイアログボックスの [**参照**] ボタンが表示されます。

 [ **新しいプロジェクト** ] ダイアログボックスの [ **場所** ] テキストボックスで、新しいプロジェクトを保存するディレクトリを指定します。 [ **参照** ] ボタンをクリックすると、[ **プロジェクトの場所** ] ダイアログボックスが表示され、このディレクトリを変更できます。このダイアログボックスでは、コンピューターから使用できる別のディレクトリに移動して、新しいプロジェクトを保存するディレクトリとして選択することができます。

## <a name="example"></a>例
 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] Windows アプリケーションでのメタデータの例を次に示します。

```xml
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic starter kit</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <EnableLocationBrowseButton>false</EnableLocationBrowseButton>
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

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)

---
title: EnableEditOfLocationField 要素 (Visual Studio テンプレート)
titleSuffix: ''
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- EnableEditOfLocationField (Visual Studio project templates)
ms.assetid: 51a91963-8a3f-4741-928e-bc90c11473bb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9baee9e7497f5b65022b8a0b938f4a8a63140ab2
ms.sourcegitcommit: 2a201c93ed526b0f7e5848657500f1111b08ac2a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2020
ms.locfileid: "89741711"
---
# <a name="enableeditoflocationfield-element-visual-studio-templates"></a>EnableEditOfLocationField 要素 (Visual Studio テンプレート)
ユーザーが [場所] フィールドを編集できるかどうかを指定します。

 \<VSTemplate> \<TemplateData>
 \<EnableEditOfLocationField>

## <a name="syntax"></a>構文

```
<EnableEditOfLocationField> true/false </EnableEditOfLocationField>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 なし

### <a name="child-elements"></a>子要素
 なし

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックス、または **[新しい項目の追加]** ダイアログ ボックスでどのように表示させるかを定義します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 テキストはまたはである必要があります。これは、ユーザーが [ `true` `false` **新しいプロジェクト**] ダイアログボックスの [**場所**] テキストボックスを編集できるかどうかを示します。

## <a name="remarks"></a>解説
 `EnableEditOfLocationField` は省略可能な要素です。 既定値は `true` で、ユーザーは [**新しいプロジェクト**] ダイアログボックスの [**場所**] テキストボックスで値を編集できます。

 [ **新しいプロジェクト** ] ダイアログボックスの [ **場所** ] テキストボックスで、新しいプロジェクトを保存するディレクトリを指定します。

## <a name="example"></a>例
 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] Windows アプリケーションでのメタデータの例を次に示します。

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic starter kit</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <EnableEditOfLocationField>false</EnableEditOfLocationField>
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

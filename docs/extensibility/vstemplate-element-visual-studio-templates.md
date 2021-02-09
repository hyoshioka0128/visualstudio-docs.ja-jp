---
title: .Vstemplate 要素 (Visual Studio テンプレート) |Microsoft Docs
description: .Vstemplate 要素について、およびプロジェクトテンプレート、項目テンプレート、またはスタートキットに関するすべてのメタデータがどのように含まれているかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#VSTemplate
helpviewer_keywords:
- VSTemplate element [Visual Studio project templates]
ms.assetid: f8ac561b-3b0b-4246-9ec9-118d2447e9a9
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5f15b21ccb52cf7aa7c857c0b6b523c02fd65461
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99905731"
---
# <a name="vstemplate-element-visual-studio-templates"></a>.Vstemplate 要素 (Visual Studio テンプレート)
プロジェクトテンプレート、項目テンプレート、またはスタートキットに関するすべてのメタデータが含まれます。

## <a name="syntax"></a>構文

```csharp
<VSTemplate Type="TemplateType" Version="x.x.x">
    <TemplateData>    </TemplateData>
    <TemplateContent>    </TemplateContent>
    ...
</VSTemplate>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

| 属性 | 説明 |
|-----------| - |
| `Type` | テンプレートをプロジェクトテンプレートまたは項目テンプレートとして識別します。 この属性には、またはの値を指定でき `Project` `Item` ます。 |
| `Version` | テンプレートのバージョン番号を指定します。 およびの [!INCLUDE[vs_dev10_long](../code-quality/includes/vs_dev10_long_md.md)] テンプレート [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)] `Version` の属性値は `3.0.0` です。 |

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートを分類するデータを指定し、[ **新しいプロジェクト** ] ダイアログボックスまたは [ **新しい項目の追加** ] ダイアログボックスでの表示方法を定義します。|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートの内容を指定します。|
|[WizardExtension](../extensibility/wizardextension-element-visual-studio-templates.md)|省略可能な要素です。|
|[WizardData](../extensibility/wizarddata-element-visual-studio-templates.md)|省略可能な要素です。|

### <a name="parent-elements"></a>親要素
 [なし] :

## <a name="remarks"></a>解説
 `VSTemplate`要素は *.vstemplate* ファイルのルート要素です。

## <a name="example"></a>例
 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] アプリケーションでのプロジェクト テンプレートのメタデータの例を次に示します。

```xml
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
            <ProjectItem>Form1.cs</ProjectItem>
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

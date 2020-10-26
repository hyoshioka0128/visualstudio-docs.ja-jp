---
title: ProjectSubType 要素 (Visual Studio テンプレート) |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectSubType
helpviewer_keywords:
- ProjectSubType element [Visual Studio Templates]
- <ProjectSubType> element [Visual Studio Templates]
ms.assetid: f6895cd4-3e95-4f0e-aa9e-8c7750f46ed4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 27396ad1bcc4e181b2b8cecd6ca863db2412630d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80701828"
---
# <a name="projectsubtype-element-visual-studio-templates"></a>ProjectSubType 要素 (Visual Studio テンプレート)
テンプレートを、要素で指定された値のサブカテゴリに分類し `ProjectType` ます。

 \<VSTemplate> \<TemplateData>
 \<ProjectSubType>

## <a name="syntax"></a>構文

```xml
<ProjectSubType> SubType </ProjectSubType>
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

 この値は、テンプレートのサブカテゴリを指定します。

## <a name="remarks"></a>解説
 `ProjectSubType` は、`TemplateData` の子要素で、省略可能な要素です。

 要素は、 `ProjectSubType` [ProjectType](../extensibility/projecttype-element-visual-studio-templates.md) 要素のサブカテゴリを提供します。 この値には次のものがあります。

- `SmartDevice-NETCFv1`: テンプレートがバージョン1.0 を対象とすることを指定し [!INCLUDE[Compact](../extensibility/includes/compact_md.md)] ます。

- `SmartDevice-NETCFv2`: テンプレートがバージョン2.0 を対象とすることを指定し [!INCLUDE[Compact](../extensibility/includes/compact_md.md)] ます。

  テンプレートに値がの要素が含まれている場合、 `ProjectType` `Web` `ProjectSubType` 要素はテンプレートのプログラミング言語を指定します。 この要素には、次の値を指定できます。

- `CSharp`: テンプレートが [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] Web プロジェクトまたは項目を作成するように指定します。

- `VisualBasic`: テンプレートが [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] Web プロジェクトまたは項目を作成するように指定します。

## <a name="example"></a>例
 次の例は、バージョン2.0 を対象とするデバイスアプリケーションのプロジェクトテンプレートのメタデータを示して [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] [!INCLUDE[Compact](../extensibility/includes/compact_md.md)] います。

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

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
- [ProjectType 要素 (Visual Studio テンプレート)](../extensibility/projecttype-element-visual-studio-templates.md)

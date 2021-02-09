---
title: LocationField 要素 (Visual Studio プロジェクト テンプレート)
titleSuffix: ''
description: LocationField 要素について、およびプロジェクトテンプレートで [新しいプロジェクト] ダイアログボックスの [場所] ボックスが有効になっているか、無効になっているか、または非表示であるかを指定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#LocationField
helpviewer_keywords:
- LocationField element [Visual Studio project templates]
ms.assetid: 6aaaa155-6ce0-4f7f-aa50-8d63d7a7c992
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cbd0d6ee6ede29be35437125f614512ff3bbeab3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99915186"
---
# <a name="locationfield-element-visual-studio-project-templates"></a>LocationField 要素 (Visual Studio プロジェクトテンプレート)
[**新しいプロジェクト**] ダイアログボックスの [**場所**] テキストボックスが、プロジェクトテンプレートに対して有効、無効、または非表示のいずれであるかを指定します。

 \<VSTemplate> \<TemplateData>
 \<LocationField>

## <a name="syntax"></a>構文

```
<LocationField> Enabled/Disabled/Hidden </LocationField>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートを分類し、 **新しいプロジェクト** での表示方法を定義します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 有効なテキスト値は次のとおりです。

- `Enabled`。 [**新しいプロジェクト**] ダイアログボックスの [**場所**] ボックスが有効になっていることを指定します。

- `Disabled`。 [**新しいプロジェクト**] ダイアログボックスの [**場所**] ボックスが無効になっていることを指定します。

- `Hidden`[**新しいプロジェクト**] ダイアログボックスの [**場所**] ボックスが非表示になるように指定します。

## <a name="remarks"></a>解説
 既定値は `Enabled` です。

 [**新しいプロジェクト**] ダイアログボックスの [**場所**] テキストボックスを使用すると、新しいプロジェクトを保存する既定のディレクトリを変更できます。

 要素で指定された値 `Location` は、基になるプロジェクトシステムでサポートされている場合にのみ、ダイアログボックスによって有効になります。

## <a name="example"></a>例
 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] テンプレートのメタデータの例を次に示します。

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <LocationField>Disabled</LocationField>
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

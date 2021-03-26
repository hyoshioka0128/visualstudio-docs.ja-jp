---
title: ProjectItem 要素 (Visual Studio 項目テンプレート) |Microsoft Docs
description: 項目テンプレートの ProjectItem 要素と、テンプレートがプロジェクトと項目のどちらであるかに応じて異なる属性を受け入れる方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectItem
helpviewer_keywords:
- <ProjectItem> element [Visual Studio item templates]
- ProjectItem element [Visual Studio item templates]
ms.assetid: 9ed94112-0c38-49df-b728-0dd2d0d1eb47
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0910486202bca781ec19b6d5895e68ed93f8c3d5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068727"
---
# <a name="projectitem-element-visual-studio-item-templates"></a>ProjectItem 要素 (Visual Studio 項目テンプレート)
項目テンプレートに含まれるファイルを指定します。

> [!NOTE]
> 要素は、 `ProjectItem` テンプレートがプロジェクトと項目のどちらであるかに応じて、異なる属性を受け取ります。 このトピックでは、item の要素について説明 `ProjectItem` します。 `ProjectItem`プロジェクトテンプレートの要素の説明については、「 [ProjectItem 要素 (Visual Studio プロジェクトテンプレート)](../extensibility/projectitem-element-visual-studio-project-templates.md)」を参照してください。

 \<VSTemplate> \<TemplateContent>
 \<ProjectItem>

## <a name="syntax"></a>構文

```
<ProjectItem
    SubType="Form/Component/CustomControl/UserControl"
    CustomTool="string"
    ItemType="string"
    ReplaceParameters="true/false"
    TargetFileName="TargetFileName.ext">
        FileName.ext
</ProjectItem>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

| 属性 | 説明 |
|---------------------| - |
| `SubType` | 省略可能な属性です。<br /><br /> 複数ファイルの項目テンプレートに含まれる項目のサブタイプを指定します。 この値は、項目を開くためにが使用するエディターを決定するために使用され [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ます。 |
| `CustomTool` | 省略可能な属性です。<br /><br /> プロジェクトファイル内の項目の CustomTool を設定します。 |
| `ItemType` | 省略可能な属性です。<br /><br /> プロジェクトファイル内の項目の ItemType を設定します。 |
| `ReplaceParameters` | 省略可能な属性です。<br /><br /> プロジェクトがテンプレートから作成されたときに置き換える必要があるパラメーター値が項目にあるかどうかを指定するブール値。 既定値は `false` です。 |
| `TargetFileName` | 省略可能な属性です。<br /><br /> テンプレートから作成された項目の名前を指定します。 この属性は、パラメーター置換を使用して項目名を作成する場合に便利です。 |

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|テンプレートの内容を指定します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 `string`テンプレート *.zip* ファイル内のファイルの名前を表す。

## <a name="remarks"></a>注釈
 `ProjectItem` は、の省略可能な子です `TemplateContent` 。

 `TargetFileName`属性を使用すると、パラメーターを使用してファイルの名前を変更できます。 たとえば、 *myfile.txt* ファイルがテンプレート *.zip* ファイルのルートディレクトリに存在するが、[ **新しい項目の追加** ] ダイアログボックスでユーザーが指定したファイル名に基づいてファイル名を指定する場合は、次の XML を使用します。

```xml
<ProjectItem TargetFileName="$fileinputname$.vb">MyFile.vb</ProjectItem>
```

 このテンプレートから項目が作成されると、[ **新しい項目の追加** ] ダイアログボックスでユーザーが入力した名前に基づいてファイル名が作成されます。 これは、複数ファイルの項目テンプレートを作成するときに便利です。 詳細については、「 [方法: 複数ファイルの項目テンプレート](../ide/how-to-create-multi-file-item-templates.md) と [テンプレートパラメーター](../ide/template-parameters.md)を作成する」を参照してください。

## <a name="example"></a>例
 次の例は、クラスの標準項目テンプレートのメタデータを示してい [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] ます。

```
<VSTemplate Type="Item" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyClass</Name>
        <Description>My custom C# class.</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <DefaultName>MyClass.cs</DefaultName>
    </TemplateData>
    <TemplateContent>
        <ProjectItem ReplaceParameters="true">MyClass.cs</ProjectItem>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
- [方法: 複数ファイルの項目テンプレートを作成する](../ide/how-to-create-multi-file-item-templates.md)
- [テンプレート パラメーター](../ide/template-parameters.md)

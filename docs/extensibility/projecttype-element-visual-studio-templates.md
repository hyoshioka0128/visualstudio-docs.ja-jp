---
title: プロジェクトタイプ要素 (Visual Studio テンプレート) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectType
helpviewer_keywords:
- ProjectType element [Visual Studio project templates]
ms.assetid: ccf9d83f-c7f3-49c7-a31f-e1f22bec004c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d794bd5e81e77a892b5a3be38ff73ab805582dd7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701804"
---
# <a name="projecttype-element-visual-studio-templates"></a>プロジェクトの種類要素
[**新しいプロジェクト**] ダイアログ ボックスまたは [**新しい項目の追加**] ダイアログ ボックスで、指定したグループの下に表示されるようにプロジェクト テンプレートを分類します。

> [!WARNING]
> プロジェクト テンプレートは、Visual Studio 2012 以降の C++ でサポートされています。 これらは、Visual Studio 2010 以前のバージョンの C++ ではサポートされていません。

 \<VS テンプレート\<>\<テンプレートデータ>プロジェクトタイプ>

## <a name="syntax"></a>構文

```xml
<ProjectType> CSharp/VisualBasic/VC/Web </ProjectType>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 [なし] :

### <a name="child-elements"></a>子要素
 [なし] :

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックス、または **[新しい項目の追加]** ダイアログ ボックスでどのように表示させるかを定義します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 この値で、テンプレートから作成されるプロジェクトの種類を指定します。値には、次のいずれかの値を含める必要があります。

- `CSharp` : テンプレートが [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] のプロジェクトまたはアイテムを作成するよう指定します。

- `VisualBasic` : テンプレートが [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] のプロジェクトまたはアイテムを作成するよう指定します。

- `Web`: テンプレートが Web プロジェクトまたは Web 項目を作成することを指定します。 要素に`ProjectType`この値が含まれている場合、プロジェクトまたは項目の言語は[、プロジェクトサブタイプ要素 (Visual Studio テンプレート)](../extensibility/projectsubtype-element-visual-studio-templates.md)で定義されます。

## <a name="remarks"></a>Remarks
 `ProjectType` は `TemplateData` に必須の子要素です。

 要素の`ProjectType`値は、**新しいプロジェクトまたは新****しい項目の追加**] ダイアログ ボックスでのテンプレートの場所を指定します。 たとえば、値`ProjectType`がの`CSharp`テンプレートは、[**新しいプロジェクト**] ダイアログ ボックスの **[Visual C#]** ノードの下に表示されます。

 テンプレートのサブタイプは[、プロジェクトサブタイプ](../extensibility/projectsubtype-element-visual-studio-templates.md)要素を使用して指定できます。

## <a name="example"></a>例
 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] アプリケーションでのプロジェクト テンプレートのメタデータの例を次に示します。

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

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ リファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
- [プロジェクトサブタイプ要素](../extensibility/projectsubtype-element-visual-studio-templates.md)

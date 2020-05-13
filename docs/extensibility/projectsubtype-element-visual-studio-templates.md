---
title: プロジェクトサブタイプ要素 (Visual Studio テンプレート) |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701828"
---
# <a name="projectsubtype-element-visual-studio-templates"></a>プロジェクトサブタイプ要素
テンプレートを要素で指定された値のサブカテゴリに分類します`ProjectType`。

 \<VS テンプレート\<>\<テンプレートデータ>プロジェクトサブタイプ>

## <a name="syntax"></a>構文

```xml
<ProjectSubType> SubType </ProjectSubType>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックス、または **[新しい項目の追加]** ダイアログ ボックスでどのように表示させるかを定義します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 この値は、テンプレートのサブカテゴリを指定します。

## <a name="remarks"></a>Remarks
 `ProjectSubType` は、`TemplateData` の子要素で、省略可能な要素です。

 要素`ProjectSubType`は、[プロジェクトの種類](../extensibility/projecttype-element-visual-studio-templates.md)要素にサブカテゴリを提供します。 この値には、次の値を含めることができます。

- `SmartDevice-NETCFv1`: テンプレートがバージョン 1.0 を対象と[!INCLUDE[Compact](../extensibility/includes/compact_md.md)]することを指定します。

- `SmartDevice-NETCFv2`: テンプレートがバージョン 2.0 を対象と[!INCLUDE[Compact](../extensibility/includes/compact_md.md)]することを指定します。

  テンプレートに値`ProjectType``Web`が含まれている場合、要素は`ProjectSubType`テンプレートのプログラミング言語を指定します。 この要素には、次の値を指定できます。

- `CSharp`: テンプレートが Web[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]プロジェクトまたは Web 項目を作成することを指定します。

- `VisualBasic`: テンプレートが Web[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]プロジェクトまたは Web 項目を作成することを指定します。

## <a name="example"></a>例
 次の例は、バージョン 2.0 を対象[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]とするデバイス アプリケーション[!INCLUDE[Compact](../extensibility/includes/compact_md.md)]のプロジェクト テンプレートのメタデータを示しています。

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
- [Visual Studio テンプレート スキーマ リファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
- [プロジェクトの種類要素](../extensibility/projecttype-element-visual-studio-templates.md)

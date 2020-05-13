---
title: 要素を作成する
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#CreateInPlace
helpviewer_keywords:
- CreateInPlace element [Visual Studio Templates]
- <CreateInPlace> element [Visual Studio Templates]
ms.assetid: 420d46ea-2470-4da9-ad8e-95165588a920
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ab2b5d68be069f30c8f71536b6d47cb1ce8823b6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739664"
---
# <a name="createinplace-element-visual-studio-templates"></a>要素を作成する
プロジェクトを作成して指定した場所でパラメータの置換を実行するか、一時的な場所でパラメータの置換を実行して、指定した場所にプロジェクトを保存するかを指定します。

 \<VS テンプレート\<>\<テンプレート データ>作成インプレース>

## <a name="syntax"></a>構文

```
<CreateInPlace> true/false </CreateInPlace>
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

 テキストは、`true` または `false` である必要があります。 場合`true`は、プロジェクトが作成され、パラメーターの置換が **[新しいプロジェクト**]ダイアログ ボックスで指定された場所で実行されます。 パラメーター`false`置換が一時的な場所で実行され、プロジェクトが指定した場所にコピーされます。

## <a name="remarks"></a>Remarks
 `CreateInPlace` は省略可能な要素です。 既定値は `true` です。

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
        <CreateInPlace>false</CreateInPlace>
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
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
- [Visual Studio テンプレート スキーマ リファレンス](../extensibility/visual-studio-template-schema-reference.md)

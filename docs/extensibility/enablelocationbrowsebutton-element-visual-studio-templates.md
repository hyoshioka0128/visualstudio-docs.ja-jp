---
title: 有効に場所の参照ボタン要素マイクロソフトドキュメント
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
ms.openlocfilehash: 263157d5c6fefc208f28caa55475ba329a0d230f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711986"
---
# <a name="enablelocationbrowsebutton-element-visual-studio-templates"></a>有効に場所の参照ボタン要素
[**新しいプロジェクト**] ダイアログ ボックスで **[参照**] ボタンを使用できるように設定します。

 \<>>有効\<にするデータ\<を有効にするテンプレート> テンプレートデータ

## <a name="syntax"></a>構文

```
<EnableLocationBrowseButton> true/false </EnableLocationBrowseButton>
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

 テキストは、 または`true``false`のいずれかで、**新しいプロジェクト**ダイアログ ボックスの **[参照**] ボタンを表示するかどうかを示す必要があります。

## <a name="remarks"></a>Remarks
 `EnableLocationBrowseButton` は省略可能な要素です。 既定値は`true`、 で、[**新しいプロジェクト**] ダイアログ ボックスの **[参照**] ボタンを表示します。

 [**新しいプロジェクト**] ダイアログ ボックスの [**場所**] テキスト ボックスに、新しいプロジェクトを保存するディレクトリを指定します。 [**参照]** ボタンをクリックすると、[**プロジェクトの場所**] ダイアログ ボックスが表示され、コンピュータから使用できる別のディレクトリに簡単に移動し、新しいプロジェクトが保存されているディレクトリとして選択できます。

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
- [Visual Studio テンプレート スキーマ リファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)

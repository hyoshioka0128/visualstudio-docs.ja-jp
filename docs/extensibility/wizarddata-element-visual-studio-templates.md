---
title: ウィザードデータ要素 (Visual Studio テンプレート) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#WizardData
helpviewer_keywords:
- WizardData element [Visual Studio Templates]
- <WizardData> element [Visual Studio Templates]
ms.assetid: d0403a16-5d07-4fe5-b474-19ae3d9fd3ab
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aa3f9d2e971d944b964f4b194d1324ff960fbd24
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740383"
---
# <a name="wizarddata-element-visual-studio-templates"></a>WizardData 要素 (Visual Studio テンプレート)

カスタム XML を指定します。

```xml
\<VSTemplate>
\<WizardData>
```

## <a name="syntax"></a>構文

```xml
<WizardData>
    <!-- XML to pass to the custom wizard extension -->
    ...
</WizardData>
```

## <a name="attributes-and-elements"></a>属性および要素

以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

[なし] :

### <a name="child-elements"></a>子要素

[なし] :

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[VSTemplate](../extensibility/vstemplate-element-visual-studio-templates.md)|必須の要素です。<br /><br /> プロジェクト テンプレート、項目テンプレート、またはスタート キットのすべてのメタデータが含まれます。|

## <a name="text-value"></a>テキスト値

テキスト値は省略可能です。

このテキストは[、WizardExtension](../extensibility/wizardextension-element-visual-studio-templates.md)要素で指定されたカスタム ウィザード拡張機能に渡すカスタム XML を指定します。

## <a name="remarks"></a>Remarks

この要素では、任意の XML を指定できます。 XML はカスタム ウィザード拡張機能にパラメーターとして渡され、この要素の内容を使用できます。 このデータに対する検証は行われません。

**WizardData**要素の内容は、メソッド内のパラメーターの文字列ディクショナリ内のパラメーターとして、変更されずに`IWizard.RunStarted`渡されます。 ディクショナリ キーの名前`$wizarddata$`は です。

## <a name="example"></a>例

C# Windows アプリケーションの標準プロジェクト テンプレートのメタデータを次の例に示します。

```xml
<VSTemplate Version="3.0.0" Type="Item"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyTemplate</Name>
        <Description>Template using IWizard extension</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
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
    <WizardExtension>
        <Assembly>MyWizard, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, Custom=null</Assembly>
        <FullClassName>MyWizard.CustomWizard</FullClassName>
    </WizardExtension>
    <WizardData>
        <!-- XML to pass to the custom wizard extension -->
    </WizardData>
</VSTemplate>
```

## <a name="see-also"></a>関連項目

- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
- [WizardExtension 要素 (Visual Studio テンプレート)](../extensibility/wizardextension-element-visual-studio-templates.md)
- [方法 : プロジェクト テンプレートを組み合わせたウィザードを使用する](../extensibility/how-to-use-wizards-with-project-templates.md)

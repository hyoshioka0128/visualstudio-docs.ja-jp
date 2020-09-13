---
title: Assembly 要素 (Visual Studio テンプレート ウィザード拡張)
titleSuffix: ''
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Assembly
helpviewer_keywords:
- Assembly element [Visual Studio Template Wizard Extension]
- <Assembly> element [Visual Studio Template Wizard Extension]
ms.assetid: 0c3dc280-1753-4ea2-a13c-d31d13b935b2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8a26584a16e290da3278c713924d2046d173eec9
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90037420"
---
# <a name="assembly-element-visual-studio-template-wizard-extension"></a>Assembly 要素 (Visual Studio テンプレートウィザード拡張)
インターフェイスを実装するアセンブリの名前または厳密な名前を指定し `IWizard` ます。

 \<VSTemplate>
\<WizardExtension>
\<Assembly>

## <a name="syntax"></a>構文

```xml
<Assembly>AssemblyName</Assembly>
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
|[WizardExtension](../extensibility/wizardextension-element-visual-studio-templates.md)|テンプレートウィザードをカスタマイズするための登録要素が含まれています。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 このテキストは、インターフェイスを実装するアセンブリを指定し `IWizard` ます。 このアセンブリ名は、完全なアセンブリ名として指定する必要があります。 たとえば、「 `MyAssembly, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11dd0a3a, Custom = null` 」のように入力します。

## <a name="remarks"></a>解説
 `Assembly` は `WizardExtension` に必須の子要素です。

## <a name="example"></a>例
 次の例は、Windows アプリケーションの標準プロジェクトテンプレートのメタデータを示してい [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] ます。

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
    <WizardExtension>
        <Assembly>MyWizard, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11dd0a3a, Custom=null</Assembly>
        <FullClassName>MyWizard.CustomWizard</FullClassName>
    </WizardExtension>
</VSTemplate>
```

## <a name="see-also"></a>関連項目

- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
- [方法: プロジェクトテンプレートでウィザードを使用する](../extensibility/how-to-use-wizards-with-project-templates.md)

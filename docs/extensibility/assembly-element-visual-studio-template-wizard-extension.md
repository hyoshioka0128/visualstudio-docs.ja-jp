---
title: アセンブリ要素 (Visual Studio テンプレート ウィザード拡張機能) |マイクロソフトドキュメント
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
ms.openlocfilehash: 43f5adb8abc17f0509fb58263f307e5051af85dc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740064"
---
# <a name="assembly-element-visual-studio-template-wizard-extension"></a>アセンブリ要素 (Visual Studio テンプレート ウィザード拡張機能)
インターフェイスを実装するアセンブリの名前または厳密な名前を`IWizard`指定します。

 \<VSTemplate \<> ウィザード\<拡張アセンブリ>>

## <a name="syntax"></a>構文

```
<Assembly>AssemblyName</Assembly>
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
|[WizardExtension](../extensibility/wizardextension-element-visual-studio-templates.md)|テンプレート ウィザードをカスタマイズするための登録要素が含まれています。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 このテキストは、インターフェイスを実装するアセンブリ`IWizard`を指定します。 このアセンブリ名は、完全なアセンブリ名として指定する必要があります。 たとえば、「 `MyAssembly, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11dd0a3a, Custom = null` 」のように入力します。

## <a name="remarks"></a>Remarks
 `Assembly` は `WizardExtension` に必須の子要素です。

## <a name="example"></a>例
 次の例は、Windows アプリケーションの標準プロジェクト テンプレートのメタデータ[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]を示しています。

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

- [Visual Studio テンプレート スキーマ リファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
- [方法: ウィザードをプロジェクト テンプレートで使用する](../extensibility/how-to-use-wizards-with-project-templates.md)

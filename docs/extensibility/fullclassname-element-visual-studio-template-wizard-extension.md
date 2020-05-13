---
title: フルクラス名要素 (VS テンプレート ウィザード拡張機能)
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#FullClassName
helpviewer_keywords:
- FullClassName element [Visual Studio project template]
ms.assetid: 651e1010-d529-4856-85ff-c77ceca5d2ed
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3e533fdf5b5497b17949581801721136b18bc2d1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711429"
---
# <a name="fullclassname-element-visual-studio-template-wizard-extension"></a>要素 (Visual Studio テンプレート ウィザード拡張機能)
`IWizard`インターフェイスを実装するクラスの完全修飾名。

 \<VSテンプレート>\<ウィザード拡張>.\<フルクラス名>

## <a name="syntax"></a>構文

```xml
<FullClassName>ClassName</FullClassName>
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

 このテキストは、インターフェイスを実装するクラス`IWizard`を指定します。 指定したクラスは[、Assembly](../extensibility/assembly-element-visual-studio-template-wizard-extension.md)要素で指定されたアセンブリに存在する必要があります。

## <a name="remarks"></a>Remarks
 `FullClassName` は `WizardExtension` に必須の子要素です。

## <a name="example"></a>例
 次の例は、Windows アプリケーションの標準プロジェクト テンプレートのメタデータ[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]を示しています。

```
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
</VSTemplate>
```

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ リファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
- [方法: ウィザードをプロジェクト テンプレートで使用する](../extensibility/how-to-use-wizards-with-project-templates.md)

---
title: FullClassName 要素 (VS テンプレートウィザード拡張)
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
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
ms.openlocfilehash: ed9ceb57f49d8c08b75aa140e45a0f4268f4336c
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85769605"
---
# <a name="fullclassname-element-visual-studio-template-wizard-extension"></a>FullClassName 要素 (Visual Studio テンプレートウィザード拡張)
インターフェイスを実装するクラスの完全修飾名 `IWizard` 。

 \<VSTemplate> \<WizardExtension>
... \<FullClassName>

## <a name="syntax"></a>構文

```xml
<FullClassName>ClassName</FullClassName>
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

 このテキストは、インターフェイスを実装するクラスを指定し `IWizard` ます。 指定されたクラスは、 [assembly](../extensibility/assembly-element-visual-studio-template-wizard-extension.md)要素によって指定されたアセンブリ内に存在する必要があります。

## <a name="remarks"></a>Remarks
 `FullClassName` は `WizardExtension` に必須の子要素です。

## <a name="example"></a>例
 次の例は、Windows アプリケーションの標準プロジェクトテンプレートのメタデータを示してい [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] ます。

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
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
- [方法: プロジェクトテンプレートでウィザードを使用する](../extensibility/how-to-use-wizards-with-project-templates.md)

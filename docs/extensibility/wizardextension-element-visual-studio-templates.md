---
title: ウィザード拡張要素 (Visual Studio テンプレート) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#WizardExtension
helpviewer_keywords:
- WizardExtension element [Visual Studio Templates]
- <WizardExtension> element [Visual Studio Templates]
ms.assetid: d54b01c1-50f5-4b65-828c-686e2321cc8c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fd81b32861114d654aa794b992826589406b1df9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740376"
---
# <a name="wizardextension-element-visual-studio-templates"></a>WizardExtension 要素 (Visual Studio テンプレート)
テンプレート ウィザードをカスタマイズするための登録要素が含まれています。

 \<>.\<ウィザード拡張>

## <a name="syntax"></a>構文

```
<WizardExtension>
    <Assembly>... </Assembly>
    <FullClassName>... </FullClassName>
</WizardExtension>
```

## <a name="attributes-and-elements"></a>属性および要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 [なし] :

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[アセンブリ](../extensibility/assembly-element-visual-studio-template-wizard-extension.md)|必須の要素です。<br /><br /> グローバル アセンブリ キャッシュに表示されるアセンブリの名前または厳密な名前を指定します。 要素には、少なくとも`Assembly`1 つの`WizardExtension`要素が必要です。|
|[FullClassName](../extensibility/fullclassname-element-visual-studio-template-wizard-extension.md)|必須の要素です。<br /><br /> `IWizard`インターフェイスを実装するクラスの完全修飾名。 要素には、少なくとも`FullClassName`1 つの`WizardExtension`要素が必要です。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[VSTemplate](../extensibility/vstemplate-element-visual-studio-templates.md)|プロジェクト テンプレート、項目テンプレート、またはスタート キットのすべてのメタデータが含まれます。|

## <a name="remarks"></a>Remarks
 `WizardExtension` は、`VSTemplate` の子要素で、省略可能な要素です。

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
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)
- [方法 : プロジェクト テンプレートを組み合わせたウィザードを使用する](../extensibility/how-to-use-wizards-with-project-templates.md)

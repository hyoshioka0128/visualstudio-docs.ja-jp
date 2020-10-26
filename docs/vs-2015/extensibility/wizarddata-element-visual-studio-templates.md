---
title: WizardData 要素 (Visual Studio テンプレート) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#WizardData
helpviewer_keywords:
- WizardData element [Visual Studio Templates]
- <WizardData> element [Visual Studio Templates]
ms.assetid: d0403a16-5d07-4fe5-b474-19ae3d9fd3ab
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d7cd59266a69140ba2ea5a7fd1d1b0b0c72f14c2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68201931"
---
# <a name="wizarddata-element-visual-studio-templates"></a>WizardData 要素 (Visual Studio テンプレート)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

カスタム XML を指定します  
  
 \<VSTemplate>  
 \<WizardData>  
  
## <a name="syntax"></a>構文  
  
```  
<WizardData>  
    <!-- XML to pass to the custom wizard extension -->  
    ...  
</WizardData>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[VSTemplate](../extensibility/vstemplate-element-visual-studio-templates.md)|必須の要素です。<br /><br /> プロジェクトテンプレート、項目テンプレート、またはスタートキットのすべてのメタデータが含まれます。|  
  
## <a name="text-value"></a>テキスト値  
 テキスト値は省略可能です。  
  
 このテキストは、 [WizardExtension](../extensibility/wizardextension-element-visual-studio-templates.md) 要素で指定されたカスタムウィザード拡張機能に渡すカスタム XML を指定します。  
  
## <a name="remarks"></a>注釈  
 この要素には、任意の XML を指定できます。 XML は、カスタムウィザード拡張機能にパラメーターとして渡されます。これにより、拡張機能はこの要素の内容を使用できるようになります。 このデータに対する検証は行われません。  
  
 要素の内容は、 `WizardData` メソッドのパラメーターの文字列ディクショナリ内のパラメーターとして、変更されずに渡され `IWizard.RunStarted` ます。 このパラメーターには $WizardData $ という名前が付けられています。  
  
## <a name="example"></a>例  
 次の例は、Windows アプリケーションの標準プロジェクトテンプレートのメタデータを示してい [!INCLUDE[csprcs](../includes/csprcs-md.md)] ます。  
  
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
    <WizardData>  
        <!-- XML to pass to the custom wizard extension -->  
    </WizardData>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>参照  
 [Visual Studio テンプレートスキーマリファレンス](../extensibility/visual-studio-template-schema-reference.md)   
 [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)   
 [WizardExtension 要素 (Visual Studio テンプレート)](../extensibility/wizardextension-element-visual-studio-templates.md)   
 [方法 : プロジェクト テンプレートを組み合わせたウィザードを使用する](../extensibility/how-to-use-wizards-with-project-templates.md)

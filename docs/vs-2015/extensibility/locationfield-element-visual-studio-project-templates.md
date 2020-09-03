---
title: LocationField 要素 (Visual Studio プロジェクトテンプレート) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#LocationField
helpviewer_keywords:
- LocationField element [Visual Studio project templates]
ms.assetid: 6aaaa155-6ce0-4f7f-aa50-8d63d7a7c992
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b28fe0e696b23724758bd877b6031287290f879e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194466"
---
# <a name="locationfield-element-visual-studio-project-templates"></a>LocationField 要素 (Visual Studio プロジェクト テンプレート)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[**新しいプロジェクト**] ダイアログボックスの [**場所**] テキストボックスが、プロジェクトテンプレートに対して有効、無効、または非表示のいずれであるかを指定します。  
  
 \<VSTemplate>  
 \<TemplateData>  
 \<LocationField>  
  
## <a name="syntax"></a>構文  
  
```  
<LocationField> Enabled/Disabled/Hidden </LocationField>  
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートを分類し、 **新しいプロジェクト**での表示方法を定義します。|  
  
## <a name="text-value"></a>テキスト値  
 テキスト値が必要です。  
  
 有効なテキスト値は次のとおりです。  
  
- `Enabled`。 [**新しいプロジェクト**] ダイアログボックスの [**場所**] ボックスが有効になっていることを指定します。  
  
- `Disabled`。 [**新しいプロジェクト**] ダイアログボックスの [**場所**] ボックスが無効になっていることを指定します。  
  
- `Hidden`[**新しいプロジェクト**] ダイアログボックスの [**場所**] ボックスが非表示になるように指定します。  
  
## <a name="remarks"></a>注釈  
 既定値は `Enabled` です。  
  
 [**新しいプロジェクト**] ダイアログボックスの [**場所**] テキストボックスを使用すると、新しいプロジェクトを保存する既定のディレクトリを変更できます。  
  
 要素で指定された値 `Location` は、基になるプロジェクトシステムでサポートされている場合にのみ、ダイアログボックスによって有効になります。  
  
## <a name="example"></a>例  
 [!INCLUDE[csprcs](../includes/csprcs-md.md)] テンプレートのメタデータの例を次に示します。  
  
```  
<VSTemplate Type="Project" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>My template</Name>  
        <Description>A basic template</Description>  
        <Icon>TemplateIcon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
        <LocationField>Disabled</LocationField>  
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
  
## <a name="see-also"></a>参照  
 [Visual Studio テンプレートスキーマリファレンス](../extensibility/visual-studio-template-schema-reference.md)   
 [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)

---
title: "\"/\" 要素 (Visual Studio テンプレート) |Microsoft Docs"
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProvideDefaultName
helpviewer_keywords:
- ProvideDefaultName element [Visual Studio project templates]
ms.assetid: 7b0e7b20-fd6b-42e2-81d0-e5100cea0528
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0bd18dd979436b02cc12a4dab5439bdb5f371e2d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68193892"
---
# <a name="providedefaultname-element-visual-studio-templates"></a>ProvideDefaultName 要素 (Visual Studio テンプレート)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)][**新しい項目の追加**] ダイアログボックスまたは [**新しいプロジェクト**] ダイアログボックスで、プロジェクトシステムがテンプレートの既定の名前を生成するかどうかを指定します。  
  
 \<VSTemplate>  
 \<TemplateData>  
 \<ProvideDefaultName>  
  
## <a name="syntax"></a>構文  
  
```  
<ProvideDefaultName> true/false </ProvideDefaultName>  
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックス、または **[新しい項目の追加]** ダイアログ ボックスでどのように表示させるかを定義します。|  
  
## <a name="text-value"></a>テキスト値  
 テキスト値が必要です。  
  
 テキストはまたはである必要があり `true` `false` ます。これは、[ **新しい項目の追加** ] または [ **新しいプロジェクト** ] ダイアログボックスでテンプレートの既定の名前を生成するかどうかを示します。  
  
## <a name="remarks"></a>注釈  
 `ProvideDefaultName` は省略可能な要素です。 既定値は `true` です。  
  
 `ProvideDefaultName`要素がの場合 `false` 、[**新しい項目の追加**] ダイアログボックスと [**新しいプロジェクト**] ダイアログボックスの [**名前**] ボックスには値が含まれ `<Enter_name>` ます。  
  
 [**新しい項目の追加**] ダイアログボックスと [**新しいプロジェクト**] ダイアログボックスで、プロジェクトまたは項目の既定の名前を指定するには、 [defaultname](../extensibility/defaultname-element-visual-studio-templates.md)要素を使用します。  
  
## <a name="example"></a>例  
 次のコード例では、 `ProvideDefaultName` 要素をに設定し `false` ます。  
  
```  
<VSTemplate Type="Item" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>MyClass</Name>  
        <Description>My custom C# class.</Description>  
        <Icon>Icon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
        <ProvideDefaultName>false</ProvideDefaultName>  
    </TemplateData>  
    <TemplateContent>  
        <ProjectItem>MyClass.cs</ProjectItem>  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>参照  
 [Visual Studio テンプレートスキーマリファレンス](../extensibility/visual-studio-template-schema-reference.md)   
 [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)

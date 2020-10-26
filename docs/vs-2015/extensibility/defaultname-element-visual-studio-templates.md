---
title: DefaultName 要素 (Visual Studio テンプレート) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#DefaultName
helpviewer_keywords:
- DefaultName element [Visual Studio project templates]
ms.assetid: 0ff056c8-b9d2-4747-9308-92adf1811491
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0bc3a18c47b78a312f3bca3762cc4ff3d658a70e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68185285"
---
# <a name="defaultname-element-visual-studio-templates"></a>DefaultName 要素 (Visual Studio テンプレート)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

プロジェクトまたはアイテムの作成時に Visual Studio プロジェクトシステムによって生成される名前を指定します。  
  
 \<VSTemplate>  
 \<TemplateData>  
 \<DefaultName>  
  
## <a name="syntax"></a>構文  
  
```  
<DefaultName>  
    Default Project Name  
</DefaultName>  
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
  
 このテキストは、プロジェクトまたはアイテムの既定の名前を指定します。  
  
## <a name="remarks"></a>注釈  
 `DefaultName` は省略可能な要素です。  
  
 プロジェクトの場合、この要素は、プロジェクトをディスクに格納するディレクトリの名前を指定します。 項目の場合は、ソースファイルのファイル名を指定します。  
  
 プロジェクトまたは項目を作成するときに、[ **名前** ] オプションを使用して既定の名前を変更できます。このオプションは、[ **新しいプロジェクト** ] ダイアログボックスまたは [ **新しい項目の追加** ] ダイアログボックスから使用できます。  
  
 プロジェクトシステムでプロジェクトまたは項目の既定の名前を生成しないようにする場合 [は、[](../extensibility/providedefaultname-element-visual-studio-templates.md) 指定] をに設定し `False` ます。  
  
## <a name="example"></a>例  
 次の例は、クラスの標準項目テンプレートのメタデータを示してい [!INCLUDE[csprcs](../includes/csprcs-md.md)] ます。  
  
```  
<VSTemplate Type="Item" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>MyClass</Name>  
        <Description>My custom C# class.</Description>  
        <Icon>Icon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
        <DefaultName>MyClass.cs</DefaultName>  
    </TemplateData>  
    <TemplateContent>  
        <ProjectItem ReplaceParameters="true">MyClass.cs</ProjectItem>  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>参照  
 [Visual Studio テンプレートスキーマリファレンス](../extensibility/visual-studio-template-schema-reference.md)   
 [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)

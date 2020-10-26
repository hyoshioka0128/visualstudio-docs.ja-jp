---
title: MaxFrameworkVersion 要素 (Visual Studio テンプレート) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <MaxFrameworkVersion> Element (Visual Studio Templates)
- MaxFrameworkVersion Element (Visual Studio Templates)
ms.assetid: f732a9d3-fc29-405b-9298-01ea83fc58b8
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4a1c27e42574429dbb6b2eaeb140db484bf29db5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194331"
---
# <a name="maxframeworkversion-element-visual-studio-templates"></a>MaxFrameworkVersion 要素 (Visual Studio テンプレート)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テンプレートに必要な .NET Framework の最大バージョンを指定します。 [新しいプロジェクト**の追加]** ダイアログボックスの [**ターゲットフレームワークのバージョン**] ボックスで選択した値に基づいて、[**新しいプロジェクトの追加**] ダイアログボックスの [**テンプレート**] セクションにテンプレートを表示するかどうかを決定します。  
  
 \<VSTemplate>  
 \<MaxFrameworkVersion>  
  
## <a name="syntax"></a>構文  
  
```  
<MaxFrameworkVersion> ... </MaxFrameworkVersion>  
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートを分類し、 **新しいプロジェクト** または [ **新しい項目の追加** ] ダイアログボックスでの表示方法を定義します。|  
  
## <a name="text-value"></a>テキスト値  
 テキスト値が必要です。  
  
 このテキストは、テンプレートで許可されている .NET Framework の最大バージョン番号である必要があります。  
  
## <a name="remarks"></a>注釈  
 `MaxFrameworkVersion` は省略可能な要素です。 `TemplateData`.Vstemplate ファイルのセクションの要素は、[**新しいプロジェクトの追加**] ダイアログボックスの [**テンプレート**] セクションのフィルターとして機能します。 [ `MaxFrameworkVersion` **新しいプロジェクトの追加**] ダイアログボックスの [**ターゲットフレームワークのバージョン**] ボックスで選択した値に基づいて、.NET Framework の要件が要素の値未満であるテンプレートのみが表示されます。 要素は、 `MaxFrameworkVersion` 必要な場合を除き、省略する必要があります。したがって、新しいバージョンの .NET Framework で使用されている場合、テンプレートが誤って表示されることはありません。  
  
## <a name="example"></a>例  
 次の例は、標準クラステンプレートのメタデータを示してい [!INCLUDE[csprcs](../includes/csprcs-md.md)] ます。  
  
```  
<VSTemplate Type="Item" Version="3.0.0"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>MyClass</Name>  
        <Description>My custom C# class template.</Description>  
        <Icon>Icon.ico</Icon>  
        <ProjectType>CSharp</ProjectType>  
        <MaxFrameworkVersion>3.5</MaxFrameworkVersion>  
        <DefaultName>MyClass</DefaultName>  
    </TemplateData>  
    <TemplateContent>  
        <ProjectItem>MyClass.cs</ProjectItem>  
    </TemplateContent>  
</VSTemplate>  
```  
  
 この例では、テンプレートに必要な .NET Framework の最大バージョン (で表される) `MaxFrameworkVersion` は3.5 です。 上記のテンプレートは、[**新しいプロジェクトの追加**] ダイアログボックスの [**ターゲットフレームワークのバージョン**] ボックスで3.0 または3.5 を選択した場合にのみ表示されます。  
  
## <a name="see-also"></a>参照  
 [Visual Studio テンプレートスキーマリファレンス](../extensibility/visual-studio-template-schema-reference.md)   
 [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)

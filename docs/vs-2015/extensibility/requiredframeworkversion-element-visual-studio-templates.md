---
title: RequiredFrameworkVersion 要素 (Visual Studio テンプレート) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <RequiredFrameworkVersion> (Visual Studio Templates)
- RequiredFrameworkVersion (Visual Studio Templates)
ms.assetid: 08a4f609-51a5-4723-b89f-99277fb18871
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ce312d7951f4c1be720604c006f9afcd63f364d3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68163650"
---
# <a name="requiredframeworkversion-element-visual-studio-templates"></a>RequiredFrameworkVersion 要素 (Visual Studio テンプレート)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テンプレートで必要な .NET Framework の最小バージョンを指定します。スキーマ階層。  
  
 \<VSTemplate>  
 \<TemplateData>  
 \<RequiredFrameworkVersion>  
  
## <a name="syntax"></a>構文  
  
```  
<RequiredFrameworkVersion> .... </RequiredFrameworkVersion>  
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
  
 このテキストは、テンプレートに必要な .NET Framework の最小バージョン番号である必要があります。  
  
## <a name="remarks"></a>注釈  
 `RequiredFrameworkVersion` は省略可能な要素です。 テンプレートが、.NET Framework の特定の最小バージョン、およびそれ以降のバージョンをサポートしている場合にのみ、この要素を使用します。  
  
## <a name="see-also"></a>参照  
 [Visual Studio テンプレートスキーマリファレンス](../extensibility/visual-studio-template-schema-reference.md)   
 [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)   
 [対象となる特定の .NET Framework バージョンの指定](../ide/targeting-a-specific-dotnet-framework-version.md)

---
title: ProjectExtensions 要素 (MSBuild) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#ProjectExtensions
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- <ProjectExtensions> element [MSBuild]
- ProjectExtensions element [MSBuild]
ms.assetid: f95f312f-ff92-41eb-9469-ad99e236a307
caps.latest.revision: 21
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0afc4f73ed287f753acf87bd0b112e6f5303e996
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62551256"
---
# <a name="projectextensions-element-msbuild"></a>ProjectExtensions 要素 (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクト ファイルに、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 以外の情報を含めることを可能にします。 `ProjectExtensions` 要素内のすべてのものは、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] によって無視されます。  
  
 \<Project>  
 \<ProjectExtensions>  
  
## <a name="syntax"></a>構文  
  
```  
<ProjectExtensions>  
    Non-MSBuild information to include in file.  
</ProjectExtensions>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし  
  
### <a name="child-elements"></a>子要素  
 なし  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[プロジェクト](../msbuild/project-element-msbuild.md)|[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクト ファイルの必須のルート要素です。|  
  
## <a name="remarks"></a>注釈  
 `ProjectExtensions` 要素は [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクトで1 つだけ使用できます。  
  
## <a name="example"></a>例  
 次のコード例は、`ProjectExtensions` 要素に格納されている統合開発環境の情報を示します。  
  
```  
<ProjectExtensions>  
    <VSIDE>  
        <External>  
            <!--  
            Raw XML passed to the IDE by an external source  
            -->  
        </External>  
    </VSIDE>  
</ProjectExtensions>  
```  
  
## <a name="see-also"></a>参照  
 [プロジェクトファイルスキーマリファレンス](../msbuild/msbuild-project-file-schema-reference.md)  
 [MSBuild](msbuild.md)

---
title: CustomParameters 要素 (Visual Studio テンプレート) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#CustomParameters
helpviewer_keywords:
- CustomParameters element [Visual Studio project templates]
ms.assetid: cf3efc91-1532-4022-bbb8-a18658424fee
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3f7be98415a4ab0d6d5c2d00891680e2959e93fe
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62555939"
---
# <a name="customparameters-element-visual-studio-templates"></a>CustomParameters 要素 (Visual Studio テンプレート)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ウィザードがパラメーター置換を行うときに、テンプレートウィザードに渡すカスタムパラメーターをグループ化します。  
  
## <a name="syntax"></a>構文  
  
```  
<CustomParameters>  
    <CustomParameter/>  
    <CustomParameter/>  
</CustomParameters>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[CustomParameter](../extensibility/customparameter-element-visual-studio-templates.md)|省略可能な要素です。<br /><br /> プロジェクトまたは項目がテンプレートから作成されるときに使用する、カスタムパラメーターの名前と値を格納します。 `CustomParameter` 要素に 0 個以上の `CustomParameters` 要素があります。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|テンプレートの内容を指定します。|  
  
## <a name="remarks"></a>注釈  
  
## <a name="example"></a>例  
 次の例は、テンプレートでいくつかのカスタムパラメーターを使用する方法を示しています。 次のカスタムパラメーターを使用してテンプレートからプロジェクトまたは項目が作成されると、テンプレートファイル内のとのすべてのインスタンス `$color1$` が、それぞれとに置き換えられ `$color2$` `Red` `Blue` ます。  
  
```  
<CustomParameters>  
    <CustomParameter Name="$color1$" Value="Red"/>  
    <CustomParameter Name="$color2$" Value="Blue "/>  
</CustomParameters>  
```  
  
## <a name="see-also"></a>参照  
 [CustomParameter 要素 (Visual Studio テンプレート)](../extensibility/customparameter-element-visual-studio-templates.md)   
 [テンプレートパラメーター](../ide/template-parameters.md)   
 [Visual Studio テンプレートスキーマリファレンス](../extensibility/visual-studio-template-schema-reference.md)

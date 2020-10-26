---
title: Assembly 要素 (Visual Studio テンプレート) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Assembly
helpviewer_keywords:
- Assembly element [Visual Studio templates]
- <Assembly> element [Visual Studio templates]
ms.assetid: 9242f76a-1273-4b8a-8f26-6606f91829ef
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 10c894f3507ae760624b6ae18f785aae6016cd5e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184705"
---
# <a name="assembly-element-visual-studio-templates"></a>Assembly 要素 (Visual Studio テンプレート)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

アセンブリに関する情報を指定します。このアセンブリは、プロジェクトにアセンブリの参照を追加するためにテンプレートで使用されます。  
  
 \<VSTemplate>  
 \<TemplateContent>  
 \<References>  
 \<Reference>  
 \<Assembly>  
  
## <a name="syntax"></a>構文  
  
```  
<Assembly> AssemblyName </Assembly>  
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
|[リファレンス](../extensibility/reference-element-visual-studio-templates.md)|項目がプロジェクトに追加されたときに追加するアセンブリ参照を指定します。|  
  
## <a name="text-value"></a>テキスト値  
 テキスト値が必要です。  
  
 このテキストは、項目テンプレートがインスタンス化されるときにプロジェクトに追加するアセンブリを指定します。 このアセンブリ名は、次のいずれかの方法で指定する必要があります。  
  
- 完全なアセンブリ名として指定します。 次に例を示します。  
  
    ```  
    <Assembly>  
        MyAssembly, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, Custom = null.  
    </Assembly>  
    ```  
  
- 単純なテキスト参照として。 次に例を示します。  
  
    ```  
    <Assembly> System </Assembly>  
    ```  
  
## <a name="remarks"></a>解説  
 `Assembly` は `Reference` に必須の子要素です。  
  
 、、およびの各要素は、 `Reference` `References,` `Assembly` 属性値がである .vstemplate ファイルでのみ使用できます `Type` `Item` 。  
  
## <a name="example"></a>例  
 次の例は、 `TemplateContent` 項目テンプレートの要素を示しています。 この XML は、System.dll アセンブリおよび System.Data.dll アセンブリへの参照を追加します。  
  
```  
<TemplateContent>  
    <References>  
        <Reference>  
            <Assembly>  
                System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089  
            </Assembly>  
        </Reference>  
        <Reference>  
            <Assembly>  
                System.Data, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089  
            </Assembly>  
        </Reference>  
    </References>  
    ...  
</TemplateContent>  
```  
  
## <a name="see-also"></a>参照  
 [Visual Studio テンプレートスキーマリファレンス](../extensibility/visual-studio-template-schema-reference.md)   
 [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)

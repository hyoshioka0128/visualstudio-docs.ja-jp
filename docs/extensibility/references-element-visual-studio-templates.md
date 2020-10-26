---
title: References 要素 (Visual Studio テンプレート) |Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#References
helpviewer_keywords:
- <References> element [Visual Studio Templates]
- References element [Visual Studio Templates]
ms.assetid: 1969146d-46bf-422d-8d46-0e9493925003
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ef31c5e7550ec7c6e4570d156d364afcf4ad6819
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80701614"
---
# <a name="references-element-visual-studio-templates"></a>References 要素 (Visual Studio テンプレート)
テンプレートによってプロジェクトに追加されるアセンブリ参照をグループ化します。

 \<VSTemplate> \<TemplateContent>
 \<References>

## <a name="syntax"></a>構文

```xml
<References>
    <Reference>... </Reference>
    <Reference>... </Reference>
    ...
</References>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[リファレンス](../extensibility/reference-element-visual-studio-templates.md)|必須の要素です。<br /><br /> 項目がプロジェクトに追加されたときに追加するアセンブリ参照を指定します。 要素には1つ以上 `Reference` の要素が必要 `References` です。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|テンプレートの内容を指定します。|

## <a name="remarks"></a>解説
 `References` は、`TemplateContent` の子要素で、省略可能な要素です。

 `Reference`要素と `References` 要素は、属性値がである *.vstemplate*ファイルでのみ使用できます `Type` `Item` 。

## <a name="example"></a>例
 次の例は、 `TemplateContent` 項目テンプレートの要素を示しています。 この XML は、 *System.dll* アセンブリおよび *System.Data.dll* アセンブリへの参照を追加します。

```xml
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

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)

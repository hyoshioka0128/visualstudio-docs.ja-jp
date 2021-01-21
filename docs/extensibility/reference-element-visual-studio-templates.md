---
title: Reference 要素 (Visual Studio テンプレート) |Microsoft Docs
description: 参照要素について、および項目がプロジェクトに追加されたときに追加するアセンブリ参照をどのように指定するかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Reference
helpviewer_keywords:
- Reference element [Visual Studio templates]
- <Reference> element [Visual Studio templates]
ms.assetid: 852772ea-c324-42e9-8c8a-6d565414a109
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dcb713a62ebc9a0c3e4daf5aa16f36779b1a1fdc
ms.sourcegitcommit: 86e98df462b574ade66392f8760da638fe455aa0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2020
ms.locfileid: "94903768"
---
# <a name="reference-element-visual-studio-templates"></a>Reference 要素 (Visual Studio テンプレート)
項目がプロジェクトに追加されたときに追加するアセンブリ参照を指定します。

 \<VSTemplate> \<TemplateContent>
 \<References>
 \<Reference>

## <a name="syntax"></a>構文

```xml
<Reference>
    <Assembly> ... </Assembly>
</Reference>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[アセンブリ](../extensibility/assembly-element-visual-studio-templates.md)|必須の要素です。<br /><br /> アセンブリに関する情報を指定します。このアセンブリは、プロジェクトにアセンブリの参照を追加するためにテンプレートで使用されます。 `Assembly`すべての要素には1つの要素が必要 `Reference` です。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[参照](../extensibility/references-element-visual-studio-templates.md)|テンプレートによってプロジェクトに追加されるアセンブリ参照をグループ化します。|

## <a name="remarks"></a>解説
 `Reference` は `References` に必須の子要素です。

 `Reference`要素と `References` 要素は、属性値がである *.vstemplate* ファイルでのみ使用できます `Type` `Item` 。

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
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)

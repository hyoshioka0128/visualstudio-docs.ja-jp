---
title: 参照要素 (Visual Studio テンプレート) |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701614"
---
# <a name="references-element-visual-studio-templates"></a>参照要素 (Visual Studio テンプレート)
テンプレートがプロジェクトに追加するアセンブリ参照をグループ化します。

 \<VSTemplate \<> テンプレート\<コンテンツ>参照>

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
 [なし] :

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[リファレンス](../extensibility/reference-element-visual-studio-templates.md)|必須の要素です。<br /><br /> 項目がプロジェクトに追加されたときに追加するアセンブリ参照を指定します。 要素には 1 つ`Reference`以上の要素`References`が必要です。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|テンプレートの内容を指定します。|

## <a name="remarks"></a>Remarks
 `References` は、`TemplateContent` の子要素で、省略可能な要素です。

 `Reference`および`References`要素は、*.vstemplate*`Type`属性値が . `Item`

## <a name="example"></a>例
 項目テンプレートの要素を`TemplateContent`次の例に示します。 この XML は *、System.dll*アセンブリおよび*System.Data.dll*アセンブリへの参照を追加します。

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
- [Visual Studio テンプレート スキーマ リファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)

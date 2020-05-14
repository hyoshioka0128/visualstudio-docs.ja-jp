---
title: 参照要素 (Visual Studio テンプレート) |マイクロソフトドキュメント
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
ms.openlocfilehash: 11d893f6268a69172d27a0f7caee707767abfe89
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701620"
---
# <a name="reference-element-visual-studio-templates"></a>参照要素 (Visual Studio テンプレート)
項目がプロジェクトに追加されたときに追加するアセンブリ参照を指定します。

 \<VSTemplate \<> テンプレート\<コンテンツ>\<参照>>参照

## <a name="syntax"></a>構文

```xml
<Reference>
    <Assembly> ... </Assembly>
</Reference>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 [なし] :

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[アセンブリ](../extensibility/assembly-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートが、そのアセンブリの参照をプロジェクトに追加するために使用する、アセンブリに関する情報を指定します。 すべての`Reference`要素に`Assembly`1 つの要素が必要です。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[参照](../extensibility/references-element-visual-studio-templates.md)|テンプレートがプロジェクトに追加するアセンブリ参照をグループ化します。|

## <a name="remarks"></a>Remarks
 `Reference` は `References` に必須の子要素です。

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
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)

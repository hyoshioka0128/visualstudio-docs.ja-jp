---
title: 順序の要素 (Visual Studio テンプレート) |Microsoft Docs
description: 順序付け要素について説明し、[新しいプロジェクト] ダイアログボックスまたは [新しい項目の追加] ダイアログボックスに表示されるテンプレートの配置に使用される値を指定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#SortOrder
helpviewer_keywords:
- SortOrder element [Visual Studio Templates]
- <SortOrder> element [Visual Studio Templates]
ms.assetid: 151932c1-f08a-4f78-a8d0-bd2f32211a9c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f07c3b62d1412564fd74c420b31b2a9fed41d1fa
ms.sourcegitcommit: 86e98df462b574ade66392f8760da638fe455aa0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2020
ms.locfileid: "94903755"
---
# <a name="sortorder-element-visual-studio-templates"></a>SortOrder 要素 (Visual Studio テンプレート)
[ **新しいプロジェクト** ] ダイアログボックスまたは [ **新しい項目の追加** ] ダイアログボックスに表示されるテンプレートを、同じカテゴリの他のテンプレートの中に配置するために使用される値を指定します。

 \<VSTemplate> \<TemplateData>
 \<SortOrder>

## <a name="syntax"></a>構文

```
<SortOrder> ... </SortOrder>
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

 `integer`並べ替え順序の値を表す。

## <a name="remarks"></a>解説
 `SortOrder` は省略可能な要素です。 既定値は100で、すべての値は10の倍数である必要があります。

 `SortOrder`ユーザーが作成したテンプレートでは、要素は無視されます。 ユーザーが作成したすべてのテンプレートはアルファベット順に並べ替えられます。

 並べ替え順序の値が低いテンプレートは、[ **新しいプロジェクト** ] ダイアログボックスまたは [ **新しい項目の追加** ] ダイアログボックスで、並べ替え順の値が大きいテンプレートよりも前に表示されます。

## <a name="example"></a>例
 次の例は、標準クラステンプレートのメタデータを示してい [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] ます。

```
<VSTemplate Type="Item" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyClass</Name>
        <Description>My custom C# class template.</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <SortOrder>290</SortOrder>
        <DefaultName>MyClass</DefaultName>
    </TemplateData>
    <TemplateContent>
        <ProjectItem>MyClass.cs</ProjectItem>
    </TemplateContent>
</VSTemplate>
```

 この例では、 `SortOrder` 要素は比較的高いです。 他の [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 項目テンプレートの `SortOrder` 値がよりも小さく、[ `290` **新しい項目** ] ダイアログボックスでこのテンプレートの前に表示される可能性があります。

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレートスキーマリファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)

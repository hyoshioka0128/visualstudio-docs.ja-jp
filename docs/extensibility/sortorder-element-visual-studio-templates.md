---
title: 並べ替え順序要素 (Visual Studio テンプレート) |マイクロソフトドキュメント
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
ms.openlocfilehash: 935d00335a21d3e129e79ce351e554ea93787447
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699963"
---
# <a name="sortorder-element-visual-studio-templates"></a>SortOrder 要素 (Visual Studio テンプレート)
**[新しいプロジェクト**] ダイアログ ボックスまたは [**新しい項目の追加**] ダイアログ ボックスに表示されるテンプレートの中で、同じカテゴリのテンプレートの中で、テンプレートを整列するために使用する値を指定します。

 \<VS テンプレート\<>\<テンプレートデータ>並べ替え順序>

## <a name="syntax"></a>構文

```
<SortOrder> ... </SortOrder>
```

## <a name="attributes-and-elements"></a>属性および要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 [なし] :

### <a name="child-elements"></a>子要素
 [なし] :

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートをカテゴリに分類し、 **[新しいプロジェクト]** ダイアログ ボックス、または **[新しい項目の追加]** ダイアログ ボックスでどのように表示させるかを定義します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 並`integer`べ替え順序の値を表す。

## <a name="remarks"></a>Remarks
 `SortOrder` は省略可能な要素です。 デフォルト値は 100 で、すべての値は 10 の倍数でなければなりません。

 ユーザー`SortOrder`が作成したテンプレートでは、この要素は無視されます。 ユーザーが作成したすべてのテンプレートは、アルファベット順に並べ替えられます。

 並べ替え順序の値が小さいテンプレートは、[**新しいプロジェクト**] または [**新しい項目の追加**] ダイアログ ボックスで、並べ替え順序の値が大きいテンプレートの前に表示されます。

## <a name="example"></a>例
 次の例は、標準[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]クラス テンプレートのメタデータを示しています。

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

 この例では、要素`SortOrder`は比較的高い。 他[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]の項目テンプレートの値は、このテンプレート`SortOrder`より小さい`290`値で、[**新しいアイテム]** ダイアログ ボックスに表示される可能性があります。

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)

---
title: 要素の既定の設定を指定する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProvideDefaultName
helpviewer_keywords:
- ProvideDefaultName element [Visual Studio project templates]
ms.assetid: 7b0e7b20-fd6b-42e2-81d0-e5100cea0528
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 192716198f605a5f6b4f62730e84dcf83b4229cc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701717"
---
# <a name="providedefaultname-element-visual-studio-templates"></a>要素を提供します。
[新しい[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]項目の追加]**ダイアログ**ボックスまたは [**新しいプロジェクト**] ダイアログ ボックスで、プロジェクト システムがテンプレートの既定の名前を生成するかどうかを指定します。

 \<VS テンプレート\<>\<テンプレート データ>既定の名前>を提供します

## <a name="syntax"></a>構文

```xml
<ProvideDefaultName> true/false </ProvideDefaultName>
```

## <a name="attributes-and-elements"></a>属性と要素
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

 テキストは、`true`または`false`のいずれかで、**新しい項目の追加または新しい****プロジェクト**ダイアログ ボックスでテンプレートの既定の名前を生成するかどうかを示す必要があります。

## <a name="remarks"></a>Remarks
 `ProvideDefaultName` は省略可能な要素です。 既定値は `true` です。

 要素が`ProvideDefaultName`の`false`場合は、[**新しい項目の追加**] ダイアログ ボックスと [**新しいプロジェクト**] ダイアログ ボックスの`<Enter_name>`**[名前**] ボックスに値が表示されます。

 [DefaultName](../extensibility/defaultname-element-visual-studio-templates.md)要素を使用して、[**新しい項目の追加]** ダイアログ ボックスおよび **[新しいプロジェクト**] ダイアログ ボックスでプロジェクトまたは項目の既定の名前を指定します。 `ProvideDefaultName`要素の値が`true`の場合、プロジェクトの要素を`DefaultName`省略すると、テンプレートの名前、つまり[Name](../extensibility/name-element-visual-studio-templates.md)要素の値がダイアログ ボックスに表示されます。

## <a name="example"></a>例
 要素を に設定する`ProvideDefaultName`コード例`false`を次に示します。

```
<VSTemplate Type="Item" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyClass</Name>
        <Description>My custom C# class.</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <ProvideDefaultName>false</ProvideDefaultName>
    </TemplateData>
    <TemplateContent>
        <ProjectItem>MyClass.cs</ProjectItem>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ リファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)

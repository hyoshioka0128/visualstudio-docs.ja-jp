---
title: MaxFrameworkVersion 要素 (Visual Studio テンプレート) |Microsoft Docs
description: MaxFrameworkVersion 要素と、テンプレートで必要な .NET Framework の最大バージョンをどのように指定するかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <MaxFrameworkVersion> Element (Visual Studio Templates)
- MaxFrameworkVersion Element (Visual Studio Templates)
ms.assetid: f732a9d3-fc29-405b-9298-01ea83fc58b8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 44345b712f448bd7eedf288d7c58cb4193e1b020
ms.sourcegitcommit: 3d96f7a8c9affab40358c3e81e3472db31d841b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2020
ms.locfileid: "94672426"
---
# <a name="maxframeworkversion-element-visual-studio-templates"></a>MaxFrameworkVersion 要素 (Visual Studio テンプレート)

テンプレートに必要な .NET Framework の最大バージョンを指定します。 [**新しいプロジェクト**] ダイアログボックスの [**ターゲットフレームワークのバージョン**] ドロップダウンで使用できる最大値を決定します。 ユーザーがフレームワークのバージョンを選択できるようにするには、テンプレートの最小 .NET Framework バージョンとして [Requiredframeworkversion](../extensibility/requiredframeworkversion-element-visual-studio-templates.md) も指定する必要があります。

> [!IMPORTANT]
> Visual Studio 2017 バージョン15.6 以降では、[**新しいプロジェクト**] ダイアログの [**テンプレート**] セクションに表示されるテンプレートの [**ターゲットフレームワークのバージョン**] ボックスの一覧が表示されなくなりました。 代わりに、[ **ターゲットフレームワークのバージョン** ] ドロップダウンは、選択したテンプレートのフレームワークの選択として機能します。

 \<VSTemplate> \<TemplateData>
 \<MaxFrameworkVersion>

## <a name="syntax"></a>構文

```xml
<MaxFrameworkVersion> ... </MaxFrameworkVersion>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートを分類し、 **新しいプロジェクト** または [ **新しい項目の追加** ] ダイアログボックスでの表示方法を定義します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 このテキストは、テンプレートで許可されている .NET Framework の最大バージョン番号である必要があります。

## <a name="remarks"></a>注釈

`MaxFrameworkVersion` は省略可能な要素です。 `MaxFrameworkVersion`テンプレートに対してサポートされている .NET Framework バージョンの範囲を誤って制限しないように、必要な場合を除き、要素を省略する必要があります。 .NET Framework がテンプレートに適用されない場合は、省略する必要もあります。

## <a name="example"></a>例

次の例は、標準クラステンプレートのメタデータを示してい [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] ます。

```xml
<VSTemplate Type="Item" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyClass</Name>
        <Description>My custom C# class template.</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>3.0</RequiredFrameworkVersion>
        <MaxFrameworkVersion>4.7.1</MaxFrameworkVersion>
        <DefaultName>MyClass</DefaultName>
    </TemplateData>
    <TemplateContent>
        <ProjectItem>MyClass.cs</ProjectItem>
    </TemplateContent>
</VSTemplate>
```

この例では、テンプレートに必要な .NET Framework の最大バージョン (で表される) `MaxFrameworkVersion` は4.7.1 です。 このテンプレートを使用して作成されたプロジェクトは、4.7.1 までのバージョンを .NET Framework ターゲットにすることができます。

## <a name="see-also"></a>関連項目

- [Visual Studio テンプレート スキーマ参照](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)

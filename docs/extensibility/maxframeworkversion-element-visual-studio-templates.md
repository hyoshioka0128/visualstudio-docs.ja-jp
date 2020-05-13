---
title: 要素のフレームワークのバージョンのバージョンのテンプレートを使用する |マイクロソフトドキュメント
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
ms.openlocfilehash: 9c3acf9c40499417fe180ce470224824cc89a113
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702623"
---
# <a name="maxframeworkversion-element-visual-studio-templates"></a>要素を変更します。

テンプレートに必要な .NET Framework の最大バージョンを指定します。 [**新しいプロジェクト**] ダイアログの **[ターゲット フレームワーク バージョン**] ドロップダウンで使用できる最大値を決定します。 ユーザーがフレームワークのバージョンを選択できるようにするには、テンプレートの最小 .NET Framework バージョンとして[RequiredFrameworkVersion](../extensibility/requiredframeworkversion-element-visual-studio-templates.md)を指定する必要があります。

> [!IMPORTANT]
> Visual Studio 2017 バージョン 15.6 以降、**ターゲット フレームワークバージョン**ドロップダウンは、[**新しいプロジェクト**] ダイアログの **[テンプレート]** セクションに表示されるテンプレートのフィルターではなくなりました。 代わりに、**ターゲット フレームワークバージョン**ドロップダウンは、選択したテンプレートのフレームワーク ピッカーとして機能します。

 \<>>テンプレート\<を>する\<

## <a name="syntax"></a>構文

```xml
<MaxFrameworkVersion> ... </MaxFrameworkVersion>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必須の要素です。<br /><br /> テンプレートを分類し、[**新しいプロジェクト**] ダイアログ ボックスまたは [**新しい項目の追加**] ダイアログ ボックスでの表示方法を定義します。|

## <a name="text-value"></a>テキスト値
 テキスト値が必要です。

 テキストは、テンプレートで許可されている .NET Framework の最大バージョン番号である必要があります。

## <a name="remarks"></a>Remarks

`MaxFrameworkVersion` は省略可能な要素です。 テンプレート`MaxFrameworkVersion`でサポートされている .NET Framework バージョンの範囲を誤って制限しないように、必要でない限り、この要素は省略する必要があります。 また、.NET Framework がテンプレートに適用できない場合は省略する必要があります。

## <a name="example"></a>例

次の例は、標準[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]クラス テンプレートのメタデータを示しています。

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

この例では、 で表される`MaxFrameworkVersion`テンプレートで必要な .NET Framework の最大バージョンは 4.7.1 です。 このテンプレートで作成されたプロジェクトは、4.7.1 までの .NET Framework バージョンを対象とできます。

## <a name="see-also"></a>関連項目

- [Visual Studio テンプレート スキーマ リファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)

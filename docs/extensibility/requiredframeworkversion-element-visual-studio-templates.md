---
title: 必要なフレームワークバージョン要素マイクロソフトドキュメント
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <RequiredFrameworkVersion> (Visual Studio Templates)
- RequiredFrameworkVersion (Visual Studio Templates)
ms.assetid: 08a4f609-51a5-4723-b89f-99277fb18871
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 060ebc0633de67d93257e24c2dff24d2aa0970da
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80701511"
---
# <a name="requiredframeworkversion-element-visual-studio-templates"></a>要素を要求します。

テンプレートに必要な .NET Framework の最小バージョンを指定します。 これにより、[**新しいプロジェクト**] ダイアログに **[ターゲット フレームワークのバージョン**] ドロップダウンが表示されます。 要素`RequiredFrameworkVersion`は、ドロップダウンで使用可能な最小値も決定します。

> [!IMPORTANT]
> Visual Studio 2017 バージョン 15.6 以降、**ターゲット フレームワークバージョン**ドロップダウンは、[**新しいプロジェクト**] ダイアログの **[テンプレート]** セクションに表示されるテンプレートのフィルターではなくなりました。 代わりに、ドロップダウンは選択したテンプレートのフレームワーク ピッカーとして機能します。

 \<VS テンプレート\<>\<テンプレート データ>必要なフレームワークの>

## <a name="syntax"></a>構文

```xml
<RequiredFrameworkVersion> .... </RequiredFrameworkVersion>
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

 テキストは、テンプレートに必要な .NET Framework の最小バージョン番号である必要があります。

## <a name="remarks"></a>Remarks

`RequiredFrameworkVersion` は省略可能な要素です。 この要素は、テンプレートが .NET Framework の特定の最小バージョン (およびそれ以降のバージョン) をサポートしている場合にのみ使用します。 要素を`RequiredFrameworkVersion`指定し、テンプレートが .NET Framework の特定の最小バージョンをサポートしていない場合は、適用できないときに **[ターゲット フレームワークのバージョン**] ドロップダウンが表示されます。

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

この例では、 で表される`RequiredFrameworkVersion`テンプレートで必要な .NET Framework の最小バージョンは 3.0 です。 このテンプレートで作成されたプロジェクトは、3.0 から始まる .NET Framework のバージョンを対象とすることができます。

## <a name="see-also"></a>関連項目

- [Visual Studio テンプレート スキーマ リファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクト テンプレートと項目テンプレートを作成する](../ide/creating-project-and-item-templates.md)
- [フレームワーク対象設定機能の概要](../ide/visual-studio-multi-targeting-overview.md)

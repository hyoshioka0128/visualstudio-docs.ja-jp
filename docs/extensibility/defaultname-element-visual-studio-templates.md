---
title: 既定の名前の要素 (Visual Studio テンプレート) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#DefaultName
helpviewer_keywords:
- DefaultName element [Visual Studio project templates]
ms.assetid: 0ff056c8-b9d2-4747-9308-92adf1811491
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 92bd29824cf1d3b91a7bdaa7220479c583ad0f23
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712306"
---
# <a name="defaultname-element-visual-studio-templates"></a>既定の名前要素
プロジェクトまたは項目の作成時に Visual Studio プロジェクト システムが生成する名前を指定します。

 \<VS テンプレート\<>\<テンプレートデータ>既定の名前>

## <a name="syntax"></a>構文

```
<DefaultName>
    Default Project Name
</DefaultName>
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

 このテキストは、プロジェクトまたは項目の既定の名前を指定します。

## <a name="remarks"></a>Remarks
 `DefaultName` は省略可能な要素です。

 プロジェクトの場合、この要素は、ディスク上にプロジェクトを格納するディレクトリの名前を指定します。 項目の場合は、ソース ファイルのファイル名を指定します。

 プロジェクトまたは項目を作成する場合は、[**Add New Item****名前**] オプションを使用して**Name**既定の名前を変更できます。

 プロジェクト システムでプロジェクトまたは項目の既定の名前を生成しない場合は、[要素の提供を](../extensibility/providedefaultname-element-visual-studio-templates.md)に`False`設定します。

## <a name="example"></a>例
 クラスの標準項目テンプレートのメタデータを次の例に[!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)]示します。

```
<VSTemplate Type="Item" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyClass</Name>
        <Description>My custom C# class.</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <DefaultName>MyClass.cs</DefaultName>
    </TemplateData>
    <TemplateContent>
        <ProjectItem ReplaceParameters="true">MyClass.cs</ProjectItem>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>関連項目
- [Visual Studio テンプレート スキーマ リファレンス](../extensibility/visual-studio-template-schema-reference.md)
- [プロジェクトテンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)

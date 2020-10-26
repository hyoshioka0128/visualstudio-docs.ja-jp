---
title: Visual Studio テンプレートマニフェストスキーマリファレンス |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: bc7d0a81-0df5-41a9-a912-1b30e5da1d13
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dbe46851d9df85569be796b4147217bd7db450ed
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80697979"
---
# <a name="visual-studio-template-manifest-schema-reference"></a>Visual Studio テンプレートマニフェストスキーマリファレンス
このスキーマは、Visual Studio プロジェクトまたは項目テンプレートに対して生成される Visual Studio テンプレートマニフェスト (*vstman*) ファイルの形式を記述します。 また、このスキーマでは、テンプレートに関する場所やその他の関連情報についても説明します。

 : 項目とプロジェクトテンプレートのディレクトリが異なるため、マニフェストには項目テンプレートとプロジェクトテンプレートが混在していてはなりません。

> [!IMPORTANT]
> このマニフェストは、Visual Studio 2017 以降で使用できます。

## <a name="vstemplatemanifest-element"></a>VSTemplateManifest 要素
 マニフェストのルート要素。

### <a name="attributes"></a>属性

- **Version**: テンプレートマニフェストのバージョンを表す文字列。 必須です。

- **Locale**: テンプレートマニフェストのロケールまたはロケールを表す文字列。 ロケール値はすべてのテンプレートに適用されます。 ロケールごとに個別のマニフェストを使用する必要があります。 省略可能。

### <a name="child-elements"></a>子要素

- **VSTemplateContainer** Optional.

- **VSTemplateDir** Optional.

### <a name="parent-element"></a>親要素
 なし。

## <a name="vstemplatecontainer"></a>VSTemplateContainer
 テンプレートマニフェスト要素のコンテナー。 マニフェストには、定義するテンプレートごとに1つのテンプレートコンテナーがあります。

### <a name="attributes"></a>属性
 **VSTemplateType**: テンプレートの種類 ( `"Project"` 、 `"Item"` 、または) を指定する文字列値 `"ProjectGroup"` 。 必須

### <a name="child-elements"></a>子要素

- **RelativePathOnDisk**: ディスク上のテンプレートファイルの相対パス。 また、この場所では、[ **新しいプロジェクト** ] ダイアログボックスまたは [ **新しい項目** ] ダイアログボックスに表示されるテンプレートツリー内のテンプレートの配置も定義されます。 ディレクトリおよび個々のファイルとして展開されたテンプレートの場合、このパスはテンプレートファイルを含むディレクトリを参照します。 *.Zip*ファイルとして展開されたテンプレートの場合、このパスは *.zip*ファイルへのパスである必要があります。

- * * VSTemplateHeader: ヘッダーを記述する [Templatedata](../extensibility/templatedata-element-visual-studio-templates.md) 要素。

### <a name="parent-element"></a>親要素
 **VSTemplateManifest**

## <a name="vstemplatedir"></a>VSTemplateDir
 テンプレートが配置されているディレクトリについて説明します。 マニフェストには複数の **VSTemplateDir** エントリを含めることができます。これにより、ディレクトリがテンプレートカテゴリツリーでの外観を制御するために、ローカライズされた名前と並べ替え順序が提供されます。

 これらの設計により、 **VSTemplateDir** エントリはロケールに指定されていないマニフェストにのみ表示されます。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素

- **RelativePath**: テンプレートのパス。 パスごとに1つのエントリしか存在できないため、最初のエントリはすべてのマニフェストに対して優先されます。

- **LocalizedName**: ローカライズされた名前を指定する **namedescriptionicon** 要素。 省略可能。

- **順序**付け: 並べ替え順序を指定する文字列。 省略可能。

- **ParentFolderOverrideName**: 親フォルダーのオーバーライドされた名前。 省略可能。 この要素には **name 属性が** あり、これは名前を指定する文字列値です。

### <a name="parent-element"></a>親要素
 **VSTemplateManifest**

## <a name="namedescriptionicon"></a>NameDescriptionIcon
 ローカライズされたテンプレートの名前と説明を指定します。 上記の **LocalizedName** を参照してください。

### <a name="attributes"></a>属性

- **Package**: パッケージを示す文字列値です。 省略可能。

- **Id**: id を指定する文字列値。 省略可能。

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-element"></a>親要素
 **LocalizedName**

## <a name="examples"></a>例
 次のコードは、プロジェクトテンプレートの *vstman* ファイルの例です。

```xml
<VSTemplateManifest Version="1.0" Locale="1033" xmlns="http://schemas.microsoft.com/developer/vstemplatemanifest/2015">
  <VSTemplateContainer TemplateType="Project">
    <RelativePathOnDisk>CSharp\1033\TestProjectTemplate</RelativePathOnDisk>
    <TemplateFileName>TestProjectTemplate.vstemplate</TemplateFileName>
    <VSTemplateHeader>
      <TemplateData xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
        <Name>TestProjectTemplate</Name>
        <Description>TestProjectTemplate</Description>
        <Icon>TestProjectTemplate.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
        <SortOrder>1000</SortOrder>
        <TemplateID>aac0aeea-7883-4003-992f-937d53d70ab1</TemplateID>
        <CreateNewFolder>true</CreateNewFolder>
        <DefaultName>TestProjectTemplate</DefaultName>
        <ProvideDefaultName>true</ProvideDefaultName>
      </TemplateData>
    </VSTemplateHeader>
  </VSTemplateContainer>
</VSTemplateManifest>

```

 次のコードは、項目テンプレートの *vstman* ファイルの例です。

```xml
<VSTemplateManifest Version="1.0" Locale="1033" xmlns="http://schemas.microsoft.com/developer/vstemplatemanifest/2015">
  <VSTemplateContainer TemplateType="Item">
    <RelativePathOnDisk>CSharp\1033\ItemTemplate1</RelativePathOnDisk>
    <TemplateFileName>ItemTemplate1.vstemplate</TemplateFileName>
    <VSTemplateHeader>
      <TemplateData xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
        <Name>ItemTemplate1</Name>
        <Description>ItemTemplate1</Description>
        <Icon>ItemTemplate1.ico</Icon>
        <TemplateID>bfeadf8e-a251-4109-b605-516b88e38c8d</TemplateID>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
        <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
        <DefaultName>Class.cs</DefaultName>
      </TemplateData>
    </VSTemplateHeader>
  </VSTemplateContainer>
</VSTemplateManifest>

```

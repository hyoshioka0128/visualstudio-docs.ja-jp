---
title: Visual Studio テンプレート マニフェスト スキーマ リファレンス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: bc7d0a81-0df5-41a9-a912-1b30e5da1d13
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dbe46851d9df85569be796b4147217bd7db450ed
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697979"
---
# <a name="visual-studio-template-manifest-schema-reference"></a>Visual Studio テンプレート マニフェスト スキーマ リファレンス
このスキーマは、Visual Studio プロジェクトまたは項目テンプレート用に生成される Visual Studio テンプレート マニフェスト (*.vstman*) ファイルの形式を記述します。 スキーマには、テンプレートに関する場所やその他の関連情報も記述されます。

 : 項目とプロジェクトのテンプレート ディレクトリが別々に存在するため、マニフェストには項目テンプレートとプロジェクト テンプレートが混在する必要はありません。

> [!IMPORTANT]
> このマニフェストは、Visual Studio 2017 以降で使用できます。

## <a name="vstemplatemanifest-element"></a>要素
 マニフェストのルート要素。

### <a name="attributes"></a>属性

- **バージョン**: テンプレート マニフェストのバージョンを表す文字列。 必須。

- **ロケール**: テンプレート マニフェストのロケールを表す文字列。 ロケール値はすべてのテンプレートに適用されます。 ロケールごとに個別のマニフェストを使用する必要があります。 省略可能。

### <a name="child-elements"></a>子要素

- **コンテナ**オプション。

- **を使用します。** オプション。

### <a name="parent-element"></a>親要素
 [なし] :

## <a name="vstemplatecontainer"></a>コンテナ
 テンプレート マニフェスト要素のコンテナー。 マニフェストには、定義する各テンプレートに対して 1 つのテンプレート コンテナーがあります。

### <a name="attributes"></a>属性
 **VSTemplateType**: テンプレート (`"Project"`、 、`"Item"`または`"ProjectGroup"`) の型を指定する文字列値。 必須

### <a name="child-elements"></a>子要素

- **相対パスオンディスク**: ディスク上のテンプレート ファイルの相対パス。 この場所によって、[**新しいプロジェクト**] または [**新しい項目]** ダイアログに表示されるテンプレート ツリー内のテンプレートの配置も定義されます。 ディレクトリおよび個別のファイルとして展開されたテンプレートの場合、このパスはテンプレート ファイルを含むディレクトリを参照します。 *.zip*ファイルとして配置されたテンプレートの場合、このパスは *.zip*ファイルへのパスにする必要があります。

- **VSTemplate ヘッダー: ヘッダーを記述する[テンプレートデータ](../extensibility/templatedata-element-visual-studio-templates.md)要素。

### <a name="parent-element"></a>親要素
 **マニフェスト**

## <a name="vstemplatedir"></a>を使用します。
 テンプレートが配置されているディレクトリを記述します。 マニフェストには複数の**VSTemplateDir**エントリを含めることで、ローカライズされた名前を指定し、ディレクトリの並べ替え順序を指定して、テンプレート カテゴリ ツリーでの外観を制御できます。

 **VSTemplateDir**エントリは、そのデザインのため、ロケール指定されていないマニフェストにのみ表示される必要があります。

### <a name="attributes"></a>属性
 [なし] :

### <a name="child-elements"></a>子要素

- **相対パス**: テンプレートのパス。 パスごとに 1 つのエントリしか存在できないので、最初のエントリはすべてのマニフェストに勝ちます。

- **ローカライズ名**: ローカライズされた**名前**を指定する要素です。 省略可能。

- **並べ替え順序**: 並べ替え順序を指定する文字列。 省略可能。

- **親フォルダのオーバーライド**名です。 省略可能。 この要素には Name**属性があり**、名前を指定する文字列値です。

### <a name="parent-element"></a>親要素
 **マニフェスト**

## <a name="namedescriptionicon"></a>名前説明アイコン
 ローカライズされたテンプレートの名前と説明を指定します。 上記**の「ローカライズされた名前**」を参照してください。

### <a name="attributes"></a>属性

- **パッケージ**: パッケージを指定する文字列値。 省略可能。

- **ID**: ID を指定する文字列値。 省略可能。

### <a name="child-elements"></a>子要素
 [なし] :

### <a name="parent-element"></a>親要素
 **LocalizedName**

## <a name="examples"></a>使用例
 次のコードは、プロジェクト テンプレート *.vstman*ファイルの例です。

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

 次のコードは、項目テンプレート *.vstman*ファイルの例です。

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

---
title: '[Content_types] .xml ファイル | の構造Microsoft Docs'
description: コンテンツタイプファイルの構造について説明します。このファイルには、VSIX パッケージ内のコンテンツの種類に関する情報が含まれています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- content_types
- content types
- opc
- vsix
ms.assetid: 9c399598-b9fa-4da7-84b5-defbf82e9335
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7117845e4756f8b0e09a8fa603e66448e705b903
ms.sourcegitcommit: 94a57a7bda3601b83949e710a5ca779c709a6a4e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/21/2020
ms.locfileid: "97715224"
---
# <a name="the-structure-of-the-content_typesxml-file"></a>[Content_types] .xml ファイルの構造
VSIX パッケージ内のコンテンツの種類に関する情報を格納します。 Visual Studio では、[Content_Types] .xml ファイルを使用してパッケージをインストールしますが、ファイル自体はインストールしません。

> [!NOTE]
> このトピックは、VSIX パッケージで使用される [Content_Type] .xml ファイルにのみ適用されますが、[Content_Types] .xml ファイルの種類は、 *Open パッケージング規則 (OPC)* 標準の一部です。 詳細については、MSDN Web サイトの「 [OPC: データをパッケージ化するための新しい標準](/archive/msdn-magazine/2007/august/opc-a-new-standard-for-packaging-your-data) 」を参照してください。

## <a name="attributes-and-elements"></a>属性および要素
 次のセクションでは、ルート要素とその属性および子要素について説明します。

### <a name="root-element"></a>Root 要素

|要素|説明|
|-------------|-----------------|
|`Types`|VSIX パッケージ内のファイルの種類を列挙する子要素が含まれています。|

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`Xmlns`|(必須)この [Content_Types] .xml ファイルに使用するスキーマの場所。|

### <a name="attribute-name-attribute"></a>{属性名}属性

| 値 | 説明 |
| - | - |
| `http://schemas.openformats.org/package/2006/content-types` | コンテンツタイプスキーマの場所。 |

### <a name="child-elements"></a>子要素
 `Types` 要素には、任意の数の `Default` 要素を含めることができます。

|要素|説明|
|-------------|-----------------|
|`Default`|VSIX パッケージのコンテンツの種類を記述します。 パッケージ内のすべてのファイルの種類は、独自の要素を持つ必要があり `Default` ます。|

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`Extension`|VSIX パッケージ内のファイルのファイル名拡張子。|
|`ContentType`|ファイル名拡張子に関連付けられているコンテンツの種類について説明します。|

### <a name="attribute-name-attribute"></a>{属性名}属性
 Visual Studio は `ContentType` 、関連付けられている型の次の値を認識 `Extension` します。

|拡張機能|ContentType|
|---------------|-----------------|
|txt|text/plain|
|.pkgdef|text/plain|
|xml|text/xml|
|source.extension.vsixmanifest|text/xml|
|htm または html|text/html|
|rtf|アプリケーション/rtf|
|pdf|アプリケーション/pdf|
|GIF|image/gif|
|jpg または jpeg|イメージ/jpg|
|tiff|image/tiff|
|vsix|アプリケーション/zip|
|zip|アプリケーション/zip|
|dll|application/octet-stream|
|その他のすべてのファイルの種類|application/octet-stream|

## <a name="example"></a>例

### <a name="description"></a>説明
 次の [Content_Types] .xml ファイルには、一般的な VSIX パッケージが記述されています。

### <a name="code"></a>コード

```
<?xml version="1.0" encoding="utf-8" ?>
<Types xmlns="http://schemas.openxmlformats.org/package/2006/content-types">
    <Default Extension="vsixmanifest" ContentType="text/xml" />
    <Default Extension="dll" ContentType="application/octet-stream" />
    <Default Extension="png" ContentType="application/octet-stream" />
    <Default Extension="txt" ContentType="text/plain" />
    <Default Extension="pkgdef" ContentType="text/plain" />
</Types>
```

## <a name="see-also"></a>関連項目
- [VSIX パッケージの構造](../extensibility/anatomy-of-a-vsix-package.md)
- [VSIX 拡張機能スキーマ1.0 リファレンス](/previous-versions/dd393700(v=vs.110))
- [OPC: データをパッケージ化するための新しい標準](/archive/msdn-magazine/2007/august/opc-a-new-standard-for-packaging-your-data)
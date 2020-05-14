---
title: '[Content_types].xml ファイルの構造 |マイクロソフトドキュメント'
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
ms.openlocfilehash: 2761e012d32516265e61c8001491e3c605372ff5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699017"
---
# <a name="the-structure-of-the-content_typesxml-file"></a>[Content_types] .xml ファイルの構造
VSIX パッケージ内のコンテンツの種類に関する情報が含まれています。 Visual Studio では 、パッケージをインストールするのに [Content_Types].xml ファイルが使用されますが、ファイル自体はインストールされません。

> [!NOTE]
> このトピックは VSIX パッケージで使用される [Content_Type].xml ファイルにのみ適用されますが、[Content_Types].xml ファイルの種類は*オープン パッケージ規則 (OPC)* 標準の一部です。 詳細については、「OPC: MSDN Web サイトで[データをパッケージ化するための新しい標準](https://msdn.microsoft.com/magazine/cc163372.aspx)」を参照してください。

## <a name="attributes-and-elements"></a>属性および要素
 次のセクションでは、ルート要素とその属性と子要素について説明します。

### <a name="root-element"></a>Root 要素

|要素|説明|
|-------------|-----------------|
|`Types`|VSIX パッケージ内のファイルの種類を列挙する子要素が含まれています。|

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`Xmlns`|(必須)この [Content_Types].xml ファイルに使用されるスキーマの場所。|

### <a name="attribute-name-attribute"></a>{属性名}属性

| [値] | 説明 |
| - | - |
| `http://schemas.openformats.org/package/2006/content-types` | コンテンツ タイプ スキーマの場所。 |

### <a name="child-elements"></a>子要素
 `Types` 要素には、任意の数の `Default` 要素を含めることができます。

|要素|説明|
|-------------|-----------------|
|`Default`|VSIX パッケージ内のコンテンツ タイプについて説明します。 パッケージ内のすべてのファイルの種類は、独自`Default`の要素を持っている必要があります。|

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|`Extension`|VSIX パッケージ内のファイルのファイル名拡張子。|
|`ContentType`|ファイル名拡張子に関連付けられているコンテンツの種類を示します。|

### <a name="attribute-name-attribute"></a>{属性名}属性
 関連付けられた`Extension`型の次`ContentType`の値が認識されます。

|拡張機能|ContentType|
|---------------|-----------------|
|txt|text/plain|
|プクデフ|text/plain|
|xml|text/xml|
|vsix マニフェスト|text/xml|
|htm または html|text/html|
|Rtf|アプリケーション/rtf|
|pdf|アプリケーション/pdf|
|GIF|image/gif|
|jpg または jpeg|画像/jpg|
|tiff|image/tiff|
|vsix|アプリケーション/ジップ|
|zip|アプリケーション/ジップ|
|dll|application/octet-stream|
|その他のすべてのファイルの種類|application/octet-stream|

## <a name="example"></a>例

### <a name="description"></a>説明
 次の [Content_Types].xml ファイルは、一般的な VSIX パッケージについて説明しています。

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
- [VSIX 拡張スキーマ 1.0 リファレンス](https://msdn.microsoft.com/library/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)
- [OPC: データをパッケージ化するための新しい標準](https://msdn.microsoft.com/magazine/cc163372.aspx)

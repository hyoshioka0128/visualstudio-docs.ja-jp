---
title: '&lt;シグネチャ &gt; (JavaScript) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- <signature> JavaScript XML tag
- signature JavaScript XML tag
ms.assetid: 319138e7-cfbe-4b37-9643-2ddb7f9c63d4
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b4c640c28ada16a8a03943fcd1362d4fd521772c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72671126"
---
# <a name="ltsignaturegt-javascript"></a>&lt;シグネチャ &gt; (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

オーバーロードされた関数のドキュメントを提供するために、関数またはメソッドの一連の関連要素をグループ化します。

## <a name="syntax"></a>構文

```
<signature externalid="id" externalFile="filename"
    helpKeyword="keyword" locid="descriptionID">
</signature>
```

#### <a name="parameters"></a>パラメーター
 `externalid` 省略可能。 `format`要素の属性がの場合 [\<loc>](../ide/loc-javascript.md) `vsdoc` 、この属性は、署名に関連付けられている XML コードを検索するために使用されるメンバー ID を指定します。 `locid` 属性とは異なり、この属性はこの ID を持つメンバーのすべての要素が読み込まれることを指定します。 XML コードに記載された関連説明情報もシグネチャで指定された要素とマージされます。 これによって、ソース ファイルで要素を指定しなくても、サイドカー ファイルに `<capability>` などの追加要素を指定できるようになります。 `externalid` は省略可能な属性です。

 `externalFile` 省略可能。 `externalid` を検索するファイルの名前を指定します。 `externalid` がない場合、この属性は無視されます。 これは省略可能な属性です。 既定値は現在のファイルの名前ですが、ファイル拡張子は .js ではなく .xml です。 既定では、ローカリゼーションのマネージド リソースのルックアップ規則がファイルの検索に使用されます。

 `helpKeyword` 省略可能。 F1 ヘルプのキーワード。

 `locid` 省略可能。 フィールドに関するローカライズ情報用の識別子。 この識別子は、メンバーの ID であるか、または OpenAjax のメタデータで定義されているメッセージ バンドル内の `name` 属性値に対応します。 識別子の型は、タグに指定されている形式によって異なり [\<loc>](../ide/loc-javascript.md) ます。

## <a name="remarks"></a>注釈
 .js ファイル内のオーバーロードされた関数の説明ごとに 1 つの `<signature>` 要素を使用するか、指定された外部メンバー ID ごとに 1 つの `<signature>` 要素を使用します。

 `<signature>` 要素は、ステートメントの前の関数本体に配置する必要があります。 要素を使用して、、または要素を使用する場合は、 [\<summary>](../ide/summary-javascript.md) [\<param>](../ide/param-javascript.md) [\<returns>](../ide/returns-javascript.md) `<signature>` ブロック内に他の要素を配置し `<signature>` ます。

## <a name="example"></a>例
 `<signature>` 要素を使用する方法を次のコード例に示します。

```javascript
// Use of <signature> with externalid.
// Requires use of the <loc> tag to identify the external functions.
function illuminate(light) {
    /// <signature externalid='M:Windows.Devices.Light.Illuminate()' />
    /// <signature externalid='M:Windows.Devices.Light.Illuminate(System.Int32)'>
    ///   <param name='light' type='Number' />
    /// </signature>
}

// Use of <signature> for overloads implemented in JavaScript.
function add(a, b) {
    /// <signature>
    /// <summary>function summary 1</summary>
    /// <param name="a" type="Number">The first number</param>
    /// <param name="b" type="Number">The second number</param>
    /// <returns type="Number" />
    /// </signature>
    /// <signature>
    /// <summary>function summary 2 – differ by number of params</summary>
    /// <param name="a" type="Number">Only 1 parameter</param>
    /// <returns type="Number" />
    /// </signature>
    /// <signature>
    /// <summary>function summary 3 – differ by parameter type</summary>
    /// <param name="a" type="Number">Number parameter</param>
    /// <param name="b" type="String">String parameter</param>
    /// <returns type="Number" />
    /// </signature>
    /// <signature>
    /// <summary>function summary 4 – differ by return type</summary>
    /// <param name="a" type="Number">The first number</param>
    /// <param name="b" type="Number">The second number</param>
    /// <returns type="String" />
    /// </signature>

    return a + b;
}
```

## <a name="see-also"></a>参照
 [XML ドキュメント コメント](../ide/xml-documentation-comments-javascript.md)

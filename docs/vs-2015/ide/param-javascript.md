---
title: '&lt;param &gt; (JavaScript) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- <param> JavaScript XML tag
- param JavaScript XML tag
ms.assetid: 2c4e0167-c1dd-4e54-83f1-c437856bddc1
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ca6207d22d82e607fa589f944230b36b46e633c2
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670361"
---
# <a name="ltparamgt-javascript"></a>&lt;param &gt; (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

関数またはメソッドのパラメーターのドキュメント情報を指定します。

## <a name="syntax"></a>構文

```
<param name="parameterName" type="ParameterType"
    integer="true|false" domElement="true|false"
    mayBeNull="true|false" elementType="ArrayElementType"
    elementInteger="true|false" elementDomElement="true|false"
    elementMayBeNull="true|false" locid="descriptionID"
    parameterArray="true|false" optional="true|false"
    value="code">description
</param>
```

#### <a name="parameters"></a>パラメーター
 `name` 必須。 パラメーターの名前。

 `type` 省略可能。 パラメーターのデータ型。 型は以下のいずれかです。

- `Number` や `Object` など、ECMAScript 5 仕様に含まれる ECMAScript 言語の型。

- `HTMLElement`、`Window`、`Document` などの DOM オブジェクト。

- JavaScript のコンストラクター関数。

  `integer` 省略可能。 `type` が `Number` である場合に、パラメーターが整数かどうかを指定します。 パラメーターが整数であることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。 Visual Studio では、この属性は IntelliSense 情報を提供するためには使用されません。

  `domElement` 省略可能。 この属性は非推奨とされました。この属性より `type` 属性が優先されます。 この属性は、ドキュメント化されたパラメーターが DOM 要素であるかどうかを指定します。 パラメーターが DOM 要素であることを指定する場合は `true` に設定します。それ以外の場合は `false` に設定します。 `type` 属性が設定されておらず `domElement` が `true` に設定されている場合、IntelliSense の入力候補機能では、ドキュメント化されたパラメーターが `HTMLElement` として処理されます。

  `mayBeNull` 省略可能。 ドキュメント化されたパラメーターを null に設定できるかどうかを指定します。 パラメーターを null に設定できることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。 既定値は `false` です。 Visual Studio では、この属性は IntelliSense 情報を提供するためには使用されません。

  `elementType` 省略可能。 `type` が `Array` であれば、この属性は、配列内の要素の型を指定します。

  `elementInteger` 省略可能。 `type` が `Array` であり、`elementType` が `Number` である場合、この属性は、配列内の要素が整数であるかどうかを指定します。 配列内の要素が整数であることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。 Visual Studio では、この属性は IntelliSense 情報を提供するためには使用されません。

  `elementDomElement` 省略可能。 この属性は非推奨とされました。この属性より `elementType` 属性が優先されます。 `type` が `Array` である場合、この属性は、配列内の要素が DOM 要素であるかどうかを指定します。 要素が DOM 要素であることを指定する場合は `true` に設定します。それ以外の場合は `false` に設定します。 `elementType` 属性が設定されておらず `elementDomElement` が `true` に設定されている場合、IntelliSense の入力候補機能では、配列内の各要素が `HTMLElement` として処理されます。

  `elementMayBeNull` 省略可能。 `type` が `Array` である場合、配列内の要素を null に設定できるかどうかを指定します。 配列内の要素を null に設定できることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。 既定値は `false` です。 Visual Studio では、この属性は IntelliSense 情報を提供するためには使用されません。

  `locid` 省略可能。 パラメーターに関するローカライズ情報用の識別子。 この識別子は、メンバーの ID であるか、または OpenAjax のメタデータで定義されているメッセージ バンドル内の `name` 属性値に対応します。 この識別子の型は、[\<loc>](../ide/loc-javascript.md) 要素で指定された形式によって異なります。

  `parameterArray` 省略可能。 `String.format` 関数でサポートされるパラメーターの繰り返しと同様に、ドキュメント化されたパラメーターを関数呼び出しで繰り返すことができるかどうかを指定します。 パラメーターを繰り返すことができることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。 Visual Studio では、この属性は IntelliSense 情報を提供するためには使用されません。

  `optional` 省略可能。 呼び出し元の関数で、ドキュメント化されたパラメーターが省略可能であるかどうかを指定します。 パラメーターが省略可能であることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。

  `value` 省略可能。 関数コード自体ではなく、IntelliSense による使用のための評価が必要なコードを指定します。 パラメーターの型が定義されていない場合に、この属性を使用して型情報を提供できます。 たとえば、`value=’1’` を使用して、パラメーターの型を数値として扱うことができます。

  `description` 省略可能。 パラメーターの説明。

## <a name="remarks"></a>解説
 必須属性は `name` だけです。 他のすべての属性は省略可能です。

 関数に注釈を付けるために使用する要素 ( [\<summary >](../ide/summary-javascript.md)、 [\<param >](../ide/param-javascript.md)、 [\<returns](../ide/returns-javascript.md)> など) は、ステートメントの前に関数本体に配置する必要があります。

 同じ名前を持つ複数の `<param>` 要素がある場合は、`<param>` 要素の 1 つが使用され、重複する要素は無視されます。 どの要素を使用するかを決める動作は定義されていません。 `name` が存在しないパラメーターを参照している場合、その要素は無視されます。

## <a name="example"></a>例
 `<param>` 要素を使用する方法を次のコード例に示します。

```javascript
function areaFunction(radiusParam)
{
    /// <summary>Determines the area of a circle when provided a radius parameter.</summary>
    /// <param name="radiusParam" type="Number">The radius of the circle.</param>
    /// <returns type="Number">The area.</returns>
    var areaVal;
    areaVal = Math.PI * radiusParam * radiusParam;
    return areaVal;
}

// Uses of <param> with the value attribute.

function calculate(a) {
    /// <param name='a' value='1'/>
    a.    // Completion list for a Number.
}

function calculate(a) {
    /// <param name='a' value='{x:0,y:0}'/>
    a.    // x and y appear in the completion list.
}

```

## <a name="see-also"></a>関連項目
 [XML ドキュメント コメント](../ide/xml-documentation-comments-javascript.md)

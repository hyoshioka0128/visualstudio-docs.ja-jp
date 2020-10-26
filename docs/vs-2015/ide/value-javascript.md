---
title: '&lt;value &gt; (JavaScript) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- <value> JavaScript XML tag
- value JavaScript XML tag
ms.assetid: 983e31de-cb1d-411e-b60d-eea6698a26f6
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: aefe710cc730d5624abc01bbdfc54d9961788787
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656400"
---
# <a name="ltvaluegt-javascript"></a>&lt;値 &gt; (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ECMAScript 3 プロパティの `get` および `set` 関数のドキュメント情報を指定します。

## <a name="syntax"></a>構文

```
<value type="ValueType" integer="true|false"
    domElement="true|false" mayBeNull="true|false"
    elementType="ArrayElementType" elementInteger="true|false"
    elementDomElement="true|false" elementMayBeNull="true|false"
    locid="descriptionID">description
</value>
```

#### <a name="parameters"></a>パラメーター
 `type` 省略可能。 プロパティのデータ型。 型は以下のいずれかです。

- `Number` や `Object` など、ECMAScript 5 仕様に含まれる ECMAScript 言語の型。

- `HTMLElement`、`Window`、`Document` などの DOM オブジェクト。

- JavaScript のコンストラクター関数。

  `integer` 省略可能。 `type` が `Number` である場合に、プロパティが整数かどうかを指定します。 プロパティが整数であることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。 Visual Studio では、この属性は IntelliSense 情報を提供するためには使用されません。

  `domElement` 省略可能。 この属性は非推奨とされました。この属性より `type` 属性が優先されます。 この属性は、ドキュメント化されたプロパティが DOM 要素であるかどうかを指定します。 プロパティが DOM 要素であることを指定する場合は `true` に設定します。それ以外の場合は `false` に設定します。 `type` 属性が設定されておらず `domElement` が `true` に設定されている場合、IntelliSense の入力候補機能では、ドキュメント化されたプロパティが `HTMLElement` として処理されます。

  `mayBeNull` 省略可能。 ドキュメント化されたプロパティを null に設定できるかどうかを指定します。 プロパティを null に設定できることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。 既定値は `false` です。 Visual Studio では、この属性は IntelliSense 情報を提供するためには使用されません。

  `elementType` 省略可能。 `type` が `Array` であれば、この属性は、配列内の要素の型を指定します。

  `elementInteger` 省略可能。 `type` が `Array` であり、`elementType` が `Number` である場合、この属性は、配列内の要素が整数であるかどうかを指定します。 配列内の要素が整数であることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。 Visual Studio では、この属性は IntelliSense 情報を提供するためには使用されません。

  `elementDomElement` 省略可能。 この属性は非推奨とされました。この属性より `elementType` 属性が優先されます。 `type` が `Array` である場合、この属性は、配列内の要素が DOM 要素であるかどうかを指定します。 要素が DOM 要素であることを指定する場合は `true` に設定します。それ以外の場合は `false` に設定します。 `elementType` 属性が設定されておらず `elementDomElement` が `true` に設定されている場合、IntelliSense の入力候補機能では、配列内の各要素が `HTMLElement` として処理されます。

  `elementMayBeNull` 省略可能。 `type` が `Array` である場合、配列内の要素を null に設定できるかどうかを指定します。 配列内の要素を null に設定できることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。 既定値は `false` です。 Visual Studio では、この属性は IntelliSense 情報を提供するためには使用されません。

  `locid` 省略可能。 プロパティに関するローカライズ情報用の識別子。 この識別子は、メンバーの ID であるか、または OpenAjax のメタデータで定義されているメッセージ バンドル内の `name` 属性値に対応します。 識別子の型は、要素で指定された形式によって異なり [\<loc>](../ide/loc-javascript.md) ます。

  `description` 省略可能。 プロパティの説明。

## <a name="remarks"></a>注釈
 ECMAScript 5 プロパティは、要素を使用し [\<summary>](../ide/summary-javascript.md) ます。

 `<value>` または `get` 関数の直前の `set` 要素を使用します。

## <a name="example"></a>例
 次のコード例に、`<value>` 関数で `get` 要素を使用する方法を示します。

```javascript
function Sys$CancelEventArgs$get_cancel() {
    /// <value type="Boolean" locid="P:J#Sys.CancelEventArgs.cancel"></value>
    if (arguments.length !== 0) throw Error.parameterCount();
    return this._cancel();
}
```

## <a name="see-also"></a>参照
 [XML ドキュメント コメント](../ide/xml-documentation-comments-javascript.md)

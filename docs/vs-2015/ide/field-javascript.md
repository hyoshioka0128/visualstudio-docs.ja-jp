---
title: '&lt;field &gt; (JavaScript) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- <field> JavaScript XML tag
- field JavaScript XML tag
ms.assetid: c494bae0-3095-42a3-aa0a-4c415188c65c
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a3fc786e4d99d1eaff4a8b152ea9496ce8400ff1
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663851"
---
# <a name="ltfieldgt-javascript"></a>&lt;field &gt; (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

オブジェクトで定義されているフィールドまたはメンバーについて、説明などのドキュメント化情報を指定します。

## <a name="syntax"></a>構文

```
<field name="fieldName" static="true|false"
    type="FieldType" integer="true|false"
    domElement="true|false" mayBeNull="true|false"
    elementType="ArrayElementType" elementInteger="true|false"
    elementDomElement="true|false" elementMayBeNull="true|false"
    helpKeyword="keyword" locid="descriptionID"
    value="code">description
</field>
```

#### <a name="parameters"></a>パラメーター
 `name` フィールドまたはメンバーの名前。 `<field>` 要素がコンストラクター関数で使用されている場合は、そのタグが適用されるメンバーを定義する `name` が必要になります。 直接 `<field>` 要素がフィールドの注釈として使用されている場合、この属性は無視され、Visual Studio で使用される名前が、ソース コード内の実際のフィールドの名前になります。

 `static` 省略可能。 フィールドがコンストラクター関数のメンバーであるか、コンストラクター関数によって返されるオブジェクトのメンバーであるかを指定します。 コンストラクター関数のメンバーとしてフィールドを処理する場合は、`true` に設定します。 コンストラクター関数によって返されるオブジェクトのメンバーとしてフィールドを処理する場合は、`false` に設定します。

 `type` 省略可能。 フィールドのデータ型。 型は以下のいずれかです。

- `Number` や `Object` など、ECMAScript 5 仕様に含まれる ECMAScript 言語の型。

- `HTMLElement`、`Window`、`Document` などの DOM オブジェクト。

- JavaScript のコンストラクター関数。

  `integer` 省略可能。 `type` が `Number` である場合に、フィールドが整数かどうかを指定します。 フィールドが整数であることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。 Visual Studio では、この属性は IntelliSense 情報を提供するためには使用されません。

  `domElement` 省略可能。 この属性は非推奨とされました。この属性より `type` 属性が優先されます。 この属性は、ドキュメント化されたフィールドが DOM 要素であるかどうかを指定します。 フィールドが DOM 要素であることを指定する場合は `true` に設定します。それ以外の場合は `false` に設定します。 `type` 属性が設定されておらず `domElement` が `true` に設定されている場合、IntelliSense の入力候補機能では、ドキュメント化されたフィールドが `HTMLElement` として処理されます。

  `mayBeNull` 省略可能。 ドキュメント化されたフィールドを null に設定できるかどうかを指定します。 フィールドを null に設定できることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。 既定値は `false` です。 Visual Studio では、この属性は IntelliSense 情報を提供するためには使用されません。

  `elementType` 省略可能。 `type` が `Array` であれば、この属性は、配列内の要素の型を指定します。

  `elementInteger` 省略可能。 `type` が `Array` であり、`elementType` が `Number` である場合、この属性は、配列内の要素が整数であるかどうかを指定します。 配列内の要素が整数であることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。 Visual Studio では、この属性は IntelliSense 情報を提供するためには使用されません。

  `elementDomElement` 省略可能。 この属性は非推奨とされました。この属性より `elementType` 属性が優先されます。 `type` が `Array` である場合、この属性は、配列内の要素が DOM 要素であるかどうかを指定します。 要素が DOM 要素であることを指定する場合は `true` に設定します。それ以外の場合は `false` に設定します。 `elementType` 属性が設定されておらず `elementDomElement` が `true` に設定されている場合、IntelliSense の入力候補機能では、配列内の各要素が `HTMLElement` として処理されます。

  `elementMayBeNull` 省略可能。 `type` が `Array` である場合、配列内の要素を null に設定できるかどうかを指定します。 配列内の要素を null に設定できることを示す場合は `true` に設定します。それ以外の場合は `false` に設定します。 既定値は `false` です。 Visual Studio では、この属性は IntelliSense 情報を提供するためには使用されません。

  `helpKeyword` 省略可能。 F1 ヘルプのキーワード。

  `locid` 省略可能。 フィールドに関するローカライズ情報用の識別子。 この識別子は、メンバーの ID であるか、または OpenAjax のメタデータで定義されているメッセージ バンドル内の `name` 属性値に対応します。 この識別子の型は、[\<loc>](../ide/loc-javascript.md) タグで指定された形式によって異なります。

  `value` 省略可能。 関数コード自体ではなく、IntelliSense による使用のための評価が必要なコードを指定します。 `<field>` では、コンストラクター関数でこの属性がサポートされますが、オブジェクト リテラルではサポートされません。 フィールドの型が定義されていない場合に、この属性を使用して型情報を提供できます。 たとえば、`value=’1’` を使用して、フィールドの種類を数値として扱うことができます。

  `description` 省略可能。 フィールドの説明。

## <a name="remarks"></a>解説
 コンストラクター関数内のフィールドをドキュメント化する場合は、`name` 属性が必要です。 それ以外のすべてのシナリオでは、`<field>` 要素の属性はすべて省略可能です。

 コンストラクター関数をドキュメント化する場合は、`<field>` 要素をフィールド宣言の直前に記述する必要があります。 `name` 属性は、ソース コードで使用されているフィールド名と一致する必要があります。 オブジェクトのメンバーの場合、`name` 要素がオブジェクト メンバー宣言の直前にあれば、`<field>` 属性は省略できます。

## <a name="example"></a>例
 `<field>` 要素を使用する方法を次のコード例に示します。

```javascript
// Use of <field> in an object definition.
var Rectangle = {
    /// <field type='Number'>The width of the rectangle.</field>
    wid: 5,
    /// <field type='Number'>The length of the rectangle.</field>
    len: 0,
    /// <field type='Number'>Returns the area of the rectangle.</field>
    getArea: function (wid, len) {
        return len * wid;
    }
}

// Use of <field> in a constructor function.
// The name attribute is required.
function Engine() {
    /// <field name='HorsePower' type='Number'>The engine's horsepower.</field>
    this.HorsePower = 150;
}
```

## <a name="example"></a>例
 次の例は、`<field>` 属性を `static` に設定して `true` 要素を使用する方法を示しています。

```javascript
function Engine() {
    /// <field name='HorsePower' static='true' type='Number'>static field desc.</field>
}

Engine.HorsePower = 140;
// IntelliSense on the field is available here.
Engine.

```

## <a name="example"></a>例
 次の例は、`<field>` 属性を `static` に設定して `false` 要素を使用する方法を示しています。

```javascript
function Engine() {
    /// <field name='HorsePower' static='false' type='Number'>Non-static field desc.</field>
}

Engine.HorsePower = 140;
var eng = new Engine();
// IntelliSense on the field is available here.
eng.

```

## <a name="example"></a>例
 次の例は、`<field>` 属性を指定して `value` 要素を使用する方法を示しています。

```javascript
function calculator(a) {
    /// <field name='f' value='1'/>
}
new calculator().f.   // Completion list for a Number.

```

## <a name="see-also"></a>関連項目
 [XML ドキュメント コメント](../ide/xml-documentation-comments-javascript.md)

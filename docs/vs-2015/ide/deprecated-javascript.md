---
title: '&lt;deprecated &gt; (JavaScript) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: cf33d371-59da-4310-95ee-d7524fd9d58c
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 343f3ebe4bea7ee999f60741c189f35defb0ac7b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665801"
---
# <a name="ltdeprecatedgt-javascript"></a>&lt;deprecated &gt; (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

非推奨の関数またはメソッドを指定します。

## <a name="syntax"></a>構文

```
<deprecated
    type="deprecate|remove"
    locid="descriptionID">description
</deprecated>
```

#### <a name="parameters"></a>パラメーター
 `type` 省略可能。 関数またはメソッドが将来のリリースで削除されるかどうか、または関数またはメソッドが既に削除されていて、使用するとエラーが発生することがあるかどうかを指定します。 関数またはメソッドが将来のリリースで削除されることを指定するには、`deprecate` に設定します。 関数またはメソッドが既に削除されたことを指定するには、`remove` に設定します。

 `locid` 省略可能。 関数またはメソッドに関するローカライズ情報用の識別子。 この識別子は、メンバーの ID であるか、または OpenAjax のメタデータで定義されているメッセージ バンドル内の `name` 属性値に対応します。 この識別子の型は、[\<loc>](../ide/loc-javascript.md) 要素で指定された形式によって異なります。

 `description` 省略可能。 非推奨となる関数またはメソッドの説明。

## <a name="remarks"></a>解説
 `<deprecated>` など、関数の注釈に使用される要素は、ステートメントの前の関数本体に配置する必要があります。 関数を非推奨としてマークした場合は、 [\<summary >](../ide/summary-javascript.md)要素を `<deprecated>` 要素に置き換えることをお勧めします。

## <a name="example"></a>例
 次のコードに、`<deprecated>` 要素を使用する方法を示します。

```javascript
function areaFunction(radiusParam) {
    /// <deprecated type="deprecate" >Determines the area of a circle when supplied a radius parameter.</deprecated>
    /// <param name="radiusParam" type="Number">The radius of the circle.</param>
    /// <returns type="Number">The area.</returns>
    var areaVal;
    areaVal = Math.PI * radiusParam * radiusParam;
    return areaVal;
}

```

## <a name="see-also"></a>関連項目
 [XML ドキュメント コメント](../ide/xml-documentation-comments-javascript.md)

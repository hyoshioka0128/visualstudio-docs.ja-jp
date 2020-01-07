---
title: '&lt;概要&gt; (JavaScript) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- summary JavaScript XML tag
- <summary> JavaScript XML tag
ms.assetid: 6540582d-bdb3-42ec-ad2f-c176783e6f9c
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f283c2c1825c4b8b02fb5b044ce113231a919317
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72646850"
---
# <a name="ltsummarygt-javascript"></a>&lt;概要&gt; (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

関数またはメソッドの説明を指定します。

## <a name="syntax"></a>構文

```
<summary locid="descriptionID">description
</summary>
```

#### <a name="parameters"></a>パラメーター
 `locid` 省略可能。 関数またはメソッドに関するローカライズ情報用の識別子。 この識別子は、メンバーの ID であるか、または OpenAjax のメタデータで定義されているメッセージ バンドル内の `name` 属性値に対応します。 この識別子の型は、[\<loc>](../ide/loc-javascript.md) 要素で指定された形式によって異なります。

 `description` 省略可能。 関数またはメソッドの説明。

## <a name="remarks"></a>解説
 [\<summary>](../ide/summary-javascript.md)、[\<param>](../ide/param-javascript.md)、[\<returns>](../ide/returns-javascript.md) など、関数の注釈に使用される要素は、ステートメントの前の関数本体に配置する必要があります。

## <a name="example"></a>例
 次のコードに、`<summary>` 要素を使用する方法を示します。

```javascript
function areaFunction(radiusParam)
{
    /// <summary>Determines the area of a circle when supplied a radius parameter.</summary>
    /// <param name="radiusParam" type="Number">The radius of the circle.</param>
    /// <returns type="Number">The area.</returns>
    var areaVal;
    areaVal = Math.PI * radiusParam * radiusParam;
    return areaVal;
}

```

## <a name="see-also"></a>関連項目
 [XML ドキュメント コメント](../ide/xml-documentation-comments-javascript.md)

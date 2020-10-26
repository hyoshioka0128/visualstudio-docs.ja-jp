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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
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
 `locid` 省略可能。 関数またはメソッドに関するローカライズ情報用の識別子。 この識別子は、メンバーの ID であるか、または OpenAjax のメタデータで定義されているメッセージ バンドル内の `name` 属性値に対応します。 識別子の型は、要素で指定された形式によって異なり [\<loc>](../ide/loc-javascript.md) ます。

 `description` 省略可能。 関数またはメソッドの説明。

## <a name="remarks"></a>注釈
 、、およびを含む関数に注釈を付けるために使用する要素は、 [\<summary>](../ide/summary-javascript.md) [\<param>](../ide/param-javascript.md) ステートメントの前の [\<returns>](../ide/returns-javascript.md) 関数本体に配置する必要があります。

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

## <a name="see-also"></a>参照
 [XML ドキュメント コメント](../ide/xml-documentation-comments-javascript.md)

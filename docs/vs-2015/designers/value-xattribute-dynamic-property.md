---
title: Value (XAttribute 動的プロパティ) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
api_name:
- XAttribute.Value
api_type:
- Assembly
ms.assetid: 019733d2-e050-4120-b537-831cd3fc008e
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e9a31b4c4182ed67a3e67d3c25c2c5ccf50e083f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72664049"
---
# <a name="value-xattribute-dynamic-property"></a>Value (XAttribute 動的プロパティ)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

XML 属性の値を取得または設定します。

## <a name="syntax"></a>構文

```
attrib.Value
```

## <a name="property-valuereturn-value"></a>プロパティ値/戻り値
 この属性の値を表す <xref:System.String> です。

## <a name="exceptions"></a>例外

|例外の種類|条件|
|--------------------|---------------|
|<xref:System.ArgumentNullException>|設定時に `value` が `null` である場合に発生します。|

## <a name="remarks"></a>Remarks
 このプロパティは、<xref:System.Xml.Linq.XAttribute.Value%2A> クラスの <xref:System.Xml.Linq.XAttribute?displayProperty=fullName> プロパティに相当します。ただし、この動的プロパティは変更通知もサポートします。

## <a name="see-also"></a>参照
 [Xattribute クラスの動的プロパティ](../designers/xattribute-class-dynamic-properties.md)[属性](../designers/attribute-xelement-dynamic-property.md)の <xref:System.Xml.Linq.XAttribute.Value%2A?displayProperty=fullName>

---
title: Attribute (XElement 動的プロパティ) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 8440fc7d-b3b4-4726-8ec8-492e6af79642
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 551e072b05e7a88ff9624c5d16e4aa199a6afd66
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657982"
---
# <a name="attribute-xelement-dynamic-property"></a>Attribute (XElement 動的プロパティ)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定された展開名に対応する属性のインスタンスの取得に使用するインデクサーを取得します。

## <a name="syntax"></a>構文

```
elem.Attribute[{namespaceName}attribName]
```

## <a name="property-valuereturn-value"></a>プロパティ値/戻り値
 `XAttribute Item(String expandedName)` 型のインデクサー。 このインデクサーは、指定された属性の展開名を受け取り、対応する <xref:System.Xml.Linq.XAttribute> を返します。指定された名前を持つ属性がない場合は、`null` を返します。

## <a name="remarks"></a>Remarks
 このプロパティは、<xref:System.Xml.Linq.XElement.Attribute%2A> クラスの <xref:System.Xml.Linq.XElement?displayProperty=fullName> メソッドに相当します。

## <a name="see-also"></a>参照
 <xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=fullName>[XElement クラスの動的プロパティ](../designers/xelement-class-dynamic-properties.md)[値](../designers/value-xattribute-dynamic-property.md)

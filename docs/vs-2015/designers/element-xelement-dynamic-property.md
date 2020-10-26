---
title: Element (XElement 動的プロパティ) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
api_name:
- XElement.Element
api_type:
- Assembly
ms.assetid: c6c25b8d-a1da-41ff-aeff-867ff1dcf749
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3c6171a5dedfd6985a6f54e748011bf86e03f4d3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72664648"
---
# <a name="element-xelement-dynamic-property"></a>Element (XElement 動的プロパティ)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定された展開名に対応する子要素のインスタンスを取得するためのインデクサーを取得します。

## <a name="syntax"></a>構文

```
elem.Element[{namespaceName}localName]
```

## <a name="property-valuereturn-value"></a>プロパティ値/戻り値
 `XElement Item(String expandedName)` 型のインデクサー。 このインデクサーは、展開名のパラメーターを取得し、対応する <xref:System.Xml.Linq.XElement> を返します。指定された名前を持つ要素がない場合は、`null` を返します。

## <a name="remarks"></a>Remarks
 このプロパティは、<xref:System.Xml.Linq.XContainer.Element%2A> クラスの <xref:System.Xml.Linq.XContainer?displayProperty=fullName> メソッドに相当します。

## <a name="see-also"></a>参照
 <xref:System.Xml.Linq.XContainer.Element%2A?displayProperty=fullName>[XElement クラスの動的プロパティ](../designers/xelement-class-dynamic-properties.md)[要素](../designers/elements-xelement-dynamic-property.md)

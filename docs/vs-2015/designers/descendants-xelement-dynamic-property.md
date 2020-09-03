---
title: Descendants (XElement 動的プロパティ) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 9611d00f-23bf-444b-ab0c-f30701bfc13d
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 0b0496a04219c88573b3b555ef879a046d90faa3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72664780"
---
# <a name="descendants-xelement-dynamic-property"></a>Descendants (XElement 動的プロパティ)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

現在の要素の子孫要素のうち指定された拡張名に一致するすべての子孫要素を取得するためのインデクサーを取得します。

## <a name="syntax"></a>構文

```
elem.Descendants[{namespaceName}localName]
```

## <a name="property-valuereturn-value"></a>プロパティ値/戻り値
 `IEnumerable<XElement> Item(String expandedName)` 型のインデクサー。 このインデクサーは、指定された子孫要素の拡張名を受け取り、<xref:System.Collections.IEnumerable>`<`<xref:System.Xml.Linq.XElement>`>` コレクション内の一致する子要素を返します。

## <a name="remarks"></a>Remarks
 このプロパティは、<xref:System.Xml.Linq.XContainer.Descendants%28System.Xml.Linq.XName%29?displayProperty=fullName> クラスの <xref:System.Xml.Linq.XContainer> メソッドに相当します。

 返されるコレクション内の要素は、XML ソース ドキュメント順になります。

 このプロパティは、遅延実行を使用します。

## <a name="see-also"></a>参照
 [XElement クラスの動的プロパティ](../designers/xelement-class-dynamic-properties.md)[要素](../designers/elements-xelement-dynamic-property.md)

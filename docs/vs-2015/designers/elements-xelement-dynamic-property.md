---
title: Elements (XElement 動的プロパティ) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
api_name:
- XElement.Elements
api_type:
- Assembly
ms.assetid: 3d5737f2-d2ed-410a-821c-349dbb2b574f
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 383101679827f19b9a85d36f0f5a39eb772c68ec
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72664693"
---
# <a name="elements-xelement-dynamic-property"></a>Elements (XElement 動的プロパティ)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

現在の要素の子要素のうち指定された拡張名に一致する子要素の取得に使用するインデクサーを取得します。

## <a name="syntax"></a>構文

```
elem.Elements[{namespaceName}localName]
```

## <a name="property-valuereturn-value"></a>プロパティ値/戻り値
 `IEnumerable<XElement> Item(String expandedName)` 型のインデクサー。 このインデクサーは、目的の子要素の拡張名を取得し、<xref:System.Collections.IEnumerable>`<`<xref:System.Xml.Linq.XElement>`>` コレクション内の一致する子要素を返します。

## <a name="remarks"></a>Remarks
 このプロパティは、<xref:System.Xml.Linq.XContainer.Elements%28System.Xml.Linq.XName%29?displayProperty=fullName> クラスの <xref:System.Xml.Linq.XContainer> メソッドに相当します。

 返されるコレクション内の要素は、XML ソース ドキュメント順になります。

 このプロパティは、遅延実行を使用します。

## <a name="see-also"></a>参照
 [XElement クラスの動的プロパティ](../designers/xelement-class-dynamic-properties.md)[要素](../designers/element-xelement-dynamic-property.md)の[子孫](../designers/descendants-xelement-dynamic-property.md)

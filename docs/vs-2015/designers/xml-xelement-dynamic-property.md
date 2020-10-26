---
title: XML (XElement 動的プロパティ) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
api_name:
- XElement.Xml
ms.assetid: 69ab2a33-4fe7-4cfa-97f8-eaf063decb18
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c794d79d62fc580001efc5cf16993d4ac5fef48b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72663847"
---
# <a name="xml-xelement-dynamic-property"></a>XML (XElement 動的プロパティ)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

要素について、書式設定されていない XML コンテンツを取得します。

## <a name="syntax"></a>構文

```
elem.Xml
```

## <a name="property-valuereturn-value"></a>プロパティ値/戻り値
 要素に関する書式設定されていない XML コンテンツを表す <xref:System.String>。

## <a name="remarks"></a>Remarks
 このプロパティは、<xref:System.Xml.Linq.XNode.ToString%28System.Xml.Linq.SaveOptions%29> パラメーターが <xref:System.Xml.Linq.XNode?displayProperty=fullName> に設定されている、`SaveOptions` クラスの <xref:System.Xml.Linq.SaveOptions> メソッドに相当します。

## <a name="see-also"></a>参照
 [XElement クラスの動的プロパティ](../designers/xelement-class-dynamic-properties.md)[値](../designers/value-xelement-dynamic-property.md)

---
title: LINQ to XML の動的プロパティ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 0455f47c-4a68-4f2e-a3f8-dd1d85b99012
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6ff0b31512711b8888b05fcfde191c8cb5c47d99
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72664259"
---
# <a name="linq-to-xml-dynamic-properties"></a>LINQ to XML の動的プロパティ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ここでは、LINQ to XML の動的プロパティに関する参照情報について説明します。 これらのプロパティは、具体的には <xref:System.Xml.Linq.XAttribute> 名前空間の <xref:System.Xml.Linq.XElement> クラスと <xref:System.Xml.Linq> クラスによって公開されます。

 トピック「 [LINQ to XML を使用した WPF データバインディングの概要](../designers/wpf-data-binding-with-linq-to-xml-overview.md)」で説明されているように、各動的プロパティは、同じクラスの標準のパブリックプロパティまたはメソッドに相当します。 ほとんどの用途では、これらの標準のメンバーを使用する必要があります。動的プロパティは、LINQ to XML のデータ バインドのシナリオ専用に用意されています。 これらのクラスの標準のメンバーに関する詳細については、リファレンス トピックの「<xref:System.Xml.Linq.XAttribute>」および「<xref:System.Xml.Linq.XElement>」を参照してください。

 このセクションの動的プロパティは、解決される値に関連して次の 2 つのカテゴリに分類されます。

- 1 つの値に解決される単純なプロパティ (`Value` クラスや <xref:System.Xml.Linq.XAttribute> クラスの <xref:System.Xml.Linq.XElement> プロパティなど)。

- インデクサー型に解決されるインデックス値 (<xref:System.Xml.Linq.XElement> の [Elements](../designers/elements-xelement-dynamic-property.md) プロパティや [Descendants](../designers/descendants-xelement-dynamic-property.md) プロパティなど)。 インデクサー型が目的の値やコレクションに解決されるようにするには、拡張名のパラメーターを渡す必要があります。

  <xref:System.Collections.Generic.IEnumerable%601> 型のインデックス値を返す動的プロパティはすべて遅延実行を使用します。 遅延実行の詳細については、「 [LINQ クエリの概要 (C#)](https://msdn.microsoft.com/library/37895c02-268c-41d5-be39-f7d936fa88a8)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容

|トピック|説明|
|-----------|-----------------|
|[XAttribute クラスの動的プロパティ](../designers/xattribute-class-dynamic-properties.md)|<xref:System.Xml.Linq.XAttribute> クラスによって公開される動的プロパティの詳細情報について説明します。|
|[XElement クラスの動的プロパティ](../designers/xelement-class-dynamic-properties.md)|<xref:System.Xml.Linq.XElement> クラスによって公開される動的プロパティの詳細情報について説明します。|

## <a name="reference"></a>リファレンス
 <xref:System.Xml.Linq>

 <xref:System.Xml.Linq.XElement?displayProperty=fullName>

 <xref:System.Xml.Linq.XAttribute?displayProperty=fullName>

## <a name="see-also"></a>参照
 Wpf で[のデータバインディング LINQ to XML](../designers/wpf-data-binding-with-linq-to-xml.md) [Wpf でのデータバインディング LINQ TO XML の概要](../designers/wpf-data-binding-with-linq-to-xml-overview.md) [LINQ クエリの概要 (C#)](https://msdn.microsoft.com/library/37895c02-268c-41d5-be39-f7d936fa88a8)

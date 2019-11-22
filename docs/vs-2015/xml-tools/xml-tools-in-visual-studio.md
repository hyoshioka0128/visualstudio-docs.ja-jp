---
title: XML ツール
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
f1_keywords:
- vb.xmldesigner
helpviewer_keywords:
- XML [Visual Studio], resources
- Enterprise Templates, XML and
- discovery files, XML
- server controls, XML and
- Web server controls, XML
- XSL
- XML [Visual Studio], data sources
- XML schemas
- XML [Visual Studio], SGML relationship to
- CSS, style sheets for XML
- XML [Visual Studio], .NET Framework classes
- data [Visual Studio], XML
- classes [Visual Studio], XML
- style sheets, for XML
- Web services
- SGML, XML
- XML [Visual Studio]
- datasets [Visual Basic], XML Schemas
- XSD schemas
- XSL, style sheets
- XMLDataDocument class
ms.assetid: 1fd5de47-2d61-4180-9539-c2c4bf9ab768
caps.latest.revision: 29
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3ee0cf61f8ec2787894c6f67b8ac75424246c507
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74297452"
---
# <a name="xml-tools-in-visual-studio"></a>Visual Studio の XML ツール
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Extensible Markup Language (XML)* is a markup language that provides a format for describing data. これにより、コンテンツの宣言がより正確になり、複数のプラットフォームをまたいだ検索結果がよりわかりやすくなります。 さらに、XML では、データと表示形式とを切り離すことができます。 たとえば、HTML では、ブラウザーでの太字や斜体によるデータの表示をタグで指定します。XML では、市の名前、気温、気圧などのデータを記述する目的でのみタグを使用します。 XML では、拡張スタイルシート言語 (XSL) やカスケード スタイル シート (CSS) などのスタイル シートを使用して、ブラウザーにデータを表示します。 XML では、データが表示形式と処理から切り離されます。 このため、適用するスタイル シートやアプリケーションを変えることによって、データの表示や処理を思いどおりに行うことができます。

 XML は SGML のサブセットで、Web を通じて送信するために最適化されています。 これは W3C (World Wide Web Consortium) が定義したものです。 この標準化によって、アプリケーションや販売元から独立している統一形式の構造化データを作成できます。

 XML は、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] および [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] の多くの機能の中核となっています。 次のトピック一覧に、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] および [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] で提供される XML 関連のツールと機能を示します。

 For more information, see the [XML Developer Center](https://go.microsoft.com/fwlink/?LinkID=100176), which provides the latest documentation, technical information, downloads, newsgroups, and other resources for XML developers.

## <a name="in-this-section"></a>このセクションの内容
 [Working with XML Data](../xml-tools/working-with-xml-data.md) Discusses the role of XML in the way data is handled in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].

 [Debugging XSLT](../xml-tools/debugging-xslt.md) Provides links to topics about using the Visual Studio debugger to debug XSLT.

## <a name="reference"></a>辞書／辞典／その他
 [Microsoft.VisualStudio.XmlEditor](https://go.microsoft.com/fwlink/?LinkID=165699) Exposes the [XML Editor](https://go.microsoft.com/fwlink/?LinkId=228249) parse tree through [System.Xml.Linq](https://go.microsoft.com/fwlink/?LinkId=228250) for any XML documents.

 [XML Standards Reference](https://msdn.microsoft.com/79c78508-c9d0-423a-a00f-672e855de401) Provides information about XML technologies, including XML, Document Type Definition (DTD), XML Schema definition language (XSD), and XSLT.

 <xref:System.Xml?displayProperty=fullName> Describes the classes and other elements that make up the <xref:System.Xml> namespace and provides links to more detailed information on each item.

 <xref:System.Xml.Serialization?displayProperty=fullName> Describes the classes and other elements that make up the <xref:System.Xml.Serialization> namespace and provides links to more detailed information about each item.

## <a name="related-sections"></a>関連項目
 [XML Document Object Model (DOM)](https://msdn.microsoft.com/library/b5e52844-4820-47c0-a61d-de2da33e9f54) Describes how the <xref:System.Xml.XmlDocument> and its associated classes comply with the W3C Document Object Model (Core) Level 1 and Level 2 namespace support specifications.

 [Reading XML with the XmlReader](https://msdn.microsoft.com/3029834c-a27e-4331-b7aa-711924062182) Describes how the <xref:System.Xml.XmlReader> provides noncached, forward only, read-only access to XML data over an XML stream.

 [Writing XML with the XmlWriter](https://msdn.microsoft.com/ea41f72c-e1d3-4e0a-ab0f-f0eb1c27ab86) Describes how the <xref:System.Xml.XmlWriter> provides noncached, forward only, way of generating XML streams and helps you build XML documents that comply with the W3C standard.

 [XSLT Transformations](https://msdn.microsoft.com/library/202f8820-224c-494f-b61e-cd127eac6e03) Describes how the <xref:System.Xml.Xsl.XslCompiledTransform> class implements the XSLT 1.0 recommendation.

 [Process XML Data Using the XPath Data Model](https://msdn.microsoft.com/library/536c6fce-1453-4654-9c72-bca54d47e081) Describes how the <xref:System.Xml.XPath.XPathNavigator> class can process XML data stored in an <xref:System.Xml.XPath.XPathDocument> or an <xref:System.Xml.XmlDocument> object. <xref:System.Xml.XPath.XPathNavigator> クラスは XQuery 1.0 および XPath 2.0 のデータ モデルに基づいており、XML データの操作と編集に使用できます。

 [XML Schema Object Model (SOM)](https://msdn.microsoft.com/library/a897a599-ffd1-43f9-8807-e58c8a7194cd) Describes the classes used for creating and manipulating XML Schemas, by providing an <xref:System.Xml.Schema.XmlSchema> class to load and edit a schema.

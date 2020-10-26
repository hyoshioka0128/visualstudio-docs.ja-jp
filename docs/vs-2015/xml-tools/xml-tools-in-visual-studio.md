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
ms.openlocfilehash: b9a46523c4c856367e77c345c7e44d0dbc87508f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75845982"
---
# <a name="xml-tools-in-visual-studio"></a>Visual Studio の XML ツール
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

拡張マークアップ言語 (XML) * は、データを記述するための形式を提供するマークアップ言語です。 これにより、コンテンツの宣言がより正確になり、複数のプラットフォームをまたいだ検索結果がよりわかりやすくなります。 さらに、XML では、データと表示形式とを切り離すことができます。 たとえば、HTML では、ブラウザーでの太字や斜体によるデータの表示をタグで指定します。XML では、市の名前、気温、気圧などのデータを記述する目的でのみタグを使用します。 XML では、拡張スタイルシート言語 (XSL) やカスケード スタイル シート (CSS) などのスタイル シートを使用して、ブラウザーにデータを表示します。 XML では、データが表示形式と処理から切り離されます。 このため、適用するスタイル シートやアプリケーションを変えることによって、データの表示や処理を思いどおりに行うことができます。

 XML は SGML のサブセットで、Web を通じて送信するために最適化されています。 これは W3C (World Wide Web Consortium) が定義したものです。 この標準化によって、アプリケーションや販売元から独立している統一形式の構造化データを作成できます。

 XML は、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] および [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] の多くの機能の中核となっています。 次のトピック一覧に、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] および [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] で提供される XML 関連のツールと機能を示します。

 詳細については、xml 開発者向けの最新のドキュメント、技術情報、ダウンロード、ニュースグループ、およびその他のリソースを提供する [Xml デベロッパーセンター](https://msdn.microsoft.com/data/bb190600.aspx)を参照してください。

## <a name="in-this-section"></a>このセクションの内容
 [XML データの操作](../xml-tools/working-with-xml-data.md) でのデータの処理方法における XML の役割について説明し [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。

 [XSLT のデバッグ](../xml-tools/debugging-xslt.md) Visual Studio デバッガーを使用して XSLT をデバッグする方法に関するトピックへのリンクを示します。

## <a name="reference"></a>リファレンス
 [Microsoft.VisualStudio.Xmlエディター](https://msdn.microsoft.com/library/microsoft.visualstudio.xmleditor.aspx)System.Xml を通じて [XML エディター](https://msdn.microsoft.com/library/ms255810.aspx) の解析ツリーを公開し [ ます。](https://msdn.microsoft.com/library/system.xml.linq.aspx) 任意の XML ドキュメントの Linq。

 [XML 標準のリファレンス](https://msdn.microsoft.com/79c78508-c9d0-423a-a00f-672e855de401) Xml、ドキュメント型定義 (DTD)、XML スキーマ定義言語 (XSD)、XSLT などの XML テクノロジについて説明します。

 <xref:System.Xml?displayProperty=fullName> 名前空間を構成するクラスとその他の要素について説明 <xref:System.Xml> し、各項目の詳細情報へのリンクを示します。

 <xref:System.Xml.Serialization?displayProperty=fullName> 名前空間を構成するクラスとその他の要素について説明 <xref:System.Xml.Serialization> し、各項目に関する詳細情報へのリンクを示します。

## <a name="related-sections"></a>関連項目
 [XML ドキュメントオブジェクトモデル (DOM)](https://msdn.microsoft.com/library/b5e52844-4820-47c0-a61d-de2da33e9f54)<xref:System.Xml.XmlDocument>とその関連クラスが、W3C ドキュメントオブジェクトモデル (コア) レベル1およびレベル2名前空間のサポート仕様にどのように準拠しているかについて説明します。

 [XmlReader を使用した XML の読み取り](https://msdn.microsoft.com/3029834c-a27e-4331-b7aa-711924062182) が <xref:System.Xml.XmlReader> xml ストリーム経由の xml データに対して、非キャッシュ、前方参照専用、読み取り専用のアクセスを提供する方法について説明します。

 [XmlWriter を使用した XML の書き込み](https://msdn.microsoft.com/ea41f72c-e1d3-4e0a-ab0f-f0eb1c27ab86) が、キャッシュ <xref:System.Xml.XmlWriter> されていない順方向専用の xml ストリームを生成する方法について説明します。 W3C 標準に準拠した xml ドキュメントの作成に役立ちます。

 [XSLT 変換](https://msdn.microsoft.com/library/202f8820-224c-494f-b61e-cd127eac6e03)<xref:System.Xml.Xsl.XslCompiledTransform>クラスが XSLT 1.0 勧告を実装する方法について説明します。

 [XPath データモデルを使用して XML データを処理する](https://msdn.microsoft.com/library/536c6fce-1453-4654-9c72-bca54d47e081)<xref:System.Xml.XPath.XPathNavigator>またはオブジェクトに格納されている XML データをクラスが処理する方法について説明し <xref:System.Xml.XPath.XPathDocument> <xref:System.Xml.XmlDocument> ます。 <xref:System.Xml.XPath.XPathNavigator> クラスは XQuery 1.0 および XPath 2.0 のデータ モデルに基づいており、XML データの操作と編集に使用できます。

 [XML スキーマオブジェクトモデル (SOM)](https://msdn.microsoft.com/library/a897a599-ffd1-43f9-8807-e58c8a7194cd) スキーマを読み込んで編集するクラスを提供することによって、XML スキーマの作成と操作に使用されるクラスについて説明し <xref:System.Xml.Schema.XmlSchema> ます。

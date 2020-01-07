---
title: XML エディターとスキーマデザイナー
ms.date: 11/04/2016
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
- XML [Visual Studio], .NET classes
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
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 87a5f069d5255a744e256bc9f7d1b48a135e85d8
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592309"
---
# <a name="xml-tools-in-visual-studio"></a>Visual Studio の XML ツール

*拡張マークアップ言語 (XML)* マークアップ言語であり、データを記述する形式を提供します。 XML は、拡張スタイルシート言語 (XSL) やカスケードスタイルシート (CSS) などの関連付けられたスタイルシートを使用して、データとそのプレゼンテーションを分離します。 Visual Studio には、XML、XSLT、および XML スキーマの操作を容易にするツールと機能が含まれています。

## <a name="xml-editor"></a>XML エディター

Xml[エディター](xml-editor.md)は、xml ドキュメントを編集するために使用されます。 完全な XML 構文チェック、入力中のスキーマ検証、カラーコーディング、IntelliSense が用意されています。 スキーマまたはドキュメント型定義が提供された場合は IntelliSense によって使用され、使用可能な要素と属性が一覧で示されます。

次のような機能も含まれています。

- XML スニペットのサポート (スキーマで生成されたスニペットを含む)

- 要素を展開および折りたたむことができるようにアウトラインを文書化する

- XSLT 変換を実行し、結果をテキスト、XML、または HTML として表示する機能

- Xml インスタンスドキュメントから XML スキーマ定義言語 (XSD) スキーマを生成する機能

- XSLT スタイルシートの編集 (IntelliSense サポートを含む) のサポート

- XML スキーマ エクスプローラー

## <a name="xml-schema-designer"></a>XML スキーマ デザイナー

Xml[スキーマデザイナー](xml-schema-designer.md)は、xml スキーマ定義言語 (XSD) スキーマを操作できるように、Visual STUDIO および xml エディターと統合されています。

## <a name="xslt-debugging"></a>XSLT のデバッグ

Visual Studio は[XSLT スタイルシートのデバッグ](../xml-tools/debugging-xslt.md)をサポートしています。 デバッガーを使用すると、XSLT スタイル シート内のブレークポイントの設定や、コードから XSLT スタイル シートへのステップ インなどが可能になります。

> [!NOTE]
> XSLT デバッガーは、Visual Studio の Enterprise edition でのみ使用できます。

## <a name="see-also"></a>関連項目

- <xref:System.Xml?displayProperty=fullName>
- [XSLT 変換](/dotnet/standard/data/xml/xslt-transformations)
- [XPath データモデルを使用して XML データを処理する](/dotnet/standard/data/xml/process-xml-data-using-the-xpath-data-model)
- [XML ドキュメント オブジェクト モデル (DOM)](/dotnet/standard/data/xml/xml-document-object-model-dom)
- [XML スキーマ オブジェクト モデル (SOM)](/dotnet/standard/data/xml/xml-schema-object-model-som)

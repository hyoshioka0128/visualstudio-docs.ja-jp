---
title: XML エディターとスキーマ デザイナー
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
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592309"
---
# <a name="xml-tools-in-visual-studio"></a>Visual Studio の XML ツール

*XML (拡張マークアップ言語)* は、データの記述形式を定めたマークアップ言語です。 XML は、拡張スタイルシート言語 (XSL) やカスケード スタイル シート (CSS) など、関連付けられたスタイル シートを使用して、データとそのプレゼンテーションを分離します。 Visual Studio には、XML、XSLT、および XML スキーマの操作を容易にするツールと機能が含まれています。

## <a name="xml-editor"></a>XML エディター

[XML エディター](xml-editor.md)は、XML ドキュメントの編集に使用します。 このエディターは、XML の完全構文チェック、入力中のスキーマ検証、コードの色分け表示、および IntelliSense を提供します。 スキーマまたはドキュメント型定義が提供された場合は IntelliSense によって使用され、使用可能な要素と属性が一覧で示されます。

次のような機能も含まれています。

- スキーマから生成されるスニペットを含めた、XML スニペットのサポート

- 要素の展開と折りたたみが可能なドキュメントのアウトライン表示

- XSLT 変換を実行し、結果をテキスト、XML、または HTML で表示する機能

- XML インスタンス ドキュメントから XML スキーマ定義言語 (XSD) スキーマを生成する機能

- IntelliSense サポートを含めた、XSLT スタイル シートの編集のサポート

- XML スキーマ エクスプローラー

## <a name="xml-schema-designer"></a>XML スキーマ デザイナー

[XML スキーマ デザイナー](xml-schema-designer.md)は Visual Studio および XML エディターに統合されており、これを使用すると、XML スキーマ定義言語 (XSD) スキーマの操作が可能になります。

## <a name="xslt-debugging"></a>XSLT のデバッグ

Visual Studio は [XSLT スタイル シート](../xml-tools/debugging-xslt.md)のデバッグをサポートしています。 デバッガーを使用すると、XSLT スタイル シート内のブレークポイントの設定や、コードから XSLT スタイル シートへのステップ インなどが可能になります。

> [!NOTE]
> XSLT デバッガーは、Visual Studio の Enterprise Edition でのみ使用できます。

## <a name="see-also"></a>関連項目

- <xref:System.Xml?displayProperty=fullName>
- [XSLT 変換](/dotnet/standard/data/xml/xslt-transformations)
- [XPath データ モデルを使用した XML データの処理](/dotnet/standard/data/xml/process-xml-data-using-the-xpath-data-model)
- [XML ドキュメント オブジェクト モデル (DOM)](/dotnet/standard/data/xml/xml-document-object-model-dom)
- [XML スキーマ オブジェクト モデル (SOM)](/dotnet/standard/data/xml/xml-schema-object-model-som)

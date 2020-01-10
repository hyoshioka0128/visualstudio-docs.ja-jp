---
title: Xml エディターでの XML ドキュメントの検証
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: abb353bd-6c4a-4978-b03b-a8c245bbfb55
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 389328e97f29d97962353e86f73c39c7c5459bfc
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592413"
---
# <a name="xml-document-validation"></a>XML ドキュメントの検証

Xml エディターでは、XML 1.0 構文がチェックされ、入力時にデータの検証も実行されます。 エディターは、ドキュメント型定義 (DTD) やスキーマを使用して検証を行うことができます。 XML 1.0 の整形式のエラーは、赤色の波下線で強調表示されます。 青色の波下線は、DTD またはスキーマの検証に基づいたセマンティック エラーを示します。 エラーの一覧には、それぞれのエラーに関連するエントリが示されます。 マウスを波下線の上に置くことで、エラー メッセージを表示させることもできます。

検証で使用されるスキーマの検索は、コンパイル済みのスキーマの `targetNamespace` と、要素の xmlns 宣言とを照合して行われます。 コンパイル済みのスキーマが読み込まれる場所を、優先度の高い順に次に示します。

- ドキュメントの**プロパティ**ウィンドウの **[スキーマ]** フィールドで指定したファイル名から。

- インラインのスキーマまたは DTD。

- 外部 DTD または `xsd:schemaLocation` および `xsd:noNamespaceSchemaLocation` 属性。

- "x-schema" XDR スキーマ名前空間 URI。

スキーマに空でない対象名前空間がある場合は、次に示す場所でスキーマが検索されることもあります。

- スキーマを含む他のエディター ウィンドウ。

- 現在のソリューション内にあるスキーマ。

- スキーマ キャッシュ ディレクトリ内にあるスキーマ。

## <a name="xslt-files"></a>XSLT ファイル
XSLT ファイルを編集するときに、スキーマキャッシュにある*xslt .xsd*ファイルが検証に使用されます。 検証エラーは、青色の波下線で表示されます。 XSLT コンパイラによるエラーは、赤色の波下線で示されます。

## <a name="xml-schema-xsd-files"></a>XML スキーマ (XSD) ファイル
XML スキーマファイルを編集するときに、スキーマキャッシュにある*xsdschema .xsd*ファイルが検証に使用されます。 検証エラーは、青色の波下線で表示されます。 コンパイル エラーも赤色の波下線で示されます。

## <a name="see-also"></a>関連項目

- [XML エディター](../xml-tools/xml-editor.md)

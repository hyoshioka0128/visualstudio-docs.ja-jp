---
title: 'チュートリアル: XSLT 階層の使用 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 5e60c8ec-cd05-4597-b856-55038218acf4
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 46e6acc8f65a9c9589348508f57cc75b04c61ccc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72669556"
---
# <a name="walkthrough-using-xslt-hierarchy"></a>チュートリアル: XSLT 階層の使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

XSLT 階層ツールは、多くの XML 開発タスクを簡素化します。 XSLT スタイル シートには、多くの場合 `includes` 命令および `imports` 命令が使用されています。 コンパイルはプリンシパル スタイル シートから開始されますが、XSLT スタイル シートのコンパイル結果としてエラーが表示された場合、プリンシパル スタイル シート以外のものがエラーの原因である可能性があります。 エラーを修正するか、スタイル シートを編集するには、インクルードまたはインポートされたスタイル シートへのアクセスが必要になる場合があります。 デバッガーでスタイル シートをステップ実行すると、インクルードまたはインポートされたスタイル シートが開かれる場合があり、1 つまたは複数のインクルードされたスタイル シートにブレークポイントを追加することができます。

 XSLT 階層ツールが役立つ別のシナリオとして、ビルトイン テンプレート規則にブレークポイントを挿入することがあります。 テンプレート規則は、スタイル シートの各モードに対して生成される特別なテンプレートであり、ノードに該当するテンプレートが他にない場合に、`xsl:apply-templates` により呼び出されます。 ビルトイン テンプレート規則でデバッグを実行するには、XSLT デバッガーで一時フォルダーに規則のファイルを作成し、プリンシパル スタイル シートと共にコンパイルします。 何らかの `xsl:apply-template` からコードへのステップ インを実行しないと、プリンシパル スタイル シートにインクルードされたスタイル シートを探したり、ビルトイン テンプレート規則を持つスタイル シートを探して開くことが困難になる場合があります。

 このトピックの例には、参照されるスタイル シート内のデバッグが示されています。

### <a name="procedure-title"></a>手順のタイトル

1. Visual Studio で XML ドキュメントを開きます。 この例では、次の `collection.xml` ドキュメントを使用しています。

    ```
    <?xml version="1.0" encoding="utf-8"?>
    <?xml-stylesheet type="text/xsl" href="xslinclude.xsl"?>
    <COLLECTION>
      <BOOK>
        <TITLE>Lover Birds</TITLE>
        <AUTHOR>Cynthia Randall</AUTHOR>
        <PUBLISHER>Lucerne Publishing</PUBLISHER>
      </BOOK>
      <BOOK>
        <TITLE>The Sundered Grail</TITLE>
        <AUTHOR>Eva Corets</AUTHOR>
        <PUBLISHER>Lucerne Publishing</PUBLISHER>
      </BOOK>
      <BOOK>
        <TITLE>Splish Splash</TITLE>
        <AUTHOR>Paula Thurman</AUTHOR>
        <PUBLISHER>Scootney</PUBLISHER>
      </BOOK>
    </COLLECTION>
    ```

2. 次の `xslincludefile.xsl` を追加します。

    ```
    <?xml version='1.0'?>
    <xsl:stylesheet version="1.0"
          xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
          xml:space="preserve">

    <xsl:template match="TITLE">
       Title - <xsl:value-of select="."/><BR/>
    </xsl:template>

    <xsl:template match="AUTHOR">
       Author - <xsl:value-of select="."/><BR/>
    </xsl:template>

    <xsl:template match="PUBLISHER">
       Publisher - <xsl:value-of select="."/><BR/><!-- removed second <BR/> -->
    </xsl:template>

    </xsl:stylesheet>
    ```

3. 次の `xslinclude.xsl` ファイルを追加します。

    ```
    <?xml version='1.0'?>
    <xsl:stylesheet version="1.0"
          xmlns:xsl="http://www.w3.org/1999/XSL/Transform">

      <xsl:output method="xml" omit-xml-declaration="yes"/>

      <xsl:template match="/">
        <xsl:for-each select="COLLECTION/BOOK">
          <xsl:apply-templates select="TITLE"/>
          <xsl:apply-templates select="AUTHOR"/>
          <xsl:apply-templates select="PUBLISHER"/>
          <BR/>
          <!-- add this -->
        </xsl:for-each>
      </xsl:template>

      <!-- The following template rule will not be called,
      because the related template in the including stylesheet
      is called. If we move this template so that
      it follows the xsl:include instruction, this one
      will be called instead.-->
      <xsl:template match="TITLE">
        <DIV STYLE="color:blue">
          Title: <xsl:value-of select="."/>
        </DIV>
      </xsl:template>

      <xsl:include href="xslincludefile.xsl" />
    </xsl:stylesheet>
    ```

4. `<xsl:include href="xslincludefile.xsl" />` 命令にブレークポイントを追加します。

5. デバッグを開始します。

6. デバッガーが `<xsl:include href="xslincludefile.xsl" />` 命令で停止したときに、ステップ イン ボタンを押します。 参照されるスタイル シート内でデバッグを継続することができます。 階層が表示され、デザイナーに正しいパスが示されます。

## <a name="see-also"></a>参照
 [チュートリアル: XSLT プロファイラー](../xml-tools/walkthrough-xslt-profiler.md)

---
title: 'チュートリアル: XSLT IntelliSense の使用'
description: このチュートリアルの手順に従って XSLT IntelliSense を使用し、一部の属性の値をオートコンプリートする方法について学習します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 079d95ac-2eaf-4ae1-9cd3-2c81a961a942
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ad3bb4024c4545dfaae7cdb9faa5d6484a66cd3e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99875030"
---
# <a name="walkthrough-using-xslt-intellisense"></a>チュートリアル: XSLT IntelliSense の使用

このチュートリアルでは、XSLT IntelliSense を使用して一部の属性値のオートコンプリートを行う方法について説明します。

## <a name="to-use-intellisense-in-the-name-attribute-of-xslwith-param-and-xslcall-template-elements"></a>xsl:with-param 要素と xsl:call-template 要素の name 属性に IntelliSense を使用するには

1. 新しい XSLT ファイルを作成して、次のコードをコピーします。

    ```xml
    <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
    <!-- These 2 elements effectively assign
         $messages = resources/en.xml/<messages>,
         then $messages is used in the "localized-message" template.  -->
    <xsl:param name="lang">en</xsl:param>
    <xsl:variable name="messages"
          select="document(concat('resources/', $lang, '.xml'))/messages"/>

    <xsl:template name="msg23" match="msg23">
    </xsl:template>

    <xsl:template name="localized-message">
      <xsl:param name="msgcode"/>
      <!-- Show message string. -->
      <xsl:message terminate="yes">
        <xsl:value-of select="$messages/message[@name=$msgcode]"/>
      </xsl:message>
    </xsl:template>
    </xsl:stylesheet>
    ```

2. `<xsl:template name="msg23" match="msg23">` の後ろにカーソルを置き、**Enter** キーを押します。 その後、次の `xsl:call-template` 要素を入力します。

    ```xml
    <xsl:call-template name="localized-message">
    </xsl:call-template>
    ```

     入力中、`name=""` 要素の `xsl:call-template` 属性にテンプレート名の一覧が表示されます。

3. `<xsl:call-template name="localized-message">` の後ろにカーソルを置き、**Enter** キーを押します。 その後、次の `xsl:with-param` 要素を入力します。

    ```xml
    <xsl:with-param name="msgcode">msg23</xsl:with-param>
    ```

     `name=""` 要素の `xsl:with-param` 属性にパラメーター名の一覧が表示されます。

## <a name="to-use-intellisense-in-the-mode-attribute-of-an-xslapply-templates-element"></a>xsl:apply-templates 要素の mode 属性に IntelliSense を使用するには

1. 新しい XSLT ファイルを作成して、次のコードをコピーします。

    ```xml
    <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
      <xsl:template match="/">
        <HTML>
          <BODY>
            <TABLE>
              <xsl:apply-templates select="customers/customer">
                <xsl:sort select="state"/>
                <xsl:sort select="name"/>
              </xsl:apply-templates>
            </TABLE>
          </BODY>
        </HTML>
      </xsl:template>
      <xsl:template match="customer">
        <TR>
          <xsl:apply-templates select="name" />
          <xsl:apply-templates select="address" />
          <xsl:apply-templates select="phone" />
        </TR>
      </xsl:template>
      <xsl:template match="name">
        <TD STYLE="font-size:14pt font-family:serif">
          <xsl:apply-templates />
        </TD>
      </xsl:template>
      <xsl:template match="address">
        <TD>
          <xsl:apply-templates />
        </TD>
      </xsl:template>
      <xsl:template match="phone">
        <TD>
          <xsl:apply-templates />
        </TD>
      </xsl:template>
      <xsl:template match="phone" mode="accountNumber">
        <xsl:param name="Area_Code"/>
        <TD STYLE="font-style:italic">
          1-<xsl:value-of select="."/>-001
        </TD>
      </xsl:template>
    </xsl:stylesheet>
    ```

2. `<xsl:apply-templates select="phone" />` の後ろにカーソルを置き、**Enter** キーを押します。 その後、次の `xsl: apply-templates` 要素を入力します。

    ```xml
    <xsl:apply-templates select="phone"  mode="accountNumber">
    ```

     `mode=""` 要素の `xsl:apply-templates` 属性にテンプレート モードの一覧が表示されます。

## <a name="to-use-intellisense-in-the-stylesheet-prefix-and-result-prefix-attributes-of-an-xslnamespace-alias-element"></a>xsl:namespace-alias 要素の stylesheet-prefix 属性および result-prefix 属性に IntelliSense を使用するには

1. 新しい XSLT ファイルを作成して、次のコードをコピーします。

    ```xml
    <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:alt="http://www.w3.org/1999/XSL/Transform-alternate"
    version="1.0">
      <xsl:param name="browser" select="'InternetExplorer'"/>
      <xsl:template match="/">
        <alt:stylesheet>
          <xsl:choose>
            <xsl:when test="$browser='InternetExplorer'">
              <alt:import href="IERoutines.xsl"/>
              <alt:template match="/">
                <div>
                  <alt:call-template name="showTable"/>
                </div>
              </alt:template>
            </xsl:when>
            <xsl:otherwise>
              <alt:import href="OtherBrowserRoutines.xsl"/>
              <alt:template match="/">
                <div>
                  <alt:call-template name="showTable"/>
                </div>
              </alt:template>
            </xsl:otherwise>
          </xsl:choose>
        </alt:stylesheet>
      </xsl:template>
    </xsl:stylesheet>
    ```

2. `<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:alt="http://www.w3.org/1999/XSL/Transform-alternate" version="1.0">` の後ろにカーソルを置き、**Enter** キーを押します。 その後、次の `xsl:namespace-alias` 要素を入力します。

    ```xml
    <xsl:namespace-alias stylesheet-prefix="alt" result-prefix="xsl"/>
    ```

     `stylesheet-prefix` 要素の `result-prefix` 属性と `xsl:namespace-alias` 属性にどのようにプレフィックスの一覧が表示されるかを確認してください。

## <a name="see-also"></a>関連項目

- [XML エディターの IntelliSense 機能](../xml-tools/xml-editor-intellisense-features.md)

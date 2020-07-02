---
title: 'CA3077: API デザイン、XML ドキュメント、および XML テキストリーダー | で安全ではない処理Microsoft Docs'
ms.date: 11/15/2016
ms.technology: vs-ide-code-analysis
ms.topic: reference
ms.assetid: 7f33771b-f3c8-4c02-bef6-f581b623c303
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: c0d6a6f6ab42d69d4503741f6625627c46d4ef77
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545107"
---
# <a name="ca3077-insecure-processing-in-api-design-xml-document-and-xml-text-reader"></a>CA3077:API のデザイン、XML ドキュメント、および XML テキスト リーダーでの安全ではない処理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|アイテム|値|
|-|-|
|TypeName|InsecureDTDProcessingInAPIDesign|
|CheckId|CA3077|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 XMLDocument と XMLTextReader から派生する API をデザインする場合、 <xref:System.Xml.XmlReaderSettings.DtdProcessing%2A>にご注意ください。  外部エンティティ ソースを参照または解決したり、XML に安全ではない値を設定したりする場合に、安全ではない DTDProcessing インスタンスを使用すると、情報漏えいにつながる可能性があります。

## <a name="rule-description"></a>ルールの説明
 [文書型定義 (DTD)](https://msdn.microsoft.com/library/aa468547.aspx) は、  [World Wide Web コンソーシアム (W3C) Extensible Markup Language (XML) 1.0](https://www.w3.org/TR/2008/REC-xml-20081126/)で定義されているように、XML パーサーが文書の妥当性を判別する 2 つの方法のうちの 1 つです。 このルールは、信頼されていないデータを受け入れてしまうプロパティとインスタンスを検索し、 [サービス拒否 (DoS)](https://msdn.microsoft.com/library/4064c89f-afa6-444a-aa7e-807ef072131c) 攻撃につながる可能性がある潜在的な [Information Disclosure](https://msdn.microsoft.com/library/dfb150f3-d598-4697-a5e6-6779e4f9b600) の脅威について開発者に警告します。 このルールは、次の場合にトリガーされます。

- <xref:System.Xml.XmlDocument>またはクラスは、 <xref:System.Xml.XmlTextReader> DTD 処理に既定の競合回避モジュールの値を使用します。

- XmlDocument または XmlTextReader から派生したクラスにコンストラクターが定義されていない。または <xref:System.Xml.XmlResolver>にセキュリティで保護された値が使用されていない。

## <a name="how-to-fix-violations"></a>違反の修正方法

- パス情報の漏えいを防ぐために、すべての XmlTextReader 例外をキャッチして処理します。

-  <xref:System.Xml.XmlSecureResolver>XmlResolver の代わりにを使用して、XmlTextReader がアクセスできるリソースを制限します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 入力が信頼できるソースからのものとわかっているのでない限り、この警告からのルールを抑制しないでください。

## <a name="pseudo-code-examples"></a>疑似コードの例

### <a name="violation"></a>違反

```csharp
using System;
using System.Xml;

namespace TestNamespace
{
    class TestClass : XmlDocument
    {
        public TestClass () {} // warn
    }

    class TestClass2 : XmlTextReader
    {
        public TestClass2() // warn
        {
        }
    }
}
```

### <a name="solution"></a>解決策

```csharp
using System;
using System.Xml;

namespace TestNamespace
{
    class TestClass : XmlDocument
    {
        public TestClass ()
        {
            XmlResolver = null;
        }
    }

    class TestClass2 : XmlTextReader
    {
        public TestClass2()
        {
               XmlResolver = null;
        }
    }
}
```

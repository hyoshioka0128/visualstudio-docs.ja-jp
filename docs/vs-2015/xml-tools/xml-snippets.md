---
title: XML スニペット |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 348dbf64-3f09-4fff-b47a-a7ecdf3221cc
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5bc8946d62f47291a6e0e3f26032589bfdf0de16
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72669360"
---
# <a name="xml-snippets"></a>XML スニペット
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Xml エディターには、xml *スニペット*と呼ばれる機能が用意されています。この機能を使用すると、xml ファイルをより迅速に作成できます。 XML スニペットは、ファイルに挿入することで再利用できます。 XML スキーマ定義言語 (XSD) スキーマに基づいて XML データを生成することもできます。

## <a name="reusable-xml-snippets"></a>再利用可能な XML スニペット
 XML エディターには、一般的なタスクを対象としたスニペットが多数含まれています。 これによって、XML ファイルをより簡単に作成できます。 たとえば、XML スキーマを作成している場合、"Complex Type Sequence Element" スニペットと "Simple Type Element" スニペットを使用すると、作成中のファイルに次の XML テキストが挿入されます。 その後で、必要に応じて `name` の値を変更します。

```
<xs:element name="name">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="name">
        <xs:simpleType>
          <xs:restriction base="xs:string"></xs:restriction>
        </xs:simpleType>
      </xs:element>
    </xs:sequence>
  </xs:complexType>
</xs:element>
```

 スニペットは 2 つの方法で挿入できます。 **[スニペットの挿入]** コマンドを使用すると、カーソル位置に XML スニペットが挿入されます。 **[ブロックの挿入]** コマンドを使用すると、選択したテキストがXML スニペットで囲まれます。 どちらのコマンドも、[**編集**] メニューの [ **IntelliSense** ] サブメニュー、またはエディターのショートカットメニューから使用できます。

 詳細については、「 [方法: XML スニペットを使用する](../xml-tools/how-to-use-xml-snippets.md)」を参照してください。

## <a name="schema-generated-xml-snippets"></a>スキーマを生成する XML スニペット
 XML エディターは、XML スキーマから XML スニペットを生成する機能も備えています。 この機能を使用すると、要素に、その要素のスキーマ情報から生成された XML 要素を格納することができます。

 詳細については、「 [方法: Xml スキーマから Xml スニペットを生成](../xml-tools/how-to-generate-an-xml-snippet-from-an-xml-schema.md)する」を参照してください。

## <a name="create-new-xml-snippets"></a>新しい XML スニペットを作成する
 既定では、Visual Studio に含まれているスニペットに加えて、 [!INCLUDE[msCoName](../includes/msconame-md.md)] 独自の XML スニペットを作成して使用することもできます。

 詳細については、「 [方法: XML スニペットを作成](../xml-tools/how-to-create-xml-snippets.md)する」を参照してください。

## <a name="see-also"></a>参照
 [XML エディター](../xml-tools/xml-editor.md)

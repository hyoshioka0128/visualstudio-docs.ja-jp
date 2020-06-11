---
title: XML スニペット
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 348dbf64-3f09-4fff-b47a-a7ecdf3221cc
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a2f2bcdd0c28d7b4b99c92d3346b32ed34aa92a0
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592322"
---
# <a name="xml-snippets"></a>XML スニペット

XML エディターには、*XML スニペット*と呼ばれる機能が用意されており、これを使用すると XML ファイルをより速く構築することができます。 XML スニペットは、ファイルに挿入することで再利用できます。 XML スキーマ定義言語 (XSD) スキーマに基づいて XML データを生成することもできます。

## <a name="reusable-xml-snippets"></a>再利用可能な XML スニペット

XML エディターには、一般的なタスクを対象としたスニペットが多数含まれています。 これによって、XML ファイルをより簡単に作成できます。 たとえば、XML スキーマを作成している場合、"Complex Type Sequence Element" スニペットと "Simple Type Element" スニペットを使用すると、作成中のファイルに次の XML テキストが挿入されます。 その後で、必要に応じて `name` の値を変更します。

```xml
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

スニペットは 2 つの方法で挿入できます。 **[スニペットの挿入]** コマンドを使用すると、カーソル位置に XML スニペットが挿入されます。 **[ブロックの挿入]** コマンドを使用すると、選択したテキストがXML スニペットで囲まれます。 どちらのコマンドも、 **[編集]** メニューの **[IntelliSense]** サブメニュー、またはエディター内の右クリック メニューから使用できます。

詳細については、[方法: XML スニペットを使用する](../xml-tools/how-to-use-xml-snippets.md)」を参照してください。

## <a name="schema-generated-xml-snippets"></a>スキーマを生成する XML スニペット

XML エディターは、XML スキーマから XML スニペットを生成する機能も備えています。 この機能を使用すると、要素に、その要素のスキーマ情報から生成された XML 要素を格納することができます。 詳細については、[方法: XML スキーマから XML スニペットを生成する](../xml-tools/how-to-generate-an-xml-snippet-from-an-xml-schema.md)」を参照してください。

## <a name="create-new-xml-snippets"></a>新しい XML スニペットを作成する

既定で Visual Studio に付属しているスニペットに加えて、独自の XML スニペットを作成して使用することもできます。 詳細については、[方法: XML スニペットを作成する](../xml-tools/how-to-create-xml-snippets.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio のコード スニペット](../ide/code-snippets.md)
- [XML エディター](../xml-tools/xml-editor.md)

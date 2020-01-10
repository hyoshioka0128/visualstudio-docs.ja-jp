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
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592322"
---
# <a name="xml-snippets"></a>XML スニペット

Xml エディターには、xml*スニペット*と呼ばれる機能が用意されています。この機能を使用すると、xml ファイルをより迅速に作成できます。 XML スニペットは、ファイルに挿入することで再利用できます。 Xml スキーマ定義言語 (XSD) スキーマに基づいて XML データを生成することもできます。

## <a name="reusable-xml-snippets"></a>再利用可能な XML スニペット

XML エディターには、いくつかの一般的なタスクに対応する多くのスニペットが含まれています。 これによって、XML ファイルをより簡単に作成できます。 たとえば、XML スキーマを作成する場合は、"複合型のシーケンス要素" と "単純型の要素" を使用して、次の XML テキストをファイルに挿入します。 その後で、必要に応じて `name` の値を変更します。

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

スニペットは 2 つの方法で挿入できます。 **[スニペットの挿入]** コマンドを実行すると、XML スニペットがカーソル位置に挿入されます。 [**ブロック**の挿入] コマンドは、選択したテキストの周囲に XML スニペットをラップします。 どちらのコマンドも、 **[編集]** メニューの **[IntelliSense]** サブメニュー、またはエディター内の右クリックメニューから使用できます。

詳細については、「[方法: XML スニペットを使用する](../xml-tools/how-to-use-xml-snippets.md)」を参照してください。

## <a name="schema-generated-xml-snippets"></a>スキーマによって生成される XML スニペット

Xml エディターでは、xml スキーマから XML スニペットを生成することもできます。 この機能を使用すると、要素に、その要素のスキーマ情報から生成された XML 要素を格納することができます。 詳細については、「[方法: xml スキーマから xml スニペットを生成](../xml-tools/how-to-generate-an-xml-snippet-from-an-xml-schema.md)する」を参照してください。

## <a name="create-new-xml-snippets"></a>新しい XML スニペットを作成する

既定では、Visual Studio に含まれているスニペットに加えて、独自の XML スニペットを作成して使用することもできます。 詳細については、「[方法: XML スニペットを作成](../xml-tools/how-to-create-xml-snippets.md)する」を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio でのコードスニペット](../ide/code-snippets.md)
- [XML エディター](../xml-tools/xml-editor.md)

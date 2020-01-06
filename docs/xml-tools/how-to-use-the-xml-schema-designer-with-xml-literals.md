---
title: '方法: XML リテラルに XML スキーマ デザイナーを使用する'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: d11803e7-f81a-41a2-a145-ba494a45cc93
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- VB
ms.workload:
- multiple
ms.openlocfilehash: b4001e705cc69e07242abeeef5919573b264c5e8
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592660"
---
# <a name="how-to-use-the-xml-schema-designer-with-xml-literals"></a>方法: xml リテラルで XML スキーマデザイナーを使用する

このトピックでは、Visual Basic プロジェクトの XML リテラルに関連付けられたスキーマを表示する方法について説明します。

## <a name="create-a-new-visual-basic-project"></a>新しい Visual Basic プロジェクトを作成する

1. Visual Studio を開きます。

2. **XMLLiterals**という名前の新しい Visual Basic**コンソールアプリ**プロジェクトを作成します。

     新しいプロジェクトには、module1.vb という Visual Basic ソースファイルが1つ含まれ*ています*。

## <a name="add-an-existing-xsd-file"></a>既存の XSD ファイルを追加する

1. メモ帳で新しいテキスト ファイルを開きます。 [注文書スキーマ](../xml-tools/sample-xsd-file-simple-schema.md)から XML スキーマのサンプルコードをコピーし、ファイルに貼り付けます。

2. *PurchaseOrderSchema*という名前の場所にファイルを保存します。

3. **ソリューションエクスプローラー**で、プロジェクトの名前を右クリックし、 **[追加]** をクリックして、 **[既存の項目]** を選択します。 **[追加 Item]** ダイアログボックスが表示されます。 *PurchaseOrderSchema*ファイルを参照して選択し、 **[追加]** をクリックします。

     XMLLiterals プロジェクトに*は、module1.vb と* *PurchaseOrderSchema*の2つのファイルが含まれるようになりました。

## <a name="add-code"></a>コードの追加

XML リテラルを使用して Visual Basic コードを追加するには、プロジェクトに含まれている XSD ファイルに基づきます。

1. Module1.vb ファイル内のコードを次の*コードに置き換え*ます。

   ```vb
   Imports <xmlns:ns="http://tempuri.org/PurchaseOrderSchema.xsd">

   Module Module1
      Sub Main()

          Dim XMLLiteral = <ns:PurchaseOrder OrderDate="1900-01-01">
                               <ns:ShipTo country="US">
                                   <ns:name>name1</ns:name>
                                   <ns:street>street1</ns:street>
                                   <ns:city>city1</ns:city>
                                   <ns:state>state1</ns:state>
                                   <ns:zip>1</ns:zip>
                               </ns:ShipTo>
                               <ns:BillTo country="US">
                                   <ns:name>name1</ns:name>
                                   <ns:street>street1</ns:street>
                                   <ns:city>city1</ns:city>
                                   <ns:state>state1</ns:state>
                                   <ns:zip>1</ns:zip>
                               </ns:BillTo>
                           </ns:PurchaseOrder>

      End Sub
   End Module
   ```

2. Xml リテラルまたは XML 名前空間インポートで任意の XML ノードを右クリックし、 **[スキーマエクスプローラーで表示]** を選択します。

   Xml**スキーマエクスプローラー**は、xml スキーマセットに関連付けられている xml リテラルを含む Visual Basic ファイルと共に表示されます。

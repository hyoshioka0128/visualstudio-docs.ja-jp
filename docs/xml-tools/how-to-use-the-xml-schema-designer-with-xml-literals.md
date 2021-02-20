---
title: '方法: XML リテラルに XML スキーマ デザイナーを使用する'
description: XML スキーマ デザイナーを使用して、Visual Basic プロジェクトの XML リテラルに関連付けられたスキーマを表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: d11803e7-f81a-41a2-a145-ba494a45cc93
author: TerryGLee
ms.author: tglee
manager: jmartens
dev_langs:
- VB
ms.workload:
- multiple
ms.openlocfilehash: f233eaed4b08e499b3a7543d10caafd36c77a480
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99969075"
---
# <a name="how-to-use-the-xml-schema-designer-with-xml-literals"></a>方法: XML リテラルに XML スキーマ デザイナーを使用する

このトピックでは、Visual Basic プロジェクトの XML リテラルに関連付けられたスキーマを表示する方法について説明します。

## <a name="create-a-new-visual-basic-project"></a>新しい Visual Basic プロジェクトの作成

1. Visual Studio を開きます。

2. **XMLLiterals** という名前の新しい Visual Basic **Console App** プロジェクトを作成します。

     新しいプロジェクトには、*Module1.vb* という 1 つの Visual Basic ソース ファイルが含まれています。

## <a name="add-an-existing-xsd-file"></a>既存の XSD ファイルを追加する

1. メモ帳で新しいテキスト ファイルを開きます。 [購買発注書のスキーマ](../xml-tools/sample-xsd-file-simple-schema.md)から XML スキーマのサンプル コードをコピーして、ファイルに貼り付けます。

2. *PurchaseOrderSchema.xsd* という名前でファイルをどこかに保存します。

3. **ソリューション エクスプローラー** で、プロジェクト名を右クリックし、 **[追加]** を選択して **[既存の項目]** をクリックします。 **[既存項目の追加]** ダイアログ ボックスが表示されます。 *PurchaseOrderSchema.xsd* ファイルを参照して選択し、 **[追加]** をクリックします。

     XMLLiterals プロジェクトに、次の 2 つのファイルが含まれるようになります:*Module1.vb* および *PurchaseOrderSchema.xsd*。

## <a name="add-code"></a>コードの追加

プロジェクトに含まれる XSD ファイルに基づいて XML リテラルの Visual Basic コードを追加するには:

1. *Module1.vb* ファイルのコードを次のコードに置き換えます。

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

2. XML リテラルまたは XML 名前空間インポートの XML ノードを右クリックして、 **[スキーマ エクスプローラーで表示]** をクリックします。

   **XML スキーマ エクスプローラー** が、XML スキーマ セットに関連付けられた XML リテラルを持つ Visual Basic ファイルと並んで表示されます。

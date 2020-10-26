---
title: '方法: xml リテラルを使用して XML スキーマデザイナーを使用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: d11803e7-f81a-41a2-a145-ba494a45cc93
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a9e82cf8387756cb4a4abe8b4c41d082485cdcdc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656290"
---
# <a name="how-to-use-the-xml-schema-designer-with-xml-literals"></a>方法: XML リテラルに XML スキーマ デザイナーを使用する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、Visual Basic プロジェクトの XML リテラルに関連付けられたスキーマを表示する方法について説明します。

### <a name="to-create-a-new-visual-basic-console-application-project"></a>新しい Visual Basic コンソール アプリケーションのプロジェクトを作成するには

1. Visual Studio 2010 を起動します。

2. **[ファイル]** メニューの **[新規作成]** を選択し、**[プロジェクト]** を選択します。 **[新しいプロジェクト]** ダイアログ ボックスが表示されます。 [ **プロジェクトの種類**] で [ **その他の言語** ] を選択し、[ **Visual Basic**] を選択します。 **テンプレート**については、[コンソールアプリケーション] を選択します。 次に、[ `XMLLiterals` **名前** ] フィールドに「」と入力し、[ **場所** ] フィールドにプロジェクトの場所を入力します。 **[OK]** をクリックします。

     新しいプロジェクトが作成されます。 XMLLiterals プロジェクトには、Module1.vb という 1 つの Visual Basic ソース ファイルが含まれています。

### <a name="to-add-an-existing-xsd-file-to-the-project"></a>既存の XSD ファイルをプロジェクトに追加するには

1. 新しいテキストファイルをメモ帳で開きます。 [注文書スキーマ](../xml-tools/sample-xsd-file-simple-schema.md) から XML スキーマのサンプルコードをコピーし、ファイルに貼り付けます。

2. PurchaseOrderSchema.xsd という名前でファイルをどこかに保存します。

3. ソリューションエクスプローラーで、プロジェクトの名前を右クリックし、[ **追加**]、[既存の **項目**] の順に選択します。 **[既存項目の追加]** ダイアログ ボックスが表示されます。 PurchaseOrderSchema.xsd ファイルを参照して選択し、 **[追加]** をクリックします。

     XMLLiterals プロジェクトに、Module1.vb および PurchaseOrderSchema.xsd という 2 つのファイルが含まれるようになります。

### <a name="to-add-visual-basic-code-with-an-xml-literal-based-on-the-xsd-file-included-in-the-project"></a>プロジェクトに含まれる XSD ファイルに基づいて XML リテラルの Visual Basic コードを追加するには

1. Module1.vb ファイルのコードを次のコードに置き換えます。

    ```
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

     XML スキーマ エクスプローラーが、XML スキーマ セットに関連付けられた XML リテラルを持つ Visual Basic ファイルと並んで表示されます。

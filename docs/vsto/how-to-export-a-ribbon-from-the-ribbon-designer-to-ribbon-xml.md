---
title: '方法: リボンをリボンデザイナーからリボン XML にエクスポートする'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom Ribbon, XML
- customizing the Ribbon, XML
- Ribbon [Office development in Visual Studio], XML
- Ribbon [Office development in Visual Studio], exporting
- XML [Office development in Visual Studio], Ribbon
- Ribbon Designer [Office development in Visual Studio]
- exporting Ribbon
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 57918e8a51a3948a2c69eb0c8ab5438b147e44f0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543469"
---
# <a name="how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml"></a>方法: リボンをリボンデザイナーからリボン XML にエクスポートする
  **リボン (ビジュアルデザイナー)** 項目は、すべての種類のリボンのカスタマイズをサポートしているわけではありません。 高度な方法でリボンをカスタマイズするには、リボンをデザイナーからリボン XML にエクスポートし、XML を直接編集します。

> [!NOTE]
> すべてのプロパティ値がリボン XML ファイルに表示されるわけではありません。 詳細については、「[リボンの概要](../vsto/ribbon-overview.md)」を参照してください。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml"></a>リボンをリボンデザイナーからリボン XML にエクスポートするには

1. **ソリューションエクスプローラー**でリボンコードファイルを右クリックし、[デザイナーの**表示**] をクリックします。

2. リボンデザイナーを右クリックし、[**リボンを XML にエクスポート**] をクリックします。

     Visual Studio によって、リボン XML ファイルとリボン XML コードファイルがプロジェクトに追加されます。

3. リボンの code クラスで、で始まるコメントを見つけ `TODO:` ます。

4. 開発しているソリューションの種類に応じて、これらのコメントのコードブロックを**ThisAddin**、 **ThisWorkbook**、 **ThisDocument**のいずれかのクラスにコピーします。

     このコードにより、Microsoft Office アプリケーションでカスタムリボンを検出して読み込むことができます。 詳細については、「 [Ribbon XML](../vsto/ribbon-xml.md)」を参照してください。

5. **ThisAddin**、 **ThisWorkbook**、 **ThisDocument**クラスで、コードブロックのコメントを解除します。

     コードのコメントを解除すると、次の例のようになります。 この例では、リボンクラスが呼び出され `MyRibbon` ます。

     [!code-csharp[Trin_Ribbon_Custom_Tab_XML#1](../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.cs#1)]
     [!code-vb[Trin_Ribbon_Custom_Tab_XML#1](../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.vb#1)]

6. リボン XML コードファイルに切り替えて、領域を検索し `Ribbon Callbacks` ます。

     ここでは、ボタンのクリックなど、ユーザーの操作を処理するコールバックメソッドを記述します。

7. リボンデザイナーコードで記述した各イベントハンドラーのコールバックメソッドを作成します。

8. イベントハンドラーのすべてのコードをイベントハンドラーからコールバックメソッドに移動し、リボン機能拡張 (RibbonX) プログラミングモデルで動作するようにコードを変更します。

     コールバックメソッドの記述と、RibbonX プログラミングモデルの使用の詳細については、「[リボン XML](../vsto/ribbon-xml.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [リボンの概要](../vsto/ribbon-overview.md)
- [リボンデザイナー](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [チュートリアル: リボンデザイナーを使用したカスタムタブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [チュートリアル: リボン XML を使用したカスタムタブの作成](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)

---
title: '方法: Visual Studio 内のワークシートにスキーマをマップする'
description: Visual Studio でワークシートを開いているときに、XML スキーマを Microsoft Office Excel ワークシートにマップする方法について説明します。
titleSuffix: ''
ms.custom: seodec18, SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XML schemas [Office development in Visual Studio], mapping
- mappings [Office development in Visual Studio], XML schemas to Excel worksheets
- Excel [Office development in Visual Studio], XML schemas
- worksheets [Office development in Visual Studio], XML schemas
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7a7e1a06e644536ce9ce881d9b9f1dc23aae03f1
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96848210"
---
# <a name="how-to-map-schemas-to-worksheets-inside-visual-studio"></a>方法: Visual Studio 内のワークシートにスキーマをマップする
  ワークシートが Visual Studio で開かれているときに、XML スキーマをワークシートにマップできます。 Visual Studio の外部でブックを開いたときに使用するのと同じ Microsoft Office Excel ツールを使用します。 Office プロジェクトでは、Excel ソリューションを作成する前または後に、ワークシートにスキーマをマップするかどうかにかかわらず、同じオブジェクトが作成されます。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

> [!NOTE]
> Excel ソリューションでは、マルチパート XML スキーマを使用できません。

## <a name="to-map-an-xml-schema-to-an-excel-worksheet-in-visual-studio"></a>Visual Studio で XML スキーマを Excel ワークシートにマップするには

1. Visual Studio 内で Excel ブックまたはテンプレートプロジェクトを開きます。

2. ワークシート内をクリックして、デザイナーにフォーカスを移動します。

3. リボンの **[開発]** タブをクリックします。

    > [!NOTE]
    > **[開発]** タブが表示されていない場合は、最初にこれを表示する必要があります。 詳細については、「 [方法: リボンに [開発者] タブを表示する](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)」を参照してください。

4. [ **XML** ] グループの [ **ソース**] をクリックします。

     [ **XML ソース** ] ウィンドウが開きます。

5. [ **Xml ソース** ] ウィンドウで、[ **xml マップ**] をクリックします。

     [ **XML マップ** ] ダイアログボックスが表示されます。

6. [ **XML マップ** ] ダイアログボックスで、[ **追加**] をクリックします。

7. スキーマファイルを参照して選択し、[ **開く**] をクリックします。

8. **[OK]** をクリックします。

     スキーマは、[ **XML ソース** ] ウィンドウに表示されます。 プロジェクトでは、スキーマに基づいて型指定されたが生成され、 <xref:System.Data.DataSet> <xref:System.Windows.Forms.BindingSource> が作成されます。

9. **XML ソース** ウィンドウから、対応するコントロールを作成するワークシート内の場所に要素をドラッグします。

     非繰り返しスキーマ要素をドラッグすると、に <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 自動的にバインドされるコントロールが Office プロジェクトによって生成され <xref:System.Windows.Forms.BindingSource> ます。

     繰り返しスキーマ要素をドラッグすると、Office プロジェクトによって、 <xref:Microsoft.Office.Tools.Excel.ListObject> 自動的にデータソースにバインドされていないコントロールが生成されます。 詳細については、「 [ドキュメントレベルのカスタマイズの XML スキーマとデータ](../vsto/xml-schemas-and-data-in-document-level-customizations.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: Visual Studio 内で Word 文書にスキーマを割り当てる](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [ドキュメントレベルのカスタマイズにおける XML スキーマとデータ](../vsto/xml-schemas-and-data-in-document-level-customizations.md)

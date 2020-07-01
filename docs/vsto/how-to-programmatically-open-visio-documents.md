---
title: '方法: プログラムによって Visio 図面を開く'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], opening Visio documents
- Visio [Office development in Visual Studio], opening Visio documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: eb21d201c282461cbe82005f56bed023bb022209
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85519991"
---
# <a name="how-to-programmatically-open-visio-documents"></a>方法: プログラムによって Visio 図面を開く
  既存の Microsoft Office Visio 図面を開くには、Open と OpenEx の2つの方法があります。 OpenEx メソッドは Open メソッドと同じですが、呼び出し元がドキュメントを開く方法を指定できる引数を提供する点が異なります。

 オブジェクト モデルの詳細については、 [Microsoft.Office.Interop.Visio.Documents.Open](/office/vba/api/Visio.Documents.Open) メソッドと [Microsoft.Office.Interop.Visio.Documents.OpenEx](/office/vba/api/Visio.Documents.OpenEx) メソッドの VBA リファレンス ドキュメントを参照してください。

## <a name="open-a-visio-document"></a>Visio 図面を開く

### <a name="to-open-a-visio-document"></a>Visio 図面を開くには

- `Microsoft.Office.Interop.Visio.Documents.Open` メソッドを呼び出し、Visio 図面の完全修飾パスを指定します。

     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#5](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#5)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#5](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#5)]

## <a name="open-a-visio-document-with-specified-arguments"></a>指定された引数を使用して Visio 図面を開く

### <a name="to-open-a-visio-document-as-read-only-and-docked"></a>読み取り専用およびドッキングとして Visio 図面を開くには

- `Microsoft.Office.Interop.Visio.Documents.OpenEx` メソッドを呼び出して、Visio 図面の完全修飾パスを指定し、必要な引数を指定します。この例では、ドッキングと読み取り専用の引数を指定しています。

     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#6](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#6)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#6](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#6)]

## <a name="compile-the-code"></a>コードのコンパイル
 このコード例で必要な要素は次のとおりです。

- という名前の Visio 図面は、 `myDrawing.vsd` `Test` *[マイドキュメント*] フォルダー (windows XP 以前の場合) または [*ドキュメント*] フォルダー (windows Vista の場合) のという名前のディレクトリに配置する必要があります。

## <a name="see-also"></a>関連項目
- [Visio ソリューション](../vsto/visio-solutions.md)
- [Visio オブジェクトモデルの概要](../vsto/visio-object-model-overview.md)
- [方法: プログラムによって新しい Visio 図面を作成する](../vsto/how-to-programmatically-create-new-visio-documents.md)
- [方法: プログラムによって Visio 図面を閉じる](../vsto/how-to-programmatically-close-visio-documents.md)
- [方法: プログラムによって Visio 図面を保存する](../vsto/how-to-programmatically-save-visio-documents.md)
- [方法: プログラムによって Visio 図面を印刷する](../vsto/how-to-programmatically-print-visio-documents.md)

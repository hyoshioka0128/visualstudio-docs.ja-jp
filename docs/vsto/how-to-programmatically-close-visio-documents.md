---
title: '方法: プログラムによって Visio 図面を閉じる'
description: Microsoft.Office.Interop.Visio.Document を使用して、active Microsoft Office Visio 図面を閉じる方法について説明します。Close メソッド。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], closing Visio documents
- Visio [Office development in Visual Studio], closing Visio documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: c1592bd500103a2db42934ab8f81392a5f1fa0d1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99903685"
---
# <a name="how-to-programmatically-close-visio-documents"></a>方法: プログラムによって Visio 図面を閉じる
  `Microsoft.Office.Interop.Visio.Document.Close` メソッドを使用すると、アクティブな Microsoft Office Visio 図面を閉じることができます。

 このメソッドの詳細については、 [Microsoft.Office.Interop.Visio.Document.Close](/office/vba/api/Visio.Document.Close) メソッドの VBA リファレンス ドキュメントを参照してください。

## <a name="close-the-active-document"></a>アクティブなドキュメントを閉じる

### <a name="to-close-the-active-document"></a>作業中のドキュメントを閉じるには

- `Microsoft.Office.Interop.Visio.Document.Close` メソッドを呼び出して、作業中のドキュメントを閉じます。

     次のコード例を使用するには、 `ThisAddIn` Visio の VSTO アドインプロジェクトのクラスで実行します。

     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#7](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#7)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#7](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#7)]

## <a name="see-also"></a>関連項目
- [Visio ソリューション](../vsto/visio-solutions.md)
- [Visio オブジェクトモデルの概要](../vsto/visio-object-model-overview.md)
- [方法: プログラムによって新しい Visio 図面を作成する](../vsto/how-to-programmatically-create-new-visio-documents.md)
- [方法: プログラムによって Visio 図面を開く](../vsto/how-to-programmatically-open-visio-documents.md)
- [方法: プログラムによって Visio 図面を保存する](../vsto/how-to-programmatically-save-visio-documents.md)
- [方法: プログラムによって Visio 図面を印刷する](../vsto/how-to-programmatically-print-visio-documents.md)

---
title: '方法: プログラムによって文書内のスペルをチェックする'
description: プログラムによって文書内のスペルをチェックする方法について説明します。 CheckSpelling メソッドを使用できます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], checking spelling
- spelling checker, documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 9afbb96cce5848894c83c8780e5855eadc0e59d0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99836138"
---
# <a name="how-to-programmatically-check-spelling-in-documents"></a>方法: プログラムによって文書内のスペルをチェックする
  ドキュメント内のスペルを確認するには、メソッドを使用し <xref:Microsoft.Office.Interop.Word._Application.CheckSpelling%2A> ます。 このメソッドは、指定されたパラメーターのスペルが正しいかどうかを示すブール値を返します。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-check-spelling-and-display-results-in-a-message-box"></a>スペルチェックを実行し、メッセージボックスに結果を表示するには

1. メソッドを呼び出し、 <xref:Microsoft.Office.Interop.Word._Application.CheckSpelling%2A> テキストの範囲を渡してスペルミスがないかどうかを確認します。 このコード例を使用するには、プロジェクトの `ThisDocument` クラスまたは `ThisAddIn` クラスからコードを実行します。

     [!code-vb[Trin_VstcoreWordAutomation#113](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#113)]
     [!code-csharp[Trin_VstcoreWordAutomation#113](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#113)]

## <a name="see-also"></a>関連項目
- [方法: プログラムによって文書内の範囲を定義および選択する](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)

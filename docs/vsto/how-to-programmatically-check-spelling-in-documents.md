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
ms.openlocfilehash: 8d7e04c542f91b9d7675eb81e7a3178e3427c52a
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828853"
---
# <a name="how-to-programmatically-check-spelling-in-documents"></a>方法: プログラムによって文書内のスペルをチェックする
  ドキュメント内のスペルを確認するには、メソッドを使用し <xref:Microsoft.Office.Interop.Word._Application.CheckSpelling%2A> ます。 このメソッドは、指定されたパラメーターのスペルが正しいかどうかを示すブール値を返します。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-check-spelling-and-display-results-in-a-message-box"></a>スペルチェックを実行し、メッセージボックスに結果を表示するには

1. メソッドを呼び出し、 <xref:Microsoft.Office.Interop.Word._Application.CheckSpelling%2A> テキストの範囲を渡してスペルミスがないかどうかを確認します。 このコード例を使用するには、プロジェクトの `ThisDocument` クラスまたは `ThisAddIn` クラスからコードを実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet113":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet113":::

## <a name="see-also"></a>関連項目
- [方法: プログラムによって文書内の範囲を定義および選択する](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)

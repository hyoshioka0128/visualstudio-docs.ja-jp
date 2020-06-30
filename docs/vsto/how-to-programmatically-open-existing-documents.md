---
title: '方法: プログラムによって既存のドキュメントを開く'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], opening
- Word [Office development in Visual Studio], opening documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: eba4d110b06147db384a4d7aafe01c7d9f272ba3
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85519900"
---
# <a name="how-to-programmatically-open-existing-documents"></a>方法: プログラムによって既存のドキュメントを開く
  メソッドは、 <xref:Microsoft.Office.Interop.Word.Documents.Open%2A> 完全修飾パスとファイル名で指定された既存の Microsoft Office Word 文書を開きます。 このメソッドは、 <xref:Microsoft.Office.Interop.Word.Document> 開いているドキュメントを表すを返します。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-open-a-document"></a>ドキュメントを開くには

- <xref:Microsoft.Office.Interop.Word.Documents.Open%2A>コレクションのメソッドを呼び出し、 <xref:Microsoft.Office.Interop.Word.Documents> ドキュメントへのパスを指定します。

     [!code-vb[Trin_VstcoreWordAutomation#5](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#5)]
     [!code-csharp[Trin_VstcoreWordAutomation#5](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#5)]

## <a name="to-open-a-document-as-read-only"></a>ドキュメントを読み取り専用として開くには

- メソッドを呼び出し <xref:Microsoft.Office.Interop.Word.Documents.Open%2A> 、ドキュメントへのパスを指定し、メソッド呼び出しで*ReadOnly*引数を**True**に設定します。

     [!code-vb[Trin_VstcoreWordAutomation#6](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#6)]
     [!code-csharp[Trin_VstcoreWordAutomation#6](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#6)]

## <a name="compile-the-code"></a>コードのコンパイル
 このコード例で必要な要素は次のとおりです。

- *NewDocument.doc*という名前のドキュメントは、C ドライブの*Test*という名前のディレクトリに存在する必要があります。

## <a name="see-also"></a>関連項目
- [方法: プログラムによって新しいドキュメントを作成する](../vsto/how-to-programmatically-create-new-documents.md)
- [方法: プログラムによって文書を閉じる](../vsto/how-to-programmatically-close-documents.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)

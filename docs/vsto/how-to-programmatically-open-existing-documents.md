---
title: '方法: プログラムによって既存のドキュメントを開く'
description: Open メソッドを使用して、完全修飾パスとファイル名で指定された既存の Microsoft Word 文書を開く方法について説明します。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 81d134c88d93b3da3b0f0e6c3ded3cbe0d6d3f89
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99951681"
---
# <a name="how-to-programmatically-open-existing-documents"></a>方法: プログラムによって既存のドキュメントを開く
  メソッドは、 <xref:Microsoft.Office.Interop.Word.Documents.Open%2A> 完全修飾パスとファイル名で指定された既存の Microsoft Office Word 文書を開きます。 このメソッドは、 <xref:Microsoft.Office.Interop.Word.Document> 開いているドキュメントを表すを返します。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-open-a-document"></a>ドキュメントを開くには

- <xref:Microsoft.Office.Interop.Word.Documents.Open%2A>コレクションのメソッドを呼び出し、 <xref:Microsoft.Office.Interop.Word.Documents> ドキュメントへのパスを指定します。

     [!code-vb[Trin_VstcoreWordAutomation#5](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#5)]
     [!code-csharp[Trin_VstcoreWordAutomation#5](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#5)]

## <a name="to-open-a-document-as-read-only"></a>ドキュメントを読み取り専用として開くには

- メソッドを呼び出し <xref:Microsoft.Office.Interop.Word.Documents.Open%2A> 、ドキュメントへのパスを指定し、メソッド呼び出しで *ReadOnly* 引数を **True** に設定します。

     [!code-vb[Trin_VstcoreWordAutomation#6](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#6)]
     [!code-csharp[Trin_VstcoreWordAutomation#6](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#6)]

## <a name="compile-the-code"></a>コードのコンパイル
 このコード例で必要な要素は次のとおりです。

- *NewDocument.doc* という名前のドキュメントは、C ドライブの *Test* という名前のディレクトリに存在する必要があります。

## <a name="see-also"></a>関連項目
- [方法: プログラムによって新しいドキュメントを作成する](../vsto/how-to-programmatically-create-new-documents.md)
- [方法: プログラムによって文書を閉じる](../vsto/how-to-programmatically-close-documents.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)

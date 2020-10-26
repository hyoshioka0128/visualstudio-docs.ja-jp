---
title: '方法: プログラムによって Word のダイアログボックスを非表示モードで使用する'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- hidden dialog boxes
- Word [Office development in Visual Studio], dialog boxes
- dialog boxes, hidden mode in Word
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 923fc7ddec0350f254968fe17494ecbe27f76b13
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85537580"
---
# <a name="how-to-programmatically-use-word-dialog-boxes-in-hidden-mode"></a>方法: プログラムによって Word のダイアログボックスを非表示モードで使用する
  1つのメソッド呼び出しで複雑な操作を実行するには、Microsoft Office Word の組み込みダイアログボックスをユーザーに表示せずに呼び出します。 これを行うには、 <xref:Microsoft.Office.Interop.Word.Dialog.Execute%2A> メソッドを呼び出さずにオブジェクトのメソッドを使用し <xref:Microsoft.Office.Interop.Word.Dialog> <xref:Microsoft.Office.Interop.Word.Dialog.Display%2A> ます。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="examples"></a>例
 次のコード例では、[ **ページ設定** ] ダイアログボックスを非表示モードで使用して、ユーザー入力なしで複数のページ設定プロパティを設定する方法を示します。 この例では、オブジェクトを使用して、 <xref:Microsoft.Office.Interop.Word.Dialog> カスタムページサイズを構成します。 ページ設定の特定の設定 (上余白、下余白など) は、オブジェクトの遅延バインディングプロパティとして使用でき <xref:Microsoft.Office.Interop.Word.Dialog> ます。 これらのプロパティは、実行時に Word によって動的に作成されます。

 **Option Strict**がオフであり、を対象とする Visual C# プロジェクトでこのタスクを Visual Basic プロジェクトで実行する方法を次の例に示し [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ます。 これらのプロジェクトでは、Visual Basic および Visual C# コンパイラで遅延バインディング機能を使用できます。 この例を使用するに `ThisDocument` は、プロジェクトのクラスまたはクラスから実行し `ThisAddIn` ます。

 [!code-vb[Trin_VstcoreWordAutomation#123](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#123)]
 [!code-csharp[Trin_VstcoreWordAutomation#123](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#123)]

 次の例は、 **Option Strict** がオンになっている Visual Basic プロジェクトでこのタスクを実行する方法を示しています。 これらのプロジェクトでは、遅延バインディングプロパティにアクセスするためにリフレクションを使用する必要があります。 この例を使用するに `ThisDocument` は、プロジェクトのクラスまたはクラスから実行し `ThisAddIn` ます。

 [!code-vb[Trin_VstcoreWordAutomation#104](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#104)]

## <a name="see-also"></a>関連項目
- [方法: プログラムによって Word の組み込みダイアログボックスを使用する](../vsto/how-to-programmatically-use-built-in-dialog-boxes-in-word.md)
- [Word オブジェクトモデルの概要](../vsto/word-object-model-overview.md)
- [Office ソリューションの遅延バインディング](../vsto/late-binding-in-office-solutions.md)
- [リフレクション (C#)](/dotnet/csharp/programming-guide/concepts/reflection)
- [リフレクション (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/reflection)

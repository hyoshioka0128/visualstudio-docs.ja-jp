---
title: '方法: 操作ウィンドウのコントロールのレイアウトを管理する'
description: ユーザーコントロールを適切にスタックするコードを記述して、操作ウィンドウのコントロールのレイアウトを管理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- actions panes [Office development in Visual Studio], control layout
- controls [Office development in Visual Studio], layout on actions panes
- smart documents [Office development in Visual Studio], control layout
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 49739b6011fcf977db84a3350929a56514040975
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99918593"
---
# <a name="how-to-manage-control-layout-on-actions-panes"></a>方法: 操作ウィンドウのコントロールのレイアウトを管理する
  既定では、操作ウィンドウは、ドキュメントまたはワークシートの右側にドッキングされます。ただし、左、上、または下にドッキングできます。 複数のユーザーコントロールを使用している場合は、[操作] ウィンドウでユーザーコントロールを適切にスタックするコードを記述できます。 詳細については、「 [操作ウィンドウの概要](../vsto/actions-pane-overview.md)」を参照してください。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 コントロールのスタックの順序は、操作ウィンドウが垂直方向または水平方向のどちらにドッキングされているかによって異なります。

> [!NOTE]
> ユーザーが実行時に操作ウィンドウのサイズを変更した場合は、操作ウィンドウでサイズを変更するようにコントロールを設定できます。 Windows フォーム コントロールの <xref:System.Windows.Forms.Control.Anchor%2A> プロパティを使用すると、コントロールを操作ウィンドウに固定できます。 詳細については、「 [方法: Windows フォームのコントロールを固定する](/dotnet/framework/winforms/controls/how-to-anchor-controls-on-windows-forms)」を参照してください。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="to-set-the-stack-order-of-the-actions-pane-controls"></a>操作ウィンドウコントロールのスタックの順序を設定するには

1. 複数のユーザーコントロールまたは入れ子になった操作ウィンドウコントロールを持つ操作ウィンドウを含む Microsoft Office Word のドキュメントレベルのプロジェクトを開きます。 詳細については、「 [方法: Word 文書または Excel ブックに操作ウィンドウを追加](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)する」を参照してください。

2. **ソリューションエクスプローラー** で [ **ThisDocument.cs** ] または [ **ThisDocument .vb** ] を右クリックし、[**コードの表示**] をクリックします。

3. <xref:Microsoft.Office.Tools.ActionsPane.OrientationChanged>操作ウィンドウのイベントハンドラーで、操作ウィンドウの向きが横になっているかどうかを確認します。

     [!code-csharp[Trin_VstcoreActionsPaneWord#30](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#30)]
     [!code-vb[Trin_VstcoreActionsPaneWord#30](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#30)]

4. 向きが水平の場合は、操作ウィンドウのコントロールを左からスタックします。それ以外の場合は、上からスタックします。

     [!code-csharp[Trin_VstcoreActionsPaneWord#31](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#31)]
     [!code-vb[Trin_VstcoreActionsPaneWord#31](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#31)]

5. C# では、のイベントハンドラーをイベントハンドラーに追加する必要があり `ActionsPane` <xref:Microsoft.Office.Tools.Word.Document.Startup> ます。 イベントハンドラーの作成の詳細については、「 [方法: Office プロジェクトでイベントハンドラーを作成](../vsto/how-to-create-event-handlers-in-office-projects.md)する」を参照してください。

     [!code-csharp[Trin_VstcoreActionsPaneWord#32](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#32)]

6. プロジェクトを実行し、操作ウィンドウがドキュメントの上部にドッキングされているときに操作ウィンドウのコントロールが左から右に積み重ねられていることを確認します。また、操作ウィンドウがドキュメントの右側にドッキングされている場合は、コントロールが上から下に積み重ねられていることを確認します。

## <a name="example"></a>例
 [!code-csharp[Trin_VstcoreActionsPaneWord#29](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#29)]
 [!code-vb[Trin_VstcoreActionsPaneWord#29](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#29)]

## <a name="compile-the-code"></a>コードのコンパイル
 この例で必要な要素は次のとおりです。

- 複数のユーザーコントロールまたは入れ子になった操作ウィンドウコントロールを含む操作ウィンドウを持つ Word 文書レベルのプロジェクト。

## <a name="see-also"></a>関連項目
- [操作ウィンドウの概要](../vsto/actions-pane-overview.md)
- [方法: Word 文書または Excel ブックに操作ウィンドウを追加する](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [方法: Word 文書または Excel ブックに操作ウィンドウを追加する](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [チュートリアル: 操作ウィンドウからドキュメントにテキストを挿入する](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)
- [チュートリアル: 操作ウィンドウからドキュメントにテキストを挿入する](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)

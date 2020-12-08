---
title: Word 文書または Excel ブックに操作ウィンドウを追加する
description: Microsoft Office Word 文書または Microsoft Excel ブックに操作ウィンドウを追加するには、まず Windows フォームユーザーコントロールを作成する必要があることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- smart documents [Office development in Visual Studio], creating in Word
- smart documents [Office development in Visual Studio], adding controls
- actions panes [Office development in Visual Studio], creating in Word
- actions panes [Office development in Visual Studio], adding controls
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 69d675209f2a3ac47e8681da8fca73c5cd86e95d
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96848067"
---
# <a name="how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks"></a>方法: Word 文書または Excel ブックに操作ウィンドウを追加する
  Microsoft Office Word 文書または Microsoft Excel ブックに操作ウィンドウを追加するには、まず Windows フォームユーザーコントロールを作成します。 次に、 <xref:Microsoft.Office.Tools.ActionsPane.Controls%2A> `ThisDocument.ActionsPane` プロジェクト内のフィールド (Word) またはフィールド (Excel) のプロパティにユーザーコントロールを追加し `ThisWorkbook.ActionsPane` ます。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="creating-the-user-control"></a>ユーザー コントロールの作成
 次の手順は、Word または Excel プロジェクトでユーザーコントロールを作成する方法を示しています。 また、テキストをクリックしたときに文書またはブックに書き込まれるボタンをユーザーコントロールに追加します。

#### <a name="to-create-the-user-control"></a>ユーザーコントロールを作成するには

1. Visual Studio で Word または Excel のドキュメントレベルのプロジェクトを開きます。

2. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

3. [ **新しい項目の追加** ] ダイアログボックスで [ **操作ウィンドウコントロール**] を選択し、「 **HelloControl**」という名前を指定して、[ **追加**] をクリックします。

    > [!NOTE]
    > 別の方法として、 **ユーザーコントロール** 項目をプロジェクトに追加することもできます。 **操作ウィンドウコントロール** と **ユーザーコントロール** の項目によって生成されるクラスは、機能的には同等です。

4. [**ツールボックス**] の [ **Windows フォーム**] タブで、**ボタン** コントロールをコントロールにドラッグします。

    > [!NOTE]
    > コントロールがデザイナーに表示されていない場合は、**ソリューションエクスプローラー** で [ **HelloControl** ] をダブルクリックします。

5. <xref:System.Windows.Forms.Control.Click>ボタンのイベントハンドラーにコードを追加します。 次の例は、Microsoft Office Word 文書のコードを示しています。

     [!code-csharp[Trin_VstcoreActionsPaneWord#12](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/HelloControl.cs#12)]
     [!code-vb[Trin_VstcoreActionsPaneWord#12](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/HelloControl.vb#12)]

6. C# では、ボタンクリック用のイベントハンドラーを追加する必要があります。 このコードは、の `HelloControl` 呼び出し後にコンストラクターに配置でき `InitializeComponent` ます。

     イベントハンドラーの作成方法の詳細については、「 [方法: Office プロジェクトでイベントハンドラーを作成](../vsto/how-to-create-event-handlers-in-office-projects.md)する」を参照してください。

     [!code-csharp[Trin_VstcoreActionsPaneWord#13](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/HelloControl.cs#13)]

## <a name="add-the-user-control-to-the-actions-pane"></a>操作ウィンドウにユーザーコントロールを追加する
 操作ウィンドウを表示するには、ユーザーコントロールを <xref:Microsoft.Office.Tools.ActionsPane.Controls%2A> `ThisDocument.ActionsPane` フィールド (Word) またはフィールド (Excel) のプロパティに追加し `ThisWorkbook.ActionsPane` ます。

### <a name="to-add-the-user-control-to-the-actions-pane"></a>操作ウィンドウにユーザーコントロールを追加するには

1. `ThisDocument`クラスまたはクラスに、クラスレベルの宣言として次のコードを追加し `ThisWorkbook` ます (メソッドにこのコードを追加しないでください)。

     [!code-csharp[Trin_VstcoreActionsPaneWord#14](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#14)]
     [!code-vb[Trin_VstcoreActionsPaneWord#14](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#14)]

2. クラスの `ThisDocument_Startup` イベントハンドラー `ThisDocument` または `ThisWorkbook_Startup` クラスのイベントハンドラーに次のコードを追加し `ThisWorkbook` ます。

     [!code-csharp[Trin_VstcoreActionsPaneWord#15](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#15)]
     [!code-vb[Trin_VstcoreActionsPaneWord#15](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#15)]

## <a name="see-also"></a>関連項目
- [操作ウィンドウの概要](../vsto/actions-pane-overview.md)
- [チュートリアル: 操作ウィンドウからドキュメントにテキストを挿入する](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)
- [方法: 操作ウィンドウのコントロールのレイアウトを管理する](../vsto/how-to-manage-control-layout-on-actions-panes.md)
- [チュートリアル: 操作ウィンドウからドキュメントにテキストを挿入する](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)

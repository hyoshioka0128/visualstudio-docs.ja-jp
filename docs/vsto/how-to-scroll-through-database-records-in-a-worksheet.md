---
title: '方法: ワークシート内のデータベースレコードをスクロールする'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- databases [Office development in Visual Studio], scrolling records
- records [Office development in Visual Studio], scrolling
- data [Office development in Visual Studio], scrolling database records
- worksheets [Office development in Visual Studio], scrolling records
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8127a5f61e292fb777be4854796535bbe01226aa
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85545796"
---
# <a name="how-to-scroll-through-database-records-in-a-worksheet"></a>方法: ワークシート内のデータベースレコードをスクロールする
  次の手順では、デザイナーを使用して、Microsoft Office Excel ワークシートのデータベーステーブルから単一のフィールドを表示する方法を示します。このコントロールには、エンドユーザーがすべてのレコードをスクロールできるようにするコントロールがあります。

 デザイナーは、ドキュメントレベルのプロジェクトでのみ使用できます。 ただし、コントロールを追加し、実行時にプログラムによってデータにバインドすることもできます。 詳細については、「 [チュートリアル: VSTO アドインプロジェクトでの単純データバインディング](../vsto/walkthrough-simple-data-binding-in-vsto-add-in-project.md)」を参照してください。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

## <a name="to-scroll-through-database-records-in-a-worksheet"></a>ワークシート内のデータベースレコードをスクロールするには

1. Visual Studio で Excel アプリケーションプロジェクトを開きます。

2. [ **データソース** ] ウィンドウを開き、データベースからデータソースを作成します。 詳細については、「 [新しい接続の追加](../data-tools/add-new-connections.md)」を参照してください。

3. 表示するデータが含まれているテーブルを展開し、特定の列を選択します。

4. コントロールの一覧を開き、[ **NamedRange**] を選択します。

5. <xref:Microsoft.Office.Tools.Excel.NamedRange>データを表示するセルにコントロールをドラッグします。

6. **ツールボックス**の [ **Windows フォーム**] タブで、 <xref:System.Windows.Forms.BindingNavigator> ワークシートにコントロールを追加し、使用するコントロールを設定します。 詳細については、「 [BindingNavigator コントロールの概要 &#40;Windows フォーム&#41;](/dotnet/framework/winforms/controls/bindingnavigator-control-overview-windows-forms)」を参照してください。

## <a name="see-also"></a>関連項目
- [Office ソリューションのコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)

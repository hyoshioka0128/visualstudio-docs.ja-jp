---
title: '方法: データベースのデータをワークシートに読み込む'
description: ソリューション内のオブジェクトのデータを使用する方法、および Windows フォームコントロールを使用してワークシートにデータを表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets [Office development in Visual Studio], populating
- databases [Office development in Visual Studio], populating worksheets
- data [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4252eac32540ac2d0b6e763b5b6e9cf0e2ac7055
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96846442"
---
# <a name="how-to-populate-worksheets-with-data-from-a-database"></a>方法: データベースのデータをワークシートに読み込む

ドキュメントレベルの Office プロジェクトのデータには、Windows フォームプロジェクトのデータにアクセスするのと同じ方法でアクセスできます。 同じツールとコードを使用してソリューションにデータを取り込むことができ、Windows フォーム コントロールを使用してデータを表示できます。 また、ホストコントロールと呼ばれるコントロールを利用することもできます。これは、イベントとデータバインディング機能によって強化された Microsoft Office Excel のネイティブオブジェクトです。 詳細については、「 [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)」を参照してください。

[!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

次の例は、デザイナーを使用してドキュメント レベルのプロジェクトにデータ バインド コントロールを追加する方法を示しています。 実行時にアプリケーションレベルのプロジェクトにデータバインドコントロールを追加する方法の例については、「 [チュートリアル: VSTO アドインプロジェクトでの複合データバインディング](../vsto/walkthrough-complex-data-binding-in-vsto-add-in-project.md)」を参照してください。

## <a name="add-a-data-bound-control-to-a-worksheet-at-design-time"></a>デザイン時にワークシートにデータバインドコントロールを追加する

### <a name="to-populate-a-worksheet-with-data-from-a-database"></a>データベースのデータをワークシートに設定するには

1. デザイナーでワークシートを開いた状態で、Visual Studio で Excel ドキュメントレベルのプロジェクトを開きます。

2. **[データ ソース]** ウィンドウを開いて、プロジェクトのデータ ソースを作成します。 詳細については、「 [新しい接続の追加](../data-tools/add-new-connections.md)」を参照してください。

3. 目的のフィールドまたはテーブルを [ **データソース** ] ウィンドウからワークシートにドラッグします。

次のいずれかのコントロールがワークシートに作成されます。

- フィールドをドラッグすると、 <xref:Microsoft.Office.Tools.Excel.NamedRange> ワークシートにコントロールが作成されます。 詳細については、「 [NamedRange control](../vsto/namedrange-control.md)」を参照してください。

- テーブルをドラッグすると、 <xref:Microsoft.Office.Tools.Excel.ListObject> ワークシートにコントロールが作成されます。 詳細については、「 [ListObject コントロール](../vsto/listobject-control.md)」を参照してください。

別のコントロールを追加するには、[ **データソース** ] ウィンドウでテーブルまたはフィールドを選択し、ドロップダウンリストから別のコントロールを選択します。

## <a name="objects-in-the-project"></a>プロジェクト内のオブジェクト

プロジェクトには、コントロールに加えて、データに関連する以下のオブジェクトも自動的に追加されます。

- データベース内の接続したデータ テーブルをカプセル化する型指定されたデータセット。 詳細については、「 [Visual Studio のデータセットツール](../data-tools/dataset-tools-in-visual-studio.md)」を参照してください。

- コントロールを型指定されたデータセットに接続する <xref:System.Windows.Forms.BindingSource>。 詳細については、「 [BindingSource コンポーネントの概要](/dotnet/framework/winforms/controls/bindingsource-component-overview)」を参照してください。

- 型指定されたデータセットをデータベースに接続する TableAdapter。 詳細については、「 [TableAdapter の概要](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview)」を参照してください。

- TableAdapterManager。階層更新を有効にするために、データセット内のテーブルアダプターを調整するために使用されます。 詳細については、「 [階層更新](../data-tools/hierarchical-update.md) と [TableAdapterManager リファレンス](../data-tools/fill-datasets-by-using-tableadapters.md#tableadaptermanager-reference)」を参照してください。

プロジェクトを実行すると、データ ソースの先頭のレコードがコントロールに表示されます。 <xref:System.Windows.Forms.BindingSource> を使用すると、ユーザーがレコードをスクロールできるようになります。

### <a name="to-scroll-through-the-records"></a>レコードをスクロールするには

- <xref:System.Windows.Forms.BindingSource.MoveNext%2A> や <xref:System.Windows.Forms.BindingSource.MovePrevious%2A> など、<xref:System.Windows.Forms.BindingSource> のメソッドを使用します。

型指定されたデータセットおよびデータベースに更新を送信する方法については、「 [方法: ホストコントロールからのデータを使用してデータソースを更新](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)する」を参照してください。

## <a name="see-also"></a>関連項目

- [Office ソリューションのコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [新しいデータ ソースの追加](../data-tools/add-new-data-sources.md)
- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [方法: オブジェクトのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-objects.md)
- [方法: データベースのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-a-database.md)
- [方法: サービスのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-services.md)
- [方法: ホストコントロールのデータを使用してデータソースを更新する](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
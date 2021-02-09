---
title: Office ソリューションのコントロールにデータをバインドする
description: Microsoft Office Word 文書または Excel ワークシート上のコントロールとホストコントロールをデータソースにバインド Windows フォーム方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office documents [Office development in Visual Studio], connecting to data
- data, data binding
- data binding
- data binding, Office solutions
- data binding, controls
- Office applications [Office development in Visual Studio], data binding
- controls, data binding
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 459c50b5f8135756f85de852a62de44b3878148d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99882480"
---
# <a name="bind-data-to-controls-in-office-solutions"></a>Office ソリューションのコントロールにデータをバインドする
  Microsoft Office Word 文書または Microsoft Office Excel ワークシート上の Windows フォーム コントロールや *ホスト コントロール* を、データ ソースにバインドできます。この場合、コントロールには自動的にデータが表示されます。 アプリケーション レベルのプロジェクトとドキュメント レベルのプロジェクトの両方で、コントロールにデータをバインドできます。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 ホスト コントロールは、Word や Excel のオブジェクト モデルにあるオブジェクトを拡張します。たとえば、Word のコンテンツ コントロールや Excel の名前付き範囲が挙げられます。 詳細については、「 [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)」を参照してください。

 Windows フォーム コントロールとホスト コントロールはいずれも Windows フォームのデータ バインディング モデルを使用します。このモデルでは、データセットやデータ テーブルなどのデータ ソースに対して *単純データ バインディング* と *複合データ バインディング* の両方がサポートされます。 Windows フォームでのデータバインディングモデルの詳細については、「 [データバインドと Windows フォーム](/dotnet/framework/winforms/data-binding-and-windows-forms)」を参照してください。

## <a name="simple-data-binding"></a>単純データ バインディング
 単純データ バインディングは、コントロール プロパティが、データ テーブル内の値など、単一のデータ要素にバインドされる場合に存在します。 たとえば、 <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールは、データセット内のフィールドにバインドできる <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> プロパティを持ちます。 データセット内のフィールドが変更されると、名前付き範囲内の値も変更されます。 <xref:Microsoft.Office.Tools.Word.XMLNodes> コントロールを除くすべてのホスト コントロールが、単純データ バインディングをサポートしています。 <xref:Microsoft.Office.Tools.Word.XMLNodes> コントロールはコレクションであるため、データ バインディングをサポートしません。

 ホスト コントロールへの単純データ バインディングを実行するには、コントロールの `DataBindings` プロパティに <xref:System.Windows.Forms.Binding> を追加します。 <xref:System.Windows.Forms.Binding> オブジェクトは、コントロールのプロパティ値とデータ要素の値との間の単純バインディングを表します。

 ドキュメント レベルのプロジェクトにあるデータ要素に <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> プロパティをバインドする方法を、次の例に示します。

 [!code-vb[Trin_BindableComponent#4](../vsto/codesnippet/VisualBasic/Trin_BindableComponent/Sheet1.vb#4)]
 [!code-csharp[Trin_BindableComponent#4](../vsto/codesnippet/CSharp/Trin_BindableComponent/Sheet1.cs#4)]

 単純なデータバインディングを示すチュートリアルについては、「チュートリアル: ドキュメントレベルのプロジェクトの [ドキュメントレベルのプロジェクトの単純なデータバインディング](../vsto/walkthrough-simple-data-binding-in-a-document-level-project.md) 」と「チュートリアル: vsto アドインプロジェクトの [vsto アドインプロジェクトの単純なデータバインディング](../vsto/walkthrough-simple-data-binding-in-vsto-add-in-project.md) 」を参照してください。

## <a name="complex-data-binding"></a>複合データ バインディング
 複合データ バインディングは、コントロール プロパティが、データ テーブル内の複数の列など、複数のデータ要素にバインドされる場合に存在します。 Excel の <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールは、複合データ バインディングをサポートする唯一のホスト コントロールです。 ただし、複合データ バインディングをサポートする Windows フォーム コントロールが数多くあります ( <xref:System.Windows.Forms.DataGridView> コントロールなど)。

 複合データ バインディングを実行するには、コントロールの `DataSource` プロパティを、複合データ バインディングでサポートされるデータ ソース オブジェクトに設定します。 たとえば、 <xref:Microsoft.Office.Tools.Excel.ListObject.DataSource%2A> コントロールの <xref:Microsoft.Office.Tools.Excel.ListObject> プロパティは、データ テーブル内の複数の列にバインドできます。 データ テーブル内のすべてのデータは <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールに表示され、データ テーブル内のデータが変更されると、 <xref:Microsoft.Office.Tools.Excel.ListObject> も変更されます。 複合データバインディングに使用できるデータソースの一覧については、「 [Windows フォームでサポートされるデータソース](/dotnet/framework/winforms/data-sources-supported-by-windows-forms)」を参照してください。

 次のコード例は、2 つの <xref:System.Data.DataSet> オブジェクトを持つ <xref:System.Data.DataTable> を作成し、そのうち 1 つのテーブルにデータを入力します。 次に、コードはデータを含むテーブルに <xref:Microsoft.Office.Tools.Excel.ListObject> をバインドします。 これは、Excel のドキュメント レベルのプロジェクト用の例です。

 [!code-csharp[Trin_ExcelListObject#18](../vsto/codesnippet/CSharp/Trin_ExcelListObject/Trin_ExcelListObject.cs#18)]
 [!code-vb[Trin_ExcelListObject#18](../vsto/codesnippet/VisualBasic/Trin_ExcelListObject/Sheet1.vb#18)]

 複雑なデータバインディングを示すチュートリアルについては、「チュートリアル: ドキュメントレベルのプロジェクトの [ドキュメントレベルのプロジェクトでの複合データバインディング](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md) 」と「チュートリアル: vsto アドインプロジェクトの [vsto アドインプロジェクトでの複合データバインディング](../vsto/walkthrough-complex-data-binding-in-vsto-add-in-project.md) 」を参照してください。

## <a name="display-data-in-documents-and-workbooks"></a>ドキュメントとブックにデータを表示する
 ドキュメント レベルのプロジェクトでは、Windows フォームで使用する場合と同じように **[データ ソース]** ウィンドウを使用して、文書やブックにデータ バインド コントロールを簡単に追加できます。 [ **データソース** ] ウィンドウの使用方法の詳細については、「 [Visual Studio でデータに Windows フォームコントロールをバインドする](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md) 」および「 [新しいデータソースを追加](../data-tools/add-new-data-sources.md)する」を参照してください。

### <a name="drag-controls-from-the-data-sources-window"></a>[データソース] ウィンドウからコントロールをドラッグする
 **[データ ソース]** ウィンドウからオブジェクトをドラッグすると、ドキュメントにコントロールが作成されます。 作成されるコントロールの種類は、単一のデータ列をバインドするか、複数のデータ列をバインドするかによって異なります。

 Excel の場合、フィールドごとに <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールがワークシートに作成され、複数の行と列を含むデータ範囲ごとに <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールが作成されます。 この既定の動作を変更するには、 **[データ ソース]** ウィンドウでテーブルまたはフィールドを選び、ドロップダウン リストで別のコントロールを選びます。

 <xref:Microsoft.Office.Tools.Word.ContentControl> コントロールが文書に追加されます。 コンテンツ コントロールの種類は、選んだフィールドのデータ型によって異なります。

### <a name="bind-data-in-document-level-projects-at-design-time"></a>デザイン時にドキュメントレベルのプロジェクトのデータをバインドする
 以下のトピックでは、デザイン時にデータをバインドする例を示しています。

- [方法: データベースのデータをワークシートに読み込む](../vsto/how-to-populate-worksheets-with-data-from-a-database.md)

- [方法: データベースのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-a-database.md)

- [方法: オブジェクトのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-objects.md)

- [方法: サービスのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-services.md)

- [方法: ワークシート内のデータベースレコードをスクロールする](../vsto/how-to-scroll-through-database-records-in-a-worksheet.md)

### <a name="bind-data-in-vsto-add-in-projects"></a>VSTO アドインプロジェクトでのデータのバインド
 VSTO アドイン プロジェクトでは、コントロールを追加できるのは実行時だけです。 以下のトピックでは、実行時にデータをバインドする例を示しています。

- [チュートリアル: VSTO アドインプロジェクトでの単純データバインディング](../vsto/walkthrough-simple-data-binding-in-vsto-add-in-project.md)

- [チュートリアル: VSTO アドインプロジェクトでの複合データバインディング](../vsto/walkthrough-complex-data-binding-in-vsto-add-in-project.md)

## <a name="update-data-that-is-bound-to-host-controls"></a>ホストコントロールにバインドされているデータの更新
 データ ソースとホスト コントロールの間のデータ バインディングでは、双方向のデータ更新が必要です。 単純データ バインディングでは、データ ソースでの変更は自動的にホスト コントロールに反映されますが、ホスト コントロールでの変更の場合、明示的な呼び出しによってデータ ソースを更新する必要があります。 これは、別のデータ バインド フィールドで行われた変更が伴わない限り、あるデータ バインド フィールドで行われた変更が受け付けられないことがあるためです。 たとえば、2 つのフィールドがあり、1 つは年齢、1 つは経験年数を示すものとします。 経験年数が年齢を上回ることはありません。 同時に変更しない限り、ユーザーは年齢を 50 から 25 に更新し、経験年数を 30 から 10 に更新することはできません。 この問題を解決するために、単純データ バインディングのフィールドは、更新がコードで明示的に送信されるまで更新されないようになっています。

 単純データ バインディングを有効にしているホスト コントロールからデータ ソースを更新するには、更新をメモリ内データ ソース ( <xref:System.Data.DataSet> や <xref:System.Data.DataTable>など) に送信する必要があります。ソリューションでバックエンド データベースを使用している場合は、バックエンド データベースにも更新を送信する必要があります。

 <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールを使用して複合データ バインディングを実行するときは、メモリ内データ ソースを明示的に更新する必要はありません。 この場合には、コードを追加しなくても、メモリ内データ ソースに変更が自動的に送信されます。

 詳細については、「 [方法: ホストコントロールのデータを使用してデータソースを更新](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)する」を参照してください。

## <a name="see-also"></a>関連項目
- [データバインディングと Windows フォーム](/dotnet/framework/winforms/data-binding-and-windows-forms)
- [方法: Windows フォームに単純バインドコントロールを作成する](/dotnet/framework/winforms/how-to-create-a-simple-bound-control-on-a-windows-form)
- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
- [TableAdapter を使用してデータを更新する](../data-tools/update-data-by-using-a-tableadapter.md)
- [キャッシュ データ](../vsto/caching-data.md)
- [Office ソリューションのデータ](../vsto/data-in-office-solutions.md)

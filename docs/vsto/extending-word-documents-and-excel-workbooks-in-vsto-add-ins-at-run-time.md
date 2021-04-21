---
title: 実行時に VSTO アドインの Word 文書 & Excel ブックに拡張する
description: VSTO アドインを使用して、さまざまな方法で Word 文書や Excel ブックをカスタマイズする方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- GetVstoObject method
- application-level add-ins [Office development in Visual Studio], adding controls to documents
- host items [Office development in Visual Studio], creating at run time in add-ins
- application-level add-ins [Office development in Visual Studio], extending Word documents
- application-level add-ins [Office development in Visual Studio], extending Excel workbooks
- controls [Office development in Visual Studio], adding at run time
- HasVstoObject method
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 90dac328f336f7204bc9a70a0dbc543ec996922a
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825668"
---
# <a name="extend-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time"></a>実行時に VSTO アドインの Word 文書と Excel ブックを拡張する
  VSTO アドインを利用すれば、Word 文書と Excel ブックを次のようにカスタマイズできます。

- 開いている文書またはブックに管理されているコントロールを追加します。

- Excel ワークシートの既存のリスト オブジェクトを、イベントを公開し、Windows フォーム データ バインディング モデルでデータにバインディングできる拡張 <xref:Microsoft.Office.Tools.Excel.ListObject> に変換します。

- 特定の文書、ブック、ワークシートに対して Word と Excel が公開するアプリケーションレベル イベントにアクセスします。

  この機能を使用するには、文書またはブックを拡張するオブジェクトを実行時に生成します。

  **適用対象:** この記事の情報は、Excel と Word の VSTO アドインのプロジェクトに適用されます。 詳細については、「 [Office アプリケーションおよびプロジェクトの種類別の使用可能な機能](../vsto/features-available-by-office-application-and-project-type.md)」を参照してください。

## <a name="generate-extended-objects-in-vsto-add-ins"></a>VSTO アドインで拡張オブジェクトを生成する
 *拡張オブジェクト* は Word または Excel オブジェクト モデルにネイティブで存在するオブジェクト ( *ネイティブ Office オブジェクト*) に機能を追加する Visual Studio Tools for Office Runtime が提供する種類のインスタンスです。 Word または Excel オブジェクトの拡張オブジェクトを生成するには`GetVstoObject` メソッドを使用します。 `GetVstoObject`指定された Word または Excel オブジェクトのメソッドを初めて呼び出すときに、指定されたオブジェクトを拡張する新しいオブジェクトを返します。 このメソッドを呼び出し、同じ Word または Excel を指定するたびに、同じ拡張オブジェクトが返されます。

 拡張オブジェクトの種類にはネイティブ Office オブジェクトの種類と同じ名前が与えられますが、この種類は <xref:Microsoft.Office.Tools.Excel> または <xref:Microsoft.Office.Tools.Word> 名前空間で定義されます。 たとえば、`GetVstoObject` メソッドを呼び出し、<xref:Microsoft.Office.Interop.Word.Document> オブジェクトを拡張した場合、このメソッドは <xref:Microsoft.Office.Tools.Word.Document> オブジェクトを返します。

 `GetVstoObject` メソッドは主に VSTO アドイン プロジェクトで使用するためのものです。 ドキュメントレベル プロジェクトでこれらのメソッドを使用することもできますが、動作が異なり、用途が少なくなります。

 特定のネイティブ Office オブジェクトに対して拡張オブジェクトが既に生成されているかどうかを確認するには、`HasVstoObject` メソッドを使用します。 詳細については、「 [Office オブジェクトが拡張されているかどうかを判断する](#HasVstoObject)」を参照してください。

### <a name="generate-host-items"></a>ホスト項目の生成
 を使用して `GetVstoObject` ドキュメントレベルのオブジェクト (つまり、、、または) を拡張すると、 <xref:Microsoft.Office.Interop.Excel.Workbook> <xref:Microsoft.Office.Interop.Excel.Worksheet> <xref:Microsoft.Office.Interop.Word.Document> 返されたオブジェクトは *ホスト項目* と呼ばれます。 ホスト項目は、他の拡張されたオブジェクトやコントロールなど、他のオブジェクトを含めることができる種類です。 Word または Excel プライマリ相互運用機能アセンブリの対応する種類と似ていますが、機能が多くなっています。 ホスト項目の詳細については、「 [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)」を参照してください。

 ホスト項目を生成したら、それを利用して管理されているコントロールを文書、ブック、ワークシートに追加できます。 詳細については、「 [ドキュメントおよびワークシートへのマネージコントロールの追加](#AddControls)」を参照してください。

#### <a name="to-generate-a-host-item-for-a-word-document"></a>Word 文書のホスト項目を生成するには

- 次のコード例はアクティブな文書のホスト項目を生成する方法を示しています。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet8":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet8":::

#### <a name="to-generate-a-host-item-for-an-excel-workbook"></a>Excel ブックのホスト項目を生成するには

- 次のコード例はアクティブなブックのホスト項目を生成する方法を示しています。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_exceladdindynamiccontrols4/ThisAddIn.vb" id="Snippet2":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_exceladdindynamiccontrols4/ThisAddIn.cs" id="Snippet2":::

#### <a name="to-generate-a-host-item-for-an-excel-worksheet"></a>Excel ワークシートのホスト項目を生成するには

- 次のコード例はプロジェクトのアクティブなワークシートのホスト項目を生成する方法を示しています。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_exceladdindynamiccontrols4/ThisAddIn.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_exceladdindynamiccontrols4/ThisAddIn.cs" id="Snippet1":::

### <a name="generate-listobject-host-controls"></a>ListObject ホストコントロールを生成する
 `GetVstoObject` メソッドを利用して <xref:Microsoft.Office.Interop.Excel.ListObject> を拡張すると、このメソッドは <xref:Microsoft.Office.Tools.Excel.ListObject> を返します。 には、 <xref:Microsoft.Office.Tools.Excel.ListObject> 元ののすべての機能があり <xref:Microsoft.Office.Interop.Excel.ListObject> ます。 また、追加の機能があり、Windows フォームデータバインディングモデルを使用してデータにバインドすることもできます。 詳細については、「 [ListObject コントロール](../vsto/listobject-control.md)」を参照してください。

#### <a name="to-generate-a-host-control-for-a-listobject"></a>ListObject のホスト コントロールを生成するには

- 次のコード例はプロジェクトのアクティブなワークシートの最初の <xref:Microsoft.Office.Tools.Excel.ListObject> に対して <xref:Microsoft.Office.Interop.Excel.ListObject> を生成する方法を示しています。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_exceladdindynamiccontrols4/ThisAddIn.vb" id="Snippet3":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_exceladdindynamiccontrols4/ThisAddIn.cs" id="Snippet3":::

### <a name="add-managed-controls-to-documents-and-worksheets"></a><a name="AddControls"></a> ドキュメントとワークシートへのマネージコントロールの追加
 <xref:Microsoft.Office.Tools.Word.Document> または <xref:Microsoft.Office.Tools.Excel.Worksheet>を生成したら、これらの拡張オブジェクトが表す文書またはワークシートにコントロールを追加できます。 コントロールを追加するに `Controls` は、またはのプロパティを使用し <xref:Microsoft.Office.Tools.Word.Document> <xref:Microsoft.Office.Tools.Excel.Worksheet> ます。 詳細については、「 [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。

 Windows フォーム コントロールまたは *ホスト コントロール* を追加できます。 ホスト コントロールは [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] により提供されるコントロールであり、Word または Excel プライマリ相互運用機能アセンブリのそれに対応するコントロールをラップします。 ホストコントロールは、基になるネイティブ Office オブジェクトのすべての動作を公開します。 また、イベントも発生し、Windows フォームデータバインディングモデルを使用してデータにバインドできます。 詳細については、「 [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)」を参照してください。

> [!NOTE]
> VSTO アドインを利用し、 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> コントロールをワークシートに、 <xref:Microsoft.Office.Tools.Word.XMLNode> または <xref:Microsoft.Office.Tools.Word.XMLNodes> コントロールを文書に追加することはできません。 これらのホスト コントロールをプログラミングで追加することはできません。 詳細については、「 [ホスト項目とホストコントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)」を参照してください。

### <a name="persist-and-remove-controls"></a>コントロールの永続化と削除
 管理されているコントロールを文書またはワークシートに追加するとき、文書を保存し、閉じても、コントロールは保持されません。 基礎となるネイティブ Office オブジェクトだけが残るようにすべてのホスト コントロールが削除されます。 たとえば、 <xref:Microsoft.Office.Tools.Excel.ListObject> が <xref:Microsoft.Office.Interop.Excel.ListObject>になります。 すべての Windows フォーム コントロールも削除されますが、ActiveX ラッパーは文書に残ります。 コントロールを消去するか、文書を次回開いたときにコントロールを再作成するには、VSTO アドインにコードを追加する必要があります。 詳細については、「 [Office ドキュメントに動的コントロールを保存](../vsto/persisting-dynamic-controls-in-office-documents.md)する」を参照してください。

## <a name="access-application-level-events-on-documents-and-workbooks"></a>ドキュメントおよびブックのアプリケーションレベルのイベントへのアクセス
 ネイティブの Word または Excel オブジェクト モデルの一部の文書、ブック、ワークシート イベントはアプリケーション レベルでのみ発生します。 たとえば、 <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> イベントは文書を Word で開いたときに発生しますが、このイベントは <xref:Microsoft.Office.Interop.Word.Application> クラスではなく、 <xref:Microsoft.Office.Interop.Word.Document> クラスに定義されています。

 VSTO アドインでネイティブ Office オブジェクトを使用するとき、これらのアプリケーションレベル イベントを処理し、イベントを発生された文書が自分でカスタマイズした文書であるかどうかを判断する追加コードを記述する必要があります。 ホスト項目は文書レベルでこれらのイベントを提供します。そのため、特定の文書のイベントを簡単に処理できます。 ホスト項目を生成し、そのホスト項目のイベントを処理できます。

### <a name="example-that-uses-native-word-objects"></a>ネイティブ Word オブジェクトを使用する例
 次のコード例は Word 文書のアプリケーションレベル イベントの処理方法を示しています。 `CreateDocument` メソッドは新しい文書を作成し、その文書が保存されないようにする <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> イベント ハンドラーを定義します。 イベントは、オブジェクトに対して発生するアプリケーションレベルのイベントです <xref:Microsoft.Office.Interop.Word.Application> 。イベントハンドラーは、パラメーターをオブジェクトと比較して、 `Doc` `document1` が保存されたドキュメントを表しているかどうかを判断する必要があり `document1` ます。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet12":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet12":::

### <a name="examples-that-use-a-host-item"></a>ホスト項目を使用する例
 次のコード例では、 <xref:Microsoft.Office.Tools.Word.Document.BeforeSave> ホスト項目の <xref:Microsoft.Office.Tools.Word.Document> イベントを処理することでこのプロセスを簡略化しています。 `CreateDocument2`これらの例のメソッドは、オブジェクトを拡張するを生成し、その <xref:Microsoft.Office.Tools.Word.Document> 後、 `document2` <xref:Microsoft.Office.Tools.Word.Document.BeforeSave> ドキュメントが保存されないようにするイベントハンドラーを定義します。 イベントハンドラーはが保存されたときにのみ呼び出され、保存さ `document2` れたドキュメントを確認するための追加の作業を行わずに保存操作を取り消すことができます。

 次のコード例はこの作業を示しています。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet13":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet13":::

## <a name="determine-whether-an-office-object-has-been-extended"></a><a name="HasVstoObject"></a> Office オブジェクトが拡張されているかどうかを確認する
 特定のネイティブ Office オブジェクトに対して拡張オブジェクトが既に生成されているかどうかを確認するには、`HasVstoObject` メソッドを使用します。 拡張オブジェクトが既に生成されている場合、このメソッドは **true** を返します。

 `Globals.Factory.HasVstoMethod` メソッドを使用します。 拡張オブジェクトに対してテストするネイティブの Word または Excel オブジェクト ( <xref:Microsoft.Office.Interop.Word.Document> や <xref:Microsoft.Office.Interop.Excel.Worksheet>など) を渡します。

 `HasVstoObject` メソッドは、指定した Office オブジェクトに拡張オブジェクトがある場合にのみ、コードの実行で便利です。 たとえば、イベントを処理して、 <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> 保存前にドキュメントからマネージコントロールを削除する WORD VSTO アドインがある場合は、メソッドを使用して `HasVstoObject` 、ドキュメントが拡張されているかどうかを確認します。 ドキュメントが拡張されていない場合は、マネージコントロールを持つことはできません。また、イベントハンドラーは、ドキュメント上のコントロールをクリーンアップせずに制御を戻すことができます。

## <a name="see-also"></a>関連項目
- [プログラム VSTO アドイン](../vsto/programming-vsto-add-ins.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)

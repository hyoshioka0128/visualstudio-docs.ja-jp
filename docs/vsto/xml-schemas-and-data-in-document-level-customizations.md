---
title: ドキュメントレベルのカスタマイズにおける XML スキーマとデータ
description: Microsoft Excel および Word には、スキーマをドキュメントにマップする機能が用意されています。これにより、ドキュメントへの XML データのインポートとエクスポートを簡単に行うことができます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XML schemas [Office development in Visual Studio]
- schemas [Office development in Visual Studio]
- XML [Office development in Visual Studio], XML schemas
- XML schemas [Office development in Visual Studio], about XML schemas and data
- Office development in Visual Studio, XML
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ece2c06e9432ca24b4a5773c9938aeec61df0270
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894414"
---
# <a name="xml-schemas-and-data-in-document-level-customizations"></a>ドキュメントレベルのカスタマイズにおける XML スキーマとデータ
  **重要** このトピックに記載されている Microsoft Word に関する情報は、microsoft word のカスタム XML に関連する特定の機能の実装が microsoft によって削除されたときに、マイクロソフトが2010年1月より前にマイクロソフトによってライセンスされた Microsoft Word 製品米国の特典と使用についてのみ提供されます。 Microsoft Word に関するこの情報は、マイクロソフトが2010年1月10日以降にライセンスを取得した microsoft Word 製品を使用しているか、microsoft Word 製品で実行されているプログラムを開発している個人または米国組織によって読み取られたり使用されたりすることはできません。これらの製品は、その日より前にライセンスされている製品と同じように動作しないか、米国の外部で使用するために購入およびライセンス供与されます。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Microsoft Office Excel と Microsoft Office Word には、スキーマをドキュメントにマップする機能が用意されています。 この機能を使用すると、ドキュメントへの XML データのインポートとエクスポートを簡単に行うことができます。

 Visual Studio は、ドキュメントレベルのカスタマイズで、マップされたスキーマ要素をプログラミングモデルのコントロールとして公開します。 Excel の場合、Visual Studio では、データベース、Web サービス、およびオブジェクトのデータにコントロールをバインドするためのサポートが追加されています。 Word および Excel の場合、Visual Studio では、操作ウィンドウのサポートが追加されます。これをスキーママップドキュメントと共に使用して、ソリューションのエンドユーザーエクスペリエンスを向上させることができます。 詳細については、「 [操作ウィンドウの概要](../vsto/actions-pane-overview.md)」を参照してください。

> [!NOTE]
> Excel ソリューションでは、マルチパート XML スキーマを使用できません。

## <a name="objects-created-when-schemas-are-attached-to-excel-workbooks"></a>スキーマが Excel ブックにアタッチされるときに作成されるオブジェクト
 ブックにスキーマをアタッチすると、Visual Studio によって複数のオブジェクトが自動的に作成され、プロジェクトに追加されます。 これらのオブジェクトは Excel で管理されているため、Visual Studio tools を使用して削除しないでください。 これらを削除するには、マップされた要素をワークシートから削除するか、Excel ツールを使用してスキーマをデタッチします。

 主に次の2つのオブジェクトがあります。

- XML スキーマ (XSD ファイル)。 ブック内のすべてのスキーマに対して、Visual Studio によってスキーマがプロジェクトに追加されます。 これは、 **ソリューションエクスプローラー** に XSD 拡張子を持つプロジェクト項目として表示されます。

- 型指定された <xref:System.Data.DataSet> クラス。 このクラスは、スキーマに基づいて作成されます。 このデータセットクラスは **クラスビュー** に表示されます。

## <a name="objects-created-when-schema-elements-are-mapped-to-excel-worksheets"></a>スキーマ要素が Excel ワークシートにマップされるときに作成されるオブジェクト
 **XML ソース** の作業ウィンドウからワークシートにスキーマ要素をマップすると、Visual Studio によって複数のオブジェクトが自動的に作成され、プロジェクトに追加されます。

- コントロール ブック内のマップされたオブジェクトごとに、 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> コントロール (非繰り返しスキーマ要素用) または <xref:Microsoft.Office.Tools.Excel.ListObject> コントロール (スキーマ要素の繰り返し用) がプログラミングモデルで作成されます。 コントロールを削除できるのは、 <xref:Microsoft.Office.Tools.Excel.ListObject> マッピングとマップされたオブジェクトをブックから削除した場合だけです。 コントロールの詳細については、「 [ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)」を参照してください。

- BindingSource. <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>非繰り返しスキーマ要素をワークシートにマップすることによってを作成すると、が作成され、 <xref:System.Windows.Forms.BindingSource> <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> コントロールがにバインドされ <xref:System.Windows.Forms.BindingSource> ます。 を、 <xref:System.Windows.Forms.BindingSource> 作成した型指定されたクラスのインスタンスなど、ドキュメントにマップされているスキーマに一致するデータソースのインスタンスにバインドする必要があり <xref:System.Data.DataSet> ます。 <xref:System.Windows.Forms.BindingSource.DataSource%2A>[ <xref:System.Windows.Forms.BindingSource.DataMember%2A> **プロパティ**] ウィンドウに表示されるプロパティとプロパティを設定して、バインドを作成します。

    > [!NOTE]
    > <xref:System.Windows.Forms.BindingSource>がオブジェクトに対して作成されていません <xref:Microsoft.Office.Tools.Excel.ListObject> 。 をデータソースに手動でバインドするには、[ <xref:Microsoft.Office.Tools.Excel.ListObject> <xref:System.Windows.Forms.BindingSource.DataSource%2A> <xref:System.Windows.Forms.BindingSource.DataMember%2A> **プロパティ** ] ウィンドウでプロパティとプロパティを設定します。

### <a name="office-mapped-schemas-and-the-visual-studio-data-sources-window"></a>Office マップスキーマと Visual Studio の [データソース] ウィンドウ
 Office のマップされたスキーマ機能と Visual Studio の [ **データソース** ] ウィンドウを使用すると、レポートや編集のために Excel ワークシートにデータを表示できます。 どちらの場合も、データ要素を Excel ワークシートにドラッグできます。 どちらのメソッドも、を通じて、や web サービスなどのデータソースにデータをバインドするコントロールを作成 <xref:System.Windows.Forms.BindingSource> <xref:System.Data.DataSet> します。

> [!NOTE]
> 繰り返しスキーマ要素をワークシートにマップすると、Visual Studio によってが作成さ <xref:Microsoft.Office.Tools.Excel.ListObject> れます。 は <xref:Microsoft.Office.Tools.Excel.ListObject> 、を介してデータに自動的にバインドされません <xref:System.Windows.Forms.BindingSource> 。 をデータソースに手動でバインドするには、[ <xref:Microsoft.Office.Tools.Excel.ListObject> <xref:System.Windows.Forms.BindingSource.DataSource%2A> <xref:System.Windows.Forms.BindingSource.DataMember%2A> **プロパティ** ] ウィンドウでプロパティとプロパティを設定します。

 次の表は、2つのメソッドの相違点の一部を示しています。

|XML スキーマ|[データ ソース] ウィンドウ|
|----------------|-------------------------|
|Office インターフェイスを使用します。|Visual Studio の [ **データソース** ] ウィンドウを使用します。|
|XML ファイルからデータをインポートおよびエクスポートするための組み込みの Office 機能を有効にします。|インポートとエクスポートの機能をプログラムで提供する必要があります。|
|生成されたコントロールにデータを格納するコードを記述する必要があります。|[ **データソース** ] ウィンドウから追加されたコントロールには、データベースサーバーを使用するときに必要な接続文字列を格納するためのコードが自動的に生成されます。|

## <a name="behavior-when-schemas-are-attached-to-word-documents"></a>Word 文書にスキーマが添付されている場合の動作
 ドキュメントレベルの Office プロジェクトで使用されている Word 文書にスキーマをアタッチした場合、データオブジェクトは作成されません。 ただし、スキーマ要素をドキュメントにマップすると、コントロールが作成されます。 コントロールの種類は、マップする要素の種類によって異なります。繰り返し要素 <xref:Microsoft.Office.Tools.Word.XMLNodes> によってコントロールが生成され、非繰り返し要素によってコントロールが生成さ <xref:Microsoft.Office.Tools.Word.XMLNode> れます。 詳細については、「 [XMLNodes コントロール](../vsto/xmlnodes-control.md) と [XMLNode コントロール](../vsto/xmlnode-control.md)」を参照してください。

## <a name="deployment-of-solutions-that-include-xml-schemas"></a>XML スキーマを含むソリューションの配置
 ドキュメントにマップされている XML スキーマを使用するソリューションを配置するには、インストーラーを作成する必要があります。 インストーラーは、ユーザーのコンピューターのスキーマライブラリにスキーマを登録する必要があります。 スキーマを登録していない場合でも、ユーザーがドキュメントを開いたときにドキュメント内の要素に基づいて一時スキーマが生成されるため、ソリューションは機能します。 ただし、ユーザーは、プロジェクトの作成に使用されたスキーマを検証または保存することはできません。 インストーラーの詳細については、「 [アプリケーション、サービス、およびコンポーネントの展開](../deployment/deploying-applications-services-and-components.md)」を参照してください。

 また、プロジェクトにコードを追加して、スキーマがライブラリ内にあり、登録されているかどうかを確認することもできます。 そうでない場合は、ユーザーに警告することができます。

 [!code-vb[Trin_VstcoreDataWord#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataWordVB/ThisDocument.vb#1)]
 [!code-csharp[Trin_VstcoreDataWord#1](../vsto/codesnippet/CSharp/Trin_VstcoreDataWordCS/ThisDocument.cs#1)]

## <a name="see-also"></a>関連項目

- [方法: Visual Studio 内で Word 文書にスキーマを割り当てる](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [方法: Visual Studio 内のワークシートにスキーマをマップする](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)

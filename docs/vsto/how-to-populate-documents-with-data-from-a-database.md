---
title: '方法: データベースのデータをドキュメントに読み込む'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents, populating with data
- data, adding to documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8470ec4acf686c016088c5f474539a1ab7ed85df
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547200"
---
# <a name="how-to-populate-documents-with-data-from-a-database"></a>方法: データベースのデータをドキュメントに読み込む

Microsoft Office のドキュメント レベルのプロジェクトでは、Windows フォーム プロジェクトでデータにアクセスする場合と同じようにデータにアクセスできます。 同じツールとコードを使用してデータベースからソリューションにデータを読み込むことができ、Windows フォーム コントロールを使用してデータを表示できます。

また、ホスト コントロールを使用してデータを表示することもできます。 ホスト コントロールは、イベントおよびデータ バインディングの機能が強化された Microsoft Office Word のネイティブ オブジェクトです。 詳細については、「[ホスト項目とホストコントロールの概要](../vsto/host-items-and-host-controls-overview.md)」を参照してください。

[!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

次の例は、デザイナーを使用してドキュメント レベルのプロジェクトにデータ バインド コントロールを追加する方法を示しています。 実行時に VSTO アドインプロジェクトのデータバインドコントロールを追加する方法の例については、「[チュートリアル: Vsto アドインプロジェクトでの単純データバインディング](../vsto/walkthrough-simple-data-binding-in-vsto-add-in-project.md)」を参照してください。

![ビデオへのリンク](../vsto/media/playvideo.gif "ビデオへのリンク")関連するビデオデモについては、「 [Office システムの Visual Studio Tools を使用して Word 2007 コンテンツコントロールにデータをバインドする (3.0)](/previous-versions/office/developer/office-2007/bb967663(v=office.12))」を参照してください。

## <a name="add-a-control-to-a-document-at-design-time"></a>デザイン時にドキュメントにコントロールを追加する

### <a name="to-populate-a-document-with-data-from-a-database"></a>データベースからドキュメントにデータを読み込むには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で Word のドキュメント レベルのプロジェクトを開き、ドキュメントをデザイナーで開きます。

2. [**データソース**] ウィンドウを開き、データベースからデータソースを作成します。 詳細については、「[新しい接続の追加](../data-tools/add-new-connections.md)」を参照してください。

3. [**データソース**] ウィンドウから目的のフィールドをドキュメントにドラッグします。

コンテンツ コントロールが文書に追加されます。 コンテンツ コントロールの種類は、選択したフィールドのデータ型によって異なります。 詳細については、「[コンテンツコントロール](../vsto/content-controls.md)」を参照してください。

[**データソース**] ウィンドウで [データ] フィールドを選択し、ドロップダウンリストから別のコントロールを選択して、別のコントロールを追加できます。

## <a name="objects-in-the-project"></a>プロジェクト内のオブジェクト

プロジェクトには、コントロールに加えて、データに関連する以下のオブジェクトも自動的に追加されます。

- データベース内の接続したデータ テーブルをカプセル化する型指定されたデータセット。 詳細については、「 [Visual Studio のデータセットツール](../data-tools/dataset-tools-in-visual-studio.md)」を参照してください。

- コントロールを型指定されたデータセットに接続する <xref:System.Windows.Forms.BindingSource>。 詳細については、「 [BindingSource コンポーネントの概要](/dotnet/framework/winforms/controls/bindingsource-component-overview)」を参照してください。

- 型指定されたデータセットをデータベースに接続する TableAdapter。 詳細については、「 [tableadapter の作成と構成](../data-tools/create-and-configure-tableadapters.md)」を参照してください。

- TableAdapterManager。階層更新を有効にするために、データセット内のテーブルアダプターを調整するために使用されます。 詳細については、「[階層更新](../data-tools/hierarchical-update.md)と[TableAdapterManager リファレンス](../data-tools/fill-datasets-by-using-tableadapters.md#tableadaptermanager-reference)」を参照してください。

プロジェクトを実行すると、データ ソースの先頭のレコードがコントロールに表示されます。 <xref:System.Windows.Forms.BindingSource> を使用すると、ユーザーがレコードをスクロールできるようになります。

### <a name="to-scroll-through-the-records"></a>レコードをスクロールするには

- <xref:System.Windows.Forms.BindingSource.MoveNext%2A> や <xref:System.Windows.Forms.BindingSource.MovePrevious%2A> など、<xref:System.Windows.Forms.BindingSource> のメソッドを使用します。

型指定されたデータセットおよびデータベースに更新を送信する方法については、「[方法: ホストコントロールからのデータを使用してデータソースを更新](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)する」を参照してください。

## <a name="see-also"></a>関連項目

- [Office ソリューションのコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [新しいデータ ソースの追加](../data-tools/add-new-data-sources.md)
- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [方法: オブジェクトのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-objects.md)
- [方法: ホストコントロールのデータを使用してデータソースを更新する](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
- [Office ソリューションのローカルデータベースファイルの使用の概要](../vsto/using-local-database-files-in-office-solutions-overview.md)
- [BindingSource コンポーネントの概要](/dotnet/framework/winforms/controls/bindingsource-component-overview)
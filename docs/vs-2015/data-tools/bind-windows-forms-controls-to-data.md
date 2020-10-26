---
title: コントロールをデータにバインド Windows フォーム |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- displaying data, Windows Forms controls
- Windows Forms, displaying data
- data sources, displaying
- data [Windows Forms], displaying
ms.assetid: 0163a34a-38cb-40b9-8f38-3058a90caf21
caps.latest.revision: 31
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3cf93d96594b65b06670567e8c23cd83ccb7f1ab
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672971"
---
# <a name="bind-windows-forms-controls-to-data"></a>Windows フォーム コントロールをデータにバインドする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[ **データソース** ] ウィンドウから Windows フォームまたはフォーム上の既存のコントロールにオブジェクトをドラッグすることにより、データソースをコントロールにバインドできます。 項目をドラッグする前に、バインド先のコントロールの種類を設定できます。 テーブル自体を選択するか、個々の列を選択するかによって、異なる値が表示されます。  また、カスタム値を設定することもできます。 テーブルの場合、"詳細" とは、各列が個別のコントロールにバインドされていることを意味します。

 ![データソースを DataGridView にバインド](../data-tools/media/raddata-bind-data-source-to-datagridview.png "データソースを DataGridView に連結するためのレーダーデータバインド")

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

## <a name="bind-to--data-in-a-datagridview-control"></a>DataGridView コントロールのデータにバインドする
 DataGridView の場合、テーブル全体がその1つのコントロールにバインドされます。 DataGridView をフォームにドラッグすると、レコード間を移動するためのツールストリップ ( <xref:System.Windows.Forms.BindingNavigator> ) も表示されます。 [データセット](../data-tools/dataset-tools-in-visual-studio.md)、TableAdapter、 <xref:System.Windows.Forms.BindingSource> 、およびが <xref:System.Windows.Forms.BindingNavigator> コンポーネントトレイに表示されます。 次の図では、Customers テーブルが Orders テーブルに関連付けられているので、TableAdapterManager も追加されています。 これらの変数はすべて、自動的に生成されるコードでは、フォームクラスのプライベートメンバーとして宣言されます。 DataGridView を埋めるための自動生成されたコードは、form_load イベントハンドラーにあります。 データベースを更新するためにデータを保存するコードは、BindingNavigator の Save イベントハンドラーにあります。 必要に応じて、このコードを移動または変更できます。

 ![BindingNavigator を使用した GridView](../data-tools/media/raddata-gridview-with-bindingnavigator.png "BindingNavigator を使用したレーダーデータ GridView")

 各の右上隅にあるスマートタグをクリックすると、DataGridView と BindingNavigator の動作をカスタマイズできます。

 ![DataGridView とバインドのナビゲーターのスマートタグ](../data-tools/media/raddata-datagridview-and-binding-navigator-smart-tags.png "レーダーデータ DataGridView とバインドナビゲーターのスマートタグ")

 アプリケーションが必要とするコントロールが [ **データソース** ] ウィンドウ内から使用できない場合は、コントロールを追加できます。 詳細については、「 [[データソース] ウィンドウにカスタムコントロールを追加する](../data-tools/add-custom-controls-to-the-data-sources-window.md)」を参照してください。

 [ **データソース** ] ウィンドウからフォーム上の既存のコントロールに項目をドラッグして、コントロールをデータにバインドすることもできます。 既にデータにバインドされているコントロールのデータバインディングは、最後にドラッグした項目にリセットされます。 有効なドロップターゲットにするには、コントロールが [ **データソース** ] ウィンドウからドラッグした項目の基になるデータ型を表示できる必要があります。 たとえば、データ型がのアイテムをにドラッグすることはできません <xref:System.DateTime> <xref:System.Windows.Forms.CheckBox> 。これは、 <xref:System.Windows.Forms.CheckBox> が日付を表示できないためです。

## <a name="bind-to--data-in-individual-controls"></a>個々のコントロールのデータにバインドする
 データソースを "詳細" にバインドすると、データセット内の各列が別のコントロールにバインドされます。

 ![データソースを詳細にバインドする](../data-tools/media/raddata-bind-data-source-to-details.png "レーダーデータバインドのデータソースの詳細")

> [!IMPORTANT]
> 前の図では、Orders テーブルからではなく、Customers テーブルの Orders プロパティからドラッグすることに注意してください。 Customer. Orders プロパティにバインドすると、DataGridView で行われたナビゲーションコマンドが、詳細コントロールにすぐに反映されます。 Orders テーブルからドラッグした場合でも、コントロールはデータセットにバインドされますが、DataGridView と同期されることはありません。

 次の図は、Customers テーブルの Orders プロパティが [ **データソース** ] ウィンドウの [詳細] にバインドされた後にフォームに追加される既定のデータバインドコントロールを示しています。

 ![Orders テーブルが詳細にバインドされました](../data-tools/media/raddata-orders-table-bound-to-details.png "詳細にバインドされている "レーダーデータの Orders" テーブル")

 各コントロールにはスマートタグがあることにも注意してください。 このタグは、そのコントロールにのみ適用されるカスタマイズを有効にします。

## <a name="see-also"></a>参照
 [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)

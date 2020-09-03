---
title: Windows フォーム コントロールをデータにバインドする
ms.date: 11/03/2017
ms.topic: how-to
helpviewer_keywords:
- data [Windows Forms], data sources
- Windows Forms, data binding
- Windows Forms, displaying data
- displaying data on forms
- forms, displaying data
- data sources, displaying data
- displaying data, Windows Forms
- data [Windows Forms], displaying
ms.assetid: 243338ef-41af-4cc5-aff7-1e830236f0ec
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: b6a1d240c865ecc6abddd399c94122a757ee0983
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85283009"
---
# <a name="bind-windows-forms-controls-to-data-in-visual-studio"></a>Visual Studio でのデータへの Windows フォーム コントロールのバインド

データを Windows フォームにバインドすることで、アプリケーションのユーザーに対してデータを表示できます。 これらのデータバインドコントロールを作成するには、[ **データソース** ] ウィンドウから Visual Studio の Windows フォームデザイナーに項目をドラッグします。

![データソースのドラッグ操作](../data-tools/media/raddata-data-source-drag-operation.png)

> [!TIP]
> [**データソース**] ウィンドウが表示されていない場合は、 **View**[  >  **他の Windows**データソースを表示する] を選択する  >  **Data Sources**か、 **Shift** + **Alt** + **D**キーを押して開くことができます。 [ **データソース** ] ウィンドウを表示するには、Visual Studio でプロジェクトを開いておく必要があります。

項目をドラッグする前に、バインド先のコントロールの種類を設定できます。 テーブル自体を選択するか、個々の列を選択するかによって、異なる値が表示されます。  また、カスタム値を設定することもできます。 テーブルの場合、 **Details** は各列が個別のコントロールにバインドされていることを意味します。

![データソースを DataGridView にバインド](../data-tools/media/raddata-bind-data-source-to-datagridview.png)

## <a name="bindingsource-and-bindingnavigator-controls"></a>BindingSource コントロールと BindingNavigator コントロール

<xref:System.Windows.Forms.BindingSource> コンポーネントは 2 つの目的で利用できます。 まず、コントロールをデータにバインドするときに抽象レイヤーを提供します。 フォーム上のコントロールは、データソースに直接ではなく、コンポーネントにバインドされ <xref:System.Windows.Forms.BindingSource> ます。 また、オブジェクトのコレクションを管理できます。 <xref:System.Windows.Forms.BindingSource> に型を追加すると、その型の一覧が作成されます。

<xref:System.Windows.Forms.BindingSource> コンポーネントの詳細については、次のトピックを参照してください。

- [BindingSource コンポーネント](/dotnet/framework/winforms/controls/bindingsource-component)

- [BindingSource コンポーネントの概要](/dotnet/framework/winforms/controls/bindingsource-component-overview)

- [BindingSource コンポーネントのアーキテクチャ](/dotnet/framework/winforms/controls/bindingsource-component-architecture)

[BindingNavigator コントロール](/dotnet/framework/winforms/controls/bindingnavigator-control-windows-forms)は、Windows アプリケーションによって表示されるデータ間を移動するためのユーザーインターフェイスを提供します。

## <a name="bind-to-data-in-a-datagridview-control"></a>DataGridView コントロールのデータにバインドする

[DataGridView コントロール](/dotnet/framework/winforms/controls/datagridview-control-overview-windows-forms)の場合、テーブル全体がその1つのコントロールにバインドされます。 **DataGridView**をフォームにドラッグすると、レコード間を移動するためのツールストリップ ( <xref:System.Windows.Forms.BindingNavigator> ) も表示されます。 [DataSet](../data-tools/dataset-tools-in-visual-studio.md)、[TableAdapter](../data-tools/create-and-configure-tableadapters.md)、<xref:System.Windows.Forms.BindingSource>、<xref:System.Windows.Forms.BindingNavigator> がコンポーネント トレイに表示されます。 次の図では、Customers テーブルが Orders テーブルに関連付けられているので、 [TableAdapterManager](https://msdn.microsoft.com/library/bb384426.aspx) も追加されています。 これらの変数はすべて、自動的に生成されるコードでは、フォームクラスのプライベートメンバーとして宣言されます。 **DataGridView**を埋めるための自動生成されたコードは、 `Form_Load` イベントハンドラーにあります。 データベースを更新するためにデータを保存するコードは、 `Save` **BindingNavigator**のイベントハンドラーにあります。 必要に応じて、このコードを移動または変更できます。

![BindingNavigator を使用した GridView](../data-tools/media/raddata-gridview-with-bindingnavigator.png)

各の右上隅にあるスマートタグをクリックすると、 **DataGridView** と **BindingNavigator** の動作をカスタマイズできます。

![DataGridView とバインドのナビゲーターのスマートタグ](../data-tools/media/raddata-datagridview-and-binding-navigator-smart-tags.png)

アプリケーションが必要とするコントロールが [ **データソース** ] ウィンドウ内から使用できない場合は、コントロールを追加できます。 詳細については、「 [[データソース] ウィンドウにカスタムコントロールを追加する](../data-tools/add-custom-controls-to-the-data-sources-window.md)」を参照してください。

[ **データソース** ] ウィンドウからフォーム上の既存のコントロールに項目をドラッグして、コントロールをデータにバインドすることもできます。 既にデータにバインドされているコントロールのデータバインディングは、最後にドラッグした項目にリセットされます。 有効なドロップターゲットにするには、コントロールが [ **データソース** ] ウィンドウからドラッグした項目の基になるデータ型を表示できる必要があります。 たとえば、データ型がのアイテムをにドラッグすることはできません <xref:System.DateTime> <xref:System.Windows.Forms.CheckBox> 。これは、 <xref:System.Windows.Forms.CheckBox> が日付を表示できないためです。

## <a name="bind-to-data-in-individual-controls"></a>個々のコントロールのデータにバインドする

データソースを **詳細**にバインドすると、データセット内の各列が別のコントロールにバインドされます。

![データソースを詳細にバインドする](../data-tools/media/raddata-bind-data-source-to-details.png)

> [!IMPORTANT]
> 前の図では、Orders テーブルからではなく、Customers テーブルの Orders プロパティからドラッグすることに注意してください。 プロパティにバインドすると `Customer.Orders` 、 **DataGridView** で行われたナビゲーションコマンドが、詳細コントロールにすぐに反映されます。 Orders テーブルからドラッグした場合でも、コントロールはデータセットにバインドされますが、 **DataGridView**と同期されることはありません。

次の図は、Customers テーブルの Orders プロパティが [**データソース**] ウィンドウの**詳細**にバインドされた後にフォームに追加される既定のデータバインドコントロールを示しています。

![Orders テーブルが詳細にバインドされました](../data-tools/media/raddata-orders-table-bound-to-details.png)

各コントロールにはスマートタグがあることにも注意してください。 このタグは、そのコントロールにのみ適用されるカスタマイズを有効にします。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [Windows フォームでのデータバインディング (.NET Framework)](/dotnet/framework/winforms/windows-forms-data-binding)

---
title: Windows フォーム アプリケーションでルックアップ テーブルを作成する
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- lookup tables
- lookup tables, creating
ms.assetid: 0edd5385-c381-4b17-9096-74e2778db9d5
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 9fe49ee90dba3edd0e2777817c4903c6101a1b47
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586771"
---
# <a name="create-lookup-tables-in-windows-forms-applications"></a>Windows フォーム アプリケーションでルックアップ テーブルを作成する

*ルックアップ テーブル*という用語は、関連する 2 つのデータ テーブルにバインドされているコントロールを表します。 この検索コントロールは、2 番目のテーブルで選択されている値に基づいて最初のテーブルからデータを表示します。

参照テーブルを作成するには、([[データソース] ウィンドウ](add-new-data-sources.md#data-sources-window)から) 親テーブルのメインノードを、関連付けられている子テーブルの列に既にバインドされているフォーム上のコントロールにドラッグします。

たとえば、販売データベースの `Orders` テーブルであれば、次のように使用されます。 `Orders` テーブルの各レコードには、注文した顧客を表す `CustomerID` が含まれます。 `CustomerID` は、`Customers` テーブルの顧客レコードを指す外部キーです。 このシナリオでは、 **[データソース]** ウィンドウで `Orders` テーブルを展開し、メインノードを **[詳細]** に設定します。 次に、<xref:System.Windows.Forms.ComboBox> (または参照バインドをサポートするその他のコントロール) を使用するように `CustomerID` 列を設定し、[`Orders`] ノードをフォームにドラッグします。 最後に、[`Customers`] ノードを、関連する列にバインドされているコントロール (この場合は、<xref:System.Windows.Forms.ComboBox> `CustomerID` 列にバインドされている) にドラッグします。

## <a name="to-databind-a-lookup-control"></a>検索コントロールをデータバインドするには

1. プロジェクトを開いた状態で、**データソース** ウィンドウを開きます。そのために**は > ** **他の Windows** > **データソース** をクリックします。

    > [!NOTE]
    > 検索テーブルを作成するには、関連付けられた 2 つのテーブルまたはオブジェクトが **[データ ソース]** ウィンドウで使用可能になっている必要があります。 詳細については、「[データセット内のリレーションシップ](relationships-in-datasets.md)」を参照してください。

2. **[データ ソース]** ウィンドウで、親テーブルとそのすべての列および関連する子テーブルとそのすべて列が表示されるまでノードを展開します。

    > [!NOTE]
    > 子テーブルのノードは、展開可能な子ノードとして親テーブルに表示されます。

3. 子テーブルのノードのコントロール一覧の **[詳細]** を選択し、子テーブルのドロップ タイプを **[詳細]** に変更します。 詳細については、「[[データソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)」を参照してください。

4. 2つのテーブル (前の例では `CustomerID` ノード) を関連付けるノードを見つけます。 コントロールリストから**ComboBox**を選択して、ドロップタイプを <xref:System.Windows.Forms.ComboBox> に変更します。

5. メインの子テーブルのノードを **[データ ソース]** ウィンドウからフォームにドラッグします。

     説明のラベルが付いたデータ バインド コントロールとツール ストリップ (<xref:System.Windows.Forms.BindingNavigator>) がフォームに表示されます。 [DataSet](../data-tools/dataset-tools-in-visual-studio.md)、[TableAdapter](../data-tools/create-and-configure-tableadapters.md)、<xref:System.Windows.Forms.BindingSource>、<xref:System.Windows.Forms.BindingNavigator> がコンポーネント トレイに表示されます。

6. 次に、 **[データ ソース]** ウィンドウからメインの親テーブルのノードを検索コントロール (<xref:System.Windows.Forms.ComboBox>) に直接ドラッグします。

     これで検索バインドが確立されます。 コントロールに設定されている特定のプロパティについては、次の表を参照してください。

    |property|設定の説明|
    |--------------| - |
    |**DataSource**|Visual Studio は、このプロパティをコントロールにドラッグしたテーブルに対して作成された <xref:System.Windows.Forms.BindingSource> に設定します (コントロールの作成時に作成された <xref:System.Windows.Forms.BindingSource> とは異なります)。<br /><br /> 調整が必要な場合は、これを、表示する列を含むテーブルの <xref:System.Windows.Forms.BindingSource> に設定します。|
    |**DisplayMember**|Visual Studio は、このプロパティをコントロールにドラッグするテーブルの主キーの後で、文字列データ型を含む最初の列に設定します。<br /><br /> 調整が必要な場合は、これを表示する列の名前に設定します。|
    |**ValueMember**|Visual Studio は、このプロパティを主キーに参加している最初の列、またはキーが定義されていない場合は、テーブルの最初の列に設定します。<br /><br /> 調整が必要な場合は、この値を、表示する列を含むテーブルの主キーに設定します。|
    |**SelectedValue**|Visual Studio は、このプロパティを **[データ ソース]** ウィンドウからドロップした元の列に設定します。<br /><br /> 調整を行う必要がある場合は、これを関連テーブルの外部キー列に設定します。|

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)

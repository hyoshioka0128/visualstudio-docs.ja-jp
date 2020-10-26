---
title: Windows フォームアプリケーションでルックアップテーブルを作成する |Microsoft Docs
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
- lookup tables
- lookup tables, creating
ms.assetid: 0edd5385-c381-4b17-9096-74e2778db9d5
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3979d08757445e9df5fc159fe7642b04bf74b995
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72630935"
---
# <a name="create-lookup-tables-in-windows-forms-applications"></a>Windows フォーム アプリケーションでルックアップ テーブルを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

*ルックアップ テーブル*という用語は、関連する 2 つのデータ テーブルにバインドされているコントロールを表します。 この検索コントロールは、2 番目のテーブルで選択されている値に基づいて最初のテーブルからデータを表示します。

 参照テーブルを作成するには、([ [データソース] ウィンドウ](https://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)から) 親テーブルのメインノードを、関連付けられている子テーブルの列に既にバインドされているフォーム上のコントロールにドラッグします。

 たとえば、販売データベースの `Orders` テーブルであれば、次のように使用されます。 `Orders` テーブルの各レコードには、注文した顧客を表す `CustomerID` が含まれます。 `CustomerID` は、`Customers` テーブルの顧客レコードを指す外部キーです。 このシナリオでは、[ `Orders` **データソース** ] ウィンドウでテーブルを展開し、メインノードを [ **詳細**] に設定します。 次に、 `CustomerID` <xref:System.Windows.Forms.ComboBox> (または参照バインドをサポートするその他のコントロール) を使用するように列を設定し、ノードをフォームにドラッグし `Orders` ます。 最後に、 `Customers` 関連する列にバインドされているコントロール (この場合は列にバインドされている) にノードをドラッグし <xref:System.Windows.Forms.ComboBox> `CustomerID` ます。

## <a name="to-databind-a-lookup-control"></a>検索コントロールをデータバインドするには

1. **[データ ソース]** ウィンドウを開く。

    > [!NOTE]
    > 検索テーブルを作成するには、関連付けられた 2 つのテーブルまたはオブジェクトが **[データ ソース]** ウィンドウで使用可能になっている必要があります。

2. **[データ ソース]** ウィンドウで、親テーブルとそのすべての列および関連する子テーブルとそのすべて列が表示されるまでノードを展開します。

    > [!NOTE]
    > 子テーブルのノードは、展開可能な子ノードとして親テーブルに表示されます。

3. 子テーブルのノードのコントロール一覧の **[詳細]** を選択し、子テーブルのドロップ タイプを **[詳細]** に変更します。 詳細については、「[ [データソース] ウィンドウからドラッグしたときに作成されるコントロールを設定する](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)」を参照してください。

4. 2つのテーブルを関連付けるノード (前の `CustomerID` 例ではノード) を見つけます。 <xref:System.Windows.Forms.ComboBox> コントロールリストから **ComboBox** を選択して、ドロップタイプをに変更します。

5. メインの子テーブルのノードを **[データ ソース]** ウィンドウからフォームにドラッグします。

     説明のラベルが付いたデータ バインド コントロールとツール ストリップ (<xref:System.Windows.Forms.BindingNavigator>) がフォームに表示されます。 [データセット](../data-tools/dataset-tools-in-visual-studio.md)、TableAdapter、 <xref:System.Windows.Forms.BindingSource> 、およびが <xref:System.Windows.Forms.BindingNavigator> コンポーネントトレイに表示されます。

6. 次に、メインの親テーブルノードを [ **データソース** ] ウィンドウから参照コントロール () に直接ドラッグし <xref:System.Windows.Forms.ComboBox> ます。

     これで検索バインドが確立されます。 コントロールに設定された個々のプロパティについては、次の表を参照してください。

    |プロパティ|設定の説明|
    |--------------|----------------------------|
    |**DataSource**|Visual Studio は、このプロパティをコントロールにドラッグしたテーブルに対して作成された <xref:System.Windows.Forms.BindingSource> に設定します (コントロールの作成時に作成された <xref:System.Windows.Forms.BindingSource> とは異なります)。<br /><br /> 調整する必要がある場合は、これを表示する列を含むテーブルの <xref:System.Windows.Forms.BindingSource> に設定します。|
    |**DisplayMember**|Visual Studio は、このプロパティをコントロールにドラッグするテーブルの主キーの後で、文字列データ型を含む最初の列に設定します。<br /><br /> 調整する必要がある場合は、これを表示する列の名前に設定します。|
    |**ValueMember**|Visual Studio は、このプロパティを主キーに参加している最初の列、またはキーが定義されていない場合は、テーブルの最初の列に設定します。<br /><br /> 調整する必要がある場合は、これを表示する列を含むテーブルの主キーに設定します。|
    |**SelectedValue**|Visual Studio は、このプロパティを **[データ ソース]** ウィンドウからドロップした元の列に設定します。<br /><br /> 調整する必要がある場合は、これを関連付けられたテーブルの外部キー列に設定します。|

## <a name="see-also"></a>参照
 [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)

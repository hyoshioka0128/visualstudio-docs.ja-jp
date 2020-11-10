---
title: 階層更新
description: 参照整合性ルールを維持したまま、更新されたデータ (2 つ以上の関連テーブルを持つデータセットから) を DB に保存する階層更新を確認します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- saving data, changed data
- data [Visual Basic], hierarchical update
- saving updated data
- datasets [Visual Basic], hierarchical update
- hierarchical update
- saving data, hierarchical update
- modified data saving
- updated data saving
- related tables, saving
ms.assetid: 68bae3f6-ec9b-45ee-a33a-69395029f54c
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: bfc0c1ca96f5bf6ce58a1b7df9ad0ea10f283e1e
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94435157"
---
# <a name="hierarchical-update"></a>階層更新

*階層更新* とは、参照整合性ルールを維持したまま、更新されたデータ (2 つ以上の関連テーブルを含むデータセットから) をデータベースに保存するプロセスのことです。 *参照整合性* とは、関連レコードの挿入、更新、および削除の動作を制御する、データベース内の制約によって提供される整合性規則を指します。 たとえば、顧客レコードの作成を強制してから、その顧客の注文を作成できるようにする参照整合性です。  データセット内のリレーションシップの詳細については、「 [データセット内のリレーションシップ](../data-tools/relationships-in-datasets.md)」を参照してください。

階層更新機能では、を使用し `TableAdapterManager` て、 `TableAdapter` 型指定されたデータセットのを管理します。 `TableAdapterManager`コンポーネントは、.net 型ではなく、Visual Studio で生成されたクラスです。 [ **データソース** ] ウィンドウから Windows フォームまたは WPF ページにテーブルをドラッグすると、Visual Studio によって TableAdapterManager 型の変数がフォームまたはページに追加され、コンポーネントトレイのデザイナーに表示されます。 クラスの詳細については `TableAdapterManager` 、「 [tableadapter](../data-tools/create-and-configure-tableadapters.md)」の「TableAdapterManager Reference」セクションを参照してください。

既定では、データセットは関連テーブルを "リレーションのみ" として扱います。これは、外部キー制約が適用されないことを意味します。 この設定は、デザイン時に **データセットデザイナー** を使用して変更できます。 2つのテーブル間のリレーション線を選択して、[ **リレーションシップ** ] ダイアログボックスを表示します。 ここで行った変更によって、 `TableAdapterManager` 関連テーブルの変更をデータベースに送信するときのの動作が決まります。

## <a name="enable-hierarchical-update-in-a-dataset"></a>データセットの階層更新を有効にする

プロジェクトで追加または作成されたすべての新しいデータセットでは、階層更新が既定で有効になっています。 データセット内の型指定されたデータセットの " **階層更新** " プロパティを **True** または **False** に設定して、階層更新をオンまたはオフにします。

![階層更新の設定](../data-tools/media/hierarchical-update-setting.png)

## <a name="create-a-new-relation-between-tables"></a>テーブル間に新しいリレーションシップを作成する

2つのテーブル間の新しいリレーションシップを作成するには、データセットデザイナーで各テーブルのタイトルバーを選択し、右クリックして [ **リレーションシップの追加** ] を選択します。

![階層更新の [リレーションシップの追加] メニュー](../data-tools/media/hierarchical-update-add-relation-menu.png)

## <a name="understand-foreign-key-constraints-cascading-updates-and-deletes"></a>外部キー制約、連鎖更新、および削除について

生成されたデータセット コードで、データベースでの外部キー制約と連鎖動作がどのように作成されるかを理解することは重要です。

既定では、データセットのデータ テーブルは、データベースでのリレーションシップと一致するリレーションシップ (<xref:System.Data.DataRelation>) が設定された状態で生成されます。 ただし、データセットでのリレーションシップは、外部キー制約としては生成されません。 は、 <xref:System.Data.DataRelation> またはが有効になっていない **リレーション** としてのみ構成され <xref:System.Data.ForeignKeyConstraint.UpdateRule%2A> <xref:System.Data.ForeignKeyConstraint.DeleteRule%2A> ます。

連鎖更新と連鎖削除は、データベースのリレーションシップで連鎖更新や連鎖削除が有効になっている場合でも、既定で無効になっています。 たとえば、新しい顧客と新しい注文を作成し、データを保存しようとすると、データベースで定義されている外部キー制約との競合が発生する可能性があります。 詳細については、「 [データセットの読み込み中に制約をオフにする](turn-off-constraints-while-filling-a-dataset.md)」を参照してください。

## <a name="set-the-order-to-perform-updates"></a>更新を実行する順序を設定する

更新を実行する順序を設定すると、データセットのすべてのテーブルのすべての変更されたデータを保存するために必要な個々の挿入、更新、および削除の順序が設定されます。 階層更新が有効な場合、まず挿入が実行され、次に更新、削除の順で実行されます。 `TableAdapterManager` には、更新、挿入、削除の順に実行できる `UpdateOrder` プロパティも用意されています。

> [!NOTE]
> 更新順序がすべて含まれていることを理解しておくことが重要です。 つまり、更新を実行すると、データセット内のすべてのテーブルに対して、挿入と削除が実行されます。

プロパティを設定するには、[ `UpdateOrder` [データソース] ウィンドウ](add-new-data-sources.md#data-sources-window) からフォームに項目をドラッグした後、 `TableAdapterManager` コンポーネントトレイでを選択し、[ `UpdateOrder` **プロパティ** ] ウィンドウでプロパティを設定します。

## <a name="create-a-backup-copy-of-a-dataset-before-performing-a-hierarchical-update"></a>階層更新を実行する前にデータセットのバックアップコピーを作成する

データを保存すると (`TableAdapterManager.UpdateAll()` メソッドを呼び出すことにより)、`TableAdapterManager` は単一のトランザクションで各テーブルのデータの更新を試みます。 任意のテーブルの更新時に、なんらかが失敗した場合、トランザクション全体がロールバックされます。 ほとんどの場合、ロールバックによってアプリケーションが元の状態に戻ります。

ただし、バックアップ コピーからデータセットを復元することもできます。 この例の1つは、自動インクリメント値を使用している場合に発生する可能性があります。 たとえば、保存操作が失敗した場合、データセットの自動インクリメント値はリセットされず、データセットは自動インクリメント値を引き続き作成します。 これにより、アプリケーションで受け入れられない可能性のある、番号付けのギャップが残ります。 これが問題となる状況では、`TableAdapterManager` に備わっている `BackupDataSetBeforeUpdate` プロパティを使用して、トランザクションが失敗した場合に既存のデータセットをバックアップ コピーと置き換えることができます。

> [!NOTE]
> バックアップコピーは、メソッドの実行中にメモリ内にのみ存在し `TableAdapterManager.UpdateAll` ます。 このため、このバックアップデータセットにはプログラムでアクセスできません。これは、メソッドの実行が完了するとすぐに元のデータセットを置き換えるか、スコープ外になるためです `TableAdapterManager.UpdateAll` 。

## <a name="modify-the-generated-save-code-to-perform-the-hierarchical-update"></a>階層更新を実行するために生成された保存コードを変更する

データセットでの関連データ テーブルへの変更をデータベースに保存するには、`TableAdapterManager.UpdateAll` メソッドを呼び出し、関連テーブルが含まれるデータセットの名前を渡します。 たとえば、NorthwindDataset 内のすべてのテーブルの更新をバックエンドのデータベースに送信するには、`TableAdapterManager.UpdateAll(NorthwindDataset)` メソッドを実行します。

**[データ ソース]** ウィンドウから項目をドロップすると、各テーブルにデータを読み込むコード (`TableAdapter.Fill` メソッド) が `Form_Load` イベントに自動的に追加されます。 <xref:System.Windows.Forms.BindingNavigator> の **[保存]** ボタン クリック イベントにも、データセットのデータをデータベースに保存するコード (`TableAdapterManager.UpdateAll` メソッド) が追加されます。

生成された保存コードには、`CustomersBindingSource.EndEdit` メソッドを呼び出すコード行も含まれています。 具体的には、 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> <xref:System.Windows.Forms.BindingSource> フォームに追加されている最初ののメソッドを呼び出します。 言い換えると、このコードは [ **データソース** ] ウィンドウからフォームにドラッグされた最初のテーブルに対してのみ生成されます。 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 呼び出しは、現在編集中のデータ バインド コントロールで実行されている変更をコミットします。 したがって、あるデータ バインド コントロールにフォーカスがある状態で **[保存]** ボタンをクリックすると、実際の保存 (`TableAdapterManager.UpdateAll` メソッド) が実行される前に、そのコントロール内のすべての保留中の編集がコミットされます。

> [!NOTE]
> **データセットデザイナー** は、 `BindingSource.EndEdit` フォームにドロップされた最初のテーブルのコードのみを追加します。 したがって、フォーム上の各関連テーブルに対して、`BindingSource.EndEdit` メソッドを呼び出すコード行を手動で追加する必要があります。 つまり、このチュートリアルでも、`OrdersBindingSource.EndEdit` メソッドの呼び出しを追加する必要があります。

### <a name="to-update-the-code-to-commit-changes-to-the-related-tables-before-saving"></a>保存前に、関連テーブルへの変更をコミットするコードを更新するには

1. <xref:System.Windows.Forms.BindingNavigator> の **[保存]** ボタンをダブルクリックし、コード エディターで **Form1** を開きます。

2. `OrdersBindingSource.EndEdit` メソッドを呼び出す行の後に、`CustomersBindingSource.EndEdit` メソッドを呼び出すコード行を追加します。 **[保存]** ボタン クリック イベントのコードは、次のようになります。

     [!code-vb[VSProDataOrcasHierarchicalUpdate#1](../data-tools/codesnippet/VisualBasic/hierarchical-update_1.vb)]
     [!code-csharp[VSProDataOrcasHierarchicalUpdate#1](../data-tools/codesnippet/CSharp/hierarchical-update_1.cs)]

データベースにデータを保存する前に関連子テーブルに対する変更をコミットするだけでなく、新しい子レコードをデータセットに追加する前に、新しく作成された親レコードをコミットすることが必要な場合もあります。 つまり、 `Customer` 外部キー制約によって新しい子レコード ( `Orders` ) がデータセットに追加される前に、データセットに新しい親レコード () を追加することが必要になる場合があります。 この操作を行うには、子 `BindingSource.AddingNew` イベントを使用します。

> [!NOTE]
> 新しい親レコードをコミットする必要があるかどうかは、データソースへのバインドに使用されるコントロールの種類によって異なります。 このチュートリアルでは、個々のコントロールを使用して親テーブルにバインドします。 これには、新しい親レコードをコミットするための追加コードが必要です。 親レコードがのような複雑なバインドコントロールに代わりに表示されていた場合 <xref:System.Windows.Forms.DataGridView> 、 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 親レコードに対するこの追加の呼び出しは必要ありません。 これは、コントロールの基になるデータバインド機能によって、新しいレコードのコミットが行われるためです。

### <a name="to-add-code-to-commit-parent-records-in-the-dataset-before-adding-new-child-records"></a>データセットで新しい子レコードを追加する前に親レコードをコミットするコードを追加するには

1. `OrdersBindingSource.AddingNew` イベントのイベント ハンドラーを作成します。

    - デザインビューで **Form1** を開き、コンポーネントトレイで [ **OrdersBindingSource** ] を選択します。次に、[ **プロパティ** ] ウィンドウで [ **イベント** ] を選択し、[ **追加** ] イベントをダブルクリックします。

2. メソッドを呼び出すイベントハンドラーにコード行を追加 `CustomersBindingSource.EndEdit` します。 `OrdersBindingSource_AddingNew` イベント ハンドラー内のコードは、次のようになります。

     [!code-vb[VSProDataOrcasHierarchicalUpdate#2](../data-tools/codesnippet/VisualBasic/hierarchical-update_2.vb)]
     [!code-csharp[VSProDataOrcasHierarchicalUpdate#2](../data-tools/codesnippet/CSharp/hierarchical-update_2.cs)]

## <a name="tableadaptermanager-reference"></a>TableAdapterManager リファレンス

既定では、 `TableAdapterManager` 関連テーブルを含むデータセットを作成すると、クラスが生成されます。 クラスが生成されないようにするには、 `Hierarchical Update` データセットのプロパティの値を false に変更します。 Windows フォームまたは WPF ページのデザインサーフェイスにリレーションシップを持つテーブルをドラッグすると、Visual Studio はクラスのメンバー変数を宣言します。 データバインドを使用しない場合は、手動で変数を宣言する必要があります。

`TableAdapterManager`クラスは .net 型ではありません。 このため、ドキュメントでは確認できません。 これは、デザイン時にデータセット作成プロセスの一部として作成されます。

クラスのよく使用されるメソッドとプロパティを次に示し `TableAdapterManager` ます。

|メンバー|説明|
|------------|-----------------|
|`UpdateAll` メソッド|すべてのデータテーブルのすべてのデータを保存します。|
|`BackUpDataSetBeforeUpdate` プロパティ|メソッドを実行する前に、データセットのバックアップコピーを作成するかどうかを決定し `TableAdapterManager.UpdateAll` ます。演算.|
|*tableName* `TableAdapter` "|を表し `TableAdapter` ます。 生成されたには、 `TableAdapterManager` 各 it が管理するのプロパティが含まれてい `TableAdapter` ます。 たとえば、Customers テーブルと Orders テーブルを含むデータセットは、プロパティとプロパティを含むを使用して生成され `TableAdapterManager` `CustomersTableAdapter` `OrdersTableAdapter` ます。|
|`UpdateOrder` プロパティ|個々の insert、update、および delete コマンドの順序を制御します。 列挙体のいずれかの値に設定 `TableAdapterManager.UpdateOrderOption` します。<br /><br /> 既定では、 `UpdateOrder` は **Insertupdatedelete** に設定されています。 これは、データセット内のすべてのテーブルに対して、挿入、更新、および削除が実行されることを意味します。|

## <a name="see-also"></a>関連項目

- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)

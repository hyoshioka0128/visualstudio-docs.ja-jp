---
title: データセットの作成と構成
ms.date: 11/21/2018
ms.topic: how-to
helpviewer_keywords:
- typed datasets, creating
- datasets, creating
- datasets, configuring
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 1065c5efdcf73016e61ee0f016511579d41acd88
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282749"
---
# <a name="how-to-create-and-configure-datasets-in-visual-studio"></a>方法: Visual Studio でデータセットを作成および構成する

データセットは、メモリ内のデータベースのデータを格納するオブジェクトのセットであり、データベースに常に接続する必要がなく、そのデータに対する作成、読み取り、更新、および削除 (CRUD) 操作を可能にするための変更の追跡をサポートします。 データセットは、データビジネスアプリケーションに対して単純な*形式*を使用するように設計されています。 新しいアプリケーションの場合は、Entity Framework を使用して、メモリにデータを格納およびモデル化することを検討してください。 データセットを操作するには、データベースの概念に関する基本的な知識が必要です。

<xref:System.Data.DataSet>**データソース構成ウィザード**を使用して、デザイン時に Visual Studio で型指定されたクラスを作成できます。 プログラムによるデータセットの作成の詳細については、「[データセットの作成」 (ADO.NET)](/dotnet/framework/data/adonet/dataset-datatable-dataview/creating-a-dataset)を参照してください。

## <a name="create-a-new-dataset-by-using-the-data-source-configuration-wizard"></a>データソース構成ウィザードを使用して新しいデータセットを作成する

1. Visual Studio でプロジェクトを開き、[**プロジェクト**] [  >  **新しいデータソースの追加**] の順に選択して、**データソース構成ウィザード**を開始します。

2. 接続するデータソースの種類を選択します。

     ![データ ソース構成ウィザード](../data-tools/media/data-source-configuration-wizard.png)

3. データセットのデータソースとなるデータベースを選択します。

     ![データソース接続の選択](../data-tools/media/data-source-choose-a-connection.png)

4. データセットで表示するデータベースのテーブル (または個々の列)、ストアドプロシージャ、関数、およびビューを選択します。

     ![データベース オブジェクトの選択](../data-tools/media/raddata-chose-objects.png)

5. **[完了]** をクリックします。

   データセットは**ソリューションエクスプローラー**のノードとして表示されます。

   ![ソリューションエクスプローラー内のデータセット](../data-tools/media/dataset-in-solution-explorer.png)

6. データセット**デザイナー**でデータセットを開くには、**ソリューションエクスプローラー**の [データセット] ノードをクリックします。 データセット内の各テーブルには、オブジェクトが関連付けられてい `TableAdapter` ます。これは下部に表示されます。 テーブルアダプターは、データセットを設定し、必要に応じてデータベースにコマンドを送信するために使用されます。

   ![データセット デザイナー](../data-tools/media/dataset-designer.png)

7. テーブルを連結するリレーション線は、データベースで定義されているテーブルリレーションシップを表します。 既定では、データベース内の外部キー制約はリレーションとして表され、更新規則と削除規則は none に設定されます。 通常は、必要なものです。 ただし、行をクリックすると、[**リレーションシップ**] ダイアログボックスが表示され、階層更新の動作を変更できます。 詳細については、「データセットと[階層更新](../data-tools/hierarchical-update.md)[のリレーションシップ](../data-tools/relationships-in-datasets.md)」を参照してください。

     ![データセットの関係ダイアログ](../data-tools/media/raddata-relation-dialog.png)

8. テーブル内のテーブル、テーブルアダプター、または列名をクリックすると、そのプロパティが [**プロパティ**] ウィンドウに表示されます。 ここでは、一部の値を変更できます。 ソースデータベースではなく、データセットを変更するだけであることに注意してください。

     ![データセット列のプロパティ](../data-tools/media/dataset-column-properties.png)

9. 新しいテーブルまたはテーブルアダプターをデータセットに追加したり、既存のテーブルアダプターに新しいクエリを追加したり、[**ツールボックス**] タブから項目をドラッグしてテーブル間の新しいリレーションシップを指定したりすることができます。このタブは、**データセットデザイナー**にフォーカスがあるときに表示されます。

     ![データセットツールボックス](../data-tools/media/raddata-dataset-toolbox.png)

次に、データセットにデータを設定する方法を指定します。 そのためには、 **TableAdapter 構成ウィザード**を使用します。 詳細については、「 [tableadapter を使用したデータセットの読み込み](../data-tools/fill-datasets-by-using-tableadapters.md)」を参照してください。

## <a name="add-a-database-table-or-other-object-to-an-existing-dataset"></a>データベーステーブルまたはその他のオブジェクトを既存のデータセットに追加する

この手順では、最初にデータセットを作成するときに使用したものと同じデータベースからテーブルを追加する方法を示します。

1. **データセットデザイナー**でフォーカスを移動するには、**ソリューションエクスプローラー**の [データセット] ノードをクリックします。

2. Visual Studio の左側の余白の [**データソース**] タブをクリックするか、検索ボックスに「**データソース**」と入力します。

3. [データセット] ノードを右クリックし、[**ウィザードでデータソースを構成する**] を選択します。

     ![データソースのコンテキストメニュー](../data-tools/media/data-source-context-menu.png)

4. ウィザードを使用して、データセットに追加する追加のテーブル、ストアドプロシージャ、またはその他のデータベースオブジェクトを指定します。

## <a name="add-a-stand-alone-data-table-to-a-dataset"></a>データセットへのスタンドアロンデータテーブルの追加

1. **データセット デザイナー**でご自分のデータセットを開きます。

2. <xref:System.Data.DataTable>**ツールボックス**の [**データセット**] タブから**データセットデザイナー**にクラスをドラッグします。

3. 列を追加してデータ テーブルを定義します。 テーブルを右クリックし、[列の**追加**] を選択し  >  **Column**ます。 必要に応じて、[**プロパティ**] ウィンドウを使用して、列のデータ型とキーを設定します。

スタンドアロンテーブル `Fill` では、データを格納できるように、スタンドアロンテーブルにロジックを実装する必要があります。 スタンドアロンデータテーブルを入力する方法については、「 [DataAdapter からのデータセットの読み込み](/dotnet/framework/data/adonet/populating-a-dataset-from-a-dataadapter)」を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio のデータセットツール](../data-tools/dataset-tools-in-visual-studio.md)
- [データセットのリレーションシップ](../data-tools/relationships-in-datasets.md)
- [階層更新](../data-tools/hierarchical-update.md)
- [TableAdapters を使用してデータセットを入力する](../data-tools/fill-datasets-by-using-tableadapters.md)

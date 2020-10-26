---
title: データセットの作成と構成
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
- typed datasets, creating
- datasets [Visual Basic], creating
ms.assetid: 58f33b43-24e1-43b1-b08b-b74329960bd6
caps.latest.revision: 39
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3c84105387c708fa16e0b1d5c3294ef909466524
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72631206"
---
# <a name="create-and-configure-datasets-in-visual-studio"></a>Visual Studio でデータセットを作成および構成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

データ *セット* は、メモリ内のデータベースのデータを格納するオブジェクトのセットであり、データベースに常に接続する必要がなく、そのデータに対して作成、読み取り、更新、削除 (CRUD) 操作を可能にするための変更の追跡をサポートします。 データセットは、データビジネスアプリケーションに対して単純な *形式* を使用するように設計されています。 新しいアプリケーションの場合は、Entity Framework を使用して、メモリにデータを格納およびモデル化することを検討してください。 データセットを操作するには、データベースの概念に関する基本的な知識が必要です。

 <xref:System.Data.DataSet>**データソース構成ウィザード**を使用して、デザイン時に Visual Studio で型指定されたクラスを作成します。 プログラムによるデータセットの作成の詳細については、「 [データセットの作成](https://msdn.microsoft.com/library/57629d8f-393e-4677-8b83-29ffde27f5fc)」を参照してください。

## <a name="create-a-new-dataset-by-using-the-data-source-configuration-wizard"></a>データソース構成ウィザードを使用して新しいデータセットを作成する

1. [ **プロジェクト** ] メニューの [ **新しいデータソースの追加** ] をクリックして、 **データソース構成ウィザード**を開始します。

2. 接続するデータソースの種類を選択します。

     ![データ ソース構成ウィザード](../data-tools/media/data-source-configuration-wizard.png "データ ソース構成ウィザード")

3. [データベース] では、データセットのデータソースとなるデータベースを選択します。

     ![データソース接続の選択](../data-tools/media/data-source-choose-a-connection.png "データソース接続の選択")

4. データセットで表示するデータベースのテーブル (または個々の列)、ストアドプロシージャ、関数、およびビューを選択します。

     ![データベース オブジェクトの選択](../data-tools/media/raddata-chose-objects.png "レーダーデータ選択オブジェクト")

5. **[完了]** をクリックします。

6. データセットは **ソリューションエクスプローラー**のノードとして表示されます。

     ![ソリューションエクスプローラー内のデータセット](../data-tools/media/dataset-in-solution-explorer.png "ソリューションエクスプローラー内のデータセット")

     そのノードをクリックすると、データセットが **データセットデザイナー**に表示されます。 データセット内の各テーブルには、関連する TableAdapter オブジェクトがあることに注意してください。これは下部に表示されます。 テーブルアダプターは、データセットを設定し、必要に応じてデータベースにコマンドを送信するために使用されます。

     ![データセット デザイナー](../data-tools/media/dataset-designer.png "データセット デザイナー")

7. テーブルを連結するリレーション線は、データベースで定義されているテーブルリレーションシップを表します。 既定では、データベース内の外部キー制約はリレーションとして表され、更新規則と削除規則は none に設定されます。 通常は、必要なものです。 ただし、行をクリックすると、[ **リレーションシップ** ] ダイアログボックスが表示され、階層更新の動作を変更できます。 詳細については、「データセットと[階層更新](../data-tools/hierarchical-update.md)[のリレーションシップ](../data-tools/relationships-in-datasets.md)」を参照してください。

     ![データセットの関係ダイアログ](../data-tools/media/raddata-relation-dialog.png "レーダーデータの関係ダイアログ")

8. テーブル内のテーブル、テーブルアダプター、または列名をクリックすると、そのプロパティが [ **プロパティ** ] ウィンドウに表示されます。 ここでは、一部の値を変更できます。 ソースデータベースではなく、データセットを変更するだけであることに注意してください。

     ![データセット列のプロパティ](../data-tools/media/dataset-column-properties.png "データセット列のプロパティ")

9. 新しいテーブルまたはテーブルアダプターをデータセットに追加したり、既存のテーブルアダプターに新しいクエリを追加したり、[ **ツールボックス** ] タブから項目をドラッグしてテーブル間の新しいリレーションシップを指定したりすることができます。このタブは、 **データセットデザイナー** にフォーカスがあるときに表示されます。

     ![データセットツールボックス](../data-tools/media/raddata-dataset-toolbox.png "レーダーデータデータセットツールボックス")

10. 次に、データセットにデータを設定する方法を指定します。 そのためには、 **TableAdapter 構成ウィザード**を使用します。 詳細については、「 [tableadapter を使用したデータセットの読み込み](../data-tools/fill-datasets-by-using-tableadapters.md) 」を参照してください。

## <a name="add-a-database-table-or-other-object-to-an-existing-dataset"></a>データベーステーブルまたはその他のオブジェクトを既存のデータセットに追加する
 この手順では、最初にデータセットを作成するときに使用したものと同じデータベースからテーブルを追加する方法を示します。

1. データセットデザイナーでフォーカスを移動するには、 **ソリューションエクスプローラー** の [データセット] ノードをクリックします。

2. Visual Studio の左側の余白の [**データソース**] タブをクリックするか、[クイック起動] に「」と入力し `Data Sources` ます。 **QuickLaunch**

3. [データセット] ノードを右クリックし、[ **ウィザードでデータソースを構成する** ] を選択します。

     ![データソースのコンテキストメニュー](../data-tools/media/data-source-context-menu.png "データソースのコンテキストメニュー")

4. ウィザードを使用して、データセットに追加する追加のテーブル、ストアドプロシージャ、または他のデータベースオブジェクトを指定します。

## <a name="add-a-stand-alone-data-table-to-a-dataset"></a>データセットへのスタンドアロンデータテーブルの追加

1. **データセット デザイナー**でご自分のデータセットを開きます。

2. <xref:System.Data.DataTable>**ツールボックス**の [**データセット**] タブから**データセットデザイナー**にクラスをドラッグします。

3. 列を追加してデータ テーブルを定義します。 詳細については、「 [方法: DataTable に列を追加](https://msdn.microsoft.com/library/8ca21f77-b99a-47a7-a656-7cfd7a1bd9df)する」を参照してください。

4. スタンドアロンテーブル `Fill` では、データを格納できるように、スタンドアロンテーブルにロジックを実装する必要があります。 スタンドアロンデータテーブルを入力する方法については、「 [DataAdapter からのデータセットの読み込み](https://msdn.microsoft.com/library/3fa0ac7d-e266-4954-bfac-3fbe2f913153)」を参照してください。

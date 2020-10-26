---
title: N 層アプリケーションのデータセットにコードを追加する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- n-tier applications, extending datasets
ms.assetid: d43c2ccd-4902-43d8-b1a8-d10ca5d3210c
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: aed37ee9cdd8c221fcfb114db426a6286ee8ad6f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72673114"
---
# <a name="add-code-to-datasets-in-n-tier-applications"></a>n 層アプリケーションのデータセットにコードを追加する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

データセットの機能を拡張するには、データセットの部分クラスファイルを作成し、そのデータセットにコードを追加します ( *DatasetName*にコードを追加するのではありません)。データセットデザイナーファイル)。 部分クラスを使用すると、特定のクラスのコードを複数の物理ファイルに分割できます。 詳細については、「 [部分](https://msdn.microsoft.com/library/7adaef80-f435-46e1-970a-269fff63b448) クラスまたは [部分クラスとメソッド](https://msdn.microsoft.com/library/804cecb7-62db-4f97-a99f-60975bd59fa1)」を参照してください。

データセットを定義するコードは、データセット定義が変更されるたびに生成されます。 このコードは、データセットの構成を変更するウィザードの実行中に変更を加えた場合にも生成されます。 データセットの再生成時にコードが削除されないようにするには、データセットの部分クラスファイルにコードを追加します。

既定では、データセットと `TableAdapter` コードを分離すると、結果としてプロジェクトごとに別個のクラス ファイルが生成されます。 元のプロジェクトには、filenamed *DatasetName*があります。デザイナー .vb (または *DatasetName*)。Designer.cs) のコードが含まれてい `TableAdapter` ます。 " **Dataset プロジェクト** " プロパティで指定されているプロジェクトには、 *DatasetName*という名前のファイルがあります。 *DatasetName*(または。DataSet.Designer.cs)。このファイルには、データセットコードが含まれています。

> [!NOTE]
> `TableAdapter`( **Dataset プロジェクト**プロパティを設定して) データセットとを分離すると、プロジェクト内の既存の部分データセットクラスは自動的には移動されません。 既存のデータセット部分クラスは、手動でデータセット プロジェクトに移動する必要があります。

> [!NOTE]
> 検証コードを追加する必要がある場合、データセットデザイナーには、 <xref:System.Data.DataTable.ColumnChanging> イベントハンドラーとイベントハンドラーを生成するための機能が用意されて <xref:System.Data.DataTable.RowChanging> います。 詳細については、「 [n 層データセットへの検証の追加](../data-tools/add-validation-to-an-n-tier-dataset.md)」を参照してください。

## <a name="add-code-to-datasets-in-n-tier-applications"></a>n 層アプリケーションのデータセットにコードを追加する

1. .Xsd ファイル (データセット) が含まれているプロジェクトを見つけます。

2. **.Xsd**ファイルを選択して、データセットを開きます。

3. コード (タイトルバーのテーブル名) を追加するデータテーブルを右クリックし、[ **コードの表示**] を選択します。

     部分クラスが作成され、コードエディターで開きます。

4. 部分クラス宣言内にコードを追加します。

     次の例は、NorthwindDataSet 内の顧客 Sdatatable にコードを追加する場所を示しています。

    ```vb
    Partial Public Class CustomersDataTable
        ' Add code here to add functionality
        ' to the CustomersDataTable.
    End Class
    ```

    ```csharp
    partial class CustomersDataTable
    {
        // Add code here to add functionality
        // to the CustomersDataTable.
    }
    ```

## <a name="see-also"></a>こちらもご覧ください

- [N 層データアプリケーションの概要](../data-tools/n-tier-data-applications-overview.md)
- [n 層アプリケーションの TableAdapters にコードを追加する](../data-tools/add-code-to-tableadapters-in-n-tier-applications.md)
- [TableAdapter](https://msdn.microsoft.com/library/09416de9-134c-4dc7-8262-6c8d81e3f364)
- [TableAdapterManager の概要](https://msdn.microsoft.com/library/33076d42-6b41-491a-ac11-6c6339aea650)
- [階層更新の概要](https://msdn.microsoft.com/library/c4f8e8b9-e4a5-4a02-8462-d03d1e8222d6)
- [Visual Studio のデータセットツール](../data-tools/dataset-tools-in-visual-studio.md)
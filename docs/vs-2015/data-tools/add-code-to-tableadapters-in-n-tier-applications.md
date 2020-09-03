---
title: N 層アプリケーションの Tableadapter にコードを追加する |Microsoft Docs
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
- TableAdapters, n-tier applications
- n-tier applications, extending TableAdapters
ms.assetid: dafac00e-df9d-4d4a-95a6-e34b4d099425
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 942850e776cdd493afaad56b782b417db2040625
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72673105"
---
# <a name="add-code-to-tableadapters-in-n-tier-applications"></a>n 層アプリケーションの TableAdapters にコードを追加する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

の機能を拡張するには `TableAdapter` 、の部分クラスファイルを作成し、DatasetName にコードを追加するのでは `TableAdapter` なく、 *DatasetName*そのクラスにコードを追加します。データセットデザイナーファイル)。 部分クラスを使用すると、特定のクラスのコードを複数の物理ファイルに分割できます。 詳細については、「 [partial](https://msdn.microsoft.com/library/7adaef80-f435-46e1-970a-269fff63b448) または [partial (型)](https://msdn.microsoft.com/library/27320743-a22e-4c7b-b0b3-53afe3607334)」を参照してください。

 を定義するコード `TableAdapter` は、に変更が行われるたびに生成され `TableAdapter` ます。 このコードは、の構成を変更するウィザードの実行中に変更が行われた場合にも生成され `TableAdapter` ます。 の再生成時にコードが削除されないようにするには、 `TableAdapter` の部分クラスファイルにコードを追加し `TableAdapter` ます。

 既定では、データセットと `TableAdapter` コードを分離すると、結果としてプロジェクトごとに別個のクラス ファイルが生成されます。 元のプロジェクトには、 *DatasetName*という名前のファイルがあります。デザイナー .vb (または *DatasetName*)。Designer.cs) のコードが含まれてい `TableAdapter` ます。 " **Dataset プロジェクト** " プロパティに指定されているプロジェクトには、 *DatasetName*という名前のファイルがあります。 *DatasetName*(または。DataSet.Designer.cs)。データセットコードが含まれています。

> [!NOTE]
> `TableAdapter`( **Dataset プロジェクト**プロパティを設定して) データセットとを分離すると、プロジェクト内の既存の部分データセットクラスは自動的には移動されません。 既存のデータセット部分クラスは、手動でデータセット プロジェクトに移動する必要があります。

> [!NOTE]
> データセットデザイナーには、 <xref:System.Data.DataTable.ColumnChanging> <xref:System.Data.DataTable.RowChanging> 検証が必要な場合にイベントハンドラーを生成する機能が用意されています。 詳細については、「 [n 層データセットへの検証の追加](../data-tools/add-validation-to-an-n-tier-dataset.md)」を参照してください。

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

### <a name="to-add-user-code-to-a-tableadapter-in-an-n-tier-application"></a>N 層アプリケーションの TableAdapter にユーザーコードを追加するには

1. .Xsd ファイル (データセット) が含まれているプロジェクトを見つけます。

2. **.Xsd**ファイルをダブルクリックして、データセットを開きます。

3. コードを追加するを右クリックし、[ `TableAdapter` **コードの表示**] を選択します。

     部分クラスが作成され、コードエディターで開きます。

4. 部分クラス宣言内にコードを追加します。

5. 次の例では、でコードをに追加する方法を示し `CustomersTableAdapter` `NorthwindDataSet` ます。

    ```vb
    Partial Public Class CustomersTableAdapter
        ' Add code here to add functionality
        ' to the CustomersTableAdapter.
    End Class
    ```

    ```csharp
    public partial class CustomersTableAdapter
    {
        // Add code here to add functionality
        // to the CustomersTableAdapter.
    }
    ```

## <a name="see-also"></a>参照
 [N 層データアプリケーションの概要](../data-tools/n-tier-data-applications-overview.md) [n 層アプリケーションのデータセットにコードを追加する](../data-tools/add-code-to-datasets-in-n-tier-applications.md) [tableadapter](https://msdn.microsoft.com/library/09416de9-134c-4dc7-8262-6c8d81e3f364) [TableAdapterManager 概要](https://msdn.microsoft.com/library/33076d42-6b41-491a-ac11-6c6339aea650)[階層更新](https://msdn.microsoft.com/library/c4f8e8b9-e4a5-4a02-8462-d03d1e8222d6)の概要
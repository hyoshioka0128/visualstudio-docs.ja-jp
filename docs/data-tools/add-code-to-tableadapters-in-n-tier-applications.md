---
title: n 層アプリケーションの TableAdapters にコードを追加する
description: N 層アプリケーションのテーブルアダプターにコードを追加します。 TableAdapter の部分クラスファイルを作成し、それにコードを追加します (DatasetName ではなく)。
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TableAdapters, n-tier applications
- n-tier applications, extending TableAdapters
ms.assetid: dafac00e-df9d-4d4a-95a6-e34b4d099425
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: ed0664b78408e91eeda5b65c26615e870e2171b6
ms.sourcegitcommit: 0893244403aae9187c9375ecf0e5c221c32c225b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2020
ms.locfileid: "94382365"
---
# <a name="add-code-to-tableadapters-in-n-tier-applications"></a>n 層アプリケーションの TableAdapters にコードを追加する
Tableadapter の部分クラスファイルを作成し、そのファイルにコードを追加することにより、TableAdapter の機能を拡張できます (コードを *DatasetName* ファイルに追加するのではなく)。 部分クラスを使用すると、特定のクラスのコードを複数の物理ファイルに分割できます。 詳細については、「 [partial](/dotnet/visual-basic/language-reference/modifiers/partial) または [partial (型)](/dotnet/csharp/language-reference/keywords/partial-type)」を参照してください。

TableAdapter を定義するコードは、データセット内の TableAdapter に変更が加えられるたびに生成されます。 このコードは、TableAdapter の構成を変更するウィザードの実行中に変更が行われた場合にも生成されます。 TableAdapter の再生成時にコードが削除されないようにするには、TableAdapter の部分クラスファイルにコードを追加します。

既定では、データセットと TableAdapter コードを分離した後、結果は各プロジェクトの不連続クラスファイルになります。 元のプロジェクトには、TableAdapter コードを含む *DatasetName* (または *DatasetName.Designer.cs* ) という名前のファイルがあります。 " **Dataset プロジェクト** " プロパティで指定されているプロジェクトには、データセットコードを含む *DatasetName* (または *DatasetName.DataSet.Designer.cs* ) という名前のファイルがあります。

> [!NOTE]
> **[DataSet プロジェクト]** プロパティを設定してデータセットと TableAdapter を分離する場合でも、プロジェクト内の既存のデータセット部分クラスは自動的には移動されません。 既存の部分データセットクラスは、データセットプロジェクトに手動で移動する必要があります。

> [!NOTE]
> データセットは、 <xref:System.Data.DataTable.ColumnChanging> <xref:System.Data.DataTable.RowChanging> 検証が必要な場合にイベントハンドラーを生成するための機能を提供します。 詳細については、「 [n 層データセットへの検証の追加](../data-tools/add-validation-to-an-n-tier-dataset.md)」を参照してください。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="to-add-user-code-to-a-tableadapter-in-an-n-tier-application"></a>N 層アプリケーションの TableAdapter にユーザーコードを追加するには

1. *.Xsd* ファイルが含まれているプロジェクトを見つけます。

2. *.Xsd* ファイルをダブルクリックして、 **データセットデザイナー** を開きます。

3. コードを追加する TableAdapter を右クリックし、[ **コードの表示** ] を選択します。

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

## <a name="see-also"></a>関連項目

- [N 層データアプリケーションの概要](../data-tools/n-tier-data-applications-overview.md)
- [n 層アプリケーションのデータセットにコードを追加する](../data-tools/add-code-to-datasets-in-n-tier-applications.md)
- [Tableadapter の作成および構成](create-and-configure-tableadapters.md)
- [階層更新の概要](hierarchical-update.md)

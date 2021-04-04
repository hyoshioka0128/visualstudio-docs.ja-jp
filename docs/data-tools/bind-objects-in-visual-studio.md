---
title: カスタムオブジェクトのデータバインド
description: Visual Studio のデータソースとしてオブジェクトをバインドします。 アプリケーションのデータソースとしてカスタムオブジェクトを操作するには、デザイン時ツールを使用します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], object binding
- data [Visual Studio], binding to objects
- object binding
- binding, to objects
ms.assetid: ed743ce6-73af-45e5-a8ff-045eddaccc86
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 140700615759404f02109c4506f4c27d083a74b1
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215540"
---
# <a name="bind-objects-as-data-sources-in-visual-studio"></a>Visual Studio でオブジェクトをデータソースとしてバインドする

Visual Studio には、アプリケーションのデータソースとしてカスタムオブジェクトを操作するためのデザイン時ツールが用意されています。 UI コントロールにバインドするオブジェクトのデータベースからデータを格納する場合は、Entity Framework を使用してクラスまたはクラスを生成する方法をお勧めします。 Entity Framework は、すべての定型変更追跡コードを自動生成します。これは、DbSet オブジェクトで AcceptChanges を呼び出したときに、ローカルオブジェクトに対する変更がデータベースに自動的に保存されることを意味します。 詳細については、 [Entity Framework のドキュメント](https://ef.readthedocs.org/en/latest/)を参照してください。

> [!TIP]
> この記事のオブジェクトバインドの方法は、アプリケーションが既にデータセットに基づいている場合にのみ検討してください。 これらの方法は、データセットを既に使い慣れていて、処理するデータが表形式で複雑すぎる場合や大きすぎる場合にも使用できます。 DataReader を使用して直接オブジェクトにデータを読み込み、データバインドを使用せずに UI を手動で更新するなど、さらに簡単な例については、「 [ADO.NET を使用した単純なデータアプリケーションの作成](../data-tools/create-a-simple-data-application-by-using-adonet.md)」を参照してください。

## <a name="object-requirements"></a>オブジェクトの要件

カスタムオブジェクトが Visual Studio のデータデザインツールで動作するための唯一の要件は、オブジェクトに少なくとも1つのパブリックプロパティが必要であることです。

一般に、カスタムオブジェクトでは、アプリケーションのデータソースとして機能する特定のインターフェイス、コンストラクター、または属性は必要ありません。 ただし、オブジェクトを [ **データソース** ] ウィンドウからデザインサーフェイスにドラッグしてデータバインドコントロールを作成し、オブジェクトがインターフェイスまたはインターフェイスを実装している場合は、 <xref:System.ComponentModel.ITypedList> <xref:System.ComponentModel.IListSource> オブジェクトに既定のコンストラクターが必要です。 そうしないと、Visual Studio はデータソースオブジェクトをインスタンス化できず、アイテムをデザイン画面にドラッグしたときにエラーが表示されます。

## <a name="examples-of-using-custom-objects-as-data-sources"></a>カスタムオブジェクトをデータソースとして使用する例

オブジェクトをデータソースとして使用する場合、アプリケーションロジックを実装する方法は数多くありますが、SQL データベースの場合は、Visual Studio で生成された TableAdapter オブジェクトを使用することによって簡略化できるいくつかの標準操作があります。 このページでは、Tableadapter を使用してこれらの標準プロセスを実装する方法について説明します。 カスタムオブジェクトを作成するためのガイドとしては使用しません。 たとえば、通常、オブジェクトの特定の実装やアプリケーションのロジックに関係なく、次のような標準的な操作を実行します。

- オブジェクトへのデータの読み込み (通常はデータベースから)。

- オブジェクトの型指定されたコレクションを作成します。

- オブジェクトをコレクションに追加したり、コレクションからオブジェクトを削除したりします。

- フォーム上のユーザーにオブジェクトデータを表示します。

- オブジェクトのデータの変更/編集。

- オブジェクトのデータをデータベースに保存し直す。

### <a name="load-data-into-objects"></a>オブジェクトへのデータの読み込み

この例では、Tableadapter を使用して、オブジェクトにデータを読み込みます。 既定では、Tableadapter は、データベースからデータをフェッチし、データテーブルを設定する2種類のメソッドを使用して作成されます。

- メソッドは、返された `TableAdapter.Fill` データを既存のデータテーブルに格納します。

- メソッドは、 `TableAdapter.GetData` データが設定された新しいデータテーブルを返します。

データを使用してカスタムオブジェクトを読み込む最も簡単な方法は、メソッドを呼び出し `TableAdapter.GetData` 、返されたデータテーブル内の行のコレクションをループ処理し、各オブジェクトに各行の値を設定することです。 `GetData`TableAdapter に追加されたすべてのクエリについて、データが設定されたデータテーブルを返すメソッドを作成できます。

> [!NOTE]
> Visual Studio では、TableAdapter クエリに既定で名前を指定し `Fill` `GetData` ますが、これらの名前は任意の有効なメソッド名に変更できます。

次の例では、データテーブル内の行をループ処理し、オブジェクトにデータを設定する方法を示します。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Form1.cs" id="Snippet4":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Form1.vb" id="Snippet4":::

### <a name="create-a-typed-collection-of-objects"></a>オブジェクトの型指定されたコレクションを作成する

オブジェクトのコレクションクラスを作成することも、 [BindingSource コンポーネント](/dotnet/framework/winforms/controls/bindingsource-component)によって自動的に提供される型指定されたコレクションを使用することもできます。

オブジェクトのカスタムコレクションクラスを作成する場合は、から継承することをお勧め <xref:System.ComponentModel.BindingList%601> します。 このジェネリッククラスは、コレクションを管理するための機能を提供するだけでなく、Windows フォームのデータバインディングインフラストラクチャに通知を送信するイベントを発生させる機能を提供します。

で自動的に生成されたコレクションは、 <xref:System.Windows.Forms.BindingSource> <xref:System.ComponentModel.BindingList%601> 型指定されたコレクションに対してを使用します。 アプリケーションで追加の機能が必要ない場合は、内でコレクションを維持することができ <xref:System.Windows.Forms.BindingSource> ます。 詳細については、 <xref:System.Windows.Forms.BindingSource.List%2A> クラスのプロパティを参照してください <xref:System.Windows.Forms.BindingSource> 。

> [!NOTE]
> の基本実装によって提供されていない機能がコレクションに必要な場合は、必要に応じ <xref:System.ComponentModel.BindingList%601> てクラスに追加できるように、カスタムコレクションを作成する必要があります。

次のコードは、厳密に型指定されたオブジェクトのコレクションのクラスを作成する方法を示してい `Order` ます。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs" id="Snippet8":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb" id="Snippet8":::

### <a name="add-objects-to-a-collection"></a>コレクションへのオブジェクトの追加

コレクションにオブジェクトを追加するに `Add` は、カスタムコレクションクラスのメソッドまたはを呼び出し <xref:System.Windows.Forms.BindingSource> ます。

> [!NOTE]
> メソッドは、 `Add` から継承するときに、カスタムコレクションに対して自動的に提供され <xref:System.ComponentModel.BindingList%601> ます。

次のコードは、の型指定されたコレクションにオブジェクトを追加する方法を示してい <xref:System.Windows.Forms.BindingSource> ます。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs" id="Snippet5":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb" id="Snippet5":::

次のコードは、から継承される型指定されたコレクションにオブジェクトを追加する方法を示してい <xref:System.ComponentModel.BindingList%601> ます。

> [!NOTE]
> この例では、 `Orders` コレクションはオブジェクトのプロパティです `Customer` 。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs" id="Snippet6":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb" id="Snippet6":::

### <a name="remove-objects-from-a-collection"></a>コレクションからオブジェクトを削除する

コレクションからオブジェクトを削除するには、 `Remove` `RemoveAt` カスタムコレクションクラスまたはのメソッドを呼び出し <xref:System.Windows.Forms.BindingSource> ます。

> [!NOTE]
> `Remove`メソッドと `RemoveAt` メソッドは、から継承するときに、カスタムコレクションに対して自動的に提供され <xref:System.ComponentModel.BindingList%601> ます。

次のコードは、メソッドを使用して、型指定されたコレクションからオブジェクトを検索および削除する方法を示してい <xref:System.Windows.Forms.BindingSource> <xref:System.Windows.Forms.BindingSource.RemoveAt%2A> ます。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs" id="Snippet7":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb" id="Snippet7":::

### <a name="display-object-data-to-users"></a>オブジェクトのデータをユーザーに表示する

オブジェクトのデータをユーザーに表示するには、 **データソース構成** ウィザードを使用してオブジェクトデータソースを作成し、オブジェクト全体または個々のプロパティを [ **データソース** ] ウィンドウからフォームにドラッグします。

### <a name="modify-the-data-in-objects"></a>オブジェクトのデータを変更する

Windows フォームコントロールにデータバインドされているカスタムオブジェクト内のデータを編集するには、単にバインドされたコントロール (またはオブジェクトのプロパティで直接) のデータを編集します。 データバインディングアーキテクチャは、オブジェクト内のデータを更新します。

アプリケーションで変更を追跡する必要がある場合、および提案された変更を元の値にロールバックする必要がある場合は、オブジェクトモデルにこの機能を実装する必要があります。 データテーブルが提案された変更を追跡する方法の例については、「」、「」、および「」を参照してください <xref:System.Data.DataRowState> <xref:System.Data.DataSet.HasChanges%2A> <xref:System.Data.DataTable.GetChanges%2A> 。

### <a name="save-data-in-objects-back-to-the-database"></a>オブジェクトのデータをデータベースに保存する

オブジェクトから TableAdapter の DBDirect メソッドに値を渡すことによって、データベースにデータを保存し直します。

Visual Studio によって、データベースに対して直接実行できる DBDirect メソッドが作成されます。 これらのメソッドは、DataSet オブジェクトまたは DataTable オブジェクトを必要としません。

|TableAdapter DBDirect メソッド|説明|
| - |-----------------|
|`TableAdapter.Insert`|データベースに新しいレコードを追加します。これにより、個々の列の値をメソッドのパラメーターとして渡すことができます。|
|`TableAdapter.Update`|データベース内の既存のレコードを更新します。 Update メソッドは、元の列と新しい列の値をメソッドのパラメーターとして受け取ります。 元の値は元のレコードを検索するために使用され、新しい値はそのレコードを更新するために使用されます。<br /><br /> メソッドは、 `TableAdapter.Update` <xref:System.Data.DataSet> <xref:System.Data.DataTable> <xref:System.Data.DataRow> <xref:System.Data.DataRow> メソッドパラメーターとしての、、、またはの配列を取得することによって、データセット内の変更をデータベースに戻すためにも使用されます。|
|`TableAdapter.Delete`|メソッドパラメーターとして渡された元の列の値に基づいて、データベースから既存のレコードを削除します。|

オブジェクトのコレクションからデータを保存するには、オブジェクトのコレクションをループ処理します (たとえば、for-next ループを使用します)。 TableAdapter の DBDirect メソッドを使用して、各オブジェクトの値をデータベースに送信します。

次の例では、dbdirect メソッドを使用して、 `TableAdapter.Insert` 新しい顧客をデータベースに直接追加する方法を示します。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs" id="Snippet23":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb" id="Snippet23":::

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)

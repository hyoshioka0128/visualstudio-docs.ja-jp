---
title: '方法: エンティティクラスに検証を追加するMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 61107da9-7fa3-4dba-b101-ae46536f52c4
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a68b0314f3c64ce9196b8d48a78844bc81990a92
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72665995"
---
# <a name="how-to-add-validation-to-entity-classes"></a>方法: エンティティ クラスに検証を追加する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

エンティティ クラスの "*検証*" とは、データ オブジェクトに入力された値が、アプリケーションに対して設定された規則に従っていること、およびオブジェクトのスキーマ内の制約に従っていることを確認するプロセスです。 基になるデータベースに更新を送信する前にデータを検証すると、エラーを減らすことができます。 アプリケーションとデータベースの間で生じる可能性のあるラウンド トリップの回数も減ります。

 [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)には、完全なエンティティの挿入、更新、および削除中に実行されるデザイナーによって生成されたコードをユーザーが拡張できる部分メソッドと、個々の列の変更中および変更後のコードが含まれます。

> [!NOTE]
> このトピックでは、[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]を使用してエンティティ クラスに検証を追加する基本的な手順を示します。 特定のエンティティ クラスを参照しないでこれらの汎用的な手順に従うのは難しい可能性があるため、実際のデータを使用するチュートリアルが用意されています。

## <a name="adding-validation-for-changes-to-the-value-in-a-specific-column"></a>特定の列の値の変更に対する検証の追加
 この手順では、列の値の変更時にデータを検証する方法を示します。 検証はユーザー インターフェイスではなくクラス定義の内部で実行されるため、値によって検証が失敗する場合は例外がスローされます。 列の値を変更しようとするアプリケーションのコードには、エラー処理を実装してください。

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

#### <a name="to-validate-data-during-a-columns-value-change"></a>列の値の変更時にデータを検証するには

1. で、新しい LINQ to SQL クラスファイル (**.dbml** ファイル) を開くか作成し [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ます。 (**ソリューション エクスプローラー**で **.dbml** ファイルをダブルクリックします。)

2. O/R デザイナーで、検証を追加するクラスを右クリックし、[ **コードの表示**] をクリックします。

    コード エディターが開き、選択したエンティティ クラスの部分クラスが表示されます。

3. 部分クラスにカーソルを置きます。

4. Visual Basic プロジェクトの場合は、次の操作を行います。

   1. **[メソッド名]** の一覧を展開します。

   2. 検証を追加する列の **On**_COLUMNNAME_**Changing** メソッドを見つけます。

   3. `On` *COLUMNNAME* `Changing` メソッドが部分クラスに追加されます。

   4. 次のコードを追加して、まず値が入力されたことを確認し、次に列に入力された値がアプリケーションで許容されることを確認します。 入力された値は `value` 引数に含まれています。そこで、これが有効な値であることを確認するロジックを追加します。

      ```vb
      If value.HasValue Then
          ' Add code to ensure that the value is acceptable.
          ' If value < 1 Then
          '    Throw New Exception("Invalid data!")
          ' End If
      End If
      ```

      C# プロジェクトの場合は、次の操作を行います。

   5. C# プロジェクトでは、イベント ハンドラーの生成は自動的には行われないため、IntelliSense を使用して列変更部分メソッドを作成します。

       「`partial`」に続けてスペースを入力して、使用可能な部分メソッドの一覧にアクセスします。 検証を追加する列の列変更メソッドをクリックします。 列変更部分メソッドを選択したときに生成されるコードは次のようになります。

      ```csharp
      partial void OnCOLUMNNAMEChanging(COLUMNDATATYPE value)
          {
             throw new System.NotImplementedException();
          }

      ```

## <a name="adding-validation-for-updates-to-an-entity-class"></a>エンティティ クラスへの更新の検証の追加
 変更時の値のチェックに加えて、エンティティ クラス全体の更新が試行されたときにデータを検証することもできます。 更新の試行時の検証では、ビジネス ルールにおける必要性に応じて複数の列の値を比較できます。 次の手順は、エンティティ クラス全体の更新が試行されたときに検証を行う方法を示しています。

> [!NOTE]
> エンティティ クラス全体の更新に対する検証コードは、特定のエンティティ クラスの部分クラスではなく、部分 <xref:System.Data.Linq.DataContext> クラスで実行されます。

#### <a name="to-validate-data-during-an-update-to-an-entity-class"></a>エンティティ クラスの更新時にデータを検証するには

1. で、新しい LINQ to SQL クラスファイル (**.dbml** ファイル) を開くか作成し [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ます。 (**ソリューション エクスプローラー**で **.dbml** ファイルをダブルクリックします。)

2. O/R デザイナーで空の領域を右クリックし、**[コードの表示]** をクリックします。

    コード エディターが開き、`DataContext` の部分クラスが表示されます。

3. `DataContext` の部分クラスにカーソルを置きます。

4. Visual Basic プロジェクトの場合は、次の操作を行います。

   1. **[メソッド名]** の一覧を展開します。

   2. [ **更新**_entityclassname_] をクリックします。

   3. `Update` *Entityclassname*メソッドが部分クラスに追加されます。

   4. 次のコードに示すように、`instance` 引数を使用して個々の列の値にアクセスします。

      ```vb
      If (instance.COLUMNNAME = x) And (instance.COLUMNNAME = y) Then
          Dim ErrorMessage As String = "Invalid data!"
          Throw New Exception(ErrorMessage)
      End If
      ```

      C# プロジェクトの場合は、次の操作を行います。

   5. C# プロジェクトではイベントハンドラーが自動的に生成されないため、IntelliSense を使用して部分クラスのメソッドを作成でき `Update` *CLASSNAME*ます。

   6. 「`partial`」に続けてスペースを入力して、使用可能な部分メソッドの一覧にアクセスします。 検証を追加するクラスの更新メソッドをクリックします。 CLASSNAME 部分メソッドを選択すると生成されるコードは次のようになり `Update` *CLASSNAME*ます。

      ```csharp
      partial void UpdateCLASSNAME(CLASSNAME instance)
      {
          if ((instance.COLUMNNAME == x) && (instance.COLUMNNAME = y))
          {
              string ErrorMessage = "Invalid data!";
              throw new System.Exception(ErrorMessage);
          }
      }
      ```

## <a name="see-also"></a>参照
 [データの検証](https://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655) [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)

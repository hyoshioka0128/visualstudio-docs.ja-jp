---
title: O/R デザイナーを使用して継承を構成する
description: 単一テーブルの継承をサポートするオブジェクトリレーショナルデザイナー (O/R デザイナー) を使用して継承を構成する方法について説明します。 継承されたデータクラスを作成しました。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: e594af12-e777-434a-bc08-7dd2dac84cdc
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: fee2c42e6ec84280f4090a8ae1dfea83a81ee369
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866828"
---
# <a name="how-to-configure-inheritance-by-using-the-or-designer"></a>方法: O/R デザイナーを使用して継承を構成する
**オブジェクトリレーショナルデザイナー** (**O/R デザイナー**) は、リレーショナルシステムに実装されることが多いため、単一テーブル継承の概念をサポートしています。 単一テーブル継承には、親情報と子情報の両方のフィールドを含む単一のデータベース テーブルがあります。 リレーショナル データでは、判別用の列に、レコードが属するクラスを決定する値が含まれています。

たとえば、 `Persons` 会社によって採用されたすべてのユーザーを含むテーブルがあるとします。 従業員の人もいれば、管理者の人もいます。 `Persons`このテーブルにはという名前の列が含まれてい `EmployeeType` ます。この列の値は、マネージャーの場合は1、従業員の場合は2になります。これは識別子列です。 このシナリオでは、従業員のサブクラスを作成して、そのクラスには `EmployeeType` の値が 2 のレコードだけを入れます。 適用されない列を各クラスから削除することもできます。

継承を使用する (およびリレーショナル データに対応する) オブジェクト モデルの作成は、わかりにくい場合があります。 次の手順では、**O/R デザイナー** で継承を設定するために必要な手順を概説します。 既存のテーブルと列を参照せずに一般的な手順を実行することは困難であるため、データを使用するチュートリアルが用意されています。 詳細な手順を使用して継承を構成するため、 **O/R デザイナー** を参照してください [チュートリアル: LINQ to SQL を作成するクラスの単一テーブル継承 (O/R デザイナー) を使用して](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)します。

## <a name="to-create-inherited-data-classes"></a>継承されたデータ クラスを作成するには

1. 既存の Visual Basic または C# プロジェクトに **LINQ to SQL クラス** 項目を追加して、 **O/R デザイナー** を開きます。

2. 基本クラスとして使用するテーブルを **O/R デザイナー** にドラッグします。

3. テーブルの2つ目のコピーを **O/R デザイナー** にドラッグし、名前を変更します。 これは、派生クラス、つまりサブクラスです。

4. **ツールボックス** の **[オブジェクト リレーショナル デザイナー]** タブで **[継承]** をクリックし、サブクラス (名前を変更したテーブル) をクリックして、基本クラスに接続します。

    > [!NOTE]
    > **ツールボックス** の **[継承]** 項目をクリックしてマウス ボタンを放し、手順 3 で作成したクラスの 2 番目のコピーをクリックしてから、手順 2 で作成した最初のクラスをクリックします。 継承線の矢印は、最初のクラスを指します。

5. 各クラスで、関連付けに使用されていない、表示する必要のないオブジェクト プロパティを削除します。 関連付けに使用されているオブジェクトのプロパティを削除しようとすると、エラーが発生します。 [ \<property name> このプロパティは \<association name> 関連付けに参加しているため、削除できません](../data-tools/the-property-property-name-cannot-be-deleted-because-it-is-participating-in-the-association-association-name.md)。

    > [!NOTE]
    > 派生クラスは基本クラスで定義されているプロパティを継承するため、各クラスに同じ列を定義することはできません  (列はプロパティとして実装されます)。派生クラスでの列の作成を有効にするには、基底クラスのプロパティで継承修飾子を設定します。 詳細については、「 [継承の基本」 (Visual Basic)](/dotnet/visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics)を参照してください。

6. **O/R デザイナー** で継承線を選択します。

7. [ **プロパティ** ] ウィンドウで、[ **識別子] プロパティ** を、クラスのレコードを区別する列名に設定します。

8. **[派生クラスの識別子の値]** プロパティに、レコードが継承された型であることを示すデータベース内の値を設定します。 (これは、識別子の列に格納され、継承されたクラスを指定するために使用される値です)。

9. **[基本クラスの識別子の値]** プロパティに、レコードが基本型であることを示す値を設定します。 (これは、識別子の列に格納され、基底クラスを指定するために使用される値です)。

10. オプションとして、**[継承の既定値]** プロパティを設定することもできます。これは、定義済みの継承コードと一致しない行を読み込むときに使用される継承階層の型を示します。 つまり、 **派生クラスの識別子** の値または **基本クラスの識別子の値** のプロパティの値と一致しない識別子の列にレコードの値がある場合、そのレコードは継承の **既定** 値として指定された型に読み込まれます。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [チュートリアル: LINQ to SQL クラスの作成 (O-R デザイナー)](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [チュートリアル: 単一テーブル継承を使用した LINQ to SQL クラスの作成 (O/R デザイナー)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)
- [継承の基本 (Visual Basic)](/dotnet/visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics)
- [継承](/dotnet/csharp/programming-guide/classes-and-structs/inheritance)

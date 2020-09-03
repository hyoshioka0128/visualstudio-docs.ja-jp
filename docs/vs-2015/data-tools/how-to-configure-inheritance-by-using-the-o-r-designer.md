---
title: '方法: O/R デザイナーを使用して継承を構成する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: e594af12-e777-434a-bc08-7dd2dac84cdc
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7f8c08546fdf96c755b3adb80021ab7269509739
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72654702"
---
# <a name="how-to-configure-inheritance-by-using-the-or-designer"></a>方法: O/R デザイナーを使用して継承を構成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vs_ordesigner_long](../includes/vs-ordesigner-long-md.md)] ([!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]) では、一般にリレーショナル システムで実装されている単一テーブル継承の概念がサポートされます。 単一テーブル継承には、親情報と子情報の両方のフィールドを含む単一のデータベース テーブルがあります。 リレーショナル データでは、判別用の列に、レコードが属するクラスを決定する値が含まれています。

 たとえば、会社に採用されたすべての人を含む Persons テーブルについて考えます。 従業員の人もいれば、管理者の人もいます。 Persons テーブルには、管理者を表す値 1 と従業員を表す値 2 がある `EmployeeType` という名前の列が含まれています。これが判別用の列です。 このシナリオでは、従業員のサブクラスを作成して、そのクラスには `EmployeeType` の値が 2 のレコードだけを入れます。 適用されない列を各クラスから削除することもできます。

 継承を使用する (およびリレーショナル データに対応する) オブジェクト モデルの作成は、わかりにくい場合があります。 次の手順では、O/R デザイナーで継承を設定するために必要な手順を概説します。 既存のテーブルと列を参照しないで汎用的な手順に従うのは難しい場合があるので、データを使用したチュートリアルが用意されています。 を使用して継承を構成するための詳細な手順につい [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ては、「 [チュートリアル: 単一テーブル継承を使用した LINQ to SQL クラスの作成 (O/R デザイナー)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)」を参照してください。

### <a name="to-create-inherited-data-classes"></a>継承されたデータ クラスを作成するには

1. [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] **LINQ to SQL Classes**項目を既存の Visual Basic または C# プロジェクトに追加して、を開きます。

2. 基本クラスとして使用するテーブルを [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]にドラッグします。

3. テーブルの2つ目のコピーをにドラッグし、 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 名前を変更します。 これは、派生クラス、つまりサブクラスです。

4. **ツールボックス**の **[オブジェクト リレーショナル デザイナー]** タブで **[継承]** をクリックし、サブクラス (名前を変更したテーブル) をクリックして、基本クラスに接続します。

    > [!NOTE]
    > **ツールボックス**の **[継承]** 項目をクリックしてマウス ボタンを放し、手順 3 で作成したクラスの 2 番目のコピーをクリックしてから、手順 2 で作成した最初のクラスをクリックします。 継承線の矢印は最初のクラスを指します。

5. 各クラスで、関連付けに使用されていない、表示する必要のないオブジェクト プロパティを削除します。 関連付けに使用されているオブジェクトのプロパティを削除しようとすると、エラーが発生します。[このプロパティは \<property name> 関連付け \<association name> に参加しているため、削除できません](../data-tools/the-property-property-name-cannot-be-deleted-because-it-is-participating-in-the-association-association-name.md)。

    > [!NOTE]
    > 派生クラスは基本クラスで定義されているプロパティを継承するため、各クラスに同じ列を定義することはできません  (列はプロパティとして実装されます)。派生クラスでの列の作成を有効にするには、基底クラスのプロパティで継承修飾子を設定します。 詳細については、「 [ビルド内にありません: プロパティとメソッドのオーバーライド](https://msdn.microsoft.com/2167e8f5-1225-4b13-9ebd-02591ba90213)」を参照してください。

6. [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]で継承線を選択します。

7. [ **プロパティ** ] ウィンドウで、[ **識別子] プロパティ** を、クラスのレコードを区別するために使用される列名に設定します。

8. **[派生クラスの識別子の値]** プロパティに、レコードが継承された型であることを示すデータベース内の値を設定します。 (これは判別用の列に格納される値で、継承されたクラスを示すために使用されます)。

9. **[基本クラスの識別子の値]** プロパティに、レコードが基本型であることを示す値を設定します。 (これは判別用の列に格納される値で、基本クラスを示すために使用されます)。

10. オプションとして、**[継承の既定値]** プロパティを設定することもできます。これは、定義済みの継承コードと一致しない行を読み込むときに使用される継承階層の型を示します。 つまり、 **派生クラスの識別子** の値または **基本クラスの識別子の値** のプロパティの値と一致しない識別子の列にレコードの値がある場合、そのレコードは継承の **既定**値として指定された型に読み込まれます。

## <a name="see-also"></a>参照
 [Visual studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)[チュートリアル: LINQ to SQL クラスの作成 (O-R デザイナー)](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233) [PAVE Visual Studio 2012 でのデータアプリケーション開発の新機能](https://msdn.microsoft.com/3d50d68f-5f44-4915-842f-6d42fce793f1) [visual studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655) [チュートリアル: 単一テーブル継承を使用した LINQ to SQL クラスの作成 (o/r デザイナー)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md) [ビルド内にありません: Visual Basic 継承での継承](https://msdn.microsoft.com/e5e6e240-ed31-4657-820c-079b7c79313c) [Inheritance](https://msdn.microsoft.com/library/81d64ee4-50f9-4d6c-a8dc-257c348d2eea)

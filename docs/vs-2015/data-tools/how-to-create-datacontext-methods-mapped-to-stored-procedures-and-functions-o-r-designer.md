---
title: '方法: ストアドプロシージャおよび関数にマップされた DataContext メソッドを作成する (O/R デザイナー) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: e7ca32f1-50b3-48af-ad92-ceafd749296a
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 70053b74a4dd2ad569e1e8195f4c9b2e7b214440
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72665975"
---
# <a name="how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-or-designer"></a>方法: ストアド プロシージャや関数にマップされる DataContext メソッドを作成する (O/R デザイナー)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ストアドプロシージャと関数は、メソッドとしてに追加でき [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] <xref:System.Data.Linq.DataContext> ます。 メソッドを呼び出して必要なパラメーターを渡すと、データベースでストアド プロシージャまたは関数が実行され、<xref:System.Data.Linq.DataContext> メソッドの戻り値の型のデータが返されます。 メソッドの詳細について <xref:System.Data.Linq.DataContext> は、「 [DataContext メソッド (O/R デザイナー)](../data-tools/datacontext-methods-o-r-designer.md)」を参照してください。

> [!NOTE]
> ストアド プロシージャを使用して、エンティティ クラスからデータベースに変更が保存されたときに挿入、更新、および削除を実行する既定の [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] ランタイムの動作をオーバーライドすることもできます。 詳細については、「 [方法: 更新、挿入、および削除を実行するストアドプロシージャを割り当てる (O/R デザイナー)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)」を参照してください。

## <a name="creating-datacontext-methods"></a>DataContext メソッドの作成
 メソッドを作成する <xref:System.Data.Linq.DataContext> には、ストアドプロシージャまたは関数を **サーバーエクスプローラー/データベースエクスプローラー** からにドラッグし [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ます。

> [!NOTE]
> 生成される <xref:System.Data.Linq.DataContext> メソッドの戻り値の型は、[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]でストアド プロシージャまたは関数をドロップする場所によって異なります。 既存のエンティティ クラスに項目を直接ドロップすると、そのエンティティ クラスを戻り値の型とする <xref:System.Data.Linq.DataContext> メソッドが作成されます。 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]の空の領域に項目をドロップすると、自動生成された型を返す <xref:System.Data.Linq.DataContext> メソッドが作成されます。 <xref:System.Data.Linq.DataContext>メソッドをメソッドペインに追加した後に、メソッドの戻り値の型を変更できます。 <xref:System.Data.Linq.DataContext> メソッドの戻り値の型を確認または変更するには、**[プロパティ]** ウィンドウでメソッドを選択し、**[戻り値の型]** プロパティを調べます。 詳細については、「 [方法: DataContext メソッドの戻り値の型を変更する (O/R デザイナー)](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md)」を参照してください。

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

#### <a name="to-create-datacontext-methods-that-return-automatically-generated-types"></a>自動生成された型を返す DataContext メソッドを作成するには

1. **サーバーエクスプローラー** / **データベースエクスプローラー**で、使用しているデータベースの [**ストアドプロシージャ**] ノードを展開します。

2. 目的のストアド プロシージャを探し、[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]の空の領域にドラッグします。

     自動生成された戻り値の型を使用して <xref:System.Data.Linq.DataContext> メソッドが作成され、**[メソッド]** ペインに表示されます。

#### <a name="to-create-datacontext-methods-that-have-the-return-type-of-an-entity-class"></a>エンティティ クラスを戻り値の型とする DataContext メソッドを作成するには

1. **サーバーエクスプローラー** / **データベースエクスプローラー**で、使用しているデータベースの [**ストアドプロシージャ**] ノードを展開します。

2. 目的のストアド プロシージャを探し、[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]の既存のエンティティ クラスにドラッグします。

     選択したエンティティ クラスを戻り値の型として <xref:System.Data.Linq.DataContext> メソッドが作成され、**[メソッド]** ペインに表示されます。

> [!NOTE]
> 既存のメソッドの戻り値の型を変更する方法の詳細については <xref:System.Data.Linq.DataContext> 、「 [方法: DataContext メソッドの戻り値の型を変更する (O/R デザイナー)](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md)」を参照してください。

## <a name="see-also"></a>参照
 [Visual Studio の DataContext メソッドの LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md) [(o/r デザイナー)](../data-tools/datacontext-methods-o-r-designer.md) [チュートリアル: LINQ to SQL クラスの作成 (o](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233) /r デザイナー) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655) [Visual Basic での linq の概要](https://msdn.microsoft.com/library/3047d86e-0d49-40e2-928b-dc02e46c7984)[方法: C# で linq クエリを記述](https://msdn.microsoft.com/library/45e47fcc-cfa1-4b72-b161-d038ae87bd23)する

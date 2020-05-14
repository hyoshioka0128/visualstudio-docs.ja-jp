---
title: '方法: O-R デザイナーで生成されたコードを拡張する'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: d6d1122e-2f55-4607-8d8b-48c3c22600fb
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 588eb0f61dbc16fb1625752417ac5257bf48320f
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2020
ms.locfileid: "76113689"
---
# <a name="how-to-extend-code-generated-by-the-or-designer"></a>方法: O/R デザイナーで生成されたコードを拡張する
**O/R デザイナー**によって生成されるコードは、デザイナー画面でエンティティクラスやその他のオブジェクトに変更が加えられたときに再生成されます。 このコードの再生成により、通常、生成されたコードに追加したコードは、デザイナーがコードを再生成するときに上書きされます。 **O/R デザイナー**には、部分クラスファイルを生成する機能が用意されており、上書きされないコードを追加できます。 **O/R デザイナー**によって生成されるコードに独自のコードを追加する1つの例は、LINQ to SQL (エンティティ) クラスにデータ検証を追加することです。 詳細については、「[方法: エンティティクラスに検証を追加](../data-tools/how-to-add-validation-to-entity-classes.md)する」を参照してください。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="add-code-to-an-entity-class"></a>エンティティクラスへのコードの追加

### <a name="to-create-a-partial-class-and-add-code-to-an-entity-class"></a>部分クラスを作成し、エンティティ クラスにコードを追加するには

1. **O/R デザイナー**で新しい LINQ to SQL クラスファイル ( **.dbml**ファイル) を開くか、作成します。 (**ソリューションエクスプローラー**または**データベースエクスプローラー**で **.dbml**ファイルをダブルクリックします)。

2. **O/R デザイナー**で、検証を追加するクラスを右クリックして、 **[コードの表示]** をクリックします。

     コード エディターが開き、選択したエンティティ クラスの部分クラスが表示されます。

3. エンティティ クラスの部分クラス宣言内にコードを追加します。

## <a name="add-code-to-a-datacontext"></a>DataContext へのコードの追加

### <a name="to-create-a-partial-class-and-add-code-to-a-datacontext"></a>部分クラスを作成し、DataContext にコードを追加するには

1. **O/R デザイナー**で新しい LINQ to SQL クラスファイル ( **.dbml**ファイル) を開くか、作成します。 (**ソリューションエクスプローラー**または**データベースエクスプローラー**で **.dbml**ファイルをダブルクリックします)。

2. **O/R デザイナー**で、デザイナーの空の領域を右クリックし、[コードの**表示**] をクリックします。

     コード エディターが開き、DataContext の部分クラスが表示されます。

3. DataContext の部分クラス宣言内にコードを追加します。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [チュートリアル: LINQ to SQL クラスの作成 (O-R デザイナー)](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)

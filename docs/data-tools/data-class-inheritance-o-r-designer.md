---
title: データ クラスの継承 (O/R デザイナー)
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: af32653c-f4e6-4217-8c5a-e32b322b4918
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 7172c868780aec61de8688614fbb93627dc23bf5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85462396"
---
# <a name="data-class-inheritance-or-designer"></a>データ クラスの継承 (O/R デザイナー)

他のオブジェクトと同様に、LINQ to SQL クラスは継承を使用し、他のクラスから派生させることができます。 コードでは、あるクラスが別のクラスから継承されていることを宣言することによって、オブジェクト間の継承関係を指定できます。 データベースでは、継承関係が複数の方法で作成されます。 **オブジェクトリレーショナルデザイナー** (**O/R デザイナー**) は、リレーショナルシステムに実装されることが多いため、単一テーブル継承の概念をサポートしています。

単一テーブル継承では、基本クラスと派生クラスの両方の列が入った単一データベース テーブルが関係します。 リレーショナル データでは、識別子の列に、特定のレコードが属するクラスを決定する値が含まれます。 たとえば、 `Persons` 会社によって採用されたすべてのユーザーを含むテーブルがあるとします。 従業員の人もいれば、管理者の人もいます。 このテーブルには、 `Persons` という名前の列が含まれています。この列の `Type` 値は、マネージャーの場合は1、従業員の場合は2になります。 `Type`列は識別子列です。 このシナリオでは、従業員のサブクラスを作成し、値が2のレコードのみをクラスに設定でき `Type` ます。

[!INCLUDE[vs_ordesigner_short](../data-tools/includes/vs_ordesigner_short_md.md)] を使用してエンティティ クラスでの継承を構成する場合、継承データを含んだ単一テーブルをデザイナーに、継承階層のクラスごとに 1 回、計 2 回ドラッグします。 デザイナーにテーブルを追加した後、**[オブジェクト リレーショナル デザイナー]** ツールボックスでそれらのテーブルを継承項目に接続して、**[プロパティ]** ウィンドウで 4 つの継承プロパティを設定します。

## <a name="inheritance-properties"></a>継承プロパティ

継承プロパティとその説明については、次の表を参照してください。

|プロパティ|説明|
|--------------|-----------------|
|**識別子プロパティ**|現在のレコードが属するクラスを判別するプロパティ (列にマップされる)。|
|**基本クラスの識別子の値**|レコードが基本クラスであることを判断する値 ( **識別子プロパティ**として指定された列)。|
|**派生クラスの識別子の値**|レコードが派生クラスであることを決定する値 ( **識別子プロパティ**として指定されたプロパティ)。|
|**継承の既定値**|**識別子プロパティ**として指定されたプロパティの値が、**基本クラスの識別子**の値または**派生クラスの識別子の値**のいずれとも一致しない場合に設定されるクラス。|

継承を使用し、リレーショナル データに対応するオブジェクト モデルの作成は、混乱しやすい場合があります。 このトピックでは、継承を構成する場合に必要な基本的な概念と個々のプロパティについて説明します。 次のトピックでは、 **O/R デザイナー**を使用して継承を構成する方法について、より明確に説明します。

|トピック|説明|
|-----------|-----------------|
|[方法: O/R デザイナーを使用して継承を構成する](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md)|**O/R デザイナー**を使用して、単一テーブル継承を使用するエンティティクラスを構成する方法について説明します。|
|[チュートリアル: 単一テーブル継承を使用した LINQ to SQL クラスの作成 (O/R デザイナー)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)|**O/R デザイナー**を使用して、単一テーブル継承を使用するエンティティクラスを構成する手順について説明します。|

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [チュートリアル: LINQ to SQL クラスの作成 (O-R デザイナー)](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [チュートリアル: 単一テーブル継承を使用した LINQ to SQL クラスの作成 (O/R デザイナー)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)
- [はじめに](/dotnet/framework/data/adonet/sql/linq/getting-started)
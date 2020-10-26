---
title: データクラスの継承 (O/R デザイナー) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: af32653c-f4e6-4217-8c5a-e32b322b4918
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9e7dfc2b1137b30a03425f663d70e12c528dad39
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657407"
---
# <a name="data-class-inheritance-or-designer"></a>データ クラスの継承 (O/R デザイナー)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] クラスは、他のオブジェクトと同様に、継承を使用して他のクラスから派生できます。 コードでは、あるクラスが別のクラスから継承されていることを宣言することによって、オブジェクト間の継承関係を指定できます。 データベースでは、継承関係が複数の方法で作成されます。 [!INCLUDE[vs_ordesigner_long](../includes/vs-ordesigner-long-md.md)] ([!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]) では、一般にリレーショナル システムで実装されている単一テーブル継承の概念がサポートされます。

 単一テーブル継承では、基本クラスと派生クラスの両方の列が入った単一データベース テーブルが関係します。 リレーショナル データでは、識別子の列に、特定のレコードが属するクラスを決定する値が含まれます。 たとえば、会社に採用されたすべての人を含む Persons テーブルについて考えます。 従業員の人もいれば、管理者の人もいます。 Persons テーブルには、Type という列があり、この列の値は管理者は 1、従業員は 2 です。 Type 列は識別子の列です。 このシナリオでは、従業員のサブクラスを作成して、そのクラスには Type の値が 2 であるレコードだけを入れるようにすることができます。

 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] を使用してエンティティ クラスでの継承を構成する場合、継承データを含んだ単一テーブルをデザイナーに、継承階層のクラスごとに 1 回、計 2 回ドラッグします。 デザイナーにテーブルを追加した後、**[オブジェクト リレーショナル デザイナー]** ツールボックスでそれらのテーブルを継承項目に接続して、**[プロパティ]** ウィンドウで 4 つの継承プロパティを設定します。

## <a name="inheritance-properties"></a>継承プロパティ
 継承プロパティとその説明については、次の表を参照してください。

|プロパティ|説明|
|--------------|-----------------|
|識別子プロパティ|現在のレコードが属するクラスを判別するプロパティ (列にマップされる)。|
|基本クラスの識別子の値|レコードが基本クラスに属することを決定する、識別子プロパティとして指定された列の値。|
|派生クラスの識別子の値|レコードが派生クラスに属することを決定する、識別子プロパティとして指定されたプロパティの値。|
|継承の既定値|**識別子プロパティ**として指定されたプロパティの値が、**基本クラスの識別子**の値または**派生クラスの識別子の値**のいずれとも一致しない場合に設定されるクラス。|

 継承を使用し、リレーショナル データに対応するオブジェクト モデルの作成は、混乱しやすい場合があります。 このトピックでは、継承を構成する場合に必要な基本的な概念と個々のプロパティについて説明します。 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] による継承の構成方法についての詳しい説明については、以下のトピックを参照してください。

|トピック|説明|
|-----------|-----------------|
|[方法: O/R デザイナーを使用して継承を構成する](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md)|[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]を使用して単一テーブル継承を使用するエンティティ クラスを構成する方法について説明します。|
|[チュートリアル: 単一テーブル継承を使用した LINQ to SQL クラスの作成 (O/R デザイナー)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)|[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]を使用して単一テーブル継承を使用するエンティティ クラスを構成するための詳細な手順を説明します。|

## <a name="see-also"></a>参照
 [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)[チュートリアル: LINQ to SQL クラスの作成 (o-r デザイナー)](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233) [チュートリアル: 単一テーブル継承を使用した LINQ to SQL クラスの作成 (o/r デザイナー)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md) [はじめに](https://msdn.microsoft.com/library/db8a557a-fef8-4f4f-bb91-8cff7250ee25)

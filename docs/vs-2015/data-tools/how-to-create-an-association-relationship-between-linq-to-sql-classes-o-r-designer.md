---
title: '方法: LINQ to SQL クラス間の関連付け (リレーションシップ) を作成する (O/R デザイナー) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 56133e65-81f3-44c3-bc28-ffdd0671a0d2
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9c2f6f6f65410336eacf72967c8360a56e8fa5ca
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72609999"
---
# <a name="how-to-create-an-association-relationship-between-linq-to-sql-classes-or-designer"></a>方法: LINQ to SQL クラス間の関連付け (リレーションシップ) を作成する (O/R デザイナー)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] のエンティティ クラス間の関連付けは、データベース内のテーブル間の関連付けに似ています。 **[関連付けエディター]** ダイアログ ボックスを使用することで、エンティティ クラス間の関連付けを作成できます。

 **[関連付けエディター]** ダイアログ ボックスを使用して関連付けを作成するときは、親クラスと子クラスを選択する必要があります。 親クラスは、主キーを含むエンティティ クラスであり、子クラスは、外部キーを含むエンティティ クラスです。 たとえば、Northwind の Customers テーブルと Orders テーブルにマップされるエンティティ クラスが作成された場合は、Customer クラスが親クラスであり、Order クラスが子クラスです。

> [!NOTE]
> **サーバーエクスプローラー** / **データベースエクスプローラー**から () にテーブルをドラッグすると [!INCLUDE[vs_ordesigner_long](../includes/vs-ordesigner-long-md.md)] [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 、データベース内の既存の外部キーリレーションシップに基づいてアソシエーションが自動的に作成されます。

 関連付けを作成した後、O/R デザイナーでアソシエーションを選択すると、[ **プロパティ** ] ウィンドウに構成可能なプロパティがいくつかあります。 (関連付けは関連するクラス間の線です)。次の表は、関連付けのプロパティの説明を示しています。

|プロパティ|説明|
|--------------|-----------------|
|**カーディナリティ**|関連付けが 1 対多と 1 対 1 のどちらであるかを制御します。|
|**子プロパティ**|コレクションのプロパティを親に作成するか、子レコードへの参照を関連付けの外部キー側に作成するかを指定します。 たとえば、Customer と Order の間の関連付けでは、 **子プロパティ** が **True**に設定されている場合、Orders という名前のプロパティが親クラスに作成されます。|
|**Parent プロパティ**|関連付けられている親クラスを参照する子クラスのプロパティです。 たとえば、Customer と Order の間の関連付けでは、注文に関連付けられている顧客を参照する Customer という名前のプロパティが Order クラスに作成されます。|
|**関与のプロパティ**|関連付けのプロパティを表示し、**[関連付けエディター]** ダイアログ ボックスを再び開く**省略記号**ボタン (...) が用意されています。|
|**[一意]**|外部ターゲット列に一意性の制約があるかどうかを示します。|

### <a name="to-create-an-association-between-entity-classes"></a>エンティティ クラス間に関連付けを作成するには

1. 関連付けの親クラスを表すエンティティ クラスを右クリックし、**[追加]** をポイントして、**[関連付け]** をクリックします。

2. **[関連付けエディター]** ダイアログ ボックスで、正しい**親クラス**が選択されていることを確認します。

3. コンボ ボックスで**子クラス**を選択します。

4. クラスに関連する **[関連付けのプロパティ]** を選択します。 通常、これはデータベースで定義されている外部キー リレーションシップにマップされます。 たとえば、Customers と Orders の関連付けでは、 **関連付けプロパティ** は各クラスの CustomerID です。

5. **[OK]** をクリックして、関連付けを作成します。

## <a name="see-also"></a>参照
 [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)[チュートリアル: LINQ to SQL クラスの作成 (o/r デザイナー)](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655) [DataContext メソッド (o/r デザイナー)](../data-tools/datacontext-methods-o-r-designer.md) [方法: 主キーを表す](https://msdn.microsoft.com/library/63c65289-6539-42b2-8493-891c232018fa)

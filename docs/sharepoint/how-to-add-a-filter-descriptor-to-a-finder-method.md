---
title: '方法: Finder メソッドにフィルター記述子を追加する |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], filter descriptors
- Business Data Connectivity service [SharePoint development in Visual Studio], add a filter
- BDC [SharePoint development in Visual Studio], add a filter
- BDC [SharePoint development in Visual Studio], filter descriptors
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 228afb2f49f4d528fa9b806e9bf8d2531f7de901
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016740"
---
# <a name="how-to-add-a-filter-descriptor-to-a-finder-method"></a>方法: Finder メソッドにフィルター記述子を追加する
  フィルター記述子を使用すると、モデルのコンシューマーは、実行前に値をメソッドに渡すことができます。 詳細については、「[ビジネスデータ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)」を参照してください。

 一般的なシナリオの1つは、SharePoint のユーザーが、いくつかの条件に一致する外部コンテンツタイプのインスタンスを取得することです。 このシナリオをサポートするには、Finder メソッドにフィルター記述子を追加します。

### <a name="to-add-a-filter-descriptor-to-a-finder-method"></a>Finder メソッドにフィルター記述子を追加するには

1. [ **BDC メソッドの詳細**] ウィンドウで、Finder メソッドのノードを展開し、[**パラメーター** ] ノードを展開して、入力パラメーターを追加します。 詳細については、「[方法: メソッドにパラメーターを追加](../sharepoint/how-to-add-a-parameter-to-a-method.md)する」を参照してください。

2. [**メソッドの詳細**] ウィンドウで、パラメーターの型記述子を選択します。

3. メニューバーで、[ **View**  >  **プロパティウィンドウ**の表示] を選択します。

4. [**プロパティ**] ウィンドウで、[**型名**] プロパティをフィルターに適したデータ型に設定します。

     たとえば、フィルターでは、注文日を使用して、メソッドによって返される販売注文の数を制限することができます。 このフィルターをサポートするには、型記述子の**Type Name**プロパティを**system.string に設定**する必要があります。

5. [**メソッドの詳細**] ウィンドウで、[**フィルター記述子**] ノードを展開します。

6. [**フィルター記述子の追加**] の一覧で、[**フィルター記述子の作成**] を選択します。

     新しいフィルター記述子が [**フィルター記述子**ノードの下に表示されます。

7. メニューバーで、[ **View**  >  **プロパティウィンドウ**の表示] を選択します。

8. [**プロパティ**] ウィンドウで、[**型**] プロパティを選択します。

9. **Type**プロパティに表示される一覧で、目的のフィルターパターンを選択します。

     たとえば、Finder メソッドで返される販売注文数を制限するために注文日を使用するフィルターを作成するには、[**比較**] を選択します。 比較フィルターにより、finder メソッドが特定の条件を満たすインスタンスだけを返すようにします。 各フィルター処理パターンの詳細については、「 [BDC でサポートされるフィルターの種類](/previous-versions/office/developer/sharepoint-2010/ee556392(v=office.14))」を参照してください。

10. [**プロパティ**] ウィンドウで、[**関連付けられている型記述子**] プロパティを選択します。

11. [**関連付けられている型記述子**] プロパティに対して表示される一覧で、この手順の前の手順で作成した型記述子を選択します。 これにより、フィルターは Finder メソッドの入力パラメーターに関連付けられます。

12. データを返す Finder メソッドにコードを追加します。 入力パラメーターは、select クエリの条件として使用できます。

     次の例では、指定された注文日を持つ販売注文を返します。

    > [!NOTE]
    > フィールドの値を `ServerName` サーバーの名前に置き換えます。

     [!code-csharp[SP_BDC#11](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/salesorderservice.cs#11)]
     [!code-vb[SP_BDC#11](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/salesorderservice.vb#11)]

## <a name="see-also"></a>関連項目
- [方法: Finder メソッドを追加する](../sharepoint/how-to-add-a-finder-method.md)
- [方法: 特定の Finder メソッドを追加する](../sharepoint/how-to-add-a-specific-finder-method.md)
- [方法: メソッドにパラメーターを追加する](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [方法: パラメーターの型記述子を定義する](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)
- [ビジネスデータ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)
- [SharePoint へのビジネスデータの統合](../sharepoint/integrating-business-data-into-sharepoint.md)

---
title: BDC モデルのデザインツールの概要 |Microsoft Docs
description: ビジネスデータ接続 (BDC) モデルで使用するためのデザインツールの概要について説明します。 Bdc デザイナー、[BDC メソッドの詳細] ウィンドウ、および BDC エクスプローラーについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.BDC.Method_Details
- VS.SharePointTools.BDC.Explorer
- VS.SharePointTools.BDC.Diagram
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], visual tools
- Business Data Connectivity service [SharePoint development in Visual Studio], visual tools
- Business Data Connectivity service [SharePoint development in Visual Studio], BDC Explorer
- BDC [SharePoint development in Visual Studio], method details
- Business Data Connectivity service [SharePoint development in Visual Studio], designer
- Business Data Connectivity service [SharePoint development in Visual Studio], method details
- BDC [SharePoint development in Visual Studio], BDC Explorer
- BDC [SharePoint development in Visual Studio], designer
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b398d9c00caf3a4fa2ca58bafa3273673a305859
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99851687"
---
# <a name="bdc-model-design-tools-overview"></a>BDC モデルのデザインツールの概要
  Bdc デザイナー、[ **Bdc メソッドの詳細** ] ウィンドウ、および **bdc エクスプローラー** を使用して、ビジネスデータ接続 (bdc) モデルを設計できます。

 **BDC エクスプローラー** を使用すると、モデルを参照したり、モデルを検索したり、型記述子を定義したりすることができます。

## <a name="bdc-designer"></a>BDC デザイナー
 BDC デザイナーを使用すると、モデル内のエンティティを定義し、相互の関係を視覚的に並べ替えることができます。 BDC デザイナーを使用して、次のタスクを実行します。

- エンティティをモデルに追加します。

- モデルからエンティティを削除します。

- エンティティ間のリレーションシップを定義します。

  BDC デザイナーを開くには、プロジェクト内のモデルファイルをダブルクリックするか、モデルファイルのショートカットメニューを開き、[ **開く**] をクリックします。 [**ツールボックス**] から **エンティティ** をデザイナーにドラッグまたはコピーして、エンティティをモデルに追加します。 2つのエンティティ間の関連付けを作成するには、**ツールボックス** で [**アソシエーション**] コントロールを選択し、最初のエンティティを選択して、2番目のエンティティを選択します。

## <a name="bdc-method-details-window"></a>BDC メソッドの詳細ウィンドウ
 [ **BDC メソッドの詳細** ] ウィンドウを使用すると、メソッドのパラメーター、インスタンス、およびフィルター記述子を定義できます。

 [ **BDC メソッドの詳細** ] ウィンドウで、Finder、特定の Finder、Creator、Updater、および削除子の各メソッドをすばやく生成できます。 これらのメソッドを生成すると、Visual Studio によって、パラメーター、インスタンス、型記述子などのメタデータがメソッドに追加されます。 このメタデータは、特定のシナリオを満たすように変更できます。

 [ **Bdc メソッドの詳細**] ウィンドウを開くには、メニューバーで [   >  **その他の Windows**  >  **BDC メソッドの詳細** を表示] を選択します。

 [ **Bdc メソッドの詳細** ] ウィンドウでメソッドを表示するには、bdc デザイナーでエンティティを選択します。 選択したエンティティのメソッドが [ **BDC メソッドの詳細** ] ウィンドウに表示されます。 BDC デザイナーでエンティティを選択しない場合、[ **Bdc メソッドの詳細** ] ウィンドウに情報は表示されません。

 [ **BDC メソッドの詳細** ] ウィンドウでノードを展開するか折りたたんで、パラメーター、インスタンス、およびフィルター記述子を定義します。 **BDC エクスプローラー** を使用して、型記述子を定義します。

## <a name="bdc-explorer"></a>BDC エクスプローラー
 **BDC エクスプローラー** には、モデルを構成する要素が表示されます。 **Bdc エクスプローラー** を開くには、メニューバーで [   >  **その他の Windows**  >  **BDC エクスプローラー** の表示] を選択します。 モデルを参照するには、 **BDC エクスプローラー** で [ノード] を展開します。 各ノードは、モデルファイルの XML 内の要素を表します。

 **BDC エクスプローラー** でノードを選択すると、選択した各ノードのプロパティが [**プロパティ**] ウィンドウに表示されます。 これらのプロパティの多くは、モデルファイルの属性に対応しています。 **BDC エクスプローラー** の上部にある [検索] ボックスを使用して、モデルを検索できます。

> [!NOTE]
> **BDC エクスプローラー** には、識別子、カスタムプロパティ、ローカライズされた文字列、関連付けグループ、アクション、フィルター記述子、アクション制御リスト、および既定のパラメーター値は表示されません。

### <a name="define-type-descriptors"></a>型記述子の定義
 **BDC エクスプローラー** を使用して、型記述子を定義します。 BDC エクスプローラーでは、型記述子を1回定義するだけで、モデル内の他の場所でその型記述子を再利用できます。 これを実現するには、型記述子をコピーし、他のパラメーターまたは型記述子に貼り付けます。

> [!NOTE]
> 元の型記述子を変更しても、その型記述子のコピーには影響しません。

 詳細については、「 [方法: パラメーターの型記述子を定義](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)する」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: BDC モデルを作成する](../sharepoint/how-to-create-a-bdc-model.md)
- [方法: モデルにエンティティを追加する](../sharepoint/how-to-add-an-entity-to-a-model.md)
- [方法: Finder メソッドを追加する](../sharepoint/how-to-add-a-finder-method.md)
- [方法: 特定の Finder メソッドを追加する](../sharepoint/how-to-add-a-specific-finder-method.md)
- [方法: Creator メソッドを追加する](../sharepoint/how-to-add-a-creator-method.md)
- [方法: 削除子メソッドを追加する](../sharepoint/how-to-add-a-deleter-method.md)
- [方法: Updater メソッドを追加する](../sharepoint/how-to-add-an-updater-method.md)
- [エンティティ間の関連付けを作成する](../sharepoint/creating-an-association-between-entities.md)
- [チュートリアル: ビジネスデータを使用した SharePoint での外部リストの作成](../sharepoint/walkthrough-creating-an-external-list-in-sharepoint-by-using-business-data.md)
- [SharePoint へのビジネス データの統合](../sharepoint/integrating-business-data-into-sharepoint.md)
- [ビジネスデータ接続モデルの作成](../sharepoint/creating-a-business-data-connectivity-model.md)
- [ビジネスデータ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)

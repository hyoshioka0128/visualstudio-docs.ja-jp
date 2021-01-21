---
title: '方法: メソッドインスタンスを定義する |Microsoft Docs'
description: Business data connectivity (BDC) モデルでメソッドのメソッドインスタンスを定義する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], method instance
- BDC [SharePoint development in Visual Studio], method instance
- BDC [SharePoint development in Visual Studio], method
- Business Data Connectivity service [SharePoint development in Visual Studio], method
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 751683873d98e6c7aedc7228e0a91fb59117993b
ms.sourcegitcommit: 86e98df462b574ade66392f8760da638fe455aa0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2020
ms.locfileid: "94903625"
---
# <a name="how-to-define-a-method-instance"></a>方法: メソッドインスタンスを定義する
  モデル内のすべてのメソッドに対して、少なくとも1つのメソッドインスタンスを定義する必要があります。

 [ **BDC メソッドの詳細** ] ウィンドウを使用して、メソッドインスタンスを追加します。 メソッドインスタンスを追加すると、Visual Studio によっ `<MethodInstance>` て、プロジェクトのモデルファイルの XML に要素が追加されます。 要素の属性の詳細については `<MethodInstance>` 、「 [MethodInstance](/previous-versions/office/developer/sharepoint-2010/ee556838(v=office.14))」を参照してください。

### <a name="to-define-a-method-instance"></a>メソッドインスタンスを定義するには

1. [ **BDC メソッドの詳細** ] ウィンドウで、メソッドのノードを展開し、[ **インスタンス** ] ノードを展開します。

2. [ **メソッドインスタンスの追加** ] ボックスの一覧で、[ **Finder インスタンスの作成**] を選択します。

     **インスタンス** ノードの下に新しいメソッドインスタンスが表示されます。

3. メニューバーで、[ **View**  >  **プロパティウィンドウ** の表示] を選択します。

4. [ **プロパティ** ] ウィンドウで、メソッドインスタンスのプロパティを設定します。 各プロパティの詳細については、「 [MethodInstance](/previous-versions/office/developer/sharepoint-2010/ee556838(v=office.14))」を参照してください。

## <a name="see-also"></a>関連項目
- [BDC モデルのデザインツールの概要](../sharepoint/bdc-model-design-tools-overview.md)
- [方法: モデルにエンティティを追加する](../sharepoint/how-to-add-an-entity-to-a-model.md)
- [方法: メソッドにパラメーターを追加する](../sharepoint/how-to-add-a-parameter-to-a-method.md)
- [方法: パラメーターの型記述子を定義する](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)
- [ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)

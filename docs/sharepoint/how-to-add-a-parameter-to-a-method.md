---
title: '方法: メソッドにパラメーターを追加する |Microsoft Docs'
description: ビジネスデータ接続 (BDC) メソッドにパラメーターを追加する方法を理解します。これにより、メソッドに情報を渡したり、メソッドから情報を返したりできます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], adding a method to a parameter
- Business Data Connectivity service [SharePoint development in Visual Studio], parameter
- BDC [SharePoint development in Visual Studio], adding a method to a parameter
- BDC [SharePoint development in Visual Studio], parameter
- Business Data Connectivity service [SharePoint development in Visual Studio], method parameters
- BDC [SharePoint development in Visual Studio], method parameters
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 179109ff4c0def002dac45887fe9491196a70d3e
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "96915402"
---
# <a name="how-to-add-a-parameter-to-a-method"></a>方法: メソッドにパラメーターを追加する
  パラメーターを使用して、メソッドに情報を渡すか、メソッドから情報を返します。 すべてのメソッドには、少なくとも1つのパラメーターが必要です。 作成するメソッドの種類をサポートするパラメーターをデザインする方法の詳細については、「 [ビジネスデータ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)」を参照してください。

 メソッドにパラメーターを追加すると、Visual Studio によって、パラメーター要素がプロジェクトのモデルファイルの XML に追加されます。 Parameter 要素の属性の詳細については、「 [parameter](/previous-versions/office/developer/sharepoint-2010/ee557705(v=office.14))」を参照してください。

### <a name="to-add-a-parameter-to-a-method"></a>メソッドにパラメーターを追加するには

1. メソッドをエンティティに追加します。

2. メニューバーで、[ **View**  >  **その他の Windows**  >  **BDC メソッドの詳細** を表示] を選択します。

     [ **BDC メソッドの詳細** ] ウィンドウが開きます。 詳細については、「 [BDC モデルデザインツールの概要](../sharepoint/bdc-model-design-tools-overview.md)」を参照してください。

3. [ **BDC メソッドの詳細** ] ウィンドウで、メソッドのノードを展開し、[ **パラメーター** ] ノードを展開します。

4. [ **パラメーターの追加** ] ボックスの一覧で、[ **パラメーターの作成**] を選択します。

     [ **パラメーター** ノードの下に新しいパラメーターが表示されます。

5. メニューバーで、[ **View**  >  **プロパティウィンドウ** の表示] を選択します。

6. [ **プロパティ** ] ウィンドウで、[ **名前** ] プロパティを意味のある任意の名前に設定します。 たとえば、メソッドが顧客を返す場合は、メソッドに **Getcustomers** という名前を指定できます。

7. [ **BDC メソッドの詳細** ] ウィンドウで、パラメーターの方向に対して表示される一覧を開き、[ **In**]、[ **InOut**]、[ **Out**]、または [ **戻る**] を選択します。

     作成する type メソッドに対して選択する方向の詳細については、「 [ビジネスデータ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)」を参照してください。

8. パラメーターの型記述子を変更します。 詳細については、「 [方法: パラメーターの型記述子を定義](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)する」を参照してください。

## <a name="see-also"></a>関連項目
- [BDC モデルのデザインツールの概要](../sharepoint/bdc-model-design-tools-overview.md)
- [方法: モデルにエンティティを追加する](../sharepoint/how-to-add-an-entity-to-a-model.md)
- [方法: パラメーターの型記述子を定義する](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)
- [方法: メソッドインスタンスを定義する](../sharepoint/how-to-define-a-method-instance.md)
- [ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)

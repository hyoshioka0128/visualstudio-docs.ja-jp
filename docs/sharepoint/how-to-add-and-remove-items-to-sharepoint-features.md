---
title: SharePoint 機能に項目を追加または削除する方法 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.FeatureDesigner
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, features
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 27c6ebfb0b0cdbff0a184859ffa2a73acab809c1
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014524"
---
# <a name="how-to-add-and-remove-items-to-sharepoint-features"></a>方法: SharePoint 機能に項目を追加および削除する
  SharePoint ソリューションを作成すると、Visual Studio によって既定の SharePoint プロジェクト項目が機能に追加されます。 配置する前に、sharepoint プロジェクト項目を追加および削除して、SharePoint 機能を変更することができます。

## <a name="add-sharepoint-project-items-to-a-feature"></a>SharePoint プロジェクトアイテムをフィーチャーに追加する

#### <a name="to-add-sharepoint-project-items-with-the-feature-designer"></a>フィーチャーデザイナーを使用して SharePoint プロジェクト項目を追加するには

1. フィーチャーデザイナーを開きます。

    詳細については、「[方法: SharePoint 機能をカスタマイズ](../sharepoint/how-to-customize-a-sharepoint-feature.md)する」を参照してください。

2. 次の手順の1つ以上を実行して、**ソリューション**リストの項目から機能一覧の**項目**に1つ以上の項目を追加します。

   - 追加する各項目をダブルクリックします。

   - 追加する項目を選択し、[**追加**] ボタン (>) を選択します。

   - [**すべて追加**] ボタン (>>) を選択します。

     SharePoint プロジェクトアイテムは、機能一覧の**アイテム**に表示されます。

## <a name="remove-sharepoint-project-items-from-a-feature"></a>フィーチャーから SharePoint プロジェクトアイテムを削除する

#### <a name="to-remove-sharepoint-items-with-the-feature-designer"></a>フィーチャーデザイナーを使用して SharePoint アイテムを削除するには

1. 機能一覧の**項目**で1つ以上の項目を選択します。

2. [**削除**] ボタン (<) を選択して、一度に1つの項目を削除するか、[**すべて削除**] ボタン (<<) を選択してすべての項目を削除します。

     SharePoint プロジェクトアイテムは、ソリューションリストの**アイテム**に表示されます。

## <a name="see-also"></a>関連項目
- [SharePoint 機能の作成](../sharepoint/creating-sharepoint-features.md)
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)

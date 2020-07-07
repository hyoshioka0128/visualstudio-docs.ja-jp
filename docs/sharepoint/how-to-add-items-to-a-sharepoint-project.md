---
title: '方法: SharePoint プロジェクトに項目を追加する |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, adding items
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1f7a36591d94e846a0024bce8c5d0b618479e647
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014700"
---
# <a name="how-to-add-items-to-a-sharepoint-project"></a>方法: SharePoint プロジェクトに項目を追加する
  SharePoint ソリューションには1つ以上のプロジェクトが含まれており、それぞれに複数の SharePoint プロジェクト項目が含まれています。 SharePoint ソリューションを開いたり作成したりした後、これらのプロジェクトに新規または既存の項目を追加できます。 たとえば、新しいワークフロープロジェクトには default.aspx という名前の既定のフォームが付属していますが、そのフォームを新しい形式または別の形式に置き換えることも、別の ASPX フォームを追加することもできます。

### <a name="to-add-a-new-project-item-to-a-sharepoint-solution"></a>SharePoint ソリューションに新しいプロジェクトアイテムを追加するには

1. で [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 、SharePoint ソリューションを開くか作成します。

2. **ソリューションエクスプローラー**で、プロジェクトのノードを選択します。

3. メニューバーで、[**プロジェクト**] [  >  **新しい項目の追加**] の順に選択し、[**新しい項目の追加**] ダイアログボックスを表示します。

4. [**インストールされたテンプレート**] の一覧で [ **SharePoint** ] ノードを展開し、[ **2010** ] ノードを選択します。

5. プロジェクト項目テンプレートの一覧で、テンプレートを選択します。

6. [**名前**] テキストボックスに名前を入力し、[ **OK** ] をクリックします。

### <a name="to-add-an-existing-project-item-to-a-sharepoint-solution"></a>既存のプロジェクトアイテムを SharePoint ソリューションに追加するには

1. で [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 、SharePoint ソリューションを開くか作成します。

2. **ソリューションエクスプローラー**で、プロジェクトのノードを選択します。

3. メニューバーで、[**プロジェクト**] [既存項目の追加] の順に選択し  >  **Add Existing Item** 、[**既存項目の追加**] ダイアログボックスを表示します。

4. 追加する項目が含まれているフォルダーを参照して選択し、[**追加**] ボタンをクリックします。

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクトとプロジェクト項目テンプレート](../sharepoint/sharepoint-project-and-project-item-templates.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)

---
title: 'パッケージデザイナー: 機能と項目をパッケージに追加 & 削除する'
titleSuffix: ''
description: Visual Studio のパッケージデザイナーを使用して、SharePoint パッケージに機能と項目を追加および削除する方法を確認します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.PackageDesignerDesign
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 45c8da30a059599a291b18155dc48c4521d6d875
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "96914947"
---
# <a name="how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer"></a>方法: パッケージデザイナーを使用してパッケージに機能と項目を追加および削除する
  SharePoint ソリューションを作成すると、Visual Studio によって既定の SharePoint 機能がソリューションのパッケージに追加されます。 最終的な配置の前に、sharepoint プロジェクトの項目と機能を追加および削除して、SharePoint パッケージを変更することができます。

 または、パッケージングエクスプローラーを使用して、SharePoint プロジェクト項目を追加および削除することもできます。 また、パッケージ (.wsp) に配置される SharePoint プロジェクトアイテムとフィーチャーの階層を表示および変更することもできます。 詳細については、「 [方法: パッケージングエクスプローラーを使用して、パッケージに機能と項目を追加および削除する](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer.md)」を参照してください。

## <a name="add-features-to-a-sharepoint-package"></a>SharePoint パッケージへの機能の追加
 パッケージデザイナーを使用して、SharePoint パッケージに機能を追加できます。

#### <a name="to-add-sharepoint-features-with-the-package-designer"></a>パッケージデザイナーを使用して SharePoint 機能を追加するには

1. **パッケージデザイナー** を開きます。

    詳細については、「 [方法: SharePoint ソリューションパッケージをカスタマイズ](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)する」を参照してください。

2. 次の手順の1つ以上を実行して、SharePoint 機能を1つ以上追加します。

   1. 追加する **ソリューションリスト内の項目** の各項目をダブルクリックします。

   2. 追加する項目を選択し、[ **追加** ] ボタン (>) を選択します。

   3. すべての項目を一度に追加するには、[ **すべて追加** ] ボタン (>>) を選択します。

      たとえば、[ **ソリューション** ] リストの項目内の項目をダブルクリックして、[ **パッケージ** ] の一覧の項目に追加することができます。

      SharePoint プロジェクトのアイテムとフィーチャーが、パッケージの一覧の **アイテム** に表示されます。

## <a name="remove-features-from-a-sharepoint-package"></a>SharePoint パッケージから機能を削除する
 パッケージデザイナーを使用して、SharePoint パッケージの機能を削除できます。

#### <a name="to-remove-sharepoint-features-with-the-package-designer"></a>パッケージデザイナーで SharePoint の機能を削除するには

1. [ **パッケージ** ] ボックスの一覧で、削除する項目を選択し、[ **削除** (<)] ボタンを選択するか、[ **すべて削除** ] ボタン (<<) を選択してすべての項目を削除します。

     SharePoint アイテムは、ソリューションリストの **アイテム** に表示されます。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションパッケージの作成](../sharepoint/creating-sharepoint-solution-packages.md)
- [方法: SharePoint ソリューションパッケージをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [方法: パッケージを作成する](/previous-versions/ee231585(v=vs.110))
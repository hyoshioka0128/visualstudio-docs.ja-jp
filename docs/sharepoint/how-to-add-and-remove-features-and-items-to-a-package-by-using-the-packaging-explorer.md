---
title: 'パッケージングエクスプローラー: 項目 & パッケージに追加 & 削除'
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.PackagingExplorer
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
ms.openlocfilehash: c3ea7e30737855cbbb9434e8763f4903d80b82da
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014554"
---
# <a name="how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer"></a>方法: パッケージングエクスプローラーを使用してパッケージに機能と項目を追加および削除する
  SharePoint のアイテムとフィーチャーを配置するようにパッケージを構成するには、パッケージングエクスプローラーを使用します。 SharePoint プロジェクトの項目と機能は、.wsp ファイル内で調整できます。

 または、パッケージングデザイナーを使用して、機能を表示して順序を変更し、アクティベーションの順序を変更することもできます。 詳細については、「[方法: パッケージデザイナーを使用して、パッケージに機能と項目を追加および削除する](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)」を参照してください。

## <a name="open-the-packaging-explorer"></a>パッケージングエクスプローラーを開く
 Visual Studio ソリューションに少なくとも1つの SharePoint プロジェクトがある場合は、次の手順を使用して、パッケージングエクスプローラーを開くことができます。 また、機能またはパッケージデザイナーを表示すると、パッケージングエクスプローラーが自動的に開きます。 すべての機能とパッケージデザイナーを閉じた後、パッケージングエクスプローラーも閉じます。

#### <a name="to-open-the-packaging-explorer"></a>パッケージングエクスプローラーを開くには

1. メニューバーで、[ **View**  >  **他の Windows**  >  **パッケージエクスプローラー**を表示] を選択します。

     **パッケージングエクスプローラー**が [**ツールボックス**] に表示されます。

## <a name="adding-a-feature-to-a-package"></a>パッケージへの機能の追加
 パッケージングエクスプローラーを使用して、パッケージに新規および既存の機能を追加できます。

#### <a name="to-add-a-sharepoint-feature"></a>SharePoint 機能を追加するには

1. **パッケージングエクスプローラー**を開き、プロジェクトのショートカットメニューを開き、[機能の**追加**] を選択します。

#### <a name="to-move-an-existing-sharepoint-feature"></a>既存の SharePoint 機能を移動するには

1. **パッケージングエクスプローラー**を開き、次のいずれかの手順を実行します。

    - **フィーチャー**をあるプロジェクトから別のプロジェクトにドラッグします。

    - 機能のショートカットメニューを開き、[**切り取り**] を選択し、フィーチャーの移動先となるプロジェクトのショートカットメニューを開き、[**貼り付け**] を選択します。

    > [!NOTE]
    > ソリューションに複数の SharePoint プロジェクトがある場合は、この手順を使用します。

## <a name="validate-a-feature-or-package"></a>機能またはパッケージを検証する
 SharePoint の機能とパッケージで、ファイルを検証することで潜在的な問題を特定できます。 警告とエラーは、[出力] ウィンドウと [エラー一覧] ウィンドウに表示されます。

#### <a name="to-validate-a-sharepoint-feature-or-package"></a>SharePoint の機能またはパッケージを検証するには

1. **パッケージングエクスプローラー**を開きます。

2. 機能またはパッケージのショートカットメニューを開き、[**検証**] を選択します。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)

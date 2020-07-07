---
title: '方法: プロジェクト出力参照を追加する |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- project output references [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, project output references
- SharePoint development in Visual Studio, advanced packaging tools
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: bea0f39ae161d8b695f872cb634c35d0cb205c91
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016759"
---
# <a name="how-to-add-a-project-output-reference"></a>方法: プロジェクト出力参照を追加する
  SharePoint 以外のプロジェクトアセンブリ (または Silverlight プロジェクト内の .xap ファイル) を SharePoint に配置するには、プロジェクト出力参照として追加します。

 このプロセスでは、2つのプロジェクト間のソリューションビルド依存関係を作成します。 プロジェクト出力参照に関連付けられているプロジェクトは、SharePoint プロジェクトのビルドと配置の前にビルドされます。

### <a name="to-add-a-project-output-reference"></a>プロジェクト出力参照を追加するには

1. 少なくとも1つの SharePoint プロジェクトと SharePoint 以外のプロジェクトを含むソリューションを読み込みます。

2. **ソリューションエクスプローラー**で、SharePoint プロジェクトノード内の項目を選択します。

3. [**プロパティ**] ウィンドウで、[**プロジェクト出力参照**] プロパティを選択し、その横にある省略記号 (![ASP.NET Mobile Designer 楕円](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) ボタンを選択します。

4. [**プロジェクト出力参照**] ダイアログボックスで、[**追加**] をクリックします。

5. プロパティペインで、[**展開の種類**] プロパティの横にある矢印を選択し、参照している SharePoint 以外の項目 ( **elementfile**など) に適切な値を選択します。

6. [**プロジェクト名**] の横にある矢印をクリックし、SharePoint 以外のプロジェクトアイテムの名前を選択して、[ **OK** ] をクリックします。

## <a name="see-also"></a>関連項目
- [プロジェクト項目でのパッケージ化と配置の情報の提供](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)
- [方法: コントロールを安全なコントロールとしてマークする](../sharepoint/how-to-mark-controls-as-safe-controls.md)
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)

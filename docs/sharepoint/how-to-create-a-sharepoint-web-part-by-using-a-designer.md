---
title: '方法: デザイナーを使用して SharePoint Web パーツを作成する |Microsoft Docs'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Web Parts [SharePoint development in Visual Studio], designer
- Web Parts [SharePoint development in Visual Studio], adding
- Web Parts [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d19822237f61d5404f42e30078541a735eb206bc
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91584114"
---
# <a name="how-to-create-a-sharepoint-web-part-by-using-a-designer"></a>方法: デザイナーを使用して SharePoint Web パーツを作成する
  Web パーツを作成するには、SharePoint プロジェクトに **視覚的 Web パーツ** 項目を追加します。 これを行うと、Visual Studio で Visual Web Developer デザイナーが開きます。このデザイナーでは、コントロールとコードを Web パーツに追加できます。 視覚的 Web パーツは Web パーツと同じように機能します。 唯一の違いは、視覚的 Web パーツのデザインは Visual Web Developer デザイナーで行うことです。

### <a name="to-create-a-project-for-visual-web-parts"></a>視覚的 Web パーツのプロジェクトを作成するには

1. メニュー バーで、 **[ファイル]**  > **[新規作成]**  >  **[プロジェクト]** を選択します。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

2. [ **新しいプロジェクト** ] ダイアログボックスの [ **Visual C#** ] または [ **Visual Basic**] で、[ **Office/SharePoint** ] ノードを展開し、[ **sharepoint ソリューション** ] カテゴリを選択します。

3. プロジェクトテンプレートの一覧で、[ **SharePoint 2013-視覚的 Web パーツ**] を選択し、[ **OK** ] をクリックします。

     **SharePoint カスタマイズウィザード**が表示されます。

4. [ **デバッグのサイトとセキュリティレベルの指定** ] ページで、ローカルコンピューター上の SharePoint サイトの URL を指定し、[ **完了** ] をクリックします。

     **ソリューションエクスプローラー**では、web パーツが表示されます。 Visual Web Developer デザイナーで web パーツをデザインした後、指定したサイトでテストを行います。

### <a name="to-add-a-visual-web-part-to-an-existing-sharepoint-project"></a>既存の SharePoint プロジェクトに視覚的 Web パーツを追加するには

1. メニューバーで、[**プロジェクト**] [  >  **新しい項目の追加**] の順に選択します。

2. [ **新しい項目の追加** ] ダイアログボックスで、[ **Office/SharePoint** ] ノードを選択します。

3. プロジェクトテンプレートの一覧で [ **視覚的 Web パーツ**] を選択し、名前を「」にして、[ **追加** ] ボタンをクリックします。

     **ソリューションエクスプローラー**では、web パーツが表示されます。 Visual Web Developer デザイナーで web パーツをデザインした後、指定したサイトでテストを行います。

## <a name="see-also"></a>関連項目
- [SharePoint の Web パーツを作成する](../sharepoint/creating-web-parts-for-sharepoint.md)
- [方法: SharePoint Web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part.md)
- [チュートリアル: SharePoint の Web パーツの作成](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)
- [チュートリアル: デザイナーを使用した SharePoint の Web パーツの作成](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)

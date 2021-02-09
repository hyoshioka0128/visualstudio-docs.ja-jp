---
title: '方法: SharePoint Web パーツを作成する |Microsoft Docs'
description: Web パーツの作成とカスタマイズは、デザイナーを使用するか、任意の SharePoint プロジェクトに web パーツ項目を追加してから web パーツのコードファイルを編集することによって行います。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Web Parts [SharePoint development in Visual Studio], adding
- Web Parts [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f15cd788d19540bdea416b36ab0f8e8d8aa95e3a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99925601"
---
# <a name="how-to-create-a-sharepoint-web-part"></a>方法: SharePoint web パーツを作成する
  Web パーツを作成してカスタマイズするには、任意の SharePoint プロジェクトに **Web パーツ** 項目を追加してから、web パーツのコードファイルを編集するか、デザイナーを使用します。 詳細については、「 [方法: デザイナーを使用して SharePoint web パーツを作成](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)する」を参照してください。

### <a name="to-create-a-sharepoint-web-part"></a>SharePoint web パーツを作成するには

1. SharePoint プロジェクトを作成するか開きます。

     詳細については、「 [SharePoint プロジェクトとプロジェクト項目テンプレート](../sharepoint/sharepoint-project-and-project-item-templates.md)」を参照してください。

2. **ソリューションエクスプローラー** で SharePoint プロジェクトノードを選択し、[**プロジェクト**] [  >  **新しい項目の追加**] の順に選択します。

3. [ **新しい項目の追加** ] ダイアログボックスで、[ **SharePoint** ] ノードを展開し、[ **2010** ] ノードを選択します。

4. SharePoint テンプレートの一覧で、[ **Web パーツ**] を選択します。

5. [ **名前** ] ボックスに web パーツの名前を指定し、[ **追加** ] をクリックします。

     Web パーツが **ソリューションエクスプローラー** に表示されます。 Web パーツに含まれるファイルの詳細については、「 [SharePoint の web パーツを作成](../sharepoint/creating-web-parts-for-sharepoint.md)する」を参照してください。

6. **ソリューションエクスプローラー** で、先ほど作成した web パーツのコードファイルを開きます。

     たとえば、web パーツの名前が *WebPart1* の場合は、 *WebPart1* (Visual Basic) または *WebPart1.cs* (C# の場合) を開きます。

7. コード ファイルで、<xref:System.Web.UI.Control.CreateChildControls%2A> メソッドにコントロールを追加します。

     例については、「 [チュートリアル: SharePoint の web パーツを作成する](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint の Web パーツを作成する](../sharepoint/creating-web-parts-for-sharepoint.md)
- [方法: デザイナーを使用して SharePoint Web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)
- [チュートリアル: SharePoint の Web パーツの作成](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)
- [チュートリアル: デザイナーを使用した SharePoint の Web パーツの作成](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)

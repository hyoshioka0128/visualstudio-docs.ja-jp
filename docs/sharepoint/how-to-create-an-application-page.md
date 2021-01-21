---
title: '方法: アプリケーションページを作成する |Microsoft Docs'
description: 1つまたは複数の SharePoint サイトに対して、Visual Studio で ASP.NET web ページ (アプリケーションページとも呼ばれます) を作成します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application pages [SharePoint development in Visual Studio], adding
- application pages [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: df52ca75ef99fe98158cb5f874e59fe4ee0c47b4
ms.sourcegitcommit: ad2c820b280b523a7f7aef89742cdb719354748f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94849858"
---
# <a name="how-to-create-an-application-page"></a>方法: アプリケーション ページを作成する
  1つ以上の SharePoint サイトに対して ASP.NET web ページを作成できます。 SharePoint では、これらのページはアプリケーションページと呼ばれます。 サイトページとは異なり、アプリケーションページには、ページの背後で実行されるコードが含まれています。 詳細については、「 [SharePoint のアプリケーションページを作成](../sharepoint/creating-application-pages-for-sharepoint.md)する」を参照してください。

### <a name="to-create-an-application-page"></a>アプリケーション ページを作成するには

1. Visual Studio で、SharePoint プロジェクトを開くか作成します。

     詳細については、「 [SharePoint プロジェクトとプロジェクト項目テンプレート](../sharepoint/sharepoint-project-and-project-item-templates.md)」を参照してください。

2. **ソリューション エクスプローラー** で、プロジェクト ノードを選択します。

3. メニューバーで、[**プロジェクト**] [  >  **新しい項目の追加**] の順に選択します。

4. [ **新しい項目の追加** ] ダイアログボックスで、[ **SharePoint** ] ノードを展開し、[ **2010** ] 項目を選択します。

5. SharePoint テンプレートの一覧で、[ **アプリケーション] ページ** を選択します。

6. [ **名前** ] ボックスで、アプリケーションページの名前を指定し、[ **追加** ] をクリックします。

     複数のフォルダーとファイルがプロジェクトに追加されます。 これらのファイルの詳細については、「 [SharePoint のアプリケーションページを作成](../sharepoint/creating-application-pages-for-sharepoint.md)する」を参照してください。

     Visual Web Developer designer の **ソース** ビューでは、ASP.NET ページファイルが表示されます。 **ツールボックス** からコントロールを追加して、コンテンツプレースホルダーに配置することで、ページをデザインできます。 詳細については、「 [ソースビュー、Web ページデザイナー](/previous-versions/aspnet/ms178154\(v\=vs.100\))」を参照してください。

7. コントロールイベントを処理する場合は、アプリケーションページのコードファイルにコードを追加します。

     コードファイルは、プロジェクトの言語に応じて、ASP.NET ページファイルのノードを展開し、 *.cs* または *.vb* 拡張子を持つ場合に表示されます。 アプリケーションページを作成する方法のエンドツーエンドの例については、「 [チュートリアル: SharePoint アプリケーションの作成」ページ](../sharepoint/walkthrough-creating-a-sharepoint-application-page.md)を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint のアプリケーション ページの作成](../sharepoint/creating-application-pages-for-sharepoint.md)
- [チュートリアル: SharePoint アプリケーション ページの作成](../sharepoint/walkthrough-creating-a-sharepoint-application-page.md)

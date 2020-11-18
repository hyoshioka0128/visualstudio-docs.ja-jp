---
title: SharePoint 接続を追加または削除する方法 |Microsoft Docs
description: Visual Studio の [サーバーエクスプローラー] ウィンドウの [SharePoint 接続] ノードを使用して、SharePoint 接続を追加または削除します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, browsing SharePoint sites
- SharePoint development in Visual Studio, SharePoint Connections
- SharePoint Connections [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b898dd0f9327c7589d0dac3436aec0299009221d
ms.sourcegitcommit: ad2c820b280b523a7f7aef89742cdb719354748f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94850716"
---
# <a name="how-to-add-or-remove-sharepoint-connections"></a>方法: SharePoint 接続を追加または削除する
  サーバーエクスプローラーを使用すると、データ接続だけでなく SharePoint サイトを参照することもできます。 ただし、SharePoint サイトのコンテンツを参照するには、sharepoint の [ **接続** ] ノードに sharepoint サイトを追加する必要があります。

### <a name="to-add-a-sharepoint-site-to-the-sharepoint-connections-node"></a>Sharepoint サイトを SharePoint 接続ノードに追加するには

1. メニューバーで、[ **表示**]、[ **サーバーエクスプローラー**] の順に選択します。

2. **サーバーエクスプローラー** で、[ **sharepoint 接続**] ノードを選択し、メニューバーで [**ツール**] [  >  **sharepoint 接続の追加**] の順に選択します。

3. [ **Sharepoint 接続の追加** ] ボックスに、sharepoint サイトのを入力します (例については、「」を入力し [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] http://testserver/sites/unittests) ます)。

### <a name="to-delete-a-sharepoint-site-from-the-sharepoint-connections-node"></a>Sharepoint 接続ノードから SharePoint サイトを削除するには

1. メニューバーで [ **表示**] を選択し、[ **サーバーエクスプローラー** ] をクリックして **サーバーエクスプローラー** を開きます。

2. [ **Sharepoint 接続** ] ノードを展開して、 **サーバーエクスプローラー** から削除する sharepoint サイトを表示します。

3. サイトを選択し、メニューバーで [削除の **編集**] を選択し  >  **Delete** ます。

    > [!NOTE]
    > この手順では、基になるサイトは削除されません。 **サーバーエクスプローラー** からの接続のみが削除されます。

## <a name="see-also"></a>関連項目
- [サーバー エクスプローラーを使用して SharePoint 接続を参照する](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)

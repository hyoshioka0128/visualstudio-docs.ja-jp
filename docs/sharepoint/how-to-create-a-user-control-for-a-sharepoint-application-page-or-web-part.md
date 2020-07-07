---
title: SharePoint アプリページまたは web パーツのユーザーコントロールを作成する
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- user controls [SharePoint development in Visual Studio], creating
- user controls [SharePoint development in Visual Studio], adding
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2fbf1b646ae9e7fb697fcab93adfb8661a4372c6
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016974"
---
# <a name="how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part"></a>方法: SharePoint アプリケーションページまたは web パーツのユーザーコントロールを作成する
  SharePoint ソリューション向けの独自の機能を備えたカスタム ユーザー コントロールを作成し、その機能をプロジェクト内で再利用することができます。 ユーザー コントロールは、Web パーツまたはアプリケーション ページに含めることができます。他の ASP.NET コントロールや SharePoint コントロールを追加し、コントロールのプロパティとメソッドを定義することもできます。 ユーザーコントロールの詳細については、「SharePoint で web パーツまたはアプリケーションページと[ユーザーコントロールおよびサーバーコントロール](https://blogs.msdn.microsoft.com/kaevans/2011/04/28/user-controls-and-server-controls-in-sharepoint/)[の再利用可能なコントロールを作成](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)する」を参照してください。

### <a name="to-create-a-user-control-for-sharepoint"></a>SharePoint のユーザー コントロールを作成するには

1. Visual Studio で、SharePoint プロジェクトを開くか作成します。

     「 [SharePoint プロジェクトとプロジェクト項目テンプレート」を](../sharepoint/sharepoint-project-and-project-item-templates.md)参照してください。

2. **ソリューション エクスプローラー**で、プロジェクト ノードを選択します。

3. メニューバーで、[**プロジェクト**] [  >  **新しい項目の追加**] の順に選択します。

     **[新しい項目の追加]** ダイアログ ボックスが開きます。

4. [**インストール済み**] ウィンドウで、[ **Office/SharePoint** ] ノードを選択します。

5. SharePoint テンプレートの一覧で、[**ユーザーコントロール (ファームソリューションのみ)**] を選択します。

    > [!NOTE]
    > ユーザー コントロールはファーム ソリューションでのみ機能します。

6. [**名前**] ボックスにユーザーコントロールの名前を指定し、[**追加**] をクリックします。

     複数のフォルダーとファイルがプロジェクトに追加されます。 これらのファイルの詳細について[は、「web パーツまたはアプリケーションページの再利用可能なコントロールを作成する](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)」を参照してください。

     既定では、ユーザーコントロールファイルは Visual Web Developer デザイナーの**ソース**ビューに表示されます。 このビューで、コントロールの XML マークアップを編集できます。 [**ツールボックス**] からコントロールをドラッグしてコントロールを視覚的にデザインする場合は、[**デザイン**] ビューに切り替えることができます。 「[デザインビュー、Web ページデザイナー」を](/previous-versions/aspnet/ms178149\(v\=vs.100\))参照してください。

7. コントロールで発生するイベントを処理する場合は、ユーザー コントロールのコード ファイルにコードを追加します。

     このファイルは、プロジェクトの言語に応じて、ユーザーコントロールファイルの下の**ソリューションエクスプローラー**に表示され、 *.cs*または *.vb*の拡張子が付いています。

## <a name="see-also"></a>関連項目
- [Web パーツまたはアプリケーションページの再利用可能なコントロールを作成する](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)
- [SharePoint のアプリケーションページの作成](../sharepoint/creating-application-pages-for-sharepoint.md)
- [SharePoint の web パーツの作成](../sharepoint/creating-web-parts-for-sharepoint.md)

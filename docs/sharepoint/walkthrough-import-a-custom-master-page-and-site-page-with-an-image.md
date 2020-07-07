---
title: イメージを含むカスタムマスターページ & サイトページのインポート
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, importing items
- importing items [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 311124b2e0b81e70c4c2a7b40754207e6c66b749
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015690"
---
# <a name="walkthrough-import-a-custom-master-page-and-site-page-with-an-image"></a>チュートリアル: イメージを使用したカスタムマスターページおよびサイトページのインポート
  このチュートリアルでは、sharepoint カスタムマスターページと、画像を含むサイトページを sharepoint プロジェクトにインポートする方法について説明し [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。

 このチュートリアルで説明する内容は次のとおりです。

- SharePoint デザイナーの画像を使用して、カスタムマスターページとサイトページを作成します。

- カスタムマスターページ、イメージ、およびサイトページを SharePoint ソリューション (*.wsp*) ファイルにエクスポートします。

- Sharepoint ソリューションパッケージのインポートプロジェクトを使用して、 *.wsp*ファイルをインポートし、sharepoint プロジェクトに配置します [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>前提条件
 このチュートリアルを完了するには、次のコンポーネントが必要です。

- および SharePoint のサポートされているエディション [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] 。

- 見ることができます。

- SharePoint デザイナー2010。

## <a name="create-items-in-sharepoint-designer"></a>SharePoint デザイナーでのアイテムの作成
 この例では、エクスポート用に SharePoint デザイナーで3つの項目を作成する方法を示します。カスタムマスターページ、カスタムマスターページを参照するサイトページ、およびサイトページに表示されるイメージファイルです。 画像は、SharePoint の/images/フォルダーに追加されます。

#### <a name="to-create-a-custom-master-page-in-sharepoint-designer"></a>SharePoint デザイナーでカスタムマスターページを作成するには

1. SharePoint Designer のナビゲーションウィンドウで、[**マスターページ**] サイトオブジェクトを選択します。

2. [**マスターページ**] リボンで、[**空のマスターページ**] を選択します。

3. [新しいマスター] ページを選択し、[**マスターページ**] リボンで、[**ファイルの編集**] を選択します。

4. SharePoint Designer の下部にある [**コード**] タブを選択します。

5. 既存のマークアップを次のマークアップに置き換えます。

    ```aspx-csharp
    <%@ Master Language="C#" %>
    <%@ Register tagprefix="SharePoint" namespace="Microsoft.SharePoint.WebControls" assembly="Microsoft.SharePoint, Version=14.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" %>
    <html dir="ltr">
    <head runat="server">
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
    <SharePoint:RobotsMetaTag runat="server" __designer:Preview="" __designer:Values="<P N='InDesign' T='False' /><P N='ID' T='ctl00' /><P N='Page' ID='1' /><P N='TemplateControl' ID='2' /><P N='AppRelativeTemplateSourceDirectory' R='-1' />"></SharePoint:RobotsMetaTag>
    <title>Web Page</title>
    </head>
    <body>
    <form id="form1" runat="server">
    <asp:ContentPlaceHolder id="ContentPlaceHolderMain"
            runat="server">
          </asp:ContentPlaceHolder>
    </form>
    </body>
    </html>
    ```

6. ページを保存し、[**マスターページ**] タブを選択して、マスターページの名前を**mybasic1**に変更します。

## <a name="add-an-image-to-the-content-database-in-sharepoint-designer"></a>SharePoint Designer でコンテンツデータベースに画像を追加する
 これで、サイトページに表示するイメージを追加できるようになりました。 イメージは SharePoint コンテンツデータベースに配置されます。

#### <a name="to-add-an-image-to-the-content-database-in-sharepoint-designer"></a>SharePoint Designer でコンテンツデータベースに画像を追加するには

1. ナビゲーションウィンドウで、[すべての**ファイル**] サイトオブジェクトを選択し、ツリービューで [**イメージ**] フォルダーを選択します。

2. [**すべてのファイル**] リボンで、[**ファイルのインポート**] を選択し、任意のファイルを選択して、[ **OK** ] をクリックします。 この例では、ファイルに**myimg1.png**という名前が付けられています。

     必要に応じて、画像を整理するためのサブフォルダーを作成することもできます。

3. [**インポート**] ダイアログボックスを閉じます。

## <a name="create-a-site-page"></a>サイトページの作成
 この基本的なサイトページでは、カスタムマスターページを使用して、前の手順で追加したイメージを表示します。

#### <a name="to-create-a-site-page"></a>サイトページを作成するには

1. ナビゲーションウィンドウで、[**サイトページ**] オブジェクトを選択します。

2. [**ページ**] リボンで、[**ページ**] ボタンを選択し、 **ASPX**ページの種類を選択して、新しいファイルに**mycontentpage1**という名前を指定します。

     必要に応じて、サイトページの整理に役立つサブフォルダーを作成することもできます。

3. [サイトページ] の一覧で [ **MyContentPage1** ] を選択してプロパティページを開き、ページの下部にある [**ファイルの編集**] リンクを選択します。

     このページにセーフモードで編集可能な領域が含まれておらず、[詳細設定] モードでこのページを開くかどうかを確認するメッセージが表示された場合は、[**はい**] をクリックします。

4. ページの下部にある [**コード**] ボタンをクリックします。

5. 既存のマークアップを次のマークアップに置き換えます。

    ```aspx-csharp
    <%@ Import Namespace="Microsoft.SharePoint.ApplicationPages" %>
    <%@ Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=14.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" %>
    <%@ Register Tagprefix="Utilities" Namespace="Microsoft.SharePoint.Utilities" Assembly="Microsoft.SharePoint, Version=14.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" %>
    <%@ Register Tagprefix="asp" Namespace="System.Web.UI" Assembly="System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35" %>
    <%@ Import Namespace="Microsoft.SharePoint" %>
    <%@ Assembly Name="Microsoft.Web.CommandUI, Version=14.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" %>
    <%@ Page Language="C#" Inherits="Microsoft.SharePoint.WebControls.LayoutsPageBase" MasterPageFile="../_catalogs/masterpage/mybasic1.master" meta:progid="SharePoint.WebPartPage.Document" %>

    <asp:Content ID="Main" ContentPlaceHolderID="ContentPlaceHolderMain" runat="server">
    <img alt="My Image" longdesc="My image from images folder" src="../images/myimg1.png" />
    </asp:Content>
    ```

6. 更新されたサイトページを保存します。

## <a name="export-the-items-from-sharepoint"></a>SharePoint からのアイテムのエクスポート
 SharePoint から SharePoint ソリューション (*.wsp*) ファイルに項目をエクスポートします。

#### <a name="to-export-items-from-sharepoint-designer"></a>SharePoint デザイナーから項目をエクスポートするには

1. SharePoint Designer のナビゲーションウィンドウで、[**チームサイト**] オブジェクトを選択し、[**サイト**] リボンで [**テンプレートとして保存**] を選択します。

2. [**テンプレートとして保存**] ダイアログボックスで、ファイル名とテンプレート名を入力し、[**コンテンツを含める**] チェックボックスをオンにして、[ **OK** ] をクリックします。

     これにより、サイトのコンテンツが *.wsp*ファイルに保存されます。

3. ソリューションのエクスポート後、[**ソリューションギャラリー** ] リンクを選択して、使用可能なソリューションファイルの一覧を表示します。

4. 新しい *.wsp*ファイルのショートカットメニューを開き、[**ターゲットに名前を付けて保存**] を選択してシステムに保存します。

## <a name="import-the-items-into-visual-studio"></a>項目を Visual Studio にインポートする
 *.Wsp*ファイルをにインポートし [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。 コンテンツがインポートされたら、それをカスタマイズし、さらに項目を追加して、展開することができます。

#### <a name="to-import-items-from-the-wsp-file-into-visual-studio"></a>.Wsp ファイルから Visual Studio に項目をインポートするには

1. で [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 、**インポート SharePoint 2010 ソリューションパッケージ**プロジェクトを作成します。

2. [**インポートする項目の選択**] ページで、[**型**] 列の [**モジュール**] の下にある [インポート] で、次の表のファイルについてのみチェックボックスをオンにします。

   | ファイル名 | 説明 |
   |------------------------|-----------------------------------------------|
   | \_catalogsmasterpage/\_ | カスタムマスターページ。 |
   | images_ | SharePoint ファイルシステム内のイメージファイル。 |
   | SitePages_ | サイトページ。 |

3. [**完了**] を選択すると、選択した項目がインポートされます。

4. **ソリューションエクスプローラー**で、[カタログ] ノードを選択し、[ \_ 配置の \_ 競合の**解決**] プロパティの値を [**自動**] に設定します。

    これにより、配置の競合が自動的に解決されるようになります。

5. 新しいマスターページに既存のページと同じ名前が付けられている場合は、既存のページが SharePoint デザイナーの既定のマスターページまたはカスタムマスターページのいずれとしてもマークされていないことを確認してください。

    既存のマスターページが既定のマスターページまたはカスタムマスターページとしてマークされている場合は、マスターページを削除できないことを示す配置エラーが発生します。 この問題を回避するには、次の手順を実行します。

   - 既存のマスターページが既定のマスターページとして設定されている場合は、一時的に別のマスターページを既定のマスターページとして設定します。 ファイルを SharePoint に配置した後、新しいマスターページを既定のマスターページとして設定します。

   - 既存のマスターページがカスタムマスターページとして設定されている場合は、一時的に別のマスターページをカスタムマスターページとして設定します。 ファイルを SharePoint に配置した後、新しいマスターページをカスタムマスターページとして設定します。

6. メニューバーで、[**ビルド**] [ソリューションの配置] の順に選択し  >  **Deploy Solution**ます。

7. SharePoint サイトを開いて、配置されたアイテムを表示します。

   ファイルを [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint にインポートして SharePoint に配置する別の方法として、のモジュールにファイルを追加する方法が [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] あります。 [!INCLUDE[crdefault](../sharepoint/includes/crdefault-md.md)][方法: マスターページまたはテーマをインポート](../sharepoint/how-to-import-a-master-page-or-theme.md)し、モジュールを使用して[ソリューションにファイルを含める](../sharepoint/using-modules-to-include-files-in-the-solution.md)

## <a name="see-also"></a>関連項目
- [既存の SharePoint サイトからのアイテムのインポート](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
- [Web パーツまたはアプリケーションページの再利用可能なコントロールを作成する](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)

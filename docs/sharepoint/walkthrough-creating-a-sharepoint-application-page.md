---
title: 'チュートリアル: SharePoint アプリケーションページの作成 |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application pages [SharePoint development in Visual Studio], developing
- application pages [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0eaf7bda4ac4ed67dae79b8dd83bb59ba6985343
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2019
ms.locfileid: "72985027"
---
# <a name="walkthrough-create-a-sharepoint-application-page"></a>チュートリアル: SharePoint アプリケーションページの作成

アプリケーション ページとは、特殊なフォームの ASP.NET ページです。 アプリケーション ページには、SharePoint のマスター ページとマージされるコンテンツが含まれます。 詳細については、「 [SharePoint のアプリケーションページを作成](../sharepoint/creating-application-pages-for-sharepoint.md)する」を参照してください。

このチュートリアルでは、アプリケーション ページを作成し、そのページをローカル SharePoint サイトを使ってデバッグする方法を説明します。 このページには、サーバー ファーム上のあらゆるサイトで、各ユーザーが作成または変更したすべての項目が表示されます。

このチュートリアルでは、次の作業について説明します。

- SharePoint プロジェクトを作成する
- SharePoint プロジェクトにアプリケーション ページを追加する
- アプリケーション ページに ASP.NET コントロールを追加する
- ASP.NET コントロールに分離コードを追加する
- アプリケーション ページをテストする

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>前提条件

- サポート対象エディションの Windows と SharePoint

## <a name="create-a-sharepoint-project"></a>SharePoint プロジェクトを作成する

最初に、**空の SharePoint プロジェクト**を作成します。 後で、このプロジェクトに**アプリケーションページ**アイテムを追加します。

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. **[新しいプロジェクト]** ダイアログボックスを開き、使用する言語の **[Office/SharePoint]** ノードを展開し、 **[sharepoint ソリューション]** ノードを選択します。

3. **[Visual Studio にインストールされたテンプレート]** ペインで、 **[SharePoint 2010-空のプロジェクト]** テンプレートを選択します。 プロジェクトに**Mysharepointproject**という名前を指定し、 **[OK]** をクリックします。

     **SharePoint カスタマイズウィザード**が表示されます。 このウィザードを使用すると、プロジェクトのデバッグに使用するサイトや、ソリューションの信頼レベルを選択できます。

4. **[ファームソリューションとして配置]** する オプションボタンをクリックし、 **[完了]** をクリックして既定のローカル SharePoint サイトを受け入れます。

## <a name="create-an-application-page"></a>アプリケーションページを作成する

アプリケーションページを作成するには、**アプリケーションページ**アイテムをプロジェクトに追加します。

1. **ソリューションエクスプローラー**で、 **mysharepointproject**プロジェクトを選択します。

2. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

3. **[新しい項目の追加]** ダイアログボックスで、[**アプリケーション] ページ ([ファームソリューションのみ**] テンプレート) を選択します。

4. ページに「 **Searchitems**」という名前を入力し、 **[追加]** ボタンをクリックします。

     Visual Web Developer デザイナーでは、**ソース**ビューにアプリケーションページが表示されます。このページでは、ページの HTML 要素を確認できます。 デザイナーにはいくつかの <xref:System.Web.UI.WebControls.Content> コントロールのマークアップが表示されます。 各コントロールは、既定のアプリケーション マスター ページに定義されている <xref:System.Web.UI.WebControls.ContentPlaceHolder> コントロールにマップされます。

## <a name="design-the-layout-of-the-application-page"></a>アプリケーションページのレイアウトをデザインする

アプリケーション ページ項目を使用すると、デザイナーで ASP.NET コントロールをアプリケーション ページに追加できます。 このデザイナーは、Visual Web Developer で使用するデザイナーと同じです。 ラベル、ラジオボタンリスト、およびテーブルをデザイナーの**ソース**ビューに追加し、標準の ASP.NET ページをデザインする場合と同様にプロパティを設定します。

1. メニュー バーで **[表示]** 、 > [ツールボックス]** の順にクリックします。

2. **ツールボックス**の [標準] ノードで、次のいずれかの手順を実行します。

    - **ラベル**項目のショートカットメニューを開き、 **[コピー]** を選択し、デザイナーの**PlaceHolderMain** content コントロールの下にある行のショートカットメニューを開き、 **[貼り付け]** を選択します。

    - **[ツールボックス]** から **[ラベル]** 項目を**PlaceHolderMain**コンテンツコントロールの本文にドラッグします。

3. 前の手順を繰り返して、 **DropDownList**項目と**テーブル**項目を**PlaceHolderMain** content コントロールに追加します。

4. デザイナーで、[ラベル] コントロールの [`Text`] 属性の値を変更して、**すべての項目を表示**します。

5. デザイナーで、`<asp:DropDownList>` 要素を次の XML に置き換えます。

    ```xml
    <asp:DropDownList ID="DropDownList1" runat="server" AutoPostBack="true"
     OnSelectedIndexChanged="DropDownList1_SelectedIndexChanged">
        <asp:ListItem Text="Created by me" Value="Author"></asp:ListItem>
        <asp:ListItem Text="Modified by me" Value="Editor"></asp:ListItem>
    </asp:DropDownList>
    ```

## <a name="handle-the-events-of-controls-on-the-page"></a>ページ上のコントロールのイベントを処理します

ASP.NET ページと同様に、アプリケーション ページのコントロールを処理します。 この手順では、ドロップダウン リストの `SelectedIndexChanged` イベントを処理します。

1. **[表示]** メニューの **[コード]** をクリックします。

     コード エディターでアプリケーション ページ コード ファイルが開きます。

2. `SearchItems` クラスに次のメソッドを追加します。 このコードでは、このチュートリアルでこれから作成するメソッドを呼び出して、<xref:System.Web.UI.WebControls.ListControl.SelectedIndexChanged> の <xref:System.Web.UI.WebControls.DropDownList> イベントを処理します。

     [!code-vb[SP_ApplicationPage#5](../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb#5)]
     [!code-csharp[SP_ApplicationPage#5](../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs#5)]

3. アプリケーション ページ コード ファイルの先頭に次のステートメントを追加します。

     [!code-vb[SP_ApplicationPage#1](../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb#1)]
     [!code-csharp[SP_ApplicationPage#1](../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs#1)]

4. `SearchItems` クラスに次のメソッドを追加します。 このメソッドでは、サーバー ファーム上のすべてのサイトについて反復処理を行い、現在のユーザーが作成または変更した項目を検索します。

     [!code-vb[SP_ApplicationPage#2](../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb#2)]
     [!code-csharp[SP_ApplicationPage#2](../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs#2)]

5. `SearchItems` クラスに次のメソッドを追加します。 このメソッドでは、現在のユーザーが作成または変更した項目をテーブルに表示します。

     [!code-vb[SP_ApplicationPage#3](../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb#3)]
     [!code-csharp[SP_ApplicationPage#3](../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs#3)]

## <a name="test-the-application-page"></a>アプリケーションページをテストする

プロジェクトを実行すると、SharePoint サイトが開き、アプリケーション ページが表示されます。

1. **ソリューションエクスプローラー**で、アプリケーションページのショートカットメニューを開き、 **[スタートアップ項目に設定]** をクリックします。

2. **F5** キーを押します。

     SharePoint サイトが開きます。

3. [アプリケーション] ページで、[**自分が変更**した] オプションを選択します。

     アプリケーション ページが更新され、サーバー ファーム上のすべてのサイトで自分が変更したすべての項目が表示されます。

4. アプリケーション ページで、一覧の **作成者** を選択します。

     アプリケーション ページが更新され、サーバー ファーム上のすべてのサイトで自分が作成したすべての項目が表示されます。

## <a name="next-steps"></a>次のステップ:

SharePoint アプリケーションページの詳細については、「 [sharepoint のアプリケーションページを作成](../sharepoint/creating-application-pages-for-sharepoint.md)する」を参照してください。

Visual Web Designer を使用して、SharePoint ページの内容をデザインする方法の詳細については、以下のトピックを参照してください。

- [SharePoint の web パーツを作成](../sharepoint/creating-web-parts-for-sharepoint.md)します。

- [Web パーツまたはアプリケーションページの再利用可能なコントロールを作成](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)します。

## <a name="see-also"></a>参照

[方法: アプリケーションページを作成](../sharepoint/how-to-create-an-application-page.md)する
[アプリケーション _Layouts ページの種類](/previous-versions/office/aa979604(v=office.14))

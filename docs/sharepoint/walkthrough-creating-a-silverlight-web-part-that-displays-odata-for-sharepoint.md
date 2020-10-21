---
title: Silverlight web パーツを作成し、SharePoint の OData を表示する
titleSuffix: ''
ms.date: 02/22/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.SPE.SilverlightWebPart
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 652f34e6a062d2c8129266a10c859c8d24abd83e
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "92298502"
---
# <a name="walkthrough-create-a-silverlight-web-part-that-displays-odata-for-sharepoint"></a>チュートリアル: SharePoint の OData を表示する Silverlight web パーツの作成
  SharePoint 2010 では、OData によってリストデータが公開されます。 SharePoint では、OData サービスは RESTful サービス ListData .svc によって実装されます。 このチュートリアルでは、Silverlight アプリケーションをホストする SharePoint web パーツを作成する方法について説明します。 Silverlight アプリケーションは、ListData. svc を使用して SharePoint アナウンスリストの情報を表示します。 詳細については、「 [SharePoint FOUNDATION REST インターフェイス](/previous-versions/office/developer/sharepoint-2010/ff521587(v=office.14)) 」と「 [Open Data Protocol](https://www.odata.org/)」を参照してください。

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポート対象エディションの Microsoft Windows および SharePoint。

- [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)].

## <a name="create-a-silverlight-application-and-silverlight-web-part"></a>Silverlight アプリケーションと Silverlight web パーツを作成する
 まず、Visual Studio で Silverlight アプリケーションを作成します。 Silverlight アプリケーションは、ListData. .svc サービスを使用して SharePoint アナウンスリストからデータを取得します。

> [!NOTE]
> 4.0 より前のバージョンの Silverlight では、SharePoint リストデータを参照するために必要なインターフェイスがサポートされていません。

#### <a name="to-create-a-silverlight-application-and-silverlight-web-part"></a>Silverlight アプリケーションと Silverlight web パーツを作成するには

1. メニューバーで [**ファイル**] [  >  **新規作成**] [プロジェクト] の順に選択し  >  **Project** 、[**新しいプロジェクト**] ダイアログボックスを表示します。

2. [ **Visual C#** ] または [ **Visual Basic**] の下にある [ **SharePoint** ] ノードを展開し、[ **2010** ] ノードを選択します。

3. [テンプレート] ペインで、[ **SharePoint 2010 Silverlight Web パーツ** ] テンプレートを選択します。

4. [ **名前** ] ボックスに「 **slwebparttest** 」と入力し、[ **OK** ] をクリックします。

    [ **SharePoint カスタマイズウィザード** ] ダイアログボックスが表示されます。

5. [ **デバッグのサイトとセキュリティレベルの指定** ] ページで、サイト定義をデバッグする SharePoint サーバーサイトの URL を入力するか、既定の場所 (http://<em>システム名</em>/) を使用します。

6. [ **この SharePoint ソリューションの信頼レベル** を指定してください] セクションで、[ **ファームソリューションとして配置** する] オプションボタンを選択します。

    この例ではファームソリューションを使用していますが、Silverlight web パーツプロジェクトは、ファームソリューションまたはサンドボックスソリューションとして配置できます。 サンドボックスソリューションとファームソリューションの詳細については、「 [サンドボックスソリューションの考慮事項](../sharepoint/sandboxed-solution-considerations.md)」を参照してください。

7. [ **Silverlight 構成情報の指定**] ページの [ **silverlight Web パーツを関連付ける方法**] セクションで、[**新しい silverlight プロジェクトを作成し、それを Web パーツに関連付ける**] オプションボタンを選択します。

8. **名前**を**slapplication**に変更し、[ **Language** ] を**Visual Basic**または**Visual C#** のいずれかに設定し、[ **silverlight バージョン**] を [ **silverlight 4.0**] に設定します。

9. **[完了]** をクリックします。 プロジェクトは **ソリューションエクスプローラー**に表示されます。

     このソリューションには、Silverlight アプリケーションと Silverlight web パーツという2つのプロジェクトが含まれています。 Silverlight アプリケーションは、SharePoint からリストデータを取得して表示します。 silverlight web パーツは Silverlight アプリケーションをホストし、SharePoint で表示できるようにします。

## <a name="customize-the-silverlight-application"></a>Silverlight アプリケーションをカスタマイズする
 Silverlight アプリケーションにコードおよびデザイン要素を追加します。

#### <a name="to-customize-the-silverlight-application"></a>Silverlight アプリケーションをカスタマイズするには

1. Silverlight アプリケーションの system.string にアセンブリ参照を追加します。 詳細については、「 [方法: [参照の追加] ダイアログボックスを使用して参照を追加または削除](/previous-versions/wkze6zky(v=vs.140))する」を参照してください。

2. **ソリューションエクスプローラー**で、[**参照**] のショートカットメニューを開き、[**サービス参照の追加**] を選択します。

    > [!NOTE]
    > Visual Basic を使用している場合は、**ソリューションエクスプローラー**の上部にある [**すべてのファイルを表示**] アイコンをクリックして [**参照**] ノードを表示する必要があります。

3. [**サービス参照の追加**] ダイアログボックスの [アドレス] ボックスに、SharePoint サイトの URL (など) を入力し、[実行] ボタンをクリックし **http://MySPSite** ます。 **Go**

     Silverlight が SharePoint OData サービス ListData .svc を検索すると、アドレスが完全なサービス URL に置き換えられます。 この例では、はに http://myserver なり http://myserver/_vti_bin/ListData.svc ます。

4. **[OK** ] をクリックしてサービス参照をプロジェクトに追加し、既定のサービス名である [servicereference1] を使用します。

5. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

6. SharePoint サービスに基づいて新しいデータソースをプロジェクトに追加します。 これを行うには、メニューバーで [ **View**  >  **その他の Windows**  >  **データソース**の表示] を選択します。

     [ **データソース** ] ウィンドウには、タスク、お知らせ、カレンダーなど、利用可能なすべての SharePoint リストデータが表示されます。

7. Silverlight アプリケーションにお知らせリストのデータを追加します。 [ **データソース** ] ウィンドウから Silverlight デザイナーに "アナウンス" をドラッグできます。

     これにより、SharePoint サイトのお知らせリストにバインドされたグリッドコントロールが作成されます。

8. Silverlight ページに合わせてグリッドコントロールのサイズを変更します。

9. Mainpage.xaml コードファイル (Visual C# の場合は*MainPage.xaml.cs* 、Visual Basic の場合は *mainpage.xaml* ) で、次の名前空間参照を追加します。

    ```vb
    ' Add the following three Imports statements.
    Imports SLApplication.ServiceReference1
    Imports System.Windows.Data
    Imports System.Data.Services.Client
    ```

    ```csharp
    // Add the following three using directives.
    using SLApplication.ServiceReference1;
    using System.Windows.Data;
    using System.Data.Services.Client;
    ```

10. 次の変数宣言をクラスの先頭に追加します。

    ```vb
    Private context As TeamSiteDataContext
    Private myCollectionViewSource As CollectionViewSource
    Private announcements As New DataServiceCollection(Of AnnouncementsItem)()
    ```

    ```csharp
    private TeamSiteDataContext context;
    private CollectionViewSource myCollectionViewSource;
    DataServiceCollection<AnnouncementsItem> announcements = new DataServiceCollection<AnnouncementsItem>();
    ```

11. プロシージャを `UserControl_Loaded` 次のように置き換えます。

    ```vb
    Private Sub UserControl_Loaded_1(sender As Object, e As RoutedEventArgs)
        ' The URL for the OData service.
        ' Replace <server name> in the next line with the name of your SharePoint server.
        context = New TeamSiteDataContext(New Uri("http://<server name>/_vti_bin/ListData.svc"))

        ' Do not load your data at design time.
        If Not System.ComponentModel.DesignerProperties.GetIsInDesignMode(Me) Then
            'Load your data here and assign the results to the CollectionViewSource.
            myCollectionViewSource =   DirectCast(Me.Resources("announcementsViewSource"), System.Windows.Data.CollectionViewSource)
            announcements.LoadCompleted += New EventHandler(Of LoadCompletedEventArgs)(AddressOf announcements_LoadCompleted)
            announcements.LoadAsync(context.Announcements)
        End If
    End Sub
    ```

    ```csharp
    private void UserControl_Loaded_1(object sender, RoutedEventArgs e)
    {
        // The URL for the OData service.
        // Replace <server name> in the next line with the name of your
        // SharePoint server.
        context = new TeamSiteDataContext(new Uri("http://ServerName>/_vti_bin/ListData.svc"));

        // Do not load your data at design time.
        if (!System.ComponentModel.DesignerProperties.GetIsInDesignMode(this))
        {
            //Load your data here and assign the results to the CollectionViewSource.
            myCollectionViewSource = (System.Windows.Data.CollectionViewSource)this.Resources["announcementsViewSource"];
            announcements.LoadCompleted += new EventHandler<LoadCompletedEventArgs>(announcements_LoadCompleted);
            announcements.LoadAsync(context.Announcements);
        }
    }
    ```

     *ServerName*プレースホルダーは、SharePoint を実行しているサーバーの名前に置き換えてください。

12. 次のエラー処理プロシージャを追加します。

    ```vb
    Private Sub announcements_LoadCompleted(sender As Object, e As LoadCompletedEventArgs)
        ' Handle any errors.
        If e.[Error] Is Nothing Then
            myCollectionViewSource.Source = announcements
        Else
            MessageBox.Show(String.Format("ERROR: {0}", e.[Error].Message))
        End If
    End Sub

    ```

    ```csharp
    void announcements_LoadCompleted(object sender, LoadCompletedEventArgs e)
    {
        // Handle any errors.
        if (e.Error == null)
        {
            myCollectionViewSource.Source = announcements;
        }
        else
        {
            MessageBox.Show(string.Format("ERROR: {0}", e.Error.Message));
        }
    }
    ```

## <a name="modify-the-silverlight-web-part"></a>Silverlight web パーツを変更する
 Silverlight web パーツプロジェクトのプロパティを変更して、Silverlight のデバッグを有効にします。

#### <a name="to-modify-the-silverlight-web-part"></a>Silverlight web パーツを変更するには

1. Silverlight web パーツプロジェクト (**Slwebparttest**) のショートカットメニューを開き、[ **プロパティ**] を選択します。

2. [ **プロパティ** ] ウィンドウで、[ **SharePoint** ] タブを選択します。

3. まだ選択されていない場合は、[ **スクリプトデバッグではなく、Silverlight デバッグを有効にする** ] チェックボックスをオンにします。

4. プロジェクトを保存します。

## <a name="test-the-silverlight-web-part"></a>Silverlight web パーツをテストする
 Sharepoint で新しい Silverlight web パーツをテストして、SharePoint リストデータが適切に表示されることを確認します。

#### <a name="to-test-the-silverlight-web-part"></a>Silverlight web パーツをテストするには

1. F5 キーを **押し** て、SharePoint ソリューションをビルドして実行します。

2. SharePoint の [サイトの **操作** ] メニューで、[ **新しいページ**] を選択します。

3. [ **新しいページ** ] ダイアログボックスで、「 **SL Web パーツテスト**」などのタイトルを入力し、[ **作成** ] ボタンをクリックします。

4. ページデザイナーの [ **編集ツール** ] タブで、[ **挿入**] を選択します。

5. タブストリップで、[ **Web パーツ**] を選択します。

6. [ **カテゴリ** ] ボックスで、[ **カスタム** ] フォルダーを選択します。

7. **Web パーツ**の一覧で、Silverlight web パーツを選択し、[**追加**] ボタンをクリックして、Web パーツをデザイナーに追加します。

8. 必要な web ページにすべての追加を行った後、[ **ページ** ] タブをクリックし、ツールバーの [ **& 閉じる** ] ボタンをクリックします。

     Silverlight web パーツには、SharePoint サイトからのアナウンスデータが表示されるようになります。 既定では、ページは SharePoint のサイトページの一覧に格納されます。

    > [!NOTE]
    > Silverlight では、ドメイン間でデータにアクセスするときに、web アプリケーションの悪用に使用できるセキュリティの脆弱性を防ぐことができます。 Silverlight でリモートデータにアクセスするときに問題が発生した場合は、「 [ドメインの境界を越えてサービスを利用できるよう](/previous-versions/windows/silverlight/dotnet-windows-silverlight/cc197955(v=vs.95))にする」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint の Web パーツを作成する](../sharepoint/creating-web-parts-for-sharepoint.md)
- [SharePoint ソリューションパッケージの配置、発行、およびアップグレード](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md)
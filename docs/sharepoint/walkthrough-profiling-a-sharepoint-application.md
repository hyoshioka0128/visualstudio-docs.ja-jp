---
title: 'チュートリアル: SharePoint アプリケーションのプロファイリング |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, profiling
- performance testing [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, performance testing
- profiling [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c900a1496d3ef864e50d40092379348c05a4706b
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86017098"
---
# <a name="walkthrough-profile-a-sharepoint-application"></a>チュートリアル: SharePoint アプリケーションのプロファイリング
  このチュートリアルでは、Visual Studio のプロファイル ツールを使用し、SharePoint アプリケーションのパフォーマンスを最適化する方法について説明します。 アプリケーション例は SharePoint フィーチャー イベント レシーバーで、これにはフィーチャー イベント レシーバーのパフォーマンスを低下させるアイドル ループが含まれています。 Visual Studio プロファイラーを使用すると、プロジェクトの最も負荷の高い (実行速度が遅い) 部分を特定し、除去することができます。これは、*ホットパス*とも呼ばれます。

 このチュートリアルでは、次のタスクについて説明します。

- [フィーチャーとフィーチャーイベントレシーバーを追加](#add-a-feature-and-feature-event-receiver)します。

- [SharePoint アプリケーションを構成して展開](#configure-and-deploy-the-sharepoint-application)します。

- [SharePoint アプリケーションを実行](#run-the-sharepoint-application)します。

- [プロファイルの結果を表示して解釈](#view-and-interpret-the-profile-results)します。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポート対象エディションの Microsoft Windows および SharePoint。

- [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)].

## <a name="create-a-sharepoint-project"></a>SharePoint プロジェクトを作成する
 まずは、SharePoint プロジェクトを作成します。

### <a name="to-create-a-sharepoint-project"></a>SharePoint プロジェクトを作成するには

1. メニューバーで [**ファイル**] [  >  **新規作成**] [プロジェクト] の順に選択し  >  **Project** 、[**新しいプロジェクト**] ダイアログボックスを表示します。

2. [ **Visual C#** ] または [ **Visual Basic**] の下にある [ **SharePoint** ] ノードを展開し、[ **2010** ] ノードを選択します。

3. [テンプレート] ペインで、[ **SharePoint 2010] プロジェクト**テンプレートを選択します。

4. [**名前**] ボックスに「 **profiletest**」と入力し、[ **OK** ] をクリックします。

    **SharePoint カスタマイズウィザード**が表示されます。

5. [**デバッグのサイトとセキュリティレベルの指定**] ページで、サイト定義をデバッグする SharePoint サーバーサイトの URL を入力するか、既定の場所 (http://<em>システム名</em>/) を使用します。

6. [**この SharePoint ソリューションの信頼レベル**を指定してください] セクションで、[**ファームソリューションとして配置**する] オプションボタンを選択します。

    現時点では、ファーム ソリューションのプロファイルのみを実行できます。 サンドボックスソリューションとファームソリューションの詳細については、「[サンドボックスソリューションの考慮事項](../sharepoint/sandboxed-solution-considerations.md)」を参照してください。

7. **[完了]** をクリックします。 プロジェクトが**ソリューションエクスプローラー**に表示されます。

## <a name="add-a-feature-and-feature-event-receiver"></a>フィーチャーとフィーチャーイベントレシーバーを追加する
 次に、フィーチャーを、そのイベント レシーバーと共にプロジェクトに追加します。 このイベント レシーバーには、プロファイル対象のコードが含まれます。

### <a name="to-add-a-feature-and-feature-event-receiver"></a>機能とフィーチャー イベント レシーバーを追加するには

1. **ソリューションエクスプローラー**で、[**機能**] ノードのショートカットメニューを開き、[**機能の追加**] を選択し、名前を既定値の [ **feature1.feature**] のままにします。

2. **ソリューションエクスプローラー**で、 **feature1.feature**のショートカットメニューを開き、[**イベントレシーバーの追加**] を選択します。

     これにより、いくつかのコメント アウトされたイベント ハンドラーを持つコード ファイルが機能に追加され、編集のためにファイルが開かれます。

3. イベント レシーバー クラスに、次の変数宣言を追加します。

    ```vb
    ' SharePoint site/subsite.
    Private siteUrl As String = "http://localhost"
    Private webUrl As String = "/"
    ```

    ```csharp
    // SharePoint site/subsite.
    private string siteUrl = "http://localhost";
    private string webUrl = "/";
    ```

4. `FeatureActivated` プロシージャを次のコードに置き換えます。

    ```vb
    Public Overrides Sub FeatureActivated(properties As SPFeatureReceiverProperties)
        Try
            Using site As New SPSite(siteUrl)
                Using web As SPWeb = site.OpenWeb(webUrl)
                    ' Reference the lists.
                    Dim announcementsList As SPList = web.Lists("Announcements")

                    ' Add a new announcement to the Announcements list.
                    Dim listItem As SPListItem = announcementsList.Items.Add()
                    listItem("Title") = "Activated Feature: " & Convert.ToString(properties.Definition.DisplayName)
                    listItem("Body") = Convert.ToString(properties.Definition.DisplayName) & " was activated on: " & DateTime.Now.ToString()
                    ' Waste some time.
                    TimeCounter()
                    ' Update the list.
                    listItem.Update()
                End Using
            End Using

        Catch e As Exception
            Console.WriteLine("Error: " & e.ToString())
        End Try
    End Sub
    ```

    ```csharp
    public override void FeatureActivated(SPFeatureReceiverProperties properties)
    {
        try
        {
            using (SPSite site = new SPSite(siteUrl))
            {
                using (SPWeb web = site.OpenWeb(webUrl))
                {
                    // Reference the lists.
                    SPList announcementsList = web.Lists["Announcements"];

                    // Add a new announcement to the Announcements list.
                    SPListItem listItem = announcementsList.Items.Add();
                    listItem["Title"] = "Activated Feature: " + properties.Definition.DisplayName;
                    listItem["Body"] = properties.Definition.DisplayName + " was activated on: " +
    DateTime.Now.ToString();
                    // Waste some time.
                    TimeCounter();
                    // Update the list.
                    listItem.Update();
                }
            }
        }

        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.ToString());
        }
    }
    ```

5. 次のプロシージャをプロシージャの下に追加 `FeatureActivated` します。

    ```vb

    Public Sub TimeCounter()
        Dim result As Integer
        For i As Integer = 0 To 99999
            For j As Integer = 0 To 9999
                result = i * j
            Next j
        Next i
    End Sub
    ```

    ```csharp
    public void TimeCounter()
    {
        for (int i = 0; i < 100000; i++)
        {
            for (int j = 0; j < 10000; j++)
            {
                int result = i * j;
            }
        }
    }
    ```

6. **ソリューションエクスプローラー**で、プロジェクト (**profiletest**) のショートカットメニューを開き、[**プロパティ**] を選択します。

7. [**プロパティ**] ダイアログボックスで、[ **SharePoint** ] タブを選択します。

8. [**アクティブな配置構成**] の一覧で、[**アクティブ化なし**] を選択します。

     この配置構成を選択することにより、後で SharePoint 内から手動で機能をアクティブ化できます。

9. プロジェクトを保存します。

## <a name="configure-and-deploy-the-sharepoint-application"></a>SharePoint アプリケーションを構成して展開する
 SharePoint プロジェクトの準備ができたので、それを構成し、SharePoint サーバーに配置します。

### <a name="to-configure-and-deploy-the-sharepoint-application"></a>SharePoint アプリケーションを構成し、配置するには

1. [**分析**] メニューの [**パフォーマンスウィザードの起動**] をクリックします。

2. **パフォーマンスウィザード**のいずれかのページで、プロファイリングの方法を [ **CPU サンプリング**] のままにし、[**次へ**] をクリックします。

     他のプロファイル方法は、より高度なプロファイルを行う場合に使用できます。 詳細については、「[パフォーマンス収集方法について](../profiling/understanding-performance-collection-methods.md)」を参照してください。

3. **パフォーマンスウィザード**の2ページ目で、プロファイルターゲットを**profiletest**のままにし、[**次へ**] をクリックします。

     ソリューションに複数のプロジェクトがある場合は、この一覧に表示されます。

4. **パフォーマンスウィザード**の3ページ目で、[**階層の相互作用プロファイルを有効にする**] チェックボックスをオフにし、[**次へ**] をクリックします。

     階層の相互作用のプロファイル (TIP) 機能は、データベースを照会するアプリケーションのパフォーマンスの測定や、Web ページが要求された回数の表示に便利です。 そのようなデータはこの例では不要なため、この機能は有効にしません。

5. **パフォーマンスウィザード**の4ページ目で、[**ウィザードの完了後にプロファイルを起動**する] チェックボックスをオンのままにして、[**完了**] をクリックします。

     このウィザードでは、サーバー上のアプリケーションプロファイリングを有効にし、[**パフォーマンスエクスプローラー** ] ウィンドウを表示して、SharePoint アプリケーションをビルド、配置、および実行します。

## <a name="run-the-sharepoint-application"></a>SharePoint アプリケーションを実行する
 `FeatureActivation` イベント コードの実行をトリガーし、SharePoint 内のフューチャーをアクティブ化します。

### <a name="to-run-the-sharepoint-application"></a>SharePoint アプリケーションを実行するには

1. SharePoint で、[**サイトの操作**] メニューを開き、[**サイトの設定**] を選択します。

2. [**サイトの操作**] の一覧で、[**サイト機能の管理**] リンクを選択します。

3. **機能**の一覧で、 **profiletest feature1.feature**の横にある [**アクティブ化**] ボタンを選択します。

     この操作を実行すると、`FeatureActivated` 関数内でアイドル ループが呼び出されることによって一時停止が発生します。

4. **クイック起動**バーで [**リスト**] を選択し、[**リスト] の一覧で**[**お知らせ**] を選択します。

     機能がアクティブになったことを示す新しいお知らせが一覧に追加されていることを確認します。

5. SharePoint サイトを閉じます。

     SharePoint を閉じた後、プロファイラーはサンプルのプロファイリングレポートを作成して表示し、 **Profiletest**プロジェクトのフォルダーに .vsp ファイルとして保存します。

## <a name="view-and-interpret-the-profile-results"></a>プロファイルの結果を表示して解釈する
 SharePoint アプリケーションを実行してプロファイルを行ったので、次はテスト結果を表示します。

### <a name="to-view-and-interpret-the-profile-results"></a>プロファイルの結果を表示して解釈するには

1. サンプルプロファイルレポートの [**最も多くの個別作業を実行する関数**] セクションで `TimeCounter` は、が一覧の一番上にあることに注意してください。

     この場所は、`TimeCounter` がサンプル数の最も多い関数の 1 つ、つまり、アプリケーション内で最大のパフォーマンス ボトルネックの 1 つであることを示しています。 ただし、これは驚くような状況はではありません。デモンストレーションのために、意図してこのようにデザインされたものであるからです。

2. [**最も多くの個別作業を実行し**ている関数] セクションで、リンクをクリックして、 `ProcessRequest` 関数のコスト配分を表示し `ProcessRequest` ます。

     の [**呼び出された関数**] セクションで、 `ProcessRequest` **FeatureActiviated**関数が最も負荷の高い関数として表示されていることに注意してください。

3. [**呼び出された関数**] セクションで、[ **featureactivated 化**] ボタンを選択します。

     **Featureactivated アクティブになっ**ている関数の [**呼び出された関数**] セクションで `TimeCounter` は、関数が最も負荷の高い呼び出された関数として一覧表示されます。 [**関数コードビュー** ] ペインで、強調表示されたコード ( `TimeCounter` ) がホットスポットであり、修正が必要な場所を示します。

4. サンプル プロファイル レポートを閉じます。

     いつでもレポートを再度表示するには、[**パフォーマンスエクスプローラー** ] ウィンドウで .vsp ファイルを開きます。

## <a name="fix-the-code-and-reprofile-the-application"></a>コードを修正してアプリケーションを再プロファイルする
 SharePoint アプリケーション内のホットスポット関数を特定したので、次はこれを修正します。

### <a name="to-fix-the-code-and-reprofile-the-application"></a>コードを修正し、アプリケーションを再プロファイルするには

1. フィーチャー イベント レシーバーのコード内で、`FeatureActivated` の `TimeCounter` メソッドの呼び出しをコメント アウトし、これが呼び出されないようにします。

2. プロジェクトを保存します。

3. **パフォーマンスエクスプローラー**で、[ターゲット] フォルダーを開き、[ **profiletest** ] ノードを選択します。

4. **パフォーマンスエクスプローラー**ツールバーの [**操作**] タブで、[**プロファイルの開始**] ボタンをクリックします。

     アプリケーションを再プロファイルする前にプロファイルプロパティを変更する場合は、[**パフォーマンスウィザードの起動**] をクリックします。

5. このトピックで前述した「 **SharePoint アプリケーションを実行**する」セクションの手順に従います。

     これで、アイドル ループへの呼び出しが削除されたため、機能のアクティブ化がより高速になりました。 このことは、サンプル プロファイル レポートに反映されます。

## <a name="see-also"></a>関連項目
- [パフォーマンスセッションの概要](../profiling/performance-session-overview.md)
- [パフォーマンスプロファイルの初心者向けガイド](../profiling/beginners-guide-to-performance-profiling.md)
- [Visual Studio プロファイラーでアプリケーションのボトルネックを見つける](https://msdn.microsoft.com/magazine/cc337887.aspx)

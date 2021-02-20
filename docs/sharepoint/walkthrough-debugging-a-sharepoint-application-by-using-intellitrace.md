---
title: IntelliTrace を使用した SharePoint アプリケーションのデバッグ
description: IntelliTrace を使用すると、SharePoint アプリケーションをより簡単にデバッグおよび修正できます。 フィーチャーレシーバーにコードを作成して追加します。 プロジェクトをテストします。 IntelliTrace データを収集します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- IntelliTrace [SharePoint development in Visual Studio]
- standalone data collector
- SharePoint development in Visual Studio, IntelliTrace
- data collector
- IntelliTrace
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e2ce8bc2c493d59b8a06a64ff69838e828315bf2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99952656"
---
# <a name="walkthrough-debug-a-sharepoint-application-by-using-intellitrace"></a>チュートリアル: IntelliTrace を使用した SharePoint アプリケーションのデバッグ

IntelliTrace を使用すると、SharePoint ソリューション簡単にデバッグできます。 従来のデバッガーでは、現時点のソリューションを示すスナップショットだけを取得できました。 IntelliTrace を使用すると、ソリューション内で過去に発生したイベントと、そのイベントが発生したコンテキストをレビューし、コードに移動できます。

 このチュートリアルでは、Microsoft Monitoring Agent を使用してデプロイされたアプリケーションから IntelliTrace データを収集することによって、Visual Studio で SharePoint 2010 または SharePoint 2013 プロジェクトをデバッグする方法について説明します。 そのデータを分析するには、Visual Studio Enterprise を使用する必要があります。 このプロジェクトには、フィーチャーがアクティブ化されたときに、タスク リストにタスクを、お知らせリストにお知らせを追加するフィーチャー レシーバーが組み込まれます。 フィーチャーが非アクティブ化されると、タスクは完了とマークされ、次のお知らせがお知らせリストに追加されます。 ただし、このプロシージャには、プロジェクトの正常な実行を妨げる論理エラーが含まれています。 IntelliTrace を使用することで、このエラーを見つけて修正できます。

 **適用対象:** このトピックの情報は、Visual Studio で作成された SharePoint 2010 および SharePoint 2013 ソリューションに適用されます。

 このチュートリアルでは、次の作業について説明します。

- [フィーチャーレシーバーを作成する](#create-a-feature-receiver)

- [フィーチャーレシーバーにコードを追加する](#add-code-to-the-feature-receiver)

- [プロジェクトをテストする](#test-the-project)

- [Microsoft Monitoring Agent を使用した IntelliTrace データの収集](#collect-intellitrace-data-by-using-microsoft-monitoring-agent)

- [SharePoint ソリューションをデバッグして修正する](#debug-and-fix-the-sharepoint-solution)

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポート対象エディションの Windows と SharePoint

- Visual Studio Enterprise。

## <a name="create-a-feature-receiver"></a>フィーチャーレシーバーを作成する

最初に、フィーチャー レシーバーがある空の SharePoint プロジェクトを作成します。

1. SharePoint 2010 または SharePoint 2013 ソリューションプロジェクトを作成し、 **IntelliTraceTest** という名前を指定します。

     **Sharepoint カスタマイズウィザード** が表示されます。このウィザードでは、プロジェクトの sharepoint サイトとソリューションの信頼レベルの両方を指定できます。

2. [ **ファームソリューションとして配置する** ] オプションを選択し、[ **完了** ] をクリックします。

     IntelliTrace は、ファーム ソリューションに対してのみ動作します。

3. **ソリューションエクスプローラー** で、[**機能**] ノードのショートカットメニューを開き、[**機能の追加**] を選択します。

     *Feature1.feature* が表示されます。

4. Feature1.feature のショートカットメニューを開き、[ **イベントレシーバーの追加** ] を選択して、機能にコードモジュールを追加します。

## <a name="add-code-to-the-feature-receiver"></a>フィーチャーレシーバーにコードを追加する

次に、フィーチャー レシーバー内の 2 つのメソッド (`FeatureActivated` と `FeatureDeactivating`) にコードを追加します。 これらのメソッドは、SharePoint でフィーチャーがアクティブ化または非アクティブ化されたときにトリガーされます。

1. `Feature1EventReceiver` クラスの一番上に次のコードを追加します。このコードは、SharePoint サイトとサブサイトを指定する変数を宣言します。

    ```vb
    ' SharePoint site and subsite.
    Private siteUrl As String = "http://localhost"
    Private webUrl As String = "/"
    ```

    ```csharp
    // SharePoint site and subsite.
    private string siteUrl = "http://localhost";
    private string webUrl = "/";
    ```

2. `FeatureActivated` メソッドを次のコードに置き換えます。

    ```vb
    Public Overrides Sub FeatureActivated(ByVal properties As SPFeatureReceiverProperties)
        Try
            Using site As New SPSite(siteUrl)
                Using web As SPWeb = site.OpenWeb(webUrl)
                    ' Reference the lists.
                    Dim announcementsList As SPList = web.Lists("Announcements")
                    Dim taskList As SPList = web.Lists("Tasks")

                    ' Add an announcement to the Announcements list.
                    Dim listItem As SPListItem = announcementsList.Items.Add()
                    listItem("Title") = "Activated Feature: " & Convert.ToString(properties.Definition.DisplayName)
                    listItem("Body") = Convert.ToString(properties.Definition.DisplayName) & " was activated on: " & DateTime.Now.ToString()
                    listItem.Update()

                    ' Add a task to the Task list.
                    Dim newTask As SPListItem = taskList.Items.Add()
                    newTask("Title") = "Deactivate feature: " & Convert.ToString(properties.Definition.DisplayName)
                    newTask.Update()
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
                    SPList taskList = web.Lists["Tasks"];

                    // Add an announcement to the Announcements list.
                    SPListItem listItem = announcementsList.Items.Add();
                    listItem["Title"] = "Activated Feature: " + properties.Definition.DisplayName;
                    listItem["Body"] = properties.Definition.DisplayName + " was activated on: " + DateTime.Now.ToString();
                    listItem.Update();

                    // Add a task to the Task list.
                    SPListItem newTask = taskList.Items.Add();
                    newTask["Title"] = "Deactivate feature: " + properties.Definition.DisplayName;
                    newTask.Update();
                }
            }
        }

        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.ToString());
        }

    }
    ```

3. `FeatureDeactivating` メソッドを次のコードに置き換えます。

    ```vb
    Public Overrides Sub FeatureDeactivating(ByVal properties As SPFeatureReceiverProperties)
        ' The following line induces an error to demonstrate debugging.
        ' Remove this line later for proper operation.
        Throw New System.InvalidOperationException("Serious error occurred!")
        Try
            Using site As New SPSite(siteUrl)
                Using web As SPWeb = site.OpenWeb(webUrl)
                    ' Reference the lists.
                    Dim taskList As SPList = web.Lists("Tasks")
                    Dim announcementsList As SPList = web.Lists("Announcements")

                    ' Add an announcement that the feature was deactivated.
                    Dim listItem As SPListItem = announcementsList.Items.Add()
                    listItem("Title") = "Deactivated Feature: " & Convert.ToString(properties.Definition.DisplayName)
                    listItem("Body") = Convert.ToString(properties.Definition.DisplayName) & " was deactivated on: " & DateTime.Now.ToString()
                    listItem.Update()

                    ' Find the task that the feature receiver added to the Task list when the
                    ' feature was activated.
                    Dim qry As New SPQuery()
                    qry.Query = "<Where><Contains><FieldRef Name='Title' /><Value Type='Text'>Deactivate</Value></Contains></Where>"
                    Dim taskItems As SPListItemCollection = taskList.GetItems(qry)

                    For Each taskItem As SPListItem In taskItems
                        ' Mark the task as complete.
                        taskItem("PercentComplete") = 1
                        taskItem("Status") = "Completed"
                        taskItem.Update()
                    Next
                End Using

            End Using

        Catch e As Exception
            Console.WriteLine("Error: " & e.ToString())
        End Try

    End Sub
    ```

    ```csharp
    public override void FeatureDeactivating(SPFeatureReceiverProperties properties)
    {
        // The following line induces an error to demonstrate debugging.
        // Remove this line later for proper operation.
        throw new System.InvalidOperationException("A serious error occurred!");
        try
        {
            using (SPSite site = new SPSite(siteUrl))
            {
                using (SPWeb web = site.OpenWeb(webUrl))
                {
                    // Reference the lists.
                    SPList taskList = web.Lists["Tasks"];
                    SPList announcementsList = web.Lists["Announcements"];

                    // Add an announcement that the feature was deactivated.
                    SPListItem listItem = announcementsList.Items.Add();
                    listItem["Title"] = "Deactivated Feature: " + properties.Definition.DisplayName;
                    listItem["Body"] = properties.Definition.DisplayName + " was deactivated on: " + DateTime.Now.ToString();
                    listItem.Update();

                    // Find the task that the feature receiver added to the Task list when the
                    // feature was activated.
                    SPQuery qry = new SPQuery();
                    qry.Query = "<Where><Contains><FieldRef Name='Title' /><Value Type='Text'>Deactivate</Value></Contains></Where>";
                    SPListItemCollection taskItems = taskList.GetItems(qry);

                    foreach (SPListItem taskItem in taskItems)
                    {
                        // Mark the task as complete.
                        taskItem["PercentComplete"] = 1;
                        taskItem["Status"] = "Completed";
                        taskItem.Update();
                    }
                }
            }

        }

        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.ToString());
        }
    }
    ```

## <a name="test-the-project"></a>プロジェクトをテストする

コードがフィーチャー レシーバーに追加され、データ コレクターが実行されているので、SharePoint ソリューションを配置して実行し、それが正常に動作するかどうかをテストします。

> [!IMPORTANT]
> この例では、FeatureDeactivating イベント ハンドラーでエラーがスローされます。 このチュートリアルの後半で、データ コレクターが作成した .iTrace ファイルを使用してこのエラーを特定します。

1. ソリューションを SharePoint に配置し、ブラウザーで SharePoint サイトを開きます。

     フィーチャーは自動的にアクティブ化され、フィーチャー レシーバーによってお知らせとタスクが自動的に追加されます。

2. お知らせリストとタスク一覧の内容を表示します。

     お知らせリストには、"アクティブ化された **機能: IntelliTraceTest_Feature1**" という名前の新しいお知らせがあります。また、[タスク] 一覧には、" **非アクティブ化機能: IntelliTraceTest_Feature1**" という名前の新しいタスクが含まれている必要があります。 このいずれかがない場合は、フィーチャーがアクティブになっているかどうかを確認します。 アクティブになっていない場合は、アクティブにします。

3. 次の手順を実行して、フィーチャーを非アクティブにします。

   1. SharePoint の [ **サイトの操作** ] メニューで、[サイトの **設定**] を選択します。

   2. [ **サイトの操作**] の [ **サイト機能の管理** ] リンクを選択します。

   3. **IntelliTraceTest feature1.feature** の横にある [**非アクティブ化**] ボタンをクリックします。

   4. [警告] ページで、[ **この機能を非アクティブ** にする] リンクを選択します。

      FeatureDeactivating() イベント ハンドラーによってエラーがスローされます。

## <a name="collect-intellitrace-data-by-using-microsoft-monitoring-agent"></a>Microsoft Monitoring Agent を使用した IntelliTrace データの収集

SharePoint を実行しているシステムに Microsoft Monitoring Agent をインストールする場合は、IntelliTrace によって返される汎用情報よりも具体的なデータを使用して、SharePoint ソリューションをデバッグできます。 エージェントは、PowerShell コマンドレットを使用して Visual Studio 外で動作し、SharePoint ソリューションの実行中にデバッグ情報をキャプチャします。

> [!NOTE]
> このセクションの構成情報は、この例に固有です。 その他の構成オプションの詳細については、「 [IntelliTrace スタンドアロンコレクターの使用](../debugger/using-the-intellitrace-stand-alone-collector.md)」を参照してください。

1. SharePoint を実行しているコンピューターで [Microsoft Monitoring Agent を設定し、ソリューションの監視を開始し](../debugger/using-the-intellitrace-stand-alone-collector.md)ます。

2. フィーチャーを非アクティブ化します。

   1. SharePoint の [ **サイトの操作** ] メニューで、[サイトの **設定**] を選択します。

   2. [ **サイトの操作**] の [ **サイト機能の管理** ] リンクを選択します。

   3. **IntelliTraceTest feature1.feature** の横にある [**非アクティブ化**] ボタンをクリックします。

   4. [警告] ページで、[ **この機能を非アクティブ** にする] リンクを選択します。

      エラーが発生します (この場合は、FeatureDeactivating() イベント ハンドラーでスローされたエラーが原因)。

3. PowerShell ウィンドウで、 [Stop-WebApplicationMonitoring](/previous-versions/system-center/powershell/system-center-2012-r2/dn472753(v=sc.20)) コマンドを実行して、itrace ファイルを作成し、監視を停止して、SharePoint ソリューションを再起動します。

     **停止-webapplicationmonitoring***" \<SharePointSite> \\<sharepointappname \> "*  

## <a name="debug-and-fix-the-sharepoint-solution"></a>SharePoint ソリューションをデバッグして修正する

この時点で、Visual Studio で IntelliTrace ログ ファイルを表示し、SharePoint ソリューションのエラーを見つけて修正することができます。

1. Visual Studio で、\IntelliTraceLogs フォルダーにある .iTrace ファイルを開きます。

     [ **IntelliTrace の概要** ] ページが表示されます。 このエラーは処理されなかったため、SharePoint 相関 ID (GUID) が [ **分析** ] セクションの [ハンドルされない例外] 領域に表示されます。 エラーが発生した呼び出し履歴を表示する場合は、[ **呼び出し履歴** ] ボタンをクリックします。

2. [ **例外のデバッグ** ] ボタンをクリックします。

     プロンプトが表示されたら、シンボル ファイルを読み込みます。 [ **IntelliTrace** ] ウィンドウでは、例外は "スローされた深刻なエラーが発生しました。" と表示されます。

     [IntelliTrace] ウィンドウで、例外を選択して失敗したコードを表示します。

3. SharePoint ソリューションを開き、FeatureDeactivating アクティブ化 () プロシージャの先頭にある **throw** ステートメントをコメントアウトするか削除することで、エラーを修正します。

4. Visual Studio でソリューションをリビルドし、SharePoint に再配置します。

5. 次の手順を実行して、フィーチャーを非アクティブにします。

    1. SharePoint の [ **サイトの操作** ] メニューで、[サイトの **設定**] を選択します。

    2. [ **サイトの操作**] の [ **サイト機能の管理** ] リンクを選択します。

    3. **IntelliTraceTest feature1.feature** の横にある [**非アクティブ化**] ボタンをクリックします。

    4. [警告] ページで、[ **この機能を非アクティブ** にする] リンクを選択します。

6. [タスク一覧] を開き、非アクティブ化タスクの [ **状態** ] の値が "Completed" で、その **% Complete** の値が100% であることを確認します。

     コードは、適切に実行されています。

## <a name="see-also"></a>関連項目

- [SharePoint コードの検証とデバッグ](../sharepoint/verifying-and-debugging-sharepoint-code.md)
- [IntelliTrace](../debugger/intellitrace.md)
- [チュートリアル: 単体テストを使用した SharePoint コードの検証](/previous-versions/visualstudio/visual-studio-2010/gg599006\(v\=vs.100\))
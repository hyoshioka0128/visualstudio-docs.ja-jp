---
title: 'チュートリアル: ワークフローへのアプリケーションページの追加 |Microsoft Docs'
description: このチュートリアルでは、SharePoint ワークフローソリューションにアプリケーションページを追加します。 ワークフローコードを修正します。 アプリケーションページを作成、コーディング、およびテストします。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, adding applications page to workflow
- application page [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c862c1de3b0630b3a5144f821e6266c34a88a5db
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "96915662"
---
# <a name="walkthrough-add-an-application-page-to-a-workflow"></a>チュートリアル: ワークフローへのアプリケーション ページの追加
  このチュートリアルでは、ワークフローから派生したデータを表示するアプリケーションページをワークフロープロジェクトに追加する方法について説明します。 このプロジェクトは、「 [チュートリアル: 関連付けフォームと開始フォームを使用したワークフローの作成](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)」で説明されているプロジェクトに基づいています。

 このチュートリアルでは、次のタスクについて説明します。

- ASPX アプリケーションページを SharePoint ワークフロープロジェクトに追加する。

- ワークフロープロジェクトからデータを取得して操作する。

- アプリケーションページのテーブルにデータを表示します。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- および SharePoint のサポートされているエディション [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] 。

- 見ることができます。

- また、「 [チュートリアル: 関連付けフォームと開始フォームを使用](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)したワークフローの作成」でもプロジェクトを完了する必要があります。

## <a name="amend-the-workflow-code"></a>ワークフローコードを修正する
 まず、ワークフローにコード行を追加して、結果列の値を経費報告書の金額に設定します。 この値は、経費報告書の概要計算で後で使用されます。

#### <a name="to-set-the-value-of-the-outcome-column-in-the-workflow"></a>ワークフローの結果列の値を設定するには

1. 「 [チュートリアル: 関連付けと開始フォームを持つワークフローの作成](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md) 」から完成したプロジェクトを読み込み [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。

2. *Workflow1.cs* または *workflow1.xaml* のコードを開きます (プログラミング言語によって異なります)。

3. メソッドの一番下に `createTask1_MethodInvoking` 次のコードを追加します。

    ```vb
    createTask1_TaskProperties1.ExtendedProperties("Outcome") =
      workflowProperties.InitiationData
    ```

    ```csharp
    createTask1_TaskProperties1.ExtendedProperties["Outcome"] =
      workflowProperties.InitiationData;
    ```

## <a name="create-an-application-page"></a>アプリケーションページを作成する
 次に、ASPX フォームをプロジェクトに追加します。 このフォームには、経費報告書ワークフロープロジェクトから取得したデータが表示されます。 これを行うには、アプリケーションページを追加します。 アプリケーションページでは、他の SharePoint ページと同じマスターページが使用されます。つまり、SharePoint サイトの他のページに似ています。

#### <a name="to-add-an-application-page-to-the-project"></a>アプリケーションページをプロジェクトに追加するには

1. ExpenseReport プロジェクトを選択し、メニューバーで [**プロジェクト**] [  >  **新しい項目の追加**] の順に選択します。

2. [ **テンプレート** ] ペインで、[ **アプリケーションページ** ] テンプレートを選択し、プロジェクト項目の既定の名前 (**ApplicationPage1**) を使用して、[ **追加** ] をクリックします。

3. [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]ApplicationPage1 ので、 `PlaceHolderMain` セクションを次のように置き換えます。

    ```aspx-csharp
    <asp:Content ID="Main" ContentPlaceHolderID="PlaceHolderMain" runat="server">
        <asp:Label ID="Label1" runat="server" Font-Bold="True"
            Text="Expenses that exceeded allotted amount" Font-Size="Medium"></asp:Label>
        <br />
        <asp:Table ID="Table1" runat="server">
        </asp:Table>
    </asp:Content>
    ```

     このコードは、タイトルと共にテーブルをページに追加します。

4. セクションを次のように置き換えて、アプリケーションページにタイトルを追加し `PlaceHolderPageTitleInTitleArea` ます。

    ```aspx-csharp
    <asp:Content ID="PageTitleInTitleArea" ContentPlaceHolderID="PlaceHolderPageTitleInTitleArea" runat="server" >
        Expense Report Summary
    </asp:Content>
    ```

## <a name="code-the-application-page"></a>アプリケーションページのコーディング
 次に、経費報告書の概要アプリケーションのページにコードを追加します。 このページを開くと、割り当てられた使用制限を超えた経費について、SharePoint のタスク一覧がスキャンされます。 このレポートには、各アイテムが経費の合計と共に一覧表示されます。

#### <a name="to-code-the-application-page"></a>アプリケーションページをコーディングするには

1. **ApplicationPage1** ノードを選択し、メニューバーで [コードの **表示**] を選択して、  >  **Code** アプリケーションページの背後にあるコードを表示します。

2. クラスの先頭にある **using** ステートメントまたは **Import** ステートメント (プログラミング言語によって異なります) を、次のように置き換えます。

    ```vb
    Imports System
    Imports Microsoft.SharePoint
    Imports Microsoft.SharePoint.WebControls
    Imports System.Collections
    Imports System.Data
    Imports System.Web.UI
    Imports System.Web.UI.WebControls
    Imports System.Web.UI.WebControls.WebParts
    Imports System.Drawing
    Imports Microsoft.SharePoint.Navigation
    ```

    ```csharp
    using System;
    using Microsoft.SharePoint;
    using Microsoft.SharePoint.WebControls;
    using System.Collections;
    using System.Data;
    using System.Web.UI;
    using System.Web.UI.WebControls;
    using System.Web.UI.WebControls.WebParts;
    using System.Drawing;
    using Microsoft.SharePoint.Navigation;
    ```

3. `Page_Load` メソッドに次のコードを追加します。

    ```vb
    Try
        ' Reference the Tasks list on the SharePoint site.
        ' Replace "TestServer" with a valid SharePoint server name.
        Dim site As SPSite = New SPSite("http://TestServer")
        Dim list As SPList = site.AllWebs(0).Lists("Tasks")
        ' string text = "";
        Dim sum As Integer = 0
        Table1.Rows.Clear()
        ' Add table headers.
        Dim hr As TableHeaderRow = New TableHeaderRow
        hr.BackColor = Color.LightBlue
        Dim hc1 As TableHeaderCell = New TableHeaderCell
        Dim hc2 As TableHeaderCell = New TableHeaderCell
        hc1.Text = "Expense Report Name"
        hc2.Text = "Amount Exceeded"
        hr.Cells.Add(hc1)
        hr.Cells.Add(hc2)
        ' Add the TableHeaderRow as the first item
        ' in the Rows collection of the table.
        Table1.Rows.AddAt(0, hr)
        ' Iterate through the tasks in the Task list and collect those
        ' that have values in the "Related Content" and "Outcome" fields
        ' - the fields written to when expense approval is required.
        For Each item As SPListItem In list.Items
            Dim s_relContent As String = ""
            Dim s_outcome As String = ""
            Try
                ' Task has the fields - treat as expense report.
                s_relContent = item.GetFormattedValue("Related Content")
                s_outcome = item.GetFormattedValue("Outcome")
            Catch erx As System.Exception
                ' Task does not have fields - skip it.
                Continue For
            End Try
            ' Convert amount to an int and keep a running total.
            If (Not String.IsNullOrEmpty(s_relContent) And Not
              String.IsNullOrEmpty(s_outcome)) Then
                sum = (sum + Convert.ToInt32(s_outcome))
                Dim relContent As TableCell = New TableCell
                relContent.Text = s_relContent
                Dim outcome As TableCell = New TableCell
                outcome.Text = ("$" + s_outcome)
                Dim dataRow2 As TableRow = New TableRow
                dataRow2.Cells.Add(relContent)
                dataRow2.Cells.Add(outcome)
                Table1.Rows.Add(dataRow2)
            End If
        Next
        ' Report the sum of the reports in the table footer.
        Dim tfr As TableFooterRow = New TableFooterRow
        tfr.BackColor = Color.LightGreen
        ' Create a TableCell object to contain the
        ' text for the footer.
        Dim ftc1 As TableCell = New TableCell
        Dim ftc2 As TableCell = New TableCell
        ftc1.Text = "TOTAL: "
        ftc2.Text = ("$" + Convert.ToString(sum))
        ' Add the TableCell object to the Cells
        ' collection of the TableFooterRow.
        tfr.Cells.Add(ftc1)
        tfr.Cells.Add(ftc2)
        ' Add the TableFooterRow to the Rows
        ' collection of the table.
        Table1.Rows.Add(tfr)
    Catch errx As Exception
        System.Diagnostics.Debug.WriteLine(("Error: " + errx.ToString))
    End Try
    ```

    ```csharp
    try
    {
        // Reference the Tasks list on the SharePoint site.
        // Replace "TestServer" with a valid SharePoint server name.
        SPSite site = new SPSite("http://TestServer");
        SPList list = site.AllWebs[0].Lists["Tasks"];

        // string text = "";
        int sum = 0;

        Table1.Rows.Clear();

        // Add table headers.
        TableHeaderRow hr = new TableHeaderRow();
        hr.BackColor = Color.LightBlue;
        TableHeaderCell hc1 = new TableHeaderCell();
        TableHeaderCell hc2 = new TableHeaderCell();
        hc1.Text = "Expense Report Name";
        hc2.Text = "Amount Exceeded";
        hr.Cells.Add(hc1);
        hr.Cells.Add(hc2);
        // Add the TableHeaderRow as the first item
        // in the Rows collection of the table.
        Table1.Rows.AddAt(0, hr);

        // Iterate through the tasks in the Task list and collect those
        // that have values in the "Related Content" and "Outcome"
        // fields - the fields written to when expense approval is
        // required.
        foreach (SPListItem item in list.Items)
        {
            string s_relContent = "";
            string s_outcome = "";

            try
            {
                // Task has the fields - treat as expense report.
                s_relContent = item.GetFormattedValue("Related
                  Content");
                s_outcome = item.GetFormattedValue("Outcome");
            }
            catch
            {
                // Task does not have fields - skip it.
                continue;
            }

            if (!String.IsNullOrEmpty(s_relContent) &&
              !String.IsNullOrEmpty(s_outcome))
            {
                // Convert amount to an int and keep a running total.
                sum += Convert.ToInt32(s_outcome);
                TableCell relContent = new TableCell();
                relContent.Text = s_relContent;
                TableCell outcome = new TableCell();
                outcome.Text = "$" + s_outcome;
                TableRow dataRow2 = new TableRow();
                dataRow2.Cells.Add(relContent);
                dataRow2.Cells.Add(outcome);
                Table1.Rows.Add(dataRow2);
            }
        }

        // Report the sum of the reports in the table footer.
           TableFooterRow tfr = new TableFooterRow();
        tfr.BackColor = Color.LightGreen;

        // Create a TableCell object to contain the
        // text for the footer.
        TableCell ftc1 = new TableCell();
        TableCell ftc2 = new TableCell();
        ftc1.Text = "TOTAL: ";
        ftc2.Text = "$" + Convert.ToString(sum);

        // Add the TableCell object to the Cells
        // collection of the TableFooterRow.
        tfr.Cells.Add(ftc1);
        tfr.Cells.Add(ftc2);

        // Add the TableFooterRow to the Rows
        // collection of the table.
        Table1.Rows.Add(tfr);
    }

    catch (Exception errx)
    {
        System.Diagnostics.Debug.WriteLine("Error: " + errx.ToString());
    }
    ```

    > [!WARNING]
    > コードの "TestServer" は、SharePoint を実行している有効なサーバーの名前に置き換えてください。

## <a name="test-the-application-page"></a>アプリケーションページをテストする
 次に、アプリケーションページに経費データが正しく表示されるかどうかを確認します。

#### <a name="to-test-the-application-page"></a>アプリケーション ページをテストするには

1. **F5** キーを押して、プロジェクトを実行し、SharePoint に配置します。

2. [ **ホーム** ] ボタンをクリックし、クイック起動バーの [ **共有ドキュメント** ] リンクをクリックして、SharePoint サイトに [共有ドキュメント] の一覧を表示します。

3. この例の経費報告書を表すには、ページの上部にある [ **Librarytools** ] タブの [**ドキュメント**] リンクを選択してから、ツールリボンの [**ドキュメントのアップロード**] ボタンを選択して、新しいドキュメントをドキュメントの一覧にアップロードします。

4. いくつかのドキュメントをアップロードした後、ページの上部にある [ **Librarytools** ] タブの [**ライブラリ**] リンクを選択し、ツールリボンの [**ライブラリの設定**] ボタンをクリックして、ワークフローをインスタンス化します。

5. [**ドキュメントライブラリの設定**] ページで、[**権限と管理**] セクションの [**ワークフロー設定**] リンクを選択します。

6. [ **ワークフロー設定** ] ページで、[ **ワークフローの追加** ] リンクを選択します。

7. [ **ワークフローの追加** ] ページで、[ **ExpenseReport-workflow1.xaml** ] ワークフローを選択し、「 **ExpenseTest**」などのワークフローの名前を入力して、[ **次へ** ] をクリックします。

    ワークフローの関連付けフォームが表示されます。 この値を使用して、経費の上限を報告します。

8. 関連付けフォームで、[**自動承認の制限**] ボックスに「 **1000** 」と入力し、[**ワークフローの関連付け**] ボタンを選択します。

9. [ **ホーム** ] ボタンをクリックして、SharePoint のホームページに戻ります。

10. クイック起動バーの [ **共有ドキュメント** ] リンクをクリックします。

11. アップロードされたドキュメントのいずれかを選択してドロップダウン矢印を表示し、それを選択して、[ **ワークフロー** ] 項目を選択します。

12. ExpenseTest の横にある画像を選択して、ワークフロー開始フォームを表示します。

13. [ **支出合計** ] テキストボックスに1000より大きい値を入力し、[ **ワークフローの開始** ] をクリックします。

     報告された経費が割り当てられた経費額を超えると、タスクがタスク一覧に追加されます。 "**完了**" という値を持つ **ExpenseTest** という名前の列も、[共有ドキュメント] の一覧の経費報告書項目に追加されます。

14. [共有ドキュメント] ボックスの一覧の他のドキュメントで、手順 11-13 を繰り返します。 (ドキュメントの正確な数は重要ではありません)。

15. Web ブラウザーで次の URL を開き、[経費報告書の概要アプリケーション] ページを表示します: **Http://**<em>SystemName</em>**/_layouts**

     経費報告書の概要ページには、割り当てられた金額を超過した経費報告書がすべて表示されます。また、超過分の金額と、すべてのレポートの合計金額が一覧表示されます。

## <a name="next-steps"></a>次のステップ
 SharePoint アプリケーションページの詳細については、「 [sharepoint のアプリケーションページを作成](../sharepoint/creating-application-pages-for-sharepoint.md)する」を参照してください。

 SharePoint ページのコンテンツをデザインする方法の詳細については、Visual Studio の Visual Web デザイナーを使用して次のトピックを参照してください。

- [SharePoint の web パーツを作成](../sharepoint/creating-web-parts-for-sharepoint.md)します。

- [Web パーツまたはアプリケーションページの再利用可能なコントロールを作成](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)します。

## <a name="see-also"></a>関連項目

- [チュートリアル: 関連付けフォームと開始フォームを持つワークフローの作成](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)
- [方法: アプリケーション ページを作成する](../sharepoint/how-to-create-an-application-page.md)
- [SharePoint のアプリケーション ページの作成](../sharepoint/creating-application-pages-for-sharepoint.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
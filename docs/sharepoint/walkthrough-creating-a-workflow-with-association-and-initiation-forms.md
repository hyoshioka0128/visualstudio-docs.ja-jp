---
title: 関連付けフォームと開始フォームを使用してワークフローを作成する
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, workflows
- SharePoint development in Visual Studio, workflow association forms
- workflows [SharePoint development in Visual Studio]
- association forms [SharePoint development in Visual Studio]
- initiation forms [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, workflow initiation forms
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6f257dfed2fe439c5ab22ab9951b6258116c6567
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86017130"
---
# <a name="walkthrough-create-a-workflow-with-association-and-initiation-forms"></a>チュートリアル: 関連付けフォームと開始フォームを使用したワークフローの作成
  このチュートリアルでは、アソシエーションフォームと開始フォームの使用を組み込む基本的なシーケンシャルワークフローを作成する方法について説明します。 これらの ASPX フォームは、ワークフローが SharePoint 管理者 (関連付けフォーム) によって最初に関連付けられたとき、およびワークフローがユーザー (開始フォーム) によって開始されたときにワークフローに追加されるようにします。

 このチュートリアルでは、次の要件を持つ経費報告書の承認ワークフローを作成する必要があるシナリオについて説明します。

- ワークフローがリストに関連付けられている場合、管理者には、経費報告書の金額の上限を入力する関連付けフォームを入力するように求められます。

- 従業員は、経費報告書を共有ドキュメントリストにアップロードし、ワークフローを開始して、ワークフロー開始フォームに経費合計を入力します。

- 従業員経費報告書の合計が管理者の定義済み制限を超えた場合、従業員の上司が経費報告書を承認するためのタスクが作成されます。 ただし、従業員の経費報告書の合計が経費の上限以下の場合、自動的に承認されたメッセージがワークフローの履歴リストに書き込まれます。

  このチュートリアルでは、次の作業について説明します。

- で SharePoint リスト定義のシーケンシャルワークフロープロジェクトを作成 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] します。

- ワークフロースケジュールを作成しています。

- ワークフローアクティビティイベントの処理。

- ワークフローの関連付けと開始フォームを作成しています。

- ワークフローの関連付け。

- ワークフローを手動で開始しています。

> [!NOTE]
> このチュートリアルではシーケンシャルワークフロープロジェクトを使用しますが、プロセスはステートマシンワークフローと同じです。
>
> また、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 次の手順では、ユーザーインターフェイス要素の一部で、コンピューターの名前や場所が異なる場合があります。 これらの要素は、所有している [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] エディションと使用する設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- および SharePoint のサポートされているエディション [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] 。

- 見ることができます。

## <a name="create-a-sharepoint-sequential-workflow-project"></a>SharePoint シーケンシャルワークフロープロジェクトを作成する
 まず、でシーケンシャルワークフロープロジェクトを作成し [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。 シーケンシャルワークフローは、最後のアクティビティが終了するまで順番に実行される一連の手順です。 この手順では、SharePoint の共有ドキュメントリストに適用されるシーケンシャルワークフローを作成します。 ワークフローのウィザードを使用すると、ワークフローをサイト定義またはリスト定義に関連付けて、ワークフローがいつ開始されるかを決定できます。

#### <a name="to-create-a-sharepoint-sequential-workflow-project"></a>SharePoint シーケンシャルワークフロープロジェクトを作成するには

1. メニューバーで [**ファイル**] [  >  **新規作成**] [プロジェクト] の順に選択し  >  **Project** 、[**新しいプロジェクト**] ダイアログボックスを表示します。

2. [ **Visual C#** ] または [ **Visual Basic**] の下にある [ **SharePoint** ] ノードを展開し、[ **2010** ] ノードを選択します。

3. [ **テンプレート** ] ペインで、[ **SharePoint 2010 プロジェクト** プロジェクト] テンプレートを選択します。

4. [ **名前** ] ボックスに「 **ExpenseReport** 」と入力し、[ **OK** ] をクリックします。

     **SharePoint カスタマイズウィザード**が表示されます。

5. [ **デバッグ用のサイトとセキュリティレベルの指定** ] ページで、[ **ファームソリューションとして配置** する] オプションを選択し、[ **完了** ] をクリックして信頼レベルと既定のサイトを受け入れます。

     また、この手順では、ソリューションの信頼レベルをファームソリューションとして設定します。これは、ワークフロープロジェクトで使用できる唯一のオプションです。

6. **ソリューション エクスプローラー**で、プロジェクト ノードを選択します。

7. メニューバーで、[**プロジェクト**] [  >  **新しい項目の追加**] の順に選択します。

8. [ **Visual C#** ] または [ **Visual Basic**で、[ **SharePoint** ] ノードを展開し、[ **2010** ] ノードを選択します。

9. [ **テンプレート** ] ペインで、[ **シーケンシャルワークフロー (ファームソリューションのみ)** ] テンプレートを選択し、[ **追加** ] をクリックします。

     **SharePoint カスタマイズウィザード**が表示されます。

10. [ **デバッグ用のワークフロー名の指定** ] ページで、既定の名前 (**ExpenseReport-workflow1.xaml**) をそのまま使用します。 既定のワークフローテンプレートの種類の値 (**リストワークフロー)** をそのままにします。 **[次へ]** ボタンをクリックします。

11. [ **デバッグセッションに自動的にワークフローを関連付けますか?** ] ページで、ワークフローテンプレートがオンになっている場合に自動的に関連付けられるボックスをオフにします。

     このステップでは、後で関連付けフォームを表示する共有ドキュメントの一覧にワークフローを手動で関連付けることができます。

12. **[完了]** をクリックします。

## <a name="add-an-association-form-to-the-workflow"></a>関連付けフォームをワークフローに追加する
 次に、を作成します。ASPX 関連付けフォーム。 SharePoint 管理者が最初にワークフローを経費報告書ドキュメントに関連付けたときに表示されます。

#### <a name="to-add-an-association-form-to-the-workflow"></a>関連付けフォームをワークフローに追加するには

1. **ソリューションエクスプローラー**で [ **workflow1.xaml** ] ノードを選択します。

2. メニューバーで、[**プロジェクト**] [  >  **新しい項目の追加**] の順に選択し、[**新しい項目の追加**] ダイアログボックスを表示します。

3. ダイアログボックスのツリービューで、(プロジェクトの言語に応じて) [ **Visual C#** ] または [ **Visual Basic** ] を展開し、[ **SharePoint** ] ノードを展開して、[ **2010** ] ノードを選択します。

4. テンプレートの一覧で、[ワークフローの **関連付けフォーム** ] テンプレートを選択します。

5. [ **名前** ] テキストボックスに、「 **ExpenseReportAssocForm**」と入力します。

6. [ **追加** ] をクリックして、フォームをプロジェクトに追加します。

## <a name="designing-and-coding-the-association-form"></a>関連付けフォームのデザインとコーディング
 この手順では、コントロールとコードを追加することによって、アソシエーションフォームに機能を導入します。

#### <a name="to-design-and-code-the-association-form"></a>関連付けフォームをデザインおよびコーディングするには

1. アソシエーションフォーム (ExpenseReportAssocForm) で、を持つ要素を見つけ `asp:Content` `ID="Main"` ます。

2. このコンテンツ要素の最初の行の直後に、次のコードを追加して、経費の承認制限 (*Autoapprovelimit*) の入力を求めるラベルとテキストボックスを作成します。

    ```aspx-csharp
    <asp:Label ID="lblAutoApproveLimit" Text="Auto Approval Limit:" runat="server" />

    <asp:TextBox ID="AutoApproveLimit" runat="server" />
    <br /><br />
    ```

3. **ソリューションエクスプローラー**の**ExpenseReportAssocForm**ファイルを展開して、依存ファイルを表示します。

    > [!NOTE]
    > プロジェクトがに含まれている場合は、[ [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] **すべてのファイルを表示** ] ボタンをクリックしてこの手順を実行する必要があります。

4. ExpenseReportAssocForm ファイルのショートカットメニューを開き、[コードの **表示**] を選択します。

5. メソッドを `GetAssociationData` 次のように置き換えます。

    ```vb
    Private Function GetAssociationData() As String
        ' TODO: Return a string that contains the association data that
        ' will be passed to the workflow. Typically, this is in XML
        ' format.
        Return Me.AutoApproveLimit.Text
    End Function
    ```

    ```csharp
    private string GetAssociationData()
    {
        // TODO: Return a string that contains the association data that
        // will be passed to the workflow. Typically, this is in XML
        // format.
        return this.AutoApproveLimit.Text;
    }
    ```

## <a name="add-an-initiation-form-to-the-workflow"></a>ワークフローへの開始フォームの追加
 次に、ユーザーが経費報告書に対してワークフローを実行したときに表示される開始フォームを作成します。

#### <a name="to-create-an-initiation-form"></a>開始フォームを作成するには

1. **ソリューションエクスプローラー**で [ **workflow1.xaml** ] ノードを選択します。

2. メニューバーで、[**プロジェクト**] [新しい項目の追加] の順に選択し  >  **Add New Item** 、[**新しい項目の追加**] ダイアログボックスを表示します。

3. ダイアログボックスのツリービューで、(プロジェクトの言語に応じて) [ **Visual C#** ] または [ **Visual Basic**  ] を展開し、[ **SharePoint** ] ノードを展開して、[ **2010** ] ノードを選択します。

4. テンプレートの一覧で、[ **ワークフロー開始フォーム** ] テンプレートを選択します。

5. [ **名前** ] テキストボックスに、「 **「」と入力し**ます。

6. [ **追加** ] をクリックして、フォームをプロジェクトに追加します。

## <a name="designing-and-coding-the-initiation-form"></a>開始フォームの設計とコーディング
 次に、コントロールとコードを追加して、開始フォームに機能を導入します。

#### <a name="to-code-the-initiation-form"></a>開始フォームをコーディングするには

1. 開始フォーム (この場合は、を含む要素) に移動し `asp:Content` `ID="Main"` ます。

2. このコンテンツ要素の最初の行のすぐ後に、次のコードを追加して、関連付けフォームに入力された経費承認制限 (*Autoapprovelimit*) を表示するラベルとテキストボックスを作成し、経費合計を求めるための別のラベルとテキストボックスを作成します *(コストの合計)。*

    ```aspx-csharp
    <asp:Label ID="lblAutoApproveLimit" Text="Auto Approval Limit:" runat="server" />

    <asp:TextBox ID="AutoApproveLimit" ReadOnly="true" runat="server" />
    <br /><br />
    <asp:Label ID="lblExpenseTotal" Text="Expense Total:" runat="server" />

    <asp:TextBox ID="ExpenseTotal" runat="server" />
    <br /><br />
    ```

3. **ソリューションエクスプローラー**で、このファイルの依存ファイルを表示するに**は、この**ファイルを展開します。

4. 使用している Sereportinitform .aspx ファイルのショートカットメニューを開き、[ **コードの表示**] を選択します。

5. メソッドを `Page_Load` 次の例に置き換えます。

    ```vb
    Protected Sub Page_Load(ByVal sender As Object, ByVal e As
      EventArgs) Handles Me.Load
        InitializeParams()
        Me.AutoApproveLimit.Text = workflowList.WorkflowAssociations(New
          Guid(associationGuid)).AssociationData
        ' Optionally, add code here to pre-populate your form fields.
    End Sub
    ```

    ```csharp
    protected void Page_Load(object sender, EventArgs e)
    {
        InitializeParams();
        this.AutoApproveLimit.Text =
          workflowList.WorkflowAssociations[new
          Guid(associationGuid)].AssociationData;
    }
    ```

6. メソッドを `GetInitiationData` 次の例に置き換えます。

    ```vb
    ' This method is called when the user clicks the button to start the workflow.
    Private Function GetInitiationData() As String
        Return Me.ExpenseTotal.Text
        ' TODO: Return a string that contains the initiation data that
        ' will be passed to the workflow. Typically, this is in XML
        ' format.
        Return String.Empty
    End Function
    ```

    ```csharp
    // This method is called when the user clicks the button to start the workflow.
    private string GetInitiationData()
    {
        // TODO: Return a string that contains the initiation data that
        // will be passed to the workflow. Typically, this is in XML
        // format.
        return this.ExpenseTotal.Text;
    }
    ```

## <a name="cutomize-the-workflow"></a>ワークフローの Cutomize
 次に、ワークフローをカスタマイズします。 後で、2つのフォームをワークフローに関連付けます。

#### <a name="to-customize-the-workflow"></a>ワークフローをカスタマイズするには

1. ワークフローデザイナーで、プロジェクトの Workflow1.xaml を開き、ワークフローを表示します。

2. **ツールボックス**で、[ **Windows Workflow** v1.0] ノードを展開し、 **IfElse**アクティビティを見つけます。

3. 次のいずれかの手順を実行して、このアクティビティをワークフローに追加します。

    - **IfElse**アクティビティのショートカットメニューを開き、[**コピー**] を選択し、ワークフローデザイナーの**onWorkflowActivated1**アクティビティの下にある行のショートカットメニューを開き、[**貼り付け**] を選択します。

    - [**ツールボックス**] から**IfElse**アクティビティをドラッグし、ワークフローデザイナーの [ **onWorkflowActiviated1** ] アクティビティの下の行に接続します。

4. ツールボックスで、[ **SharePoint ワークフロー** ] ノードを展開し、 **createtask** アクティビティを見つけます。

5. 次のいずれかの手順を実行して、このアクティビティをワークフローに追加します。

    - **Createtask**アクティビティのショートカットメニューを開き、[**コピー**] を選択し、ワークフローデザイナーの**IfElseActivity1**内の2つの**ドロップアクティビティ**のいずれかのショートカットメニューを開き、[**貼り付け**] を選択します。

    - [**ツールボックス**] の**createtask**アクティビティを、 **IfElseActivity1**内の [ここにある2つの**アクティビティをドロップ**します] 領域のいずれかにドラッグします。

6. [**プロパティ**] ウィンドウで、 **Correlationtoken**プロパティの*tasktoken*のプロパティ値を入力します。

7. [ **Correlationtoken** ] プロパティを展開します。横にあるプラス記号 (![TreeView +](../sharepoint/media/plus.gif "TreeView 正符号")) を選択します。

8. **OwnerActivityName**サブプロパティのドロップダウン矢印をクリックし、 *workflow1.xaml*の値を設定します。

9. [ **TaskId** ] プロパティを選択し、省略記号 (![ASP.NET Mobile Designer 楕円](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) ボタンをクリックして [ **プロパティのバインド** ] ダイアログボックスを表示します。

10. [ **新しいメンバーにバインドする** ] タブを選択し、[ **フィールドの作成** ] オプションボタンをクリックして、[ **OK** ] をクリックします。

11. **Taskproperties**プロパティを選択し、省略記号 (![ASP.NET Mobile Designer 楕円](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) ボタンをクリックして [**プロパティのバインド**] ダイアログボックスを表示します。

12. [ **新しいメンバーにバインドする** ] タブを選択し、[ **フィールドの作成** ] オプションボタンをクリックして、[ **OK** ] をクリックします。

13. [ **ツールボックス**] で、[ **SharePoint ワークフロー** ] ノードを展開し、 **logtohistory listactivity** アクティビティを見つけます。

14. 次のいずれかの手順を実行して、このアクティビティをワークフローに追加します。

    - **Logtohistory listactivity**アクティビティのショートカットメニューを開き、[**コピー**] を選択し、ワークフローデザイナーの**IfElseActivity1**内のその他の [**アクティビティをここにドロップ**します] 領域のショートカットメニューを開き、[**貼り付け**] を選択します。

    - [**ツールボックス**] から**Logtohistory listactivity**アクティビティをドラッグし、 **IfElseActivity1**内の他の [**ここにアクティビティをドロップ**します] 領域にドロップします。

## <a name="add-code-to-the-workflow"></a>ワークフローにコードを追加する
 次に、コードをワークフローに追加して、機能を提供します。

#### <a name="to-add-code-to-the-workflow"></a>ワークフローにコードを追加するには

1. ワークフローデザイナーで **createTask1** アクティビティのショートカットメニューを開き、[ **コードの表示**] を選択します。

2. 次のメソッドを追加します。

    ```vb
    Private Sub createTask1_MethodInvoking(ByVal sender As
      System.Object, ByVal e As System.EventArgs)
        createTask1_TaskId1 = Guid.NewGuid
        createTask1_TaskProperties1.AssignedTo = "somedomain\\someuser"
        createTask1_TaskProperties1.Description = "Please approve the
          expense report"
        createTask1_TaskProperties1.Title = "Expense Report Approval
          Needed"
    End Sub
    ```

    ```csharp
    private void createTask1_MethodInvoking(object sender, EventArgs e)
    {
        createTask1_TaskId1 = Guid.NewGuid();
        createTask1_TaskProperties1.AssignedTo = "somedomain\\someuser";
        createTask1_TaskProperties1.Description = "Please approve the
          expense report";
        createTask1_TaskProperties1.Title = "Expense Report Approval
          Needed";
    }
    ```

    > [!NOTE]
    > コードで、を、 `somedomain\\someuser` タスクが作成されるドメインとユーザー名 ("" など) に置き換え `Office\\JoeSch` ます。 テストでは、開発中のアカウントを使用するのが最も簡単です。

3. メソッドの下 `MethodInvoking` に、次の例を追加します。

    ```vb
    Private Sub checkApprovalNeeded(ByVal sender As Object, ByVal e As
      ConditionalEventArgs)
        Dim approval As Boolean = False
        If (Convert.ToInt32(workflowProperties.InitiationData) >
          Convert.ToInt32(workflowProperties.AssociationData)) Then
            approval = True
        End If
        e.Result = approval
    End Sub
    ```

    ```csharp
    private void checkApprovalNeeded(object sender, ConditionalEventArgs
      e)
    {
        bool approval = false;
        if (Convert.ToInt32(workflowProperties.InitiationData) >
          Convert.ToInt32(workflowProperties.AssociationData))
        {
            approval = true;
        }
        e.Result = approval;
    }
    ```

4. ワークフローデザイナーで、 **ifElseBranchActivity1** アクティビティを選択します。

5. [ **プロパティ** ] ウィンドウで、 **condition** プロパティのドロップダウン矢印をクリックし、 *コード条件* の値を設定します。

6. [ **条件** ] プロパティを展開します。その横にあるプラス記号 (![TreeView](../sharepoint/media/plus.gif "TreeView 正符号")) を選択し、その値を *checkapprovalneeded*に設定します。

7. ワークフローデザイナーで、 **logToHistoryListActivity1** アクティビティのショートカットメニューを開き、[ **ハンドラーの生成** ] を選択して、イベントの空のメソッドを生成し `MethodInvoking` ます。

8. コードを `MethodInvoking` 次のコードに置き換えます。

    ```vb
    Private Sub logToHistoryListActivity1_MethodInvoking(ByVal sender As
      System.Object, ByVal e As System.EventArgs)
        Me.logToHistoryListActivity1.HistoryOutcome = ("Expense was auto
          approved for " + workflowProperties.InitiationData)
    End Sub
    ```

    ```csharp
    private void logToHistoryListActivity1_MethodInvoking(object sender,
      EventArgs e)
    {
        this.logToHistoryListActivity1.HistoryOutcome = "Expense was
          auto approved for " + workflowProperties.InitiationData;
    }
    ```

9. F5 キーを **押し** てプログラムをデバッグします。

     これにより、アプリケーションがコンパイルされ、パッケージ化されて展開され、機能がアクティブ化され、アプリケーションプールがリサイクルされ、 [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] [ **サイトの Url** ] プロパティで指定した場所でブラウザーが起動します。

## <a name="associating-the-workflow-to-the-documents-list"></a>ワークフローをドキュメントリストに関連付ける
 次に、ワークフローを SharePoint サイトの **Shareddocuments** リストに関連付けて、ワークフロー関連付けフォームを表示します。

#### <a name="to-associate-the-workflow"></a>ワークフローを関連付けるには

1. クイック起動バーの [ **共有ドキュメント** ] リンクをクリックします。

2. [**ライブラリツール**] タブの [**ライブラリ**] リンクを選択し、[**ライブラリの設定**] リボンボタンをクリックします。

3. [**権限と管理**] セクションで、[**ワークフロー設定**] リンクを選択し、 **[ワークフロー] ページの**[ワークフローの**追加**] リンクを選択します。

4. [ワークフロー設定] ページの上部にある一覧で、 **ExpenseReport-workflow1.xaml** テンプレートを選択します。

5. 次のフィールドに「"によっては、「" に **よって」と入力し** 、[ **次へ** ] をクリックします。

     これにより、ワークフローが **共有ドキュメント** の一覧に関連付けられ、ワークフローの関連付けフォームが表示されます。

6. [ **自動承認の制限** ] テキストボックスに「 **1200** 」と入力し、[ **ワークフローの関連付け** ] ボタンを選択します。

## <a name="start-the-workflow"></a>ワークフローを開始する
 次に、ワークフローを [ **共有ドキュメント** ] リスト内のいずれかのドキュメントに関連付け、ワークフロー開始フォームを表示します。

#### <a name="to-start-the-workflow"></a>ワークフローを開始するには

1. SharePoint ページで、[ **ホーム** ] ボタンを選択します。

2. クイック起動バーの [ **共有ドキュメント** ] リンクをクリックすると、 **共有ドキュメント** の一覧が表示されます。

3. ページの上部にある [**ライブラリツール**] タブの [**ドキュメント**] リンクを選択し、リボンの [**ドキュメントのアップロード**] ボタンをクリックして、[**共有ドキュメント**] の一覧に新しいドキュメントをアップロードします。

4. [ **ドキュメントのアップロード** ] ダイアログボックスで、[ **参照** ] ボタンをクリックし、任意のドキュメントファイルを選択し、[ **開く** ] ボタンをクリックして、[ **OK** ] をクリックします。

     このダイアログボックスでドキュメントの設定を変更することはできますが、[ **保存** ] ボタンをクリックすると、既定値のままにしておきます。

5. アップロードしたドキュメントを選択し、表示されるドロップダウン矢印をクリックして、[ **ワークフロー** ] 項目を選択します。

6. [のイメージ] をクリックして、[イメージ] を選択します。

     これにより、ワークフロー開始フォームが表示されます。 ([ **自動承認の制限** ] ボックスに表示される値は、関連付けフォームに入力されているため、読み取り専用です)。

7. [ **支出合計** ] テキストボックスに「 **1600**」と入力し、[ **ワークフローの開始** ] をクリックします。

     これにより、[ **共有ドキュメント** ] の一覧が再度表示されます。 "完了" という **値を持つ** 、" **完了** " という名前の新しい列が、ワークフローが開始した項目に追加されます。

8. アップロードしたドキュメントの横にあるドロップダウン矢印をクリックし、 **[ワークフロー] 項目を** 選択して [ワークフローの状態] ページを表示します。 [完了した**ワークフロー**] で、**完了**した値を選択します。 タスクは、[ **タスク** ] セクションの下に一覧表示されます。

9. タスクのタイトルを選択して、タスクの詳細を表示します。

10. **Shareddocuments**リストに戻り、同じドキュメントまたは別のドキュメントを使用してワークフローを再開します。

11. 開始ページで、[関連付け] ページに入力した量以下の金額を入力します (**1200**)。

     このエラーが発生すると、タスクではなく履歴リストのエントリが作成されます。 [ワークフローの状態] ページの [ **ワークフローの履歴** ] セクションにエントリが表示されます。 History イベントの [ **結果** 」列にメッセージが記録されていることを確認します。 これには、 `logToHistoryListActivity1.MethodInvoking` 自動承認された金額を含む、イベントに入力されたテキストが含まれます。

## <a name="next-steps"></a>次のステップ
 ワークフローテンプレートを作成する方法の詳細については、次のトピックを参照してください。

- SharePoint ワークフローの詳細については、「 [Windows Sharepoint Services のワークフロー](/previous-versions/office/developer/sharepoint-2010/ms416312(v=office.14))」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint ワークフローソリューションの作成](../sharepoint/creating-sharepoint-workflow-solutions.md)
- [チュートリアル: ワークフローへのアプリケーションページの追加](../sharepoint/walkthrough-add-an-application-page-to-a-workflow.md)

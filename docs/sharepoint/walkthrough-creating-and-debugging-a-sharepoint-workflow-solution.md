---
title: SharePoint ワークフローソリューションの作成 & デバッグ
description: このチュートリアルでは、SharePoint ワークフローソリューションを作成およびデバッグします。 基本的なシーケンシャルワークフローテンプレートを作成します。 ワークフローアクティビティを作成し、イベントを処理します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.Workflow.WorkflowConditions
- VS.SharePointTools.Workflow.WorkflowList
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, workflows
- workflows [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 637d46eaa9ac9306d63befed1c011c278b46af24
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99952721"
---
# <a name="walkthrough-create-and-debug-a-sharepoint-workflow-solution"></a>チュートリアル: SharePoint ワークフロー ソリューションの作成とデバッグ
  このチュートリアルでは、基本的なシーケンシャルワークフローテンプレートを作成する方法について説明します。 ワークフローは、共有ドキュメントライブラリのプロパティをチェックして、ドキュメントがレビューされているかどうかを確認します。 ドキュメントがレビューされている場合は、ワークフローが終了します。

 このチュートリアルでは、次の作業について説明します。

- で SharePoint リスト定義のシーケンシャルワークフロープロジェクトを作成 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] します。

- ワークフローアクティビティを作成しています。

- ワークフローアクティビティイベントの処理。

> [!NOTE]
> このチュートリアルではシーケンシャルワークフロープロジェクトを使用しますが、ステートマシンワークフロープロジェクトでもプロセスは同じです。
>
> また、次の手順では、Visual Studio のユーザーインターフェイス要素の一部で、コンピューターの名前または場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポート対象エディションの Microsoft Windows および SharePoint。

- 見ることができます。

## <a name="add-properties-to-the-sharepoint-shared-documents-library"></a>SharePoint 共有ドキュメントライブラリにプロパティを追加する
 **共有ドキュメント** ライブラリ内のドキュメントのレビューステータスを追跡するには、SharePoint サイト上の共有ドキュメントに対して、、、およびの3つの新しいプロパティを作成します `Status` `Assignee` `Review Comments` 。 これらのプロパティは、 **共有ドキュメント** ライブラリで定義します。

#### <a name="to-add-properties-to-the-sharepoint-shared-documents-library"></a>SharePoint 共有ドキュメントライブラリにプロパティを追加するには

1. Http:///SitePages/Home.aspx などの SharePoint サイトを \<system name> Web ブラウザーで開きます。

2. [クイック起動] バーで、[ **Shareddocuments**] を選択します。

3. [**ライブラリツール**] リボンの [**ライブラリ**] を選択し、リボンの [**列の作成**] ボタンをクリックして新しい列を作成します。

4. 列に " **ドキュメントの状態**" という名前を設定し、その種類を **[選択] (メニューから選択)** に設定します。次の3つの選択肢を指定し、[ **OK** ] をクリックします。

    - **レビューが必要**

    - **レビュー完了**

    - **要求された変更**

5. さら **に 2** つの列を作成し、担当者に名前を付けると共に、 **コメントをレビュー** します。 担当者の列の種類を1行のテキストとして設定し、レビューコメント列の種類を複数行のテキストとして設定します。

## <a name="enable-documents-to-be-edited-without-requiring-a-check-out"></a>チェックアウトせずにドキュメントを編集できるようにする
 ドキュメントをチェックアウトせずに編集できる場合は、ワークフローテンプレートをテストする方が簡単です。次の手順では、これを有効にするように SharePoint サイトを構成します。

#### <a name="to-enable-documents-to-be-edited-without-checking-them-out"></a>チェックアウトせずにドキュメントを編集できるようにするには

1. クイック起動バーで、[ **共有ドキュメント** ] リンクを選択します。

2. [ **ライブラリツール** ] リボンで、[ **ライブラリ** ] タブを選択し、[ **ライブラリの設定** ] ボタンをクリックして [ **ドキュメントライブラリの設定** ] ページを表示します。

3. **[全般設定**] セクションで、[**バージョン管理の設定**] リンクを選択して、[**バージョン管理の設定**] ページを表示します。

4. [ **編集可能にする前にドキュメントをチェックアウトする必要** があります] の設定が [ **いいえ**] になっていることを確認します。 そうでない場合は、[ **いいえ** ] に変更し、[ **OK** ] をクリックします。

5. ブラウザーを閉じます。

## <a name="create-a-sharepoint-sequential-workflow-project"></a>SharePoint シーケンシャルワークフロープロジェクトを作成する
 シーケンシャルワークフローは、最後のアクティビティが終了するまで順番に実行される一連のステップです。 この手順では、共有ドキュメントリストに適用されるシーケンシャルワークフローを作成します。 ワークフローウィザードを使用して、ワークフローをサイト定義またはリスト定義のいずれかに関連付けることができます。これにより、ワークフローをいつ開始するかを決定できます。

#### <a name="to-create-a-sharepoint-sequential-workflow-project"></a>SharePoint シーケンシャルワークフロープロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. メニューバーで [**ファイル**] [  >  **新規作成**] [プロジェクト] の順に選択し  >   、[**新しいプロジェクト**] ダイアログボックスを表示します。

3. [ **Visual C#** ] または [ **Visual Basic**] の下にある [ **SharePoint** ] ノードを展開し、[ **2010** ] ノードを選択します。

4. [ **テンプレート** ] ペインで、[ **SharePoint 2010] プロジェクト** テンプレートを選択します。

5. [ **名前** ] ボックスに「 **mysharepointworkflow** 」と入力し、[ **OK** ] をクリックします。

     **SharePoint カスタマイズウィザード** が表示されます。

6. [ **デバッグ用のサイトとセキュリティレベルの指定** ] ページで、[ **ファームソリューションとして配置** する] オプションを選択し、[ **完了** ] をクリックして信頼レベルと既定のサイトを受け入れます。

     この手順では、ソリューションの信頼レベルをファームソリューションとして設定します。これは、ワークフロープロジェクトに使用できる唯一のオプションです。 詳細については、「 [サンドボックスソリューションの考慮事項](../sharepoint/sandboxed-solution-considerations.md)」を参照してください。

7. **ソリューションエクスプローラー** で、プロジェクトノードを選択し、メニューバーで [**プロジェクト**] [  >  **新しい項目の追加**] の順に選択します。

8. [ **Visual C#** ] または [ **Visual Basic** で、[ **SharePoint** ] ノードを展開し、[ **2010** ] ノードを選択します。

9. [ **テンプレート** ] ペインで、[ **シーケンシャルワークフロー (ファームソリューションのみ)** ] テンプレートを選択し、[ **追加** ] をクリックします。

     **SharePoint カスタマイズウィザード** が表示されます。

10. [ **デバッグ用のワークフロー名の指定** ] ページで、既定の名前 (**mysharepointworkflow-workflow1.xaml**) をそのまま使用します。 [既定のワークフローテンプレートの種類] の値をそのままにして [ **ワークフローの一覧表示**] を選択し、[ **次へ** ] をクリックします。

11. [ **デバッグセッションに自動的にワークフローを関連付けますか?** ] ページで、[ **次へ** ] をクリックして、すべての既定の設定をそのまま使用します。

     このステップでは、ワークフローが自動的に共有ドキュメントライブラリに関連付けられます。

12. [ **ワークフローの開始方法の条件の指定** ] ページで、[ **ワークフローの開始方法** を選択してください] セクションで既定のオプションを選択したままにして、[ **完了** ] をクリックします。

     このページでは、ワークフローの開始時点を指定できます。 既定では、ユーザーが SharePoint で手動で開始したとき、またはワークフローが関連付けられているアイテムが作成されたときに、ワークフローが開始されます。

## <a name="create-workflow-activities"></a>ワークフローアクティビティの作成
 ワークフローには、実行するアクションを表す1つ以上の *アクティビティ* が含まれています。 ワークフローデザイナーを使用して、ワークフローのアクティビティを並べ替えます。 この手順では、HandleExternalEventActivity と OnWorkFlowItemChanged の2つのアクティビティをワークフローに追加します。 これらのアクティビティは、[ **共有ドキュメント** ] リスト内のドキュメントのレビューステータスを監視します。

#### <a name="to-create-workflow-activities"></a>ワークフローアクティビティを作成するには

1. ワークフローがワークフローデザイナーに表示されます。 そうでない場合は、**ソリューションエクスプローラー** で **Workflow1.cs** または **workflow1.xaml** を開きます。

2. デザイナーで、[ **OnWorkflowActivated1** ] アクティビティを選択します。

3. [**プロパティ**] ウィンドウで、**呼び出さ** れたプロパティの横に「 **onworkflowactivated 化**」と入力し、enter キーを押します。

     コードエディターが開き、onWorkflowActivated 化という名前のイベントハンドラーメソッドが Workflow1.xaml コードファイルに追加されます。

4. ワークフローデザイナーに戻り、[ツールボックス] を開き、[ **Windows workflow** v1.0] ノードを展開します。

5. **ツールボックス** の [ **Windows Workflow** v1.0] ノードで、次のいずれかの手順を実行します。

    1. **While** アクティビティのショートカットメニューを開き、[**コピー**] を選択します。 ワークフローデザイナーで、 **onWorkflowActivated1** アクティビティの下にある行のショートカットメニューを開き、[ **貼り付け**] を選択します。

    2. [ **While** ] アクティビティを **ツールボックス** からワークフローデザイナーにドラッグし、アクティビティを **onWorkflowActivated1** アクティビティの下の行に接続します。

6. **WhileActivity1** アクティビティを選択します。

7. [ **プロパティ** ] ウィンドウで、[ **条件** ] を「コード条件」に設定します。

8. **Condition** プロパティを展開し、子 **条件** プロパティの横に「 **isworkflowpending** 」と入力して、enter キーを押します。

     コードエディターが開き、isWorkflowPending という名前のメソッドが Workflow1.xaml コードファイルに追加されます。

9. ワークフローデザイナーに戻り、[ツールボックス] を開いて、[ **SharePoint ワークフロー** ] ノードを展開します。

10. **ツールボックス** の [ **SharePoint Workflow** ] ノードで、次のいずれかの手順を実行します。

    - **Onworkflowitemchanged** アクティビティのショートカットメニューを開き、[**コピー**] を選択します。 ワークフローデザイナーで、 **whileActivity1** アクティビティ内の行のショートカットメニューを開き、[ **貼り付け**] を選択します。

    - [**ツールボックス**] から [ **Onworkflowitemchanged** ] アクティビティをワークフローデザイナーにドラッグし、アクティビティを **whileActivity1** アクティビティ内の行に接続します。

11. **OnWorkflowItemChanged1** アクティビティを選択します。

12. [ **プロパティ** ] ウィンドウで、次の表に示すようにプロパティを設定します。

    |プロパティ|値|
    |--------------|-----------|
    |**CorrelationToken**|**workflowToken**|
    |**Invoked**|**onWorkflowItemChanged**|

## <a name="handle-activity-events"></a>アクティビティイベントの処理
 最後に、各アクティビティからドキュメントの状態を確認します。 ドキュメントがレビューされている場合、ワークフローは終了します。

#### <a name="to-handle-activity-events"></a>アクティビティイベントを処理するには

1. *Workflow1.cs* または *workflow1.xaml* で、クラスの先頭に次のフィールドを追加し `Workflow1` ます。 このフィールドは、ワークフローが終了したかどうかを判断するためにアクティビティで使用されます。

    ```vb
    Dim workflowPending As Boolean = True
    ```

    ```csharp
    Boolean workflowPending = true;
    ```

2. 次のメソッドを `Workflow1` クラスに追加します。 このメソッドは、ドキュメント `Document Status` リストのプロパティの値をチェックして、ドキュメントが確認されているかどうかを確認します。 `Document Status`プロパティがに設定されている場合、 `Review Complete` `checkStatus` メソッドはフィールドを false に設定して、 `workflowPending` ワークフローが完了する準備ができていることを示します。 

    ```vb
    Private Sub checkStatus()
        If CStr(workflowProperties.Item("Document Status")) = "Review Complete" Then
            workflowPending = False
        End If
    End Sub
    ```

    ```csharp
    private void checkStatus()
    {
        if ((string)workflowProperties.Item["Document Status"] == "Review Complete")
        workflowPending = false;
    }
    ```

3. メソッドとメソッドを呼び出すメソッドに次のコードを追加し `onWorkflowActivated` `onWorkflowItemChanged` `checkStatus` ます。 ワークフローが開始されると、 `onWorkflowActivated` メソッドはメソッドを呼び出して、ドキュメントが `checkStatus` 既にレビューされているかどうかを確認します。 レビューされていない場合、ワークフローは続行されます。 ドキュメントを保存すると、メソッドは `onWorkflowItemChanged` メソッドを `checkStatus` 再度呼び出して、ドキュメントがレビューされているかどうかを確認します。 `workflowPending`フィールドが **true** に設定されている場合、ワークフローは引き続き実行されます。

    ```vb
    Private Sub onWorkflowActivated(ByVal sender As System.Object, ByVal e As System.Workflow.Activities.ExternalDataEventArgs)
        checkStatus()
    End Sub

    Private Sub onWorkflowItemChanged(ByVal sender As System.Object, ByVal e As System.Workflow.Activities.ExternalDataEventArgs)
        checkStatus()
    End Sub
    ```

    ```csharp
    private void onWorkflowActivated(object sender, ExternalDataEventArgs e)
    {
        // Check the status.
        checkStatus();
    }

    private void onWorkflowItemChanged(object sender, ExternalDataEventArgs e)
    {
        // Check the status.
        checkStatus();
    }
    ```

4. 次のコードをメソッドに追加して、 `isWorkflowPending` プロパティの状態を確認し `workflowPending` ます。 ドキュメントが保存されるたびに、 **whileActivity1** アクティビティはメソッドを呼び出し `isWorkflowPending` ます。 このメソッドは、 <xref:System.Workflow.Activities.ConditionalEventArgs.Result%2A> オブジェクトのプロパティを調べて、 <xref:System.Workflow.Activities.ConditionalEventArgs> **WhileActivity1** アクティビティを続行するか終了するかを決定します。 プロパティが **true** に設定されている場合、アクティビティは続行されます。 それ以外の場合は、アクティビティが終了し、ワークフローが終了します。

    ```vb
    Private Sub isWorkflowPending(ByVal sender As System.Object, ByVal e As System.Workflow.Activities.ConditionalEventArgs)
        e.Result = workflowPending
    End Sub
    ```

    ```csharp
    private void isWorkflowPending(object sender, ConditionalEventArgs e)
    {
        e.Result = workflowPending;
    }
    ```

5. プロジェクトを保存します。

## <a name="test-the-sharepoint-workflow-template"></a>SharePoint ワークフローテンプレートをテストする
 デバッガーを起動すると、によって [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ワークフローテンプレートが SharePoint サーバーに配置され、ワークフローが **共有ドキュメント** の一覧に関連付けられます。 ワークフローをテストするには、[ **共有ドキュメント** ] リストのドキュメントからワークフローのインスタンスを開始します。

#### <a name="to-test-the-sharepoint-workflow-template"></a>SharePoint ワークフローテンプレートをテストするには

1. *Workflow1.cs* または *Workflow1.xaml* で、 **onworkflowactivated 化** メソッドの横にブレークポイントを設定します。

2. F5 キーを **押し** て、ソリューションをビルドして実行します。

     SharePoint サイトが表示されます。

3. SharePoint のナビゲーションウィンドウで、[ **共有ドキュメント** ] リンクを選択します。

4. [**共有ドキュメント**] ページで、[**ライブラリツール**] タブの [**ドキュメント**] リンクを選択し、[**ドキュメントのアップロード**] ボタンを選択します。

5. [ **ドキュメントのアップロード** ] ダイアログボックスで、[ **参照** ] ボタンをクリックし、任意のドキュメントファイルを選択し、[ **開く** ] ボタンをクリックして、[ **OK** ] をクリックします。

     これにより、選択したドキュメントが **共有ドキュメント** の一覧にアップロードされ、ワークフローが開始されます。

6. で [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 、メソッドの横にあるブレークポイントでデバッガーが停止することを確認し `onWorkflowActivated` ます。

7. F5 キーを **押し** て実行を続行します。

8. ここでドキュメントの設定を変更することはできますが、[ **保存** ] ボタンを選択すると、ここでは既定値のままにしておきます。

     これにより、既定の SharePoint Web サイトの [ **共有ドキュメント** ] ページに戻ります。

9. [ **共有ドキュメント** ] ページで、[ **mysharepointworkflow-workflow1.xaml** ] 列の下の値が **[処理** 中] に設定されていることを確認します。 これは、ワークフローが進行中であり、ドキュメントがレビューを待機していることを示します。

10. [ **共有ドキュメント** ] ページで、ドキュメントを選択し、表示される矢印をクリックして、[ **プロパティの編集** ] メニュー項目を選択します。

11. [ **ドキュメントの状態** ] を [ **レビュー完了**] に設定し、[ **保存** ] をクリックします。

     これにより、既定の SharePoint Web サイトの [ **共有ドキュメント** ] ページに戻ります。

12. [ **共有ドキュメント** ] ページで、[ **ドキュメントの状態** ] 列の下の値が [ **完了の確認**] に設定されていることを確認します。 [ **共有ドキュメント** ] ページを更新し、[ **mysharepointworkflow-workflow1.xaml** ] 列の下の値が [ **完了**] に設定されていることを確認します。 これは、ワークフローが完了し、ドキュメントがレビューされたことを示します。

## <a name="next-steps"></a>次のステップ
 ワークフローテンプレートを作成する方法の詳細については、次のトピックを参照してください。

- SharePoint ワークフローアクティビティの詳細については、「 [Sharepoint Foundation のワークフローアクティビティ](/previous-versions/office/developer/sharepoint-2010/ms446847(v=office.14))」を参照してください。

- Windows Workflow Foundation アクティビティの詳細については、「system.string [名前空間](/dotnet/api/system.windows.media.color)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint ワークフロー ソリューションの作成](../sharepoint/creating-sharepoint-workflow-solutions.md)
- [SharePoint プロジェクトとプロジェクト項目テンプレート](../sharepoint/sharepoint-project-and-project-item-templates.md)
- [SharePoint ソリューションのビルドとデバッグ](../sharepoint/building-and-debugging-sharepoint-solutions.md)

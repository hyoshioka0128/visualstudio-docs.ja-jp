---
title: 'チュートリアル: SharePoint Designer の再利用可能なワークフローのインポート |Microsoft Docs'
titleSuffix: ''
description: このチュートリアルでは、SharePoint デザイナーで作成した再利用可能なワークフローを Visual Studio SharePoint ワークフロープロジェクトにインポートします。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.WSPImport.ImportWF
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, importing reusable workflows
- reusable workflows [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 0c78a7b1ea0e8de96146367782d9de274f413a5f
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217607"
---
# <a name="walkthrough-import-a-sharepoint-designer-reusable-workflow"></a>チュートリアル: SharePoint Designer の再利用可能なワークフローのインポート

  このチュートリアルでは、sharepoint Designer 2010 で作成された再利用可能なワークフローを sharepoint ワークフロープロジェクトにインポートする方法について説明し [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。

 SharePoint デザイナーで作成したワークフロー、または *宣言型のワークフロー* は、コードではなくステートメントで構成され [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] ます。 SharePoint デザイナー2010では *再利用可能なワークフロー* が導入されています。これは、sharepoint サイトのさまざまなリストで使用できる、移植性のある、宣言型のワークフローです。

 シーケンシャルおよびステートマシンのワークフローなど、で作成されたワークフロー [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)] は、 *コードワークフロー* と呼ばれます。 コードワークフローは、ユーザーがワークフローの動作をカスタマイズできる XML ファイルとコードモジュールで構成されています。

 Visual Studio では、SharePoint デザイナー2010で作成された再利用可能なワークフローをインポートして、SharePoint サイトで使用するためにコードワークフローに変換することができます。

 このチュートリアルでは、次のタスクについて説明します。

- SharePoint デザイナーで、単純な再利用可能なワークフローを作成します。

- SharePoint Designer の再利用可能なワークフローを *.wsp* ファイルと sharepoint にエクスポートします。

-  [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 再利用可能なワークフロープロジェクトのインポートを使用して、.wsp ファイルをにインポートします。

- コードを追加してワークフローを変更する。

- SharePoint サイトでインポートしたワークフローを使用します。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- および SharePoint のサポートされているエディション [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] 。

- 見ることができます。

- Microsoft [!INCLUDE[TLA2#tla_office](../sharepoint/includes/tla2sharptla-office-md.md)] SharePoint Designer 2010。

## <a name="create-target-sharepoint-subsites"></a>ターゲット SharePoint サブサイトの作成
 まず、2つの新しい SharePoint サブサイトを作成します。1つは SharePoint Designer から再利用可能なワークフローをホストし、もう1つは変換されたワークフローをホストします。

#### <a name="to-create-sharepoint-subsites"></a>SharePoint サブサイトを作成するには

1. SharePoint デザイナー2010のメニューバーで、[**ファイル**] [  >  **新しい空の Web サイト**] の順に選択します。

2. [ **新しい空の Web サイト** ] ダイアログボックスで、ワークフローを作成する SharePoint サイトを参照するか、http://<em>SystemName</em>/の値を使用して、[ **OK** ] をクリックします。

    ホームページが表示されます。

3. [ **サブサイト** ] セクションで、[ **新規** ] ボタンをクリックします。

4. [ **新規** ] ダイアログボックスで、左ペインの一覧から [ **SharePoint テンプレート** ] を選択し、右ペインの一覧から [ **チームサイト** ] を選択します。

5. [ **Web サイトの場所を指定** します] ボックスで、URL の " **サブサイト** " を **SPD1** に置き換え、[ **OK** ] をクリックします。

    これにより、新しいサブサイトが SharePoint デザイナーに表示されます。 SharePoint Designer のこのインスタンスを閉じて、最初のインスタンス (最上位サイト) に戻ります。

6. 手順 3-5 を繰り返して2番目のサブサイトを作成します。今度は、の word **サブサイト** を [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] **SPD2** に置き換えます。

## <a name="create-a-sharepoint-designer-reusable-workflow"></a>SharePoint Designer の再利用可能なワークフローを作成する
 SharePoint には、この例で使用できる再利用可能なワークフローが含まれていないため、作成します。 この単純なワークフローでは、ユーザーが特定のタイトルを持つタスク一覧に新しいタスクを入力すると、そのユーザーにタスクが割り当てられます。

#### <a name="to-create-a-sharepoint-designer-reusable-workflow"></a>SharePoint Designer の再利用可能なワークフローを作成するには

1. [ **サブサイト** ] セクションで、 **SPD1** サイトを選択して変更します。

2. リボンで、[ **再利用可能なワークフロー** ] ボタンを選択します。

     再利用可能なワークフローの作成ウィザードが表示されます。

3. [ **名前** ] ボックスに、「 **SPD Task Workflow**」と入力します。

4. [ **コンテンツタイプ** ] の一覧で [ **タスク**] を選択し、[ **OK** ] をクリックします。

     SharePoint Designer ワークフローデザイナーでワークフローが開きます。

5. ワークフローデザイナーで、[手順 1] を選択し、リボンの [ **条件** ] ボタンをクリックします。

6. 条件の一覧で、[ **現在の項目のフィールドが値と等しいかどうか**] を選択します。

     このステップで **は、フィールドが値と等しい場合** にという名前の条件を追加します。

7. [ **フィールドが値と等しい場合** ] 条件で、[ **フィールド]** リンクを選択します。

8. 値の一覧で [ **タイトル**] を選択します。

9. [ **フィールドが値と等しい場合** ] 条件で、[ **値** ] リンクを選択します。

10. ボックスに「 **New task**」と入力します。

     Condition ステートメントは、 **現在の項目: Title が New task であるかどうか** を読み取ります。

11. Condition ステートメントの下にある行を選択し、リボンで [ **アクション** ] ボタンを選択します。

12. アクションの一覧で、[ **現在のアイテムのフィールドの設定**] を選択します。

13. [ **フィールドを値に設定]** アクションで、[ **フィールド]** リンクを選択し、一覧で [ **担当** 者] を選択します。

14. [ **フィールドを値に設定]** アクションで、[ **値** ] リンクを選択し、既存のユーザーとグループの一覧で、アイテムを **作成したユーザー** を選択します。

15. [ **追加** ] ボタンをクリックし、[ **OK** ] をクリックします。

     アクションステートメントが、 **Set 割り当て先ユーザー/グループを現在の項目に** 読み取るようになりました: CreatedBy。

## <a name="save-and-deploy-the-reusable-workflow"></a>再利用可能なワークフローを保存してデプロイする
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]は *.wsp* ファイルのみをインポートするため、再利用可能なワークフローを *.wsp* ファイルとして保存し、SharePoint に配置してからにインポートする必要があり [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。

> [!IMPORTANT]
> 次の手順を実行する実行時エラーが発生した場合は、SharePoint サイトにアクセスできるシステムでこの手順を実行する必要があります。

#### <a name="to-save-and-deploy-the-reusable-workflow"></a>再利用可能なワークフローを保存してデプロイするには

1. SharePoint Designer の上部にある [ **保存** ] をクリックして進行状況を保存し、[ **発行** ] をクリックしてワークフローを **SPD1** SharePoint サイトに配置します。

2. ナビゲーションウィンドウで、[ **ワークフロー** ] オブジェクトを選択します。

3. [ **再利用可能なワークフロー**] で、[ **SPD タスクワークフロー**] を選択します。

4. リボンの [ **テンプレートとして保存** ] ボタンをクリックして、ワークフローを *.wsp* ファイルとして保存します。

5. SharePoint で *.wsp* ファイルを表示するには、ブラウザーで **SPD1** SharePoint サイトを開きます。

6. クイック起動バーで、[ **ライブラリ** ] リンクを選択します。

7. [ **ドキュメントライブラリ** ] セクションで、[ **サイトアセット** ] リンクを選択します。

     **SPD タスクワークフロー** ファイルは、他のサイト資産と共に一覧表示されます。

8. ファイルの一覧で、そのファイルの名前を選択します。

9. [ **ファイルのダウンロード** ] ダイアログボックスで、[ **保存** ] をクリックして、 *.wsp* ファイルをローカルシステムに保存します。

## <a name="import-the-wsp-file-into-visual-studio"></a>.Wsp ファイルを Visual Studio にインポートする
  [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 再利用可能なワークフロープロジェクトのインポートを使用して、.wsp ファイルをにインポートします。 このプロジェクトは、再利用可能な宣言型ワークフローからコードワークフローにワークフローを変換します。 ワークフローが変換された後、コードを使用してその動作を変更します。

#### <a name="to-import-a-workflow-from-a-wsp-file-and-modify-it"></a>.Wsp ファイルからワークフローをインポートして変更するには

1. の [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] メニューバーで、[**ファイル**] [  >  **新規作成**] [プロジェクト] の順に選択し  >  ます。

2. [**新しいプロジェクト**] ダイアログボックスで、[ **Visual C#** ] または [ **Visual Basic**] の下にある [ **SharePoint** ] ノードを展開し、[ **2010** ] ノードを選択します。

3. [ **テンプレート** ] ペインで、[ **再利用可能な SharePoint 2010 のインポート] ワークフロー** テンプレートを選択し、プロジェクトの名前は **WorkflowImportProject1** のままにして、[ **OK** ] をクリックします。

    SharePoint カスタマイズ ウィザードが表示されます。

4. [ **デバッグのサイトとセキュリティレベルの指定** ] ページで、 [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] 前に作成した2番目の SharePoint サブサイトのを入力します。 Http://<em>system name</em>/SPD2.

5. [ **この SharePoint ソリューションの信頼レベル** を指定してください] セクションで、[ **ファームソリューションとして配置** する] オプションを選択し、[ **次へ** ] をクリックします。

    サンドボックスソリューションとファームソリューションの詳細については、「 [サンドボックスソリューションの考慮事項](../sharepoint/sandboxed-solution-considerations.md)」を参照してください。

6. [ **新しいプロジェクトソースの指定** ] ページで、以前に *.wsp* ファイルを保存したシステム上の場所を参照し、ファイルを開き、[ **次へ** ] をクリックします。

   > [!NOTE]
   > [ **完了** ] をクリックすると、 *.wsp* ファイル内の使用可能なすべての項目がインポートされます。

    これにより、インポートに使用できる再利用可能なワークフローの一覧が表示されます。

7. **[インポートする項目の選択**] ボックスで、 **SPD タスクワークフロー** ワークフローを選択し、[**完了**] をクリックします。

    インポート操作が完了すると、 **SPD_Workflow_TestFT** という名前のワークフローを含む **WorkflowImportProject1** という名前のプロジェクトが作成されます。 このフォルダーには、ワークフローの定義ファイル *Elements.xml* とワークフローデザイナーファイル (*xoml*) があります。 デザイナーには、規則ファイル (規則) と分離コードファイル (プロジェクトのプログラミング言語に応じて *.cs* または *.vb*) の2つのファイルがあります。

8. **ソリューションエクスプローラー** で、[**その他のインポート** されたファイル] フォルダーを削除します。

9. *Elements.xml* ファイルで、を削除 `InstantiationURL="_layouts/IniErkflIP.sspx"` します。

10. **ソリューションエクスプローラー** で、[ **WorkflowImportProject1**] を選択し、メニューバーで [**プロジェクト**] を [  >  **スタートアッププロジェクトに設定**] を選択して **WorkflowImportProject1** をスタートアップアイテムとして設定します。

     これにより、プロジェクトのデバッグ時に一覧がすぐに表示されます。

11. " **再利用可能な SharePoint 2010 のインポート" ワークフロー** テンプレートでは、インポートされたワークフローの関連付けプロパティの値がインポートされないため、これらの値を入力する必要があります。 これを行うには、次の手順を実行します。

    1. **ソリューションエクスプローラー** で、[ **SPD_Workflow_TestFT** ] ノードを選択します。

    2. [**ターゲットリスト**] プロパティなど、一覧のプロパティの1つの横にある省略記号 (![ASP.NET Mobile Designer 楕円](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) ボタンをクリックします。

    3. SharePoint カスタマイズウィザードで欠損値を入力し、[ **完了** ] をクリックします。

12. Xoml ファイルを選択し、メニューバーで [デザイナーの **表示**] を選択して、  >  ワークフローデザイナーでインポートしたワークフローを表示します。

13. **ツールボックス** の [ **Windows Workflow** v1.0] ノードで、次のいずれかの手順を実行します。

    - **Code** アクティビティのショートカットメニューを開き、[**コピー**] をクリックします。 ワークフローデザイナーで、 **SequenceActivity1** アクティビティの下にある行のショートカットメニューを開き、[ **貼り付け**] を選択します。

    - [**ツールボックス**] から [ **Code** ] アクティビティをワークフローデザイナーにドラッグし、 **SequenceActivity1** アクティビティの下の行に接続します。

      これにより、 **CodeActivity1** という名前のワークフローデザイナーにアクティビティが追加されます。 このアクティビティでは、ユーザーがワークフローを開始したときにお知らせリストにアナウンスを作成するコードアクションを追加します。

14. 次のいずれかの操作を実行します。

    - **CodeActivity1** をダブルクリックしてイベントハンドラーを生成し、コードを表示します。

    - **CodeActivity1** の [**プロパティ**] ウィンドウで、 **executecode** プロパティの値を **codeActivity_ExecuteCode** に設定します。

15. 既存の **using** ディレクティブまたは **Imports** ディレクティブの下に次のを追加します。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.vb" id="Snippet1":::

16. `codeActivity1_ExecuteCode`を次のように置き換えます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.cs" id="Snippet2":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/workflowimportproject1/workflows/spd_task_workflowft/spd task workflow.xoml.vb" id="Snippet2":::

## <a name="deploy-the-project-and-associate-the-workflow"></a>プロジェクトを配置し、ワークフローを関連付ける
 次に、WorkflowImportProject1 を実行して SharePoint サイトに配置し、ワークフローをタスク一覧に関連付けて、変更された変換済みのワークフローを表示してテストします。

#### <a name="to-deploy-the-project-and-associate-the-workflow"></a>プロジェクトを配置し、ワークフローを関連付けるには

1. で [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 、 **F5** キーを押して実行し、変換されたワークフロープロジェクトを配置します。

2. クイック起動バーで [ **タスク** ] リンクをクリックして、[タスク] の一覧を表示します。

3. [ **リストツール** ] タブで、[ **項目** ] ボタンを選択し、[ **新しい項目** ] ボタンをクリックします。

     [ **タスク-新しい項目** ] ダイアログボックスが表示されます。

4. [ **タイトル** ] ボックスに「 **新しいタスク**」と入力し、[ **保存** ] をクリックします。

5. [ **リストツール** ] タブで、[ **リスト** ] ボタンを選択し、[ **リストの設定** ] ボタンを選択します。

     [ **リストの設定** ] ページが表示されます。

6. [ **権限と管理** ] セクションで、[ **ワークフロー設定** ] リンクを選択します。

     [ **ワークフロー設定** ] ページが表示されます。

7. [ **ワークフローの追加** ] リンクをクリックします。

8. [ **ワークフロー** ] ボックスの一覧で、[ **WorkflowImportProject1**] を選択します。

9. [ **名前** ] ボックスに「 **SPD Workflow Test**」と入力し、[ **OK** ] をクリックします。

10. クイック起動バーで、[ **タスク** ] ボックスの一覧を選択します。

11. [ **新しいタスク**] の横にある矢印をクリックし、一覧で [ **ワークフロー**] を選択します。

12. [ **新しいワークフローの開始** ] セクションで、 **SPD ワークフローテスト** のリンクを選択し、[ **開始** ] をクリックしてワークフローを開始します。

    > [!NOTE]
    > または、ワークフロー設定ウィザードを実行し、ワークフローを自動関連付けに設定することにより、ワークフローをリストに自動的に関連付けることができます。

     ワークフローによって2つのアクションが実行されていることに注意してください。名前はタスクの [ **割り当て先ユーザー/グループ** ] 列に表示され、アナウンスは [ **お知らせ** ] ボックスの一覧に表示されます。

## <a name="see-also"></a>関連項目
- [既存の SharePoint サイトからのアイテムのインポート](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
- [Web パーツまたはアプリケーション ページの再利用できるコントロールを作成する](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)

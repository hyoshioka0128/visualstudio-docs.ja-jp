---
title: SharePoint ワークフローソリューションの作成 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
f1_keywords:
- VSTO.NewSharePointWorkflowWizard.Page3
- VS.SharePointTools.Workflow.WorkflowName
- VSTO.NewSharePointWorkflowWizard.Page2
- VSTO.NewSharePointWorkflowWizard.Page1
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, workflows
- workflows [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2c787009577735213437140513ec095f81c3f43b
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015290"
---
# <a name="create-sharepoint-workflow-solutions"></a>SharePoint ワークフローソリューションの作成

[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]には、SharePoint Web サイトのドキュメントとリストアイテムのライフサイクルを管理するカスタムワークフローを作成するためのツールが用意されています。 提供される項目には、デザイナー、一連のアクティビティコントロール、および必要なアセンブリ参照があります。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]には、ワークフローを作成および構成するための**SharePoint カスタマイズウィザード**も含まれています。

SharePoint の詳細については、「 [Microsoft Sharepoint 製品およびテクノロジ](/sharepoint/dev/)」を参照してください。

## <a name="workflows-in-sharepoint"></a>SharePoint のワークフロー
 ワークフローを SharePoint ライブラリまたはリストに追加する場合は、ライブラリまたはリスト内のすべてのアイテムにビジネスプロセスを適用します。 ワークフローでは、システムまたはユーザーが各項目に対して実行する必要があるアクション (編集する項目の送信、レビューの対象など) を記述します。 これらのアクション (*アクティビティ*と呼ばれます) は、ワークフローの構成要素です。

 で SharePoint ワークフローを作成 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] し、Sharepoint Web サイトに配置することができます。 ワークフローを SharePoint に配置したら、それをライブラリまたはリストに関連付けます。 その後、自動的に、プロセスによって、またはユーザーが手動で起動できます。 ワークフロー操作の詳細については、「 [Visual Studio を使用した SharePoint ワークフローの開発](/sharepoint/dev/general-development/develop-sharepoint-workflows-using-visual-studio)」を参照してください。

## <a name="create-custom-sharepoint-workflows"></a>カスタム SharePoint ワークフローを作成する
 では、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] **シーケンシャルワークフロー**と**ステートマシンワークフロー**の2つの SharePoint ワークフロープロジェクトを使用できます。

 *シーケンシャルワークフロー*は、一連の手順を表します。 最後のアクティビティが完了するまで、ステップは1つずつ実行されます。 シーケンシャルワークフローは、常に実行時に常に連続しています。 外部イベントを受信し、並列ロジックフローを含めることができるため、実行の正確な順序が異なる場合があります。 次の図は、シーケンシャルワークフローの例を示しています。

 ![シーケンシャル ワークフロー](../sharepoint/media/sp-sequential.png "シーケンシャル ワークフロー")

 *ステートマシンワークフロー*は、状態、遷移、およびアクションのセットを表します。 ステートマシンワークフローの手順は、非同期的に実行されます。 つまり、これらは必ずしも1つずつ実行されるわけではなく、アクションと状態によってトリガーされます。 1つの状態が開始状態として割り当てられ、イベントに基づいて、別の状態に遷移が行われます。 ステートマシンには、ワークフローの終了を決定する最終状態を設定できます。 次の図は、ステートマシンワークフローの例を示しています。

 ![ステート マシン ワークフロー](../sharepoint/media/sp-state.png "ステート マシン ワークフロー")

 ワークフローの種類の詳細については、「[ワークフローの種類](/previous-versions/office/developer/sharepoint-2010/ms468447(v=office.14))」を参照してください。

### <a name="use-the-wizard"></a>ウィザードを使用する
 で SharePoint ワークフロープロジェクトを作成する場合は [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 、まず、 **Sharepoint カスタマイズウィザード**で設定を指定します。 このウィザードでは、これらの設定を使用して**ソリューションエクスプローラー**でプロジェクトを作成します。 このプロジェクトには、コードファイル、ワークフローの配置に使用される複数のファイル、およびカスタム SharePoint ワークフローを作成するために必要なアセンブリへの参照が含まれています。

 ワークフローを作成したら、プロパティウィンドウでそのワークフローのプロパティを変更できます。 ほとんどのワークフロープロパティはプロパティウィンドウで直接変更できますが、一部のプロパティでは、省略記号ボタン (![ASP.NET Mobile Designer 楕円](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) をクリックして値を変更する必要があります。 このボタンをクリックすると、 **SharePoint カスタマイズウィザード**が再起動します。 プロパティ値を変更したら、[**完了**] をクリックしてプロパティを確定します。

> [!NOTE]
> "**ワークフローの種類**" プロパティは読み取り専用であり、変更することはできません。 ワークフローの種類を変更する場合は、別のワークフローを作成する必要があります。

## <a name="design-a-sharepoint-workflow"></a>SharePoint ワークフローのデザイン
 ビジネスプロセスのすべての手順を定義したら、ワークフローデザイナーを使用して [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint ワークフローを設計します。 デザイナーを開くには、**ソリューションエクスプローラー**で Workflow1.cs または workflow1.xaml をダブルクリックするか、いずれかのファイルのショートカットメニューを開いて [**開く**] を選択します。

### <a name="activities"></a>アクティビティ
 ワークフローをデザインするには、デザイナーの [**ツールボックス**] から*ワークフロースケジュール*にアクティビティを追加します。 ワークフロースケジュールには、実行する順序でアクティビティのシーケンスが含まれています。

 次の 2 種類のアクティビティがあります。

- *単純なアクティビティ*は、"1 日の遅延" や "Web サービスの開始" など、1つの作業単位を実行します。

- *複合アクティビティ*には他のアクティビティが含まれます。たとえば、条件付きアクティビティに2つの分岐が含まれている場合があります。

  どちらの種類のアクティビティも、**ツールボックス**で使用できます。

  アクティビティには、プロパティ、メソッド、およびイベントを含めることができます。 [**プロパティ**] ウィンドウを使用すると、アクティビティのプロパティを設定できます。

  カスタムアクティビティを作成することもできます。 詳細については、「[チュートリアル: カスタムサイトワークフローアクティビティを作成する](../sharepoint/walkthrough-create-a-custom-site-workflow-activity.md)」を参照してください。

  アクティビティは、**ツールボックス**の次のタブで構成されます。

- **SharePoint ワークフロー**

- **Windows Workflow version 3.0**

- **Windows Workflow version 3.5**

  すべての主要なワークフローアクティビティが SharePoint でサポートされているわけではありません。 詳細については、「 [Windows SharePoint Services のワークフローアクティビティの概要](/previous-versions/office/developer/sharepoint-2010/ms446847(v=office.14))」を参照してください。

#### <a name="sharepoint-workflow-activities"></a>SharePoint ワークフローアクティビティ
 SharePoint の [**ワークフロー** ] タブには、で使用するための特殊なアクティビティが含まれて [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] います。 これらのアクティビティにより、ドキュメントライフサイクルワークフローの開発が簡素化され、効率化されます。 [ **Sharepoint ワークフロー** ] タブに表示されるアクティビティの詳細については、「 [Windows Sharepoint Services のワークフローアクティビティの概要](/previous-versions/office/developer/sharepoint-2010/ms446847(v=office.14))」を参照してください。

#### <a name="windows-workflow-activities"></a>Windows workflow アクティビティ
 [ **Windows Workflow** ] タブには、によって提供されるアクティビティが含まれて [!INCLUDE[TLA#tla_workflow](../sharepoint/includes/tlasharptla-workflow-md.md)] います。 これらのアクティビティを使用して、あらゆる種類の Windows ワークフローアプリケーションのワークフロースケジュールを作成できます。

 [ **Windows ワークフロー** ] タブに表示されるアクティビティの詳細については、「 [Windows Workflow Foundation のアクティビティ](/previous-versions/dotnet/netframework-3.5/ms733615(v=vs.90))」を参照してください。 Windows Workflow Foundation の詳細については、「 [Windows Workflow Foundation の概要](/previous-versions/dotnet/netframework-3.5/ms734631(v=vs.90))」を参照してください。

### <a name="work-with-activities-in-the-designer"></a>デザイナーでのアクティビティの操作
 ワークフロースケジュールには、Windows Workflow アクティビティと SharePoint ワークフローアクティビティの組み合わせを含めることができます。

 デザイナーには、アクティビティを適切に配置および構成するための視覚的な手掛かりが表示されます。 ワークフローのスケジュールにアクティビティをドラッグまたはコピーすると、ワークフロー内のそのアクティビティの有効な場所を示す緑色の正符号 (+) アイコンが表示されます。 アクティビティを無効な場所に配置することはできません。 たとえば、送信アクティビティを Listen アクティビティ分岐の最初のアクティビティとして配置することはできません。 詳細については、「 [SharePoint Designer デベロッパーセンター](https://developer.microsoft.com/office/docs)」を参照してください。

## <a name="collect-information-during-the-workflow"></a>ワークフロー中に情報を収集する
 ワークフローで事前に定義された時間にユーザーから情報を収集することができます。 フォームまたはアイテムのプロパティを使用して、情報を収集できます。

### <a name="forms"></a>フォーム
 フォームは、質問を含むダイアログボックスに似ており、ユーザーが回答を提供する方法を提供します。

 ワークフローで使用できるフォームには、次の4種類があります。

- 関連付け

- 確立

- 変更

- タスク

  これらには、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] アソシエーションフォームと開始フォームの項目テンプレートが含まれています。 *関連付けフォーム*の例としては、ワークフローをインストールする管理者が、コストワークフローの使用制限など、ワークフローに関連するパラメーターを入力することができます。 *開始フォーム*の例として、コストワークフローのユーザーがワークフローに費やした金額を入力できるようにするものがあります。 これらの種類のフォームの詳細については、「 [SharePoint プロジェクトとプロジェクト項目テンプレート](../sharepoint/sharepoint-project-and-project-item-templates.md)」を参照してください。

### <a name="item-properties"></a>項目のプロパティ
 SharePoint ライブラリまたはリストのアイテムのプロパティを使用して、ユーザーから情報を収集することもできます。 メインコードファイル (Workflow1.cs または Workflow1.xaml) は、という名前の SPWorkflowActivationProperties クラスのインスタンスを宣言します `workflowProperties` 。 オブジェクトを使用して、 `workflowProperties` コード内のライブラリまたは一覧のプロパティにアクセスします。 例については、「[チュートリアル: SharePoint ワークフローソリューションの作成とデバッグ](../sharepoint/walkthrough-creating-and-debugging-a-sharepoint-workflow-solution.md)」を参照してください。

## <a name="debug-a-sharepoint-workflow-template"></a>SharePoint ワークフローテンプレートのデバッグ
 SharePoint ワークフロープロジェクトは、他の Web ベースのプロジェクトをデバッグする場合と同じようにデバッグでき [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。 デバッガーを起動すると [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] **sharepoint カスタマイズウィザード**で指定した設定を使用して適切な sharepoint Web サイトが開き、ワークフローテンプレートが適切なライブラリまたはリストに自動的に関連付けられます。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]また、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] *w3wp.exe*という名前のプロセスにデバッガーをアタッチします。

 ワークフローをテストするには、手動で開始する必要があります。 詳細については、「 [SharePoint ソリューションのデバッグ](../sharepoint/debugging-sharepoint-solutions.md)」の「ワークフローのデバッグ」を参照してください。 Web アプリケーションのデバッグの詳細について [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] は、「 [web アプリケーションとスクリプトのデバッグ](../debugger/how-to-enable-debugging-for-aspnet-applications.md)」を参照してください。

## <a name="deploy-a-sharepoint-workflow-template"></a>SharePoint ワークフローテンプレートの配置
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]SharePoint ワークフロープロジェクトは、他の sharepoint プロジェクトと同様に配置 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] できます。 詳細については、「 [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)」を参照してください。

## <a name="import-globally-reusable-workflows"></a>グローバルに再利用可能なワークフローをインポートする
 SharePoint Designer を使用すると、サイト固有の再利用可能なワークフローを作成できるだけでなく、*グローバルに再利用*可能なワークフローを作成できます。これは、任意の sharepoint サイトで使用できるワークフローです。 現在、の再利用可能なワークフロープロジェクトのインポートでは、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] グローバルに再利用可能なワークフローはインポートされません。 ただし、SharePoint デザイナーを使用して、グローバルに再利用可能なワークフローを再利用可能なワークフローに変換することも、変換されていない宣言型のワークフローとしてワークフローをインポートすることもできます。 詳細については、「[既存の SharePoint サイトからのアイテムのインポート](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[チュートリアル: SharePoint ワークフローソリューションの作成とデバッグ](../sharepoint/walkthrough-creating-and-debugging-a-sharepoint-workflow-solution.md)|単純なワークフローを作成およびデバッグする手順について説明し [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。|
|[チュートリアル: 関連付けフォームと開始フォームを使用したワークフローの作成](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)|[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]関連付けフォームと開始フォームを使用して、より完全な機能を備えたワークフローを作成する手順について説明します。|
|[チュートリアル: ワークフローへのアプリケーションページの追加](../sharepoint/walkthrough-add-an-application-page-to-a-workflow.md)|「チュートリアル: ワークフローに入力されたデータを報告する追加の *.aspx*アプリケーションページを追加することによって、[アソシエーションフォームと開始フォームを持つワークフローを作成](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)する」を参照してください。|
|[チュートリアル: カスタムサイトワークフローアクティビティの作成](../sharepoint/walkthrough-create-a-custom-site-workflow-activity.md)|サイトレベルワークフローの作成とカスタムワークフローアクティビティの作成という2つの主要なタスクを実行する方法を示します。|
|[チュートリアル: SharePoint Designer の再利用可能なワークフローを Visual Studio にインポートする](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)|Sharepoint Designer 2010 で作成された再利用可能な宣言型ワークフローを sharepoint プロジェクトにインポートする方法を示し [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。|

## <a name="see-also"></a>関連項目

- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
- [SharePoint ソリューションのビルドとデバッグ](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [SharePoint のアプリケーションページの作成](../sharepoint/creating-application-pages-for-sharepoint.md)
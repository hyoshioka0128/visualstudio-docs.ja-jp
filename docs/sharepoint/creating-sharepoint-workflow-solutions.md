---
title: SharePoint ワークフロー ソリューションの作成 | Microsoft Docs
description: Sharepoint Web サイトのドキュメントとリスト アイテムのライフサイクルを管理するカスタム ワークフローを作成するには、ツールを使用して SharePoint ワークフロー ソリューションを作成します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: dd3f88df661537434c79a8b0049f90ddbce14c70
ms.sourcegitcommit: ad2c820b280b523a7f7aef89742cdb719354748f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94850612"
---
# <a name="create-sharepoint-workflow-solutions"></a>SharePoint ワークフロー ソリューションの作成

[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] には、SharePoint Web サイト上のドキュメントとリスト項目のライフ サイクルを管理するカスタム ワークフロー作成用のツールが用意されています。 用意されている項目として、デザイナー、一連のアクティビティ コントロール、必要なアセンブリ参照があります。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] には、ワークフローの作成および構成に役立つ **SharePoint カスタマイズ ウィザード** も含まれています。

SharePoint の詳細については、[Microsoft SharePoint 製品およびテクノロジ](/sharepoint/dev/)のページを参照してください。

## <a name="workflows-in-sharepoint"></a>SharePoint のワークフロー
 ワークフローを SharePoint ライブラリまたはリストに追加する場合は、ライブラリまたはリスト内のすべての項目にビジネス プロセスを適用します。 ワークフローでは、各項目に対して実行される必要があるシステムまたはユーザーによるアクション (編集とその後のレビューの対象である項目を送信するなど) を記述します。 このようなアクションは、"*アクティビティ*" と呼ばれ、ワークフローの構成要素です。

 SharePoint ワークフローは [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で作成し、SharePoint Web サイトに配置することができます。 SharePoint への配置後、ワークフローをライブラリまたはリストに関連付けます。 その後、自動的にまたはプロセスによって、あるいはユーザーが手動で起動できます。 ワークフロー操作の詳細については、「[Visual Studio を使用して SharePoint ワークフローを開発する](/sharepoint/dev/general-development/develop-sharepoint-workflows-using-visual-studio)」を参照してください。

## <a name="create-custom-sharepoint-workflows"></a>カスタム SharePoint ワークフローを作成する
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] では、2 つの SharePoint ワークフロー プロジェクトを使用できます。**シーケンシャル ワークフロー** と **ステート マシン ワークフロー** です。

 "*シーケンシャル ワークフロー*" は一連のステップを表します。 最後のアクティビティが完了するまで、ステップが 1 つずつ実行されます。 シーケンシャル ワークフローの実行は常に、厳密に逐次処理されます。 外部イベントを受信する場合や、並列ロジック フローを含む場合があるため、実行の正確な順序は一定でない可能性があります。 次の図は、シーケンシャル ワークフローの例を示しています。

 ![シーケンシャル ワークフロー](../sharepoint/media/sp-sequential.png "シーケンシャル ワークフロー")

 "*ステート マシン ワークフロー*" は、一連の状態、遷移、アクションを表します。 ステート マシン ワークフローのステップは、非同期的に実行されます。 つまり、それらは必ずしも次々に実行されるわけではなく、アクションと状態によってトリガーされます。 1 つの状態が開始状態として割り当てられ、その後、イベントに基づいて別の状態への遷移が行われます。 ステート マシンには、ワークフローの終了を決定する最終状態を設定できます。 次の図は、ステート マシン ワークフローの例を示しています。

 ![ステート マシン ワークフロー](../sharepoint/media/sp-state.png "ステート マシン ワークフロー")

 ワークフローの種類の詳細については、「[ワークフローの種類](/previous-versions/office/developer/sharepoint-2010/ms468447(v=office.14))」を参照してください。

### <a name="use-the-wizard"></a>ウィザードを使用する
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で SharePoint ワークフロー プロジェクトを作成する場合は、まず、**SharePoint カスタマイズ ウィザード** で設定を指定します。 このウィザードでは、これらの設定を使用して **ソリューション エクスプローラー** でプロジェクトを作成します。 このプロジェクトには、コード ファイル、ワークフローの配置に使用される複数のファイル、カスタム SharePoint ワークフローを作成するために必要なアセンブリへの参照が含まれています。

 ワークフローを作成した後、プロパティ ウィンドウでそのプロパティを変更できます。 ほとんどのワークフロー プロパティはプロパティ ウィンドウで直接変更できますが、一部のプロパティについては、省略記号ボタン (![ASP.NET モバイル デザイナーの省略記号](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) をクリックして値を変更する必要があります。 このボタンによって **SharePoint カスタマイズ ウィザード** が再起動されます。 プロパティ値を変更した後、 **[完了]** ボタンを選択して設定を確定します。

> [!NOTE]
> **[ワークフローの種類]** プロパティは読み取り専用であるため、変更できません。 ワークフローの種類を変更したい場合は、別のワークフローを作成する必要があります。

## <a name="design-a-sharepoint-workflow"></a>SharePoint ワークフローを設計する
 ビジネス プロセスのすべてのステップを定義したら、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ワークフロー デザイナーを使用して SharePoint ワークフローを設計します。 デザイナーを開くには、**ソリューション エクスプローラー** で Workflow1.cs または Workflow1.vb をダブルクリックするか、それらのファイルのいずれかのショートカット メニューを開いて **[開く]** を選択します。

### <a name="activities"></a>アクティビティ
 ワークフローを設計するには、**ツールボックス** から、デザイナーの *ワークフロー スケジュール* にアクティビティを追加します。 ワークフロースケジュールには、一連のアクティビティが実行される順序で含まれています。

 次の 2 種類のアクティビティがあります。

- "*単純なアクティビティ*" は、"1 日の遅延" や "Web サービスの開始" など、1 つの作業単位を実行します。

- "*複合アクティビティ*" には、他のアクティビティが含まれています。たとえば、条件付きアクティビティに 2 つの分岐が含まれている場合があります。

  どちらの種類のアクティビティも、**ツールボックス** で使用できます。

  アクティビティにはプロパティ、メソッド、およびイベントを設定できます。 アクティビティのプロパティを設定するには、 **[プロパティ]** ウィンドウを使用します。

  カスタム アクティビティを作成することもできます。 詳細については、「[チュートリアル:サイトのカスタム ワークフロー アクティビティの作成](../sharepoint/walkthrough-create-a-custom-site-workflow-activity.md)」を参照してください。

  アクティビティは、**ツールボックス** の次のタブで構成されています。

- **SharePoint ワークフロー**

- **Windows Workflow v3.0**

- **Windows Workflow v3.5**

  すべての主要なワークフロー アクティビティが SharePoint でサポートされているわけではありません。 詳細については、[Windows SharePoint Services のワークフロー アクティビティの概要](/previous-versions/office/developer/sharepoint-2010/ms446847(v=office.14))に関するページを参照してください。

#### <a name="sharepoint-workflow-activities"></a>SharePoint ワークフローのアクティビティ
 **[SharePoint ワークフロー]** タブには、[!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] で使用するための特殊なアクティビティが含まれています。 これらのアクティビティにより、ドキュメントのライフ サイクル ワークフローの開発が簡素化され、効率化されます。 **[SharePoint ワークフロー]** タブに表示されるアクティビティの詳細については、[Windows SharePoint Services のワークフロー アクティビティの概要](/previous-versions/office/developer/sharepoint-2010/ms446847(v=office.14))に関するページを参照してください。

#### <a name="windows-workflow-activities"></a>Windows Workflow のアクティビティ
 **Windows Workflow** のタブには、[!INCLUDE[TLA#tla_workflow](../sharepoint/includes/tlasharptla-workflow-md.md)] によって提供されるアクティビティが含まれています。 これらのアクティビティを使用して、あらゆる種類の Windows ワークフロー アプリケーションのワークフロー スケジュールを作成できます。

 **Windows Workflow** のタブに表示されるアクティビティの詳細については、「[Windows Workflow Foundation アクティビティ](/previous-versions/dotnet/netframework-3.5/ms733615(v=vs.90))」を参照してください。 Windows Workflow Foundation の詳細については、「[Windows Workflow Foundation の概要](/previous-versions/dotnet/netframework-3.5/ms734631(v=vs.90))」を参照してください。

### <a name="work-with-activities-in-the-designer"></a>デザイナーでアクティビティを操作する
 ワークフロー スケジュールには、Windows Workflow アクティビティと SharePoint ワークフロー アクティビティの組み合わせを含めることができます。

 デザイナーには、アクティビティを適切に配置および構成するための視覚的な手掛かりが表示されます。 ワークフロー スケジュールにアクティビティをドラッグまたはコピーするとき、ワークフロー内でのそのアクティビティの有効な位置を示す緑色の正符号 (+) アイコンが、デザイナーに表示されます。 アクティビティを無効な場所に配置することはできません。 たとえば、送信アクティビティをリッスン アクティビティ分岐の最初のアクティビティとして配置することはできません。 詳細については、[SharePoint Designer デベロッパー センター](https://developer.microsoft.com/office/docs)を参照してください。

## <a name="collect-information-during-the-workflow"></a>ワークフロー中に情報を収集する
 ワークフローで事前に定義された時間にユーザーから情報を収集することができます。 フォームまたは項目のプロパティを使用して、情報を収集できます。

### <a name="forms"></a>フォーム
 フォームは、質問を含むダイアログ ボックスに似ており、ユーザーが回答を入力する方法を提供するものです。

 ワークフローで使用できるフォームには、次の 4 種類があります。

- 関連付け

- 開始

- 変更

- タスク

  これらのうち、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] には、関連付けフォームと開始フォームの項目テンプレートが含まれています。 "*関連付けフォーム*" の例としては、ワークフローをインストールする管理者が、ワークフローに関連するパラメーター (経費ワークフローの支出限度など) を入力できるものがあります。 "*開始フォーム*" の例としては、経費ワークフローのユーザーがワークフローに支出額を入力できるものがあります。 これらの種類のフォームに関する詳細については、「[SharePoint プロジェクトとプロジェクト項目テンプレート](../sharepoint/sharepoint-project-and-project-item-templates.md)」を参照してください。

### <a name="item-properties"></a>項目のプロパティ
 SharePoint ライブラリまたはリストの項目のプロパティを使用して、ユーザーから情報を収集することもできます。 メイン コード ファイル (Workflow1.cs または Workflow1.vb) で、`workflowProperties` という名前の Microsoft.SharePoint.Workflow.SPWorkflowActivationProperties.WorkflowProperties クラスのインスタンスを宣言します。 コード内で `workflowProperties` オブジェクトを使用して、ライブラリまたは一覧のプロパティにアクセスします。 例については、「[チュートリアル: SharePoint ワークフロー ソリューションの作成とデバッグ](../sharepoint/walkthrough-creating-and-debugging-a-sharepoint-workflow-solution.md)」を参照してください。

## <a name="debug-a-sharepoint-workflow-template"></a>SharePoint ワークフロー テンプレートをデバッグする
 SharePoint ワークフロー プロジェクトは、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] の他の Web ベース プロジェクトをデバッグする場合と同じようにデバッグできます。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] デバッガーを起動すると、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、**SharePoint カスタマイズ ウィザード** で指定した設定を使用して適切な SharePoint Web サイトが開かれ、ワークフロー テンプレートが適切なライブラリまたはリストに自動的に関連付けられます。 また、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によって、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] デバッガーが *w3wp.exe* という [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] プロセスにアタッチされます。

 ワークフローをテストするには、手動で開始する必要があります。 詳細については、「[SharePoint ソリューションのデバッグ](../sharepoint/debugging-sharepoint-solutions.md)」の「ワークフローのデバッグ」のセクションを参照してください。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Web アプリケーションのデバッグの詳細については、[Web アプリケーションとスクリプトのデバッグ](../debugger/how-to-enable-debugging-for-aspnet-applications.md)に関するページを参照してください。

## <a name="deploy-a-sharepoint-workflow-template"></a>SharePoint ワークフロー テンプレートを配置する
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint ワークフロー プロジェクトは、他の [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint プロジェクトと同様に配置できます。 詳細については、「[SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)」を参照してください。

## <a name="import-globally-reusable-workflows"></a>グローバルに再利用可能なワークフローをインポートする
 SharePoint Designer を使用すると、サイト固有の再利用可能なワークフローを作成できるだけでなく、"*グローバルに再利用可能なワークフロー*" を作成できます。これは、どの SharePoint サイトでも使用できるワークフローです。 現在、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] の再利用可能なワークフロー プロジェクトのインポートによって、グローバルに再利用可能なワークフローはインポートされません。 ただし、SharePoint Designer を使用して、グローバルに再利用可能なワークフローを再利用可能なワークフローに変換することや、変換されていない宣言型のワークフローとしてワークフローをインポートすることができます。 詳細については、「[既存の SharePoint サイトからのアイテムのインポート](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[チュートリアル: SharePoint ワークフロー ソリューションの作成とデバッグ](../sharepoint/walkthrough-creating-and-debugging-a-sharepoint-workflow-solution.md)|単純な [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ワークフローを作成およびデバッグする手順について説明します。|
|[チュートリアル: 関連付けフォームと開始フォームを持つワークフローの作成](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)|関連付けフォームと開始フォームを使用して完全な機能を備えた [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ワークフローを作成する手順について説明します。|
|[チュートリアル: ワークフローへのアプリケーション ページの追加](../sharepoint/walkthrough-add-an-application-page-to-a-workflow.md)|「[チュートリアル: 関連付けフォームと開始フォームを持つワークフローの作成](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)」のトピックに基づいて、ワークフローに入力されたデータを報告する *.aspx* アプリケーション ページを追加します。|
|[チュートリアル: サイトのカスタム ワークフロー アクティビティの作成](../sharepoint/walkthrough-create-a-custom-site-workflow-activity.md)|サイトレベル ワークフローの作成およびカスタム ワークフロー アクティビティの作成という 2 つの主要なタスクを実行する方法を示します。|
|[チュートリアル: SharePoint Designer の再利用可能なワークフローを Visual Studio にインポートする](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)|SharePoint Designer 2010 で作成した再利用可能な宣言型ワークフローを [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint プロジェクトにインポートする方法について説明します。|

## <a name="see-also"></a>関連項目

- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
- [SharePoint ソリューションのビルドとデバッグ](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [SharePoint のアプリケーション ページの作成](../sharepoint/creating-application-pages-for-sharepoint.md)
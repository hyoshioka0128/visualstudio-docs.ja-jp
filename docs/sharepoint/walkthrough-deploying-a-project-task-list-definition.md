---
title: 'チュートリアル: プロジェクトタスク一覧 Definition | の配置Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, deploying
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b5639fe7a1b35dea41b14be3730986ad7c7309b7
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015766"
---
# <a name="walkthrough-deploy-a-project-task-list-definition"></a>チュートリアル: プロジェクトタスクリスト定義の配置

このチュートリアルでは、を使用し [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)] て、プロジェクトタスクを追跡する SharePoint リストを作成、カスタマイズ、デバッグ、および配置する方法について説明します。

[!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>前提条件

- サポート対象エディションの Microsoft Windows および SharePoint。

- Visual Studio 2017 または Azure DevOps Services。

## <a name="create-a-sharepoint-list"></a>SharePoint リストを作成する

SharePoint リストプロジェクトを作成し、リスト定義をタスクに関連付けます。

1. [**新しいプロジェクト**] ダイアログボックスを開き、[ **SharePoint** ] ノードを展開して、[ **2010** ] ノードを選択します。

2. [**テンプレート**] ペインで、[ **SharePoint 2010] プロジェクト**テンプレートを選択し、プロジェクトに**projecttasklist**という名前を指定して、[ **OK** ] をクリックします。

     **SharePoint カスタマイズウィザード**が表示されます。

3. デバッグに使用するローカル SharePoint サイトを指定し、[**ファームソリューションとして配置**する] オプションボタンをクリックして、[**完了**] をクリックします。

4. プロジェクトのショートカットメニューを開き、[ **Add**  >  **新しい項目**の追加] を選択します。

5. [**テンプレート**] ペインで、**リスト**テンプレートを選択し、[**追加**] をクリックします。

     **SharePoint カスタマイズウィザード**が表示されます。

6. [**一覧に表示する名前**を指定してください] ボックスに、「 **Project タスク一覧**」と入力します。

7. [**既存のリストの種類に基づいてカスタマイズ可能ではないリストを作成する**] オプションボタンを選択し、一覧で [**タスク**] を選択し、[**完了**] をクリックします。

     リスト、機能、およびパッケージが**ソリューションエクスプローラー**に表示されます。

## <a name="add-an-event-receiver"></a>イベントレシーバーを追加する

タスク一覧では、タスクの期限と説明を自動的に設定するイベントレシーバーを追加できます。 次の手順では、単純なイベントハンドラーをイベントレシーバーとしてリストインスタンスに追加します。

1. プロジェクトノードのショートカットメニューを開き、[**追加**]、[**新しい項目**] の順に選択します。

2. SharePoint テンプレートの一覧で、[**イベントレシーバー** ] テンプレートを選択し、「 **Projecttasklisteventreceiver**」という名前を指定します。

     **SharePoint カスタマイズウィザード**が表示されます。

3. [**イベントレシーバー設定の選択**] ページで、[イベントレシーバー**の**種類] ボックスの一覧から [**リスト項目イベント**] を選択します。

4. [**イベントソース**] ボックスの一覧で、[**タスク**] を選択します。

5. 処理するイベントの一覧で、**項目**の横にあるチェックボックスをオンにし、[**完了**] をクリックします。

     新しいイベントレシーバーノードが、 **Projecttasklisteventreceiver**という名前のコードファイルと共にプロジェクトに追加されます。

6. `ItemAdded` **Projecttasklisteventreceiver**コードファイルのメソッドにコードを追加します。 新しいタスクが追加されるたびに、既定の期限日と説明がタスクに追加されます。 既定の期限は2009年7月1日です。

     [!code-vb[SPProjectTaskList#1](../sharepoint/codesnippet/VisualBasic/projecttasklist1/projecttasklisteventreceiver/projecttasklisteventreceiver.vb#1)]
     [!code-csharp[SPProjectTaskList#1](../sharepoint/codesnippet/CSharp/projecttasklist/projecttasklisteventreceiver/projecttasklisteventreceiver.cs#1)]

## <a name="customize-the-project-task-list-feature"></a>プロジェクトタスク一覧機能のカスタマイズ

SharePoint ソリューションを作成すると、Visual Studio によって既定のプロジェクト項目の機能が自動的に作成されます。 フィーチャーデザイナーを使用して、SharePoint サイトのプロジェクトタスク一覧の設定をカスタマイズできます。

1. **ソリューションエクスプローラー**で、[**機能**] を展開します。

2. **Feature1.feature**のショートカットメニューを開き、[**デザイナーの表示**] を選択します。

3. [**タイトル**] ボックスに「 **Project タスク一覧機能**」と入力します。

4. [**スコープ**] ボックスの一覧で [ **Web**] を選択します。

5. [**プロパティ**] ウィンドウで、[**バージョン**] プロパティの値として「 **1.0.0.0** 」と入力します。

## <a name="customize-the-project-task-list-package"></a>プロジェクトタスク一覧パッケージのカスタマイズ

SharePoint プロジェクトを作成すると、既定のプロジェクト項目を含む機能が Visual Studio によって自動的にパッケージに追加されます。 パッケージデザイナーを使用して、SharePoint サイトのプロジェクトタスク一覧の設定をカスタマイズできます。

1. **Solutionexplorer**で、[**パッケージ**] のショートカットメニューを開き、[**デザイナーの表示**] を選択します。

2. [**名前**] ボックスに、「 **Projecttasklistpackage**」と入力します。

3. [ **Web サーバーのリセット**] チェックボックスをオンにします。

## <a name="build-and-test-the-project-task-list"></a>プロジェクトタスクリストのビルドとテスト

プロジェクトを実行すると、SharePoint サイトが開きます。 ただし、手動でタスク一覧の場所に移動する必要があります。

1. F5 キーを**押し**て、プロジェクトのタスク一覧をビルドおよび配置します。

     SharePoint サイトが開きます。

2. [**ホーム**] タブを選択します。

3. 左側のサイドバーで、[**プロジェクトタスク一覧**] リンクを選択します。

     [プロジェクトのタスク一覧] ページが表示されます。

4. [**リストツール**] タブで、[**項目**] タブを選択します。

5. [**項目**] グループで、[**新しい項目**] ボタンをクリックします。

6. [**タイトル**] ボックスに「 **Task1**」と入力します。

7. [**保存**] ボタンをクリックします。

     サイトが更新されると、 **Task1**タスクに期限日7/1/2009 が表示されます。

8. [ **Task1**] を選択します。

     タスクの詳細ビューが表示され、説明に "これは重要なタスクです。" と表示されます。

## <a name="deploy-the-project-task-list"></a>プロジェクトタスク一覧の配置

プロジェクトタスクリストをビルドしてテストしたら、それを*ローカルシステム*または*リモートシステム*に配置できます。 ローカルシステムは、ソリューションを開発したコンピューターと同じですが、リモートシステムは別のコンピューターです。

### <a name="to-deploy-the-project-task-list-to-the-local-system"></a>ローカルシステムにプロジェクトタスク一覧を配置するには

Visual Studio のメニューバーで、[**ビルド**] [ソリューションの配置] の順に選択し  >  **Deploy Solution**ます。

Visual Studio は IIS アプリケーションプールをリサイクルし、ソリューションの既存のバージョンを取り消し、ソリューションパッケージ (*.wsp*) ファイルを SharePoint にコピーして、機能をアクティブ化します。 これで、SharePoint でソリューションを使用できるようになりました。 配置構成の手順の詳細については、「[方法: SharePoint の配置構成を編集する](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md)」を参照してください。

### <a name="to-deploy-the-project-task-list-to-a-remote-system"></a>リモートシステムにプロジェクトタスク一覧を配置するには

1. Visual Studio のメニューバーで、[**ビルド**] [発行] の順に選択し  >  **Publish**ます。

2. [**発行**] ダイアログボックスで、[**ファイルシステムに発行する**] オプションボタンをクリックします。

     [**発行**] ダイアログボックスで目的の場所を変更するには、省略記号ボタンの![省略記号アイコン](../sharepoint/media/ellipsisicon.gif "省略記号アイコン")をクリックし、別の場所に移動します。

3. **[発行]** をクリックします。

     ソリューションの *.wsp*ファイルが作成されます。

4. *.Wsp*ファイルをリモートの SharePoint システムにコピーします。

5. PowerShell コマンドを使用して、 `Add-SPUserSolution` リモートの SharePoint インストールにパッケージをインストールします。 (ファームソリューションの場合は、コマンドを使用し `Add-SPSolution` ます)。

     たとえば、「 `Add-SPUserSolution C:\MyProjects\ProjectTaskList\ProjectTaskList\bin\Debug\ProjectTaskList.wsp` 」のように入力します。

6. PowerShell コマンドを使用し `Install-SPUserSolution` て、ソリューションを配置します。 (ファームソリューションの場合は、コマンドを使用し `Install-SPSolution` ます)。

     たとえば、「 `Install-SPUserSolution -Identity ProjectTaskList.wsp -Site http://NewSiteName` 」のように入力します。

     リモート配置の詳細については、「SharePoint 2010 での[ソリューションの使用](/previous-versions/office/developer/sharepoint-2010/ee534972(v=office.14))と[PowerShell を使用したソリューションの追加と配置](http://www.dotnetmafia.com/blogs/dotnettipoftheday/archive/2009/12/02/adding-and-deploying-solutions-with-powershell-in-sharepoint-2010.aspx)」を参照してください。

## <a name="next-steps"></a>次のステップ

SharePoint ソリューションをカスタマイズおよび展開する方法の詳細については、次のトピックを参照してください。

- [チュートリアル: SharePoint のサイト列、コンテンツタイプ、およびリストの作成](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)

- [方法: イベントレシーバーを作成する](../sharepoint/how-to-create-an-event-receiver.md)

- [SharePoint Server 用 Windows PowerShell 2010](/powershell/module/sharepoint-server)

## <a name="see-also"></a>関連項目
[SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)

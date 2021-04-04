---
title: 'チュートリアル: カスタムサイトワークフロー活動を作成する |Microsoft Docs'
description: このチュートリアルでは、「Visual Studio を使用してサイトレベルの SharePoint ワークフローのカスタムアクティビティを作成する方法」を参照してください。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom workflow activities [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, custom workflow activities
- site workflows [SharePoint development in Visual Studio]
- workflow activities [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, site workflows
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 29a3cd6fe37ec824a3db3a2c83aad7434d0018cb
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106218049"
---
# <a name="walkthrough-create-a-custom-site-workflow-activity"></a>チュートリアル: サイトのカスタム ワークフロー アクティビティの作成
  このチュートリアルでは、を使用してサイトレベルワークフローのカスタムアクティビティを作成する方法について説明し [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。 (サイトレベルのワークフローは、サイトのリストだけでなく、サイト全体に適用されます)。カスタムアクティビティでは、バックアップのアナウンスリストを作成し、お知らせリストの内容をそこにコピーします。

 このチュートリアルでは、次のタスクについて説明します。

- サイトレベルのワークフローを作成する。

- カスタムワークフローアクティビティを作成しています。

- SharePoint リストの作成と削除。

- 項目を1つのリストから別のリストにコピーする。

- クイック起動バーにリストを表示します。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- および SharePoint のサポートされているエディション [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] 。

- 見ることができます。

## <a name="create-a-site-workflow-custom-activity-project"></a>サイトワークフローカスタムアクティビティプロジェクトの作成
 まず、カスタムワークフローアクティビティを保持してテストするプロジェクトを作成します。

#### <a name="to-create-a-site-workflow-custom-activity-project"></a>サイトワークフローカスタムアクティビティプロジェクトを作成するには

1. メニューバーで [**ファイル**] [  >  **新規作成**] [プロジェクト] の順に選択し  >   、[**新しいプロジェクト**] ダイアログボックスを表示します。

2. [ **Visual C#** ] または [ **Visual Basic**] の下にある [ **SharePoint** ] ノードを展開し、[ **2010** ] ノードを選択します。

3. [ **テンプレート** ] ペインで、[ **SharePoint 2010] プロジェクト** テンプレートを選択します。

4. [ **名前** ] ボックスに「" **アナウンス ementbackup**"」と入力し、[ **OK** ] をクリックします。

     **SharePoint カスタマイズウィザード** が表示されます。

5. [ **デバッグ用のサイトとセキュリティレベルの指定** ] ページで、[ **ファームソリューションとして配置** する] オプションを選択し、[ **完了** ] をクリックして信頼レベルと既定のサイトを受け入れます。

     この手順では、ソリューションの信頼レベルをファームソリューションとして設定します。これは、ワークフロープロジェクトに使用できる唯一のオプションです。

6. **ソリューションエクスプローラー** で、プロジェクトノードを選択し、メニューバーで [**プロジェクト**] [  >  **新しい項目の追加**] の順に選択します。

7. [ **Visual C#** ] または [ **Visual Basic** で、[ **SharePoint** ] ノードを展開し、[ **2010** ] ノードを選択します。

8. [ **テンプレート** ] ペインで、[ **シーケンシャルワークフロー (ファームソリューションのみ)** ] テンプレートを選択し、[ **追加** ] をクリックします。

     **SharePoint カスタマイズウィザード** が表示されます。

9. [ **デバッグ用のワークフロー名の指定** ] ページで、既定の名前をそのまま使用します (workflow1.xaml)。 ワークフローテンプレートの種類を [ **サイトのワークフロー**] に変更し、[ **次へ** ] をクリックします。

10. 残りの既定の設定をそのまま使用するには、[ **完了** ] をクリックします。

## <a name="add-a-custom-workflow-activity-class"></a>カスタムワークフローアクティビティクラスを追加する
 次に、クラスをプロジェクトに追加して、カスタムワークフローアクティビティのコードを含めます。

#### <a name="to-add-a-custom-workflow-activity-class"></a>カスタムワークフローアクティビティクラスを追加するには

1. メニューバーで、[**プロジェクト**] [  >  **新しい項目の追加**] の順に選択し、[**新しい項目の追加**] ダイアログボックスを表示します。

2. [ **インストールされたテンプレート** ] ツリービューで、[ **コード** ] ノードを選択し、プロジェクト項目テンプレートの一覧で **クラス** テンプレートを選択します。 既定の名前である Class1 を使用します。 **[追加]** ボタンを選びます。

3. Class1 のすべてのコードを次のコードに置き換えます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/announcementbackup/class1.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/announcementbackupvb/class1.vb" id="Snippet1":::

4. プロジェクトを保存し、メニューバーで [ビルド] [ソリューションの **ビルド**] の順に選択し  >  ます。

     Class1 は、[**発表**] タブの [**ツールボックス**] にカスタムアクションとして表示されます。

## <a name="add-the-custom-activity-to-the-site-workflow"></a>サイトワークフローにカスタムアクティビティを追加する
 次に、カスタムコードを含むアクティビティをワークフローに追加します。

#### <a name="to-add-a-custom-activity-to-the-site-workflow"></a>サイトワークフローにカスタムアクティビティを追加するには

1. ワークフローデザイナーの [デザイン] ビューで Workflow1.xaml を開きます。

2. [ **ツールボックス** ] から [class1] をドラッグしてアクティビティの下に表示されるようにするか、[ `onWorkflowActivated1` class1] のショートカットメニューを開き、[ **コピー**] を選択して、アクティビティの下にある行のショートカットメニューを開き、 `onWorkflowActivated1` [ **貼り付け**] を選択します。

3. プロジェクトを保存します。

## <a name="test-the-site-workflow-custom-activity"></a>サイトワークフローのカスタムアクティビティのテスト
 次に、プロジェクトを実行し、サイトのワークフローを開始します。 カスタムアクティビティでは、バックアップアナウンスリストが作成され、現在のアナウンスリストの内容がそこにコピーされます。 また、このコードでは、バックアップリストが既に存在しているかどうかも確認してから作成します。 バックアップリストが既に存在する場合は、削除されます。 また、このコードでは、SharePoint サイトのクイック起動バーに新しい一覧へのリンクも追加されます。

#### <a name="to-test-the-site-workflow-custom-activity"></a>サイトワークフローのカスタムアクティビティをテストするには

1. **F5** キーを押してプロジェクトを実行し、SharePoint に配置します。

2. クイック起動バーで [ **リスト** ] リンクを選択すると、SharePoint サイトで使用できるすべてのリストが表示されます。 **お知らせという** 名前のアナウンスの一覧は1つだけであることに注意してください。

3. SharePoint web ページの上部で、[ **サイトワークフロー** ] リンクを選択します。

4. [新しいワークフローを開始します] セクションで、[ **workflow1.xaml** ] リンクを選択します。 これにより、サイトのワークフローが開始され、カスタムアクションのコードが実行されます。

5. クイック起動バーで、[ **アナウンスメントバックアップ** ] リンクを選択します。 **お知らせ** リストに含まれているすべてのお知らせが、この新しいリストにコピーされていることに注意してください。

## <a name="see-also"></a>関連項目
- [方法: イベント レシーバーを作成する](../sharepoint/how-to-create-an-event-receiver.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)

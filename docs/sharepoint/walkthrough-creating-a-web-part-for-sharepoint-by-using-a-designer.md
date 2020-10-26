---
title: デザイナーを使用した SharePoint の web パーツの作成
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Web Parts [SharePoint development in Visual Studio], designer
- Web Parts [SharePoint development in Visual Studio], creating
- Web Parts [SharePoint development in Visual Studio], designing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 732bd9fe3d34a768e0c6f71315f212c49bdf02af
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86016390"
---
# <a name="walkthrough-create-a-web-part-for-sharepoint-by-using-a-designer"></a>チュートリアル: デザイナーを使用した SharePoint の web パーツの作成

SharePoint サイトの Web パーツを作成すれば、ユーザーはブラウザーを使用して、そのサイトを構成するページのコンテンツ、外観、動作を直接変更できます。 このチュートリアルでは、Visual Studio の SharePoint **Visual Web パーツ** プロジェクトテンプレートを使用して、web パーツを視覚的に作成する方法について説明します。

ここで作成する Web パーツには、月間カレンダー ビューと、サイトで使用する各カレンダー リストのチェック ボックスが表示されます。 ユーザーがチェック ボックスをオンにすると、それに対応するカレンダー リストが月間カレンダー ビューに追加されます。

このチュートリアルでは、次の作業について説明します。

- **視覚的 Web パーツ**プロジェクトテンプレートを使用して web パーツを作成する。
- Visual Studio の Visual Web Developer デザイナーを使用して Web パーツをデザインする
- Web パーツに配置したコントロールのイベントを処理するコードを追加する
- SharePoint で Web パーツをテストする

    > [!NOTE]
    > このチュートリアルに記載されている Visual Studio ユーザー インターフェイスの一部の要素は、お使いのコンピューターに実際に表示される名前や場所と異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポート対象エディションの Windows と SharePoint

## <a name="create-a-web-part-project"></a>Web パーツプロジェクトを作成する

まず、 **Visual Web パーツ** プロジェクトテンプレートを使用して、web パーツプロジェクトを作成します。

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)][**管理者として実行**] オプションを使用して開始します。

2. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

3. [ **新しいプロジェクト** ] ダイアログボックスの [ **Visual C#** ] または [ **Visual Basic**] で、[ **Office/SharePoint**] を展開し、[ **SharePoint ソリューション** ] カテゴリを選択します。

4. テンプレートの一覧で、[ **SharePoint 2013-視覚的 Web パーツ** ] テンプレートを選択し、[ **OK** ] をクリックします。

     **SharePoint カスタマイズウィザード**が表示されます。 このウィザードでは、プロジェクトのデバッグ時に使用するサイトやソリューションの信頼レベルを指定できます。

5. [ **この SharePoint ソリューションの信頼レベル** を指定してください] セクションで、[ **ファームソリューションとして配置** する] オプションボタンを選択します。

6. [ **完了** ] をクリックして、既定のローカル SharePoint サイトを受け入れます。

## <a name="designing-the-web-part"></a>Web パーツをデザインする

Visual Web Developer デザイナーの画面に **ツールボックス** からコントロールを追加して、web パーツをデザインします。

1. Visual Web Developer designer で、[ **デザイン** ] タブを選択してデザインビューに切り替えます。

2. メニューバーで、[ **View**  >  **ツールボックス**の表示] を選択します。

3. **ツールボックス**の [**標準**] ノードで、[ **CheckBoxList** ] コントロールを選択し、次のいずれかの手順を実行します。

    - **CheckBoxList**コントロールのショートカットメニューを開き、[**コピー**] を選択し、デザイナーの最初の行のショートカットメニューを開き、[**貼り付け**] を選択します。

    - **ツールボックス**から**CheckBoxList**コントロールをドラッグし、コントロールをデザイナーの最初の行に接続します。

4. 前の手順を繰り返します。ただし、ここでは、デザイナーの次の行へボタンを移動します。

5. デザイナーで、[ **Button1** ] ボタンを選択します。

6. メニューバーで、[ **View**  >  **プロパティウィンドウ**の表示] を選択します。

     **[プロパティ]** ウィンドウが開きます。

7. ボタンの [ **テキスト** ] プロパティに、「 **Update**」と入力します。

## <a name="handling-the-events-of-controls-on-the-web-part"></a>Web パーツ上のコントロールのイベントを処理する

ユーザーがマスター カレンダー ビューにカレンダーを追加できるようにするコードを追加します。

1. 次のいずれかの操作を実行します。

   - デザイナーで、[ **更新** ] ボタンをダブルクリックします。

   - [**更新**] ボタンの [**プロパティ**] ウィンドウで、[**イベント**] ボタンを選択します。 [プロパティ **]** で、「 **Button1_Click**」と入力し、enter キーを押します。

     ユーザー コントロール コード ファイルがコード エディターで開き、`Button1_Click` イベント ハンドラーが表示されます。 後で、このイベントハンドラーにコードを追加します。

2. ユーザー コントロール コード ファイルの先頭に次のステートメントを追加します。

     [!code-vb[SP_VisualWebPart#1](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb#1)]
     [!code-csharp[SP_VisualWebPart#1](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs#1)]

3. `VisualWebPart1` クラスに次のコード行を追加します。 このコードでは、月間カレンダー ビュー コントロールを宣言します。

     [!code-vb[SP_VisualWebPart#2](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb#2)]
     [!code-csharp[SP_VisualWebPart#2](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs#2)]

4. `Page_Load` クラスの `VisualWebPart1` メソッドを次のコードに置き換えます。 このコードは、以下のタスクを実行します。

   - 月間カレンダー ビューをユーザー コントロールに追加します。

   - サイト上の各カレンダー リストにチェック ボックスを追加します。

   - カレンダー ビューに表示される項目の種類ごとにテンプレートを指定します。

     [!code-vb[SP_VisualWebPart#3](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb#3)]
     [!code-csharp[SP_VisualWebPart#3](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs#3)]

5. `Button1_Click` クラスの `VisualWebPart1` メソッドを次のコードに置き換えます。 このコードでは、選択したカレンダーの項目をマスター カレンダー ビューに追加します。

     [!code-vb[SP_VisualWebPart#4](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb#4)]
     [!code-csharp[SP_VisualWebPart#4](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs#4)]

## <a name="test-the-web-part"></a>Web パーツをテストする

プロジェクトを実行すると、SharePoint サイトが開きます。 SharePoint の Web パーツ ギャラリーに Web パーツが自動的に追加されます。 このプロジェクトをテストするには、次のタスクを実行します。

- 2 つのカレンダー リストそれぞれにイベントを追加します。
- Web パーツを Web パーツ ページに追加します。
- 月間カレンダー ビューに含めるリストを指定します。

### <a name="to-add-events-to-calendar-lists-on-the-site"></a>サイト上のカレンダー リストにイベントを追加するには

1. Visual Studio で、F5 キーを **押し** ます。

     SharePoint サイトが開き、 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] [クイック起動] バーがページに表示されます。

2. [クイック起動] バーの [ **リスト**] で、[ **カレンダー** ] リンクを選択します。

     [ **予定表** ] ページが表示されます。

     クイック起動バーに予定表のリンクが表示されない場合は、[ **サイトのコンテンツ** ] リンクを選択します。 [サイトコンテンツ] ページに **予定表** アイテムが表示されない場合は、アイテムを作成します。

3. [カレンダー] ページで、1日を選択し、選択した日の [ **追加** ] リンクをクリックしてイベントを追加します。

4. [ **タイトル** ] ボックスで、 **既定の暦に「Event**」と入力し、[ **保存** ] をクリックします。

5. [ **サイトコンテンツ** ] リンクを選択し、[ **アプリの追加** ] タイルを選択します。

6. [ **作成** ] ページで、 **カレンダー** の種類を選択し、カレンダーに名前を指定して、[ **作成** ] ボタンを選択します。

7. 新しいカレンダーにイベントを追加し、 **カスタムカレンダーにイベントイベント**の名前を付けてから、[ **保存** ] をクリックします。

### <a name="to-add-the-web-part-to-a-web-part-page"></a>Web パーツを Web パーツ ページに追加するには

1. [ **サイトコンテンツ** ] ページで、[ **サイトページ** ] フォルダーを開きます。

2. リボンで [ **ファイル** ] タブを選択し、[ **新しいドキュメント** ] メニューを開き、[ **Web パーツページ** ] コマンドを選択します。

3. [ **新しい Web パーツページ** ] ページで、ページに **samplewebpartpage**という名前を指定し、[ **作成** ] ボタンをクリックします。

     Web パーツ ページが表示されます。

4. [Web パーツ] ページの上部にある [ **挿入** ] タブを選択し、[ **web パーツ** ] をクリックします。

5. **カスタム**フォルダーを選択し、 **VisualWebPart1** web パーツを選択し、[**追加**] ボタンを選択します。

     ページに Web パーツが表示されます。 Web パーツに次のコントロールが表示されます。

    - 月間カレンダー ビュー

    - **更新**ボタン。

    - **カレンダー**のチェックボックス。

    - [ **カスタムカレンダー** ] チェックボックス。

### <a name="to-specify-lists-to-include-in-the-monthly-calendar-view"></a>月間カレンダー ビューに追加するリストを指定するには

Web パーツで、月間予定表ビューに含める予定表を指定し、[ **更新** ] ボタンをクリックします。

指定したすべてのカレンダーのイベントが月間カレンダー ビューに表示されます。

## <a name="see-also"></a>関連項目

SharePoint の web[パーツの作成](../sharepoint/creating-web-parts-for-sharepoint.md) 
[方法: SharePoint web パーツ](../sharepoint/how-to-create-a-sharepoint-web-part.md) 
 を作成する[チュートリアル: SharePoint の web パーツの作成](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)

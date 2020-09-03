---
title: 'チュートリアル: フィーチャーイベントレシーバーの追加 |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, advanced packaging tools
- SharePoint development in Visual Studio, event receivers
- SharePoint development in Visual Studio, feature event receivers
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f40358c157ec24557947f36b0c6eadb6d8a2622d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86015359"
---
# <a name="walkthrough-add-feature-event-receivers"></a>チュートリアル: フィーチャーイベントレシーバーの追加
  フィーチャーイベントレシーバーは、SharePoint で次の機能に関連するイベントのいずれかが発生したときに実行されるメソッドです。

- 機能がインストールされています。

- フィーチャーがアクティブ化されます。

- 機能が非アクティブ化されています。

- 機能が削除されます。

  このチュートリアルでは、SharePoint プロジェクトの機能にイベントレシーバーを追加する方法について説明します。 次のタスクについて説明します。

- フィーチャーイベントレシーバーを使用して空のプロジェクトを作成する。

- **Featuredeactivating 非アクティブ**化メソッドを処理しています。

- SharePoint プロジェクトオブジェクトモデルを使用してお知らせリストにお知らせを追加します。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポート対象エディションの Microsoft Windows および SharePoint。

- 見ることができます。

## <a name="create-a-feature-event-receiver-project"></a>フィーチャーイベントレシーバープロジェクトを作成する
 まず、フィーチャーイベントレシーバーを含むプロジェクトを作成します。

#### <a name="to-create-a-project-with-a-feature-event-receiver"></a>フィーチャーイベントレシーバーを使用してプロジェクトを作成するには

1. メニューバーで [**ファイル**] [  >  **新規作成**] [プロジェクト] の順に選択し  >  **Project** 、[**新しいプロジェクト**] ダイアログボックスを表示します。

2. [ **Visual C#** ] または [ **Visual Basic**] の下にある [ **SharePoint** ] ノードを展開し、[ **2010** ] ノードを選択します。

3. [ **テンプレート** ] ペインで、[ **SharePoint 2010] プロジェクト** テンプレートを選択します。

     フィーチャーイベントレシーバーには、プロジェクトテンプレートがないため、このプロジェクトの種類を使用します。

4. [ **名前** ] ボックスに「 **featureevttest**」と入力し、[ **OK** ] をクリックして **SharePoint カスタマイズウィザード**を表示します。

5. [ **デバッグのサイトとセキュリティレベルの指定** ] ページで、新しいカスタムフィールド項目を追加する SharePoint サーバーサイトの URL を入力するか、既定の場所 (http:///) を使用し \<*system name*> ます。

6. [ **この SharePoint ソリューションの信頼レベル** を指定してください] セクションで、[ **ファームソリューションとして配置** する] オプションボタンを選択します。

     サンドボックスソリューションとファームソリューションの詳細については、「 [サンドボックスソリューションの考慮事項](../sharepoint/sandboxed-solution-considerations.md)」を参照してください。

7. [ **完了** ] をクリックし、feature1.feature という名前の機能が [ **機能** ] ノードの下に表示されることを確認します。

## <a name="add-an-event-receiver-to-the-feature"></a>イベントレシーバーを機能に追加する
 次に、機能にイベントレシーバーを追加し、機能が非アクティブになったときに実行されるコードを追加します。

#### <a name="to-add-an-event-receiver-to-the-feature"></a>イベントレシーバーを機能に追加するには

1. [機能] ノードのショートカットメニューを開き、[機能の **追加** ] を選択して機能を作成します。

2. [ **機能** ] ノードで **feature1.feature**のショートカットメニューを開き、[ **イベントレシーバーの追加** ] を選択して、この機能にイベントレシーバーを追加します。

     これにより、Feature1.feature の下にコードファイルが追加されます。 この場合、プロジェクトの開発言語に応じて、 *Feature1.EventReceiver.cs* または *feature1.feature*のいずれかという名前が付けられます。

3. プロジェクトがに記述されている場合は [!INCLUDE[csprcs](../sharepoint/includes/csprcs-md.md)] 、イベントレシーバーの先頭に次のコードを追加します (まだ存在していない場合)。

     [!code-csharp[SP_FeatureEvt#1](../sharepoint/codesnippet/CSharp/featureevttest2/features/feature1/feature1.eventreceiver.cs#1)]

4. イベントレシーバークラスには、イベントとして機能するいくつかのコメントアウトされたメソッドが含まれています。 **Featuredeactivating 非アクティブ**化メソッドを次のように置き換えます。

     [!code-vb[SP_FeatureEvt#2](../sharepoint/codesnippet/VisualBasic/featureevt2vb/features/feature1/feature1.eventreceiver.vb#2)]
     [!code-csharp[SP_FeatureEvt#2](../sharepoint/codesnippet/CSharp/featureevttest2/features/feature1/feature1.eventreceiver.cs#2)]

## <a name="test-the-feature-event-receiver"></a>フィーチャーイベントレシーバーをテストする
 次に、機能を非アクティブ化して、 **featuredeactivating** メソッドが SharePoint アナウンスリストにアナウンスを出力するかどうかをテストします。

#### <a name="to-test-the-feature-event-receiver"></a>フィーチャーイベントレシーバーをテストするには

1. プロジェクトの [ **アクティブな配置構成** プロパティの値をアクティブ **化なし**に設定する。

     このプロパティを設定すると、SharePoint で機能をアクティブにできなくなり、機能イベントレシーバーをデバッグできるようになります。 詳細については、「 [SharePoint ソリューションのデバッグ](../sharepoint/debugging-sharepoint-solutions.md)」を参照してください。

2. **F5**キーを押してプロジェクトを実行し、SharePoint に配置します。

3. SharePoint Web ページの上部にある [ **サイトの操作** ] メニューを開き、[ **サイトの設定**] を選択します。

4. [**サイトの設定**] ページの [**サイトの操作**] セクションで、[**サイト機能の管理**] リンクを選択します。

5. [**機能**] ページで、 **Featureevttest feature1.feature**機能の横にある [**アクティブ化**] ボタンを選択します。

6. [**機能**] ページで、 **Featureevttest feature1.feature**機能の横にある [**非アクティブ化**] ボタンを選択し、機能を非アクティブ化するために [この機能の確認を**非アクティブ**にする] リンクを選択します。

7. [ **ホーム** ] ボタンをクリックします。

     機能が非アクティブ化されると、 **お知らせ** リストにお知らせが表示されます。

## <a name="see-also"></a>関連項目

- [方法: イベントレシーバーを作成する](../sharepoint/how-to-create-an-event-receiver.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
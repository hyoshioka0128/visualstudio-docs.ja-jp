---
title: 'ワークフローデザイナー: アクティビティデリゲートを定義および使用する'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: c68e42ad-3ec0-4c2d-b104-fe36c6d83b5e
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
author: TerryGLee
ms.openlocfilehash: 4309294a2be703b7511355b87c97341fee06d405
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75593903"
---
# <a name="how-to-define-and-consume-activity-delegates-in-the-workflow-designer"></a>ワークフロー デザイナーでアクティビティ デリゲートを定義および使用する方法

.NET Framework 4.5 には、<xref:System.Activities.Statements.InvokeDelegate> アクティビティ用の既定のデザイナーが含まれています。 このデザイナーを使用すると、<xref:System.Activities.ActivityDelegate> や <xref:System.Activities.ActivityAction> など、<xref:System.Activities.ActivityFunc%601> から派生するアクティビティにデリゲートを割り当てることができます。

## <a name="define-an-activity-delegate"></a>アクティビティ デリゲートの定義

1. 新しい**ワークフローコンソールアプリケーション**プロジェクトを作成します。

   > [!NOTE]
   > **ワークフロー**プロジェクトテンプレートが表示されない場合は、まず Visual Studio の**Windows Workflow Foundation**コンポーネントをインストールします。 詳細については、「 [Install Windows Workflow Foundation](developing-applications-with-the-workflow-designer.md#install-windows-workflow-foundation)」を参照してください。

3. **ソリューションエクスプローラー**でプロジェクトを右クリックし、[ > **新しい項目**の**追加**] を選択します。 **[ワークフロー]** カテゴリを選択し、 **[アクティビティ]** 項目 テンプレートを選択します。 新しいアクティビティに「 **Myforeach** 」という名前を指定し、[ **OK]** を選択します。

   アクティビティがワークフローデザイナーで開きます。

4. ワークフローデザイナーで、 **[引数]** タブをクリックします。

5. **[引数の作成]** をクリックします。 新しい引数の**項目**に名前を指定します。

6. **[引数の型]** 列で、 **[[T] の配列**] を選択します。

7. 型ブラウザーで **[オブジェクト]** を選択し、[ **OK]** を選択します。

8. **[引数の作成]** をもう一度クリックします。 新しい引数の**本体**に名前を指定します。 新しい引数の **[方向]** 列で、 **[プロパティ]** を選択します。

9. 引数の型 列で、**型の参照** を選択します。

10. 型ブラウザーで、 **[型名]** フィールドに「 **activityaction** 」と入力します。 ツリービューで [ **Activityaction\<t >** ] を選択します。 表示されるドロップダウンで **[オブジェクト]** を選択して、型の**activityaction\<オブジェクト >** を引数に割り当てます。

11. ツールボックスの **[制御フロー]** セクションから <xref:System.Activities.Statements.While> アクティビティをデザイナー画面にドラッグします。

12. <xref:System.Activities.Statements.While> アクティビティを選択し、 **[変数]** タブを選択します。

13. **[変数の作成]** を選択します。 新しい変数の**インデックス**に名前を付けます。

14. **[変数の型]** 列で **[Int32]** を選択します。 [**スコープ** **] はそのままにし**、**既定**の列は空白のままにします。

15. <xref:System.Activities.Statements.While> アクティビティの**Condition**プロパティを**index < Items. Length;** に設定します。

16. ツールボックスの **[プリミティブ]** セクションから <xref:System.Activities.Statements.While> アクティビティの**本文**に <xref:System.Activities.Statements.InvokeDelegate> アクティビティをドラッグします。

17. デリゲート ドロップダウンで **本文** を選択します。

18. <xref:System.Activities.Statements.InvokeDelegate> アクティビティの**プロパティ**グリッドで、 **Delegate 引数**プロパティの [.. **.** ] ボタンをクリックします。

19. Argument という名前の引数の**値**列に「 **Items [Index]** **」と入力**します。 **[Ok]** をクリックして、 **[DelegateArguments]** ダイアログボックスを閉じます。

20. <xref:System.Activities.Statements.Assign> アクティビティを <xref:System.Activities.Statements.InvokeDelegate> アクティビティの下の水平線にドラッグします。 <xref:System.Activities.Statements.Assign> アクティビティが作成され、<xref:System.Activities.Statements.Sequence> アクティビティが自動的に作成され、 **Myforeach**アクティビティの**Body**セクションに2つのアクティビティが含まれます。 **Body**セクションには1つのアクティビティのみを含めることができるため、シーケンスが必要です。 新しい <xref:System.Activities.Statements.Sequence> アクティビティの自動作成は、.NET Framework 4.5 の新機能です。

21. <xref:System.Activities.Statements.Assign> アクティビティの**To**プロパティを**index**に設定します。 **Assign**アクティビティの**Value**プロパティを**index + 1**に設定します。

    カスタム**Myforeach**アクティビティは、 **Items**コレクションを通じて渡された値ごとに任意のアクティビティを呼び出し、コレクション内の値をアクティビティの入力として使用します。

## <a name="use-the-custom-activity-in-a-workflow"></a>ワーク フローでのカスタム アクティビティの使用

1. **Ctrl**+**Shift**+**B**キーを押してプロジェクトをビルドします。

2. **ソリューションエクスプローラー**で、デザイナーで**workflow1.xaml**を開きます。

3. ツールボックス から  **Myforeach** アクティビティをデザイナー画面にドラッグします。 アクティビティは、プロジェクトと同じ名前のツールボックスのセクションにあります。

4. **Myforeach**アクティビティの**Items**プロパティを**新しいオブジェクト [] {1, "abc"}** に設定します。

5. ツールボックス の **プリミティブ** セクションから、 **myforeach**アクティビティの **Delegate: Body** セクションに <xref:System.Activities.Statements.WriteLine> アクティビティをドラッグします。

6. <xref:System.Activities.Statements.WriteLine> アクティビティの**Text**プロパティを**Argument. ToString ()** に設定します。

ワークフローを実行すると、コンソールに次の出力が表示されます。

**1**
**abc**

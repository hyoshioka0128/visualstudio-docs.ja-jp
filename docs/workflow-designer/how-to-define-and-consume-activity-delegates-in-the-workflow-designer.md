---
title: アクティビティ デリゲートの定義と使用
description: ワークフローデザイナーでは、.NET Framework 4.5 に、アクティビティデリゲートを定義および使用するために使用できる InvokeDelegate アクティビティ用の既定のデザイナーが含まれていることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: c68e42ad-3ec0-4c2d-b104-fe36c6d83b5e
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
author: TerryGLee
ms.openlocfilehash: 0ce9e59eec2cc9229a5f1104d79337b26115c92a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99971623"
---
# <a name="how-to-define-and-consume-activity-delegates-in-the-workflow-designer"></a>ワークフロー デザイナーでアクティビティ デリゲートを定義および使用する方法

.NET Framework 4.5 には、アクティビティのための既定のデザイナーが含まれてい <xref:System.Activities.Statements.InvokeDelegate> ます。 このデザイナーを使用すると、<xref:System.Activities.ActivityDelegate> や <xref:System.Activities.ActivityAction> など、<xref:System.Activities.ActivityFunc%601> から派生するアクティビティにデリゲートを割り当てることができます。

## <a name="define-an-activity-delegate"></a>アクティビティ デリゲートの定義

1. 新しい **ワークフローコンソールアプリケーション** プロジェクトを作成します。

   > [!NOTE]
   > **ワークフロー** プロジェクトテンプレートが表示されない場合は、まず Visual Studio の **Windows Workflow Foundation** コンポーネントをインストールします。 詳細については、「 [Install Windows Workflow Foundation](developing-applications-with-the-workflow-designer.md#install-windows-workflow-foundation)」を参照してください。

3. **ソリューションエクスプローラー** でプロジェクトを右クリックし、[新しい項目の **追加**] を選択し  >  ます。 [ **ワークフロー** ] カテゴリを選択し、[ **アクティビティ** 項目] テンプレートを選択します。 新しいアクティビティに「 **Myforeach** 」という名前を指定し、[ **OK]** を選択します。

   アクティビティがワークフローデザイナーで開きます。

4. ワークフローデザイナーで、[ **引数** ] タブをクリックします。

5. [**Create Argument**] (引数の作成) をクリックします。 新しい引数の **項目** に名前を指定します。

6. [ **引数の型** ] 列で、 **[[T] の配列**] を選択します。

7. 型ブラウザーで [ **オブジェクト** ] を選択し、[ **OK]** を選択します。

8. [ **引数の作成** ] をもう一度クリックします。 新しい引数の **本体** に名前を指定します。 新しい引数の [ **方向** ] 列で、[ **プロパティ**] を選択します。

9. [引数の型] 列で、[**型の参照**] を選択します。

10. 型ブラウザーで、[**型名**] フィールドに「 **activityaction** 」と入力します。 ツリービューで [ **Activityaction \<T>** ] を選択します。 表示されるドロップダウンで [**オブジェクト**] を選択して、引数に **activityaction \<Object>** 型を割り当てます。

11. <xref:System.Activities.Statements.While>ツールボックスの [**制御フロー** ] セクションからデザイナー画面にアクティビティをドラッグします。

12. アクティビティを選択 <xref:System.Activities.Statements.While> し、[ **変数** ] タブを選択します。

13. [ **変数の作成**] を選択します。 新しい変数の **インデックス** に名前を付けます。

14. [ **変数の型** ] 列で [ **Int32**] を選択します。 [ **スコープ** **] はそのままにし**、 **既定** の列は空白のままにします。

15. アクティビティの **Condition** プロパティ <xref:System.Activities.Statements.While> を **Index < Items. Length;** に設定します。

16. [ <xref:System.Activities.Statements.InvokeDelegate> ツールボックス] の [ **プリミティブ** ] セクションからアクティビティの **本文** にアクティビティをドラッグし <xref:System.Activities.Statements.While> ます。

17. [デリゲート] ドロップダウンで [ **本文** ] を選択します。

18. アクティビティの **プロパティ** グリッドで、 <xref:System.Activities.Statements.InvokeDelegate> **Delegate 引数** プロパティの [.. **.** ] ボタンをクリックします。

19. Argument という名前の引数の **値** 列に「 **Items [Index]** **」と入力** します。 [ **Ok** ] をクリックして、[ **DelegateArguments** ] ダイアログボックスを閉じます。

20. <xref:System.Activities.Statements.Assign> アクティビティを <xref:System.Activities.Statements.InvokeDelegate> アクティビティの下の水平線にドラッグします。 <xref:System.Activities.Statements.Assign>アクティビティが作成され、 <xref:System.Activities.Statements.Sequence> **Myforeach** アクティビティの **Body** セクションに2つのアクティビティが含まれるように、アクティビティが自動的に作成されます。 **Body** セクションには1つのアクティビティのみを含めることができるため、シーケンスが必要です。 新しいアクティビティを自動的に作成すること <xref:System.Activities.Statements.Sequence> は、.NET Framework 4.5 の新機能です。

21. アクティビティの **to プロパティを** <xref:System.Activities.Statements.Assign> **index** に設定します。 **Assign** アクティビティの **Value** プロパティを **index + 1** に設定します。

    カスタム **Myforeach** アクティビティは、 **Items** コレクションを通じて渡された値ごとに任意のアクティビティを呼び出し、コレクション内の値をアクティビティの入力として使用します。

## <a name="use-the-custom-activity-in-a-workflow"></a>ワーク フローでのカスタム アクティビティの使用

1. **Ctrl** + **Shift** + **B** キーを押してプロジェクトをビルドします。

2. **ソリューションエクスプローラー** で、デザイナーで **workflow1.xaml** を開きます。

3. [ツールボックス] から [ **Myforeach** ] アクティビティをデザイナー画面にドラッグします。 アクティビティは、プロジェクトと同じ名前のツールボックスのセクションにあります。

4. **Myforeach** アクティビティの **Items** プロパティを **新しいオブジェクト [] {1, "abc"}** に設定します。

5. <xref:System.Activities.Statements.WriteLine>ツールボックスの [**プリミティブ**] セクションから、 **Myforeach** アクティビティの [ **Delegate: Body** ] セクションにアクティビティをドラッグします。

6. アクティビティの **Text** プロパティ <xref:System.Activities.Statements.WriteLine> を **Argument. ToString ()** に設定します。

ワークフローを実行すると、コンソールに次の出力が表示されます。

**1** 
**abc**

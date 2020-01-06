---
title: 'チュートリアル: Windows フォームでの簡単な WCF サービスの作成'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- WCF, walkthrough [Visual Studio]
- WCF, Visual Studio tools for
- WCF services
- WCF services, walkthrough
ms.assetid: 5fef1a64-27a4-4f10-aa57-29023e28a2d6
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 3d3f2e80ff3e2b94c46d1e2658c40bccf2e6c365
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586017"
---
# <a name="walkthrough-create-a-simple-wcf-service-in-windows-forms"></a>チュートリアル: Windows フォームで簡単な WCF サービスを作成する

このチュートリアルでは、単純な Windows Communication Foundation (WCF) サービスを作成し、テストしてから、Windows フォームアプリケーションからアクセスする方法について説明します。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="create-a-service"></a>サービスを作成する

1. Visual Studio を開きます。

::: moniker range="vs-2017"

2. **[ファイル]** メニューの [**新しい**>**プロジェクト**] をクリックします。

3. **[新しいプロジェクト]** ダイアログボックスで、 **[Visual Basic]** または **[ C#ビジュアル]** ノードを展開し、 **[wcf]** 、 **[wcf サービスライブラリ]** の順に選択します。

4. **[OK]** をクリックして、プロジェクトを作成します。

   ![WCF サービス ライブラリ プロジェクト](../data-tools/media/wcf1.png)

::: moniker-end

::: moniker range=">=vs-2019"

2. スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。

3. **新しいプロジェクトの作成** ページの 検索 ボックスに「 **wcf サービスライブラリ**」と入力します。 C# **WCF サービスライブラリ**のまたは Visual Basic テンプレートを選択し、 **[次へ]** をクリックします。

   ![Visual Studio 2019 で新しい WCF サービスライブラリプロジェクトを作成する](media/vs-2019/create-new-wcf-service-library.png)

   > [!TIP]
   > テンプレートが表示されない場合は、Visual Studio の**Windows Communication Foundation**コンポーネントのインストールが必要になることがあります。 [**その他のツールと機能をインストール**する] を選択して Visual Studio インストーラーを開きます。 **[個々のコンポーネント]** タブをクリックし、 **[開発アクティビティ]** まで下にスクロールして、 **[Windows Communication Foundation]** を選択します。 **[変更]** をクリックします。

4. **[新しいプロジェクトの構成]** ページで、 **[作成]** をクリックします。

::: moniker-end

   > [!NOTE]
   > これにより、テストしてアクセスすることが可能な機能するサービスが作成されます。 次の 2 つの手順は、別のデータ型を使用するように既定の方法を変更する方法を示しています。 実際のアプリケーションで、独自の関数をサービスに追加することもできます。

5. **ソリューションエクスプローラー**で、 **IService1**または**IService1.cs**をダブルクリックします。

   ![IService1 ファイル](../data-tools/media/wcf2.png)

   次の行を見つけます。

   [!code-csharp[WCFWalkthrough#4](../data-tools/codesnippet/CSharp/walkthrough-creating-a-simple-wcf-service-in-windows-forms_1.cs)]
   [!code-vb[WCFWalkthrough#4](../data-tools/codesnippet/VisualBasic/walkthrough-creating-a-simple-wcf-service-in-windows-forms_1.vb)]

   `value` パラメーターの型を文字列に変更します。

   [!code-csharp[WCFWalkthrough#1](../data-tools/codesnippet/CSharp/walkthrough-creating-a-simple-wcf-service-in-windows-forms_2.cs)]
   [!code-vb[WCFWalkthrough#1](../data-tools/codesnippet/VisualBasic/walkthrough-creating-a-simple-wcf-service-in-windows-forms_2.vb)]

   上記のコードで、`<OperationContract()>` または `[OperationContract]` 属性に注意してください。 これらの属性は、サービスによって公開されている任意のメソッドに必要です。

6. **ソリューションエクスプローラー**で、 **Service1**または**Service1.cs**をダブルクリックします。

   ![Service1 ファイル](../data-tools/media/wcf3.png)

   次の行を見つけます。

   [!code-vb[WCFWalkthrough#5](../data-tools/codesnippet/VisualBasic/walkthrough-creating-a-simple-wcf-service-in-windows-forms_3.vb)]
   [!code-csharp[WCFWalkthrough#5](../data-tools/codesnippet/CSharp/walkthrough-creating-a-simple-wcf-service-in-windows-forms_3.cs)]

   `value` パラメーターの型を文字列に変更します。

   [!code-csharp[WCFWalkthrough#2](../data-tools/codesnippet/CSharp/walkthrough-creating-a-simple-wcf-service-in-windows-forms_4.cs)]
   [!code-vb[WCFWalkthrough#2](../data-tools/codesnippet/VisualBasic/walkthrough-creating-a-simple-wcf-service-in-windows-forms_4.vb)]

## <a name="test-the-service"></a>サービスをテストする

1. **F5** キーを押してサービスを実行します。 **WCF テストクライアント**フォームが表示され、サービスが読み込まれます。

2. **[WCF のテスト用クライアント]** フォームで、**IService1** の下の **GetData()** メソッドをダブルクリックします。 **[GetData]** タブが表示されます。

     ![GetData&#40; &#41;メソッド](../data-tools/media/wcf4.png)

3. **[要求]** ボックスで、 **[値]** フィールドを選択して「`Hello`」と入力します。

     ![[値] フィールド](../data-tools/media/wcf5.png)

4. **[起動]** ボタンをクリックします。 **[セキュリティの警告]** ダイアログボックスが表示されたら、[ **OK]** をクリックします。 結果は **[応答]** ボックスに表示されます。

     ![[応答] ボックスに結果が表示される](../data-tools/media/wcf6.png)

5. **[ファイル]** メニューの **[終了]** をクリックして、テスト フォームを閉じます。

## <a name="access-the-service"></a>サービスへのアクセス

### <a name="reference-the-wcf-service"></a>WCF サービスを参照する

1. **[ファイル]** メニューの **[追加]** をポイントし、 **[新しいプロジェクト]** をクリックします。

2. **[新しいプロジェクト]** ダイアログボックスで、 **Visual Basic**または**ビジュアルC#** ノードを展開し、 **[Windows]** を選択して、 **[Windows フォームアプリケーション]** を選択します。 **[OK]** をクリックして、プロジェクトを開きます。

     ![Windows フォーム アプリケーション プロジェクト](../data-tools/media/wcf7.png)

3. **[WindowsApplication1]** を右クリックして **[サービス参照の追加]** をクリックします。 **[サービス参照の追加]** ダイアログボックスが表示されます。

4. **[サービス参照の追加]** ダイアログ ボックスで **[探索]** をクリックします。

     ![[サービス参照の追加] ダイアログ ボックス](../data-tools/media/wcf8.png)

     **Service1**が **[サービス]** ウィンドウに表示されます。

5. **[OK]** をクリックしてサービス参照を追加します。

### <a name="build-a-client-application"></a>クライアント アプリケーションを構築します

1. **ソリューション エクスプローラー**で、 **[Form1.vb]** または **[Form1.cs]** をダブルクリックして、Windows フォーム デザイナーを (まだ開いていない場合に) 開きます。

2. **ツールボックス**で、`TextBox` コントロール、`Label` コントロール、および `Button` コントロールをフォームにドラッグします。

     ![フォームへのコントロールの追加](../data-tools/media/wcf9.png)

3. `Button` をダブルクリックし、`Click` イベント ハンドラーに次のコードを追加します。

     [!code-csharp[WCFWalkthrough#3](../data-tools/codesnippet/CSharp/walkthrough-creating-a-simple-wcf-service-in-windows-forms_5.cs)]
     [!code-vb[WCFWalkthrough#3](../data-tools/codesnippet/VisualBasic/walkthrough-creating-a-simple-wcf-service-in-windows-forms_5.vb)]

4. **ソリューション エクスプローラー**で、 **[WindowsApplication1]** を右クリックして **[スタートアップ プロジェクトに設定]** をクリックします。

5. **F5** キーを押してプロジェクトを実行します。 いくつかのテキストを入力し、ボタンをクリックします。 ラベルに「入力した内容:」と入力したテキストが表示されます。

     ![結果を表示するフォーム](../data-tools/media/wcf10.png)

## <a name="see-also"></a>関連項目

- [Visual Studio での Windows Communication Foundation サービスと WCF データ サービス](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)

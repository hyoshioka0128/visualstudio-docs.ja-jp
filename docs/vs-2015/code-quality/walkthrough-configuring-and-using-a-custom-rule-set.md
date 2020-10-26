---
title: 'チュートリアル: カスタム規則セットの構成と使用 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- code analysis, walkthroughs
- code analysis, rule sets
ms.assetid: 7fe0a4e3-1ce0-4f38-a87a-7d81238ec7cd
caps.latest.revision: 42
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 8239afd1cf4e8c0a5e702f2b0e4ed64408cada09
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72645738"
---
# <a name="walkthrough-configuring-and-using-a-custom-rule-set"></a>チュートリアル: カスタム規則セットの構成と使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、クラスライブラリでカスタマイズした *規則セット* を使用するように構成されているコード分析ツールを使用する方法について説明します。 ソリューションに対して指定したプロジェクトの種類に関連する規則セットを選択できます。また、別の規則セットを選択して、特定のニーズに対応するために、分離されていない方法で修正できる問題について、レガシコードのスキャンなどを行うことができます。 どちらの場合も、規則セットをカスタマイズして、プロジェクトの要件に合わせて微調整することができます。

 このチュートリアルでは、次のプロセスについて説明します。

- クラスライブラリを作成します。

- **Microsoft 基本デザインガイドライン規則**のコード分析規則セットを選択します。

- 独自のコードをクラスに追加します。

- コード分析を実行します。

- 規則セットをカスタマイズします。

- コード分析を実行し、ルールセットのカスタマイズ動作のしくみを確認します。

## <a name="prerequisites"></a>前提条件

- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]、 [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)]、または [!INCLUDE[vsPro](../includes/vspro-md.md)]

## <a name="using-rule-sets-with-code-analysis"></a>コード分析での規則セットの使用
 まず、単純なクラスライブラリを作成します。

#### <a name="create-a-class-library"></a>クラス ライブラリを作成する

1. **[ファイル]** メニューの **[新規作成]** をクリックし、 **[プロジェクト]** をクリックします。

2. [ **新しいプロジェクト** ] ダイアログボックスの [ **プロジェクトの種類**] で、[ **Visual C#**] をクリックします。

3. [ **Visual C#**] で [ **クラスライブラリ**] を選択します。

4. [ **名前** ] テキストボックスに「 **rulesetsample** 」と入力し、[ **OK]** をクリックします。

   次に、[ **Microsoft 基本デザインガイドライン規則** ] 規則セットを選択し、プロジェクトと共に保存します。

#### <a name="select-a-code-analysis-rule-set"></a>コード分析規則セットの選択

1. [ **分析** ] メニューの [ **rulesetsample のコード分析の構成**] をクリックします。

    コード分析の構成設定が表示されます。

2. [ **この規則セットを実行** ] ドロップダウンリストで、[ **Microsoft すべての規則**] を選択します。

    使用可能な規則セットの詳細については、「 [コード分析規則セットのリファレンス](../code-quality/code-analysis-rule-set-reference.md)」を参照してください。

    [ファイル] メニューの [ **選択した項目を保存** ] をクリックして、プロジェクトファイルを、選択した規則セットおよびその設定に関する情報で更新します。

   > [!TIP]
   > 実際の状況では、コード分析で対象とする問題の優先順位を設定するために使用することをお勧めします。まず、[ **最小推奨規則** ] 規則セットから開始し、必要な問題を修正してから、追加の問題を見つけて修正するための規則または規則セットを段階的に追加します。

   次に、クラスライブラリにいくつかのコードを追加します。これは、CA1704 の "識別子のスペルが正しい" コード分析規則の違反を示すために使用されます。 詳細については、「 [CA1704: 識別子は正しく入力されている必要があり](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md)ます」を参照してください。

#### <a name="add-your-own-code"></a>独自のコードを追加する

- ソリューションエクスプローラーで、Class1.cs ファイルを開き、既存のコードを次のコードに置き換えます。

  ```
  using System;
  using System.Collections.Generic;
  using System.Text;

  namespace RuleSetSample
  {
      public class Class1
      {
          //The variable parameter names "a" and "b" will cause
          //the warning CA 1704 Microsoft.Naming "Consider
          //providing a more meaningful name" to fire
          public int AddIntegers(int a, int b)
          {

              int sum = a + b;

              return (sum);
          }
      }
  }

  ```

  RuleSetSample プロジェクトに対してコード分析を実行し、[エラー一覧] ウィンドウで生成されたエラーと警告を探すことができるようになりました。

#### <a name="run-code-analysis-on-the-rulesetsample-project"></a>RuleSetSample プロジェクトでコード分析を実行する

1. [ **分析** ] メニューの [ **Rulesetsample でコード分析を実行**] をクリックします。

2. [エラー一覧] ウィンドウで [ **警告** ] をクリックし、[ **説明** ] 列ヘッダーをクリックして、警告英数字順を並べ替えます。

    実際のアプリケーションでは、この時点で修正が必要なルール違反を修正するか、または修正が必要でないと判断した場合にルールをオフまたは非表示にすることができます。 詳細については、「[SuppressMessage 属性を使用した警告の抑制](../code-quality/suppress-warnings-by-using-the-suppressmessage-attribute.md)」を参照してください。

3. CA1704 の警告に注意してください。 この規則に違反するのは、"パラメーターにわかりやすい名前を指定することを考慮する必要がある" ということです。 コード内の問題を修正するか、次の手順で説明するように、ルールを無効にすることができます。

   次に、CA1704 警告を除外するように規則セットをカスタマイズします。 "識別子は正しく入力されている必要があります"。

#### <a name="customize-the-rule-set-for-your-project-to-disable-a-specific-rule"></a>特定のルールを無効にするようにプロジェクトの規則セットをカスタマイズする

1. [ **分析** ] メニューの [ **rulesetsample のコード分析の構成**] をクリックします。

2. [ **この規則セットを実行** ] ドロップダウンリストで、[ **Microsoft All Rules** ] 規則セットが強調表示されていることを確認し、[ **開く**] をクリックします。 [ルールセット] ページが表示されます。

3. [Microsoft. 名前付けカテゴリ] ノードを展開し、CA1704 警告を選択します。

4. [ **アクション** ] 列で [なし] を選択し **ます。** これにより、[エラー一覧] ウィンドウに CA1704 が警告またはエラーとして表示されるのを防ぐことができます。

    ここでは、さまざまなツールバーボタンとフィルターオプションを試してみるとよいでしょう。 たとえば、[ **グループ化** ] ドロップダウンリストを使用して、特定のルールまたはルールのカテゴリを見つけることができます。 もう1つの例として、[ルールセットページ] ツールバーの [ **無効なルールの非表示** ] ボタンを使用して、[ **アクション** ] 列が **[なし**] に設定されているすべてのルールを非表示にしたり表示したりできます これは、無効にしたルールをスキャンして、無効にする必要があることを確認する場合に便利です。

5. [表示] メニューの [プロパティ ウィンドウ] をクリックします。 プロパティツールウィンドウの [名前] ボックスに「 **My Custom Rule Set** 」と入力します。 これにより、IDE の新しい規則セットの表示名が変更され [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] ます。

6. [ **ファイル** ] メニューの [ **Microsoft すべてのルールの保存** ] をクリックして、カスタマイズしたルールセットを保存します。 プロジェクトのルートフォルダーに移動します。 [ **ファイル名** ] ボックスに「 **mycustomruleset セット**」と入力します。 これで、プロジェクトで使用するカスタム規則セットを選択できるようになりました。

   新しいルールセットを作成したので、プロジェクト設定を構成して、新しいルールセットを使用するように指定する必要があります。

#### <a name="specify-the-new-rule-set-for-use-with-your-project"></a>プロジェクトで使用する新しい規則セットを指定します

1. ソリューションエクスプローラーで、プロジェクトを右クリックし、[ **プロパティ**] を選択します。

2. [ **プロパティ** ] タブで、[ **コード分析**] をクリックします。

    [ **この規則セットを実行** ] ドロップダウンリストで、をクリックし **\<Browse..>** ます。 コードプロジェクトのルートフォルダーに移動し、[ **Mycustomruleset**セット] を選択します。 これは、前の手順で作成した新しい規則セットです。

3. [ **ファイル** ] メニューの [ **保存** ] をクリックして、プロジェクトの構成を保存します。 これで、カスタム規則セットをプロジェクトで使用できるようになりました。

   最後に、MyCustomRuleSet セットを使用してコード分析を再度実行します。 [エラー一覧] ウィンドウに CA1704 パフォーマンスルール違反が表示されないことに注意してください。

#### <a name="run-code-analysis-on-the-rulesetsample-project-for-the-second-time"></a>RuleSetSample プロジェクトで2回目のコード分析を実行する

1. [ **分析** ] メニューの [ **Rulesetsample でコード分析を実行**] をクリックします。

2. [エラー一覧] ウィンドウで、[ **警告**] をクリックすると、"識別子は正しく入力されている必要があります" という CA1704 の警告違反が表示されなくなります。

## <a name="see-also"></a>参照
 [方法: マネージコードのコード分析を構成するプロジェクト](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)[コード分析規則セットの参照](../code-quality/code-analysis-rule-set-reference.md)

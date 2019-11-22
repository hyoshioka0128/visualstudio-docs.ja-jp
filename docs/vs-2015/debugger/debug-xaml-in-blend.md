---
title: Debug XAML in Blend | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 29a37182-2a2c-47e4-a4a9-2d5412738fed
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d90e495ba64018479758e4fa38de0035601a8f0d
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298328"
---
# <a name="debug-xaml-in-blend"></a>Blend での XAML のデバッグ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

アプリの XAML をデバッグするために [!INCLUDE[blend_first](../includes/blend-first-md.md)] のツールを使用できます。 プロジェクトをビルドする場合、エラーは **[結果]** パネルに表示されます。 エラーをダブルクリックして、エラーに関連するマークアップを検索します。 作業領域を増やす必要がある場合は、F12 キーを押して **[結果]** パネルを非表示にできます。  
  
## <a name="syntax-errors"></a>構文エラー  
 構文エラーは、XAML または分離コード ファイルが言語のフォーマット規則に従っていない場合に発生します。 エラーの説明を参照すると、エラーの解決に役立ちます。 一覧では、エラーの発生しているファイルの名前と行番号も確認できます。 XAML エラーは **[結果]** パネルの **[マークアップ]** タブに一覧されます。  
  
> [!TIP]
> XAML は XML に基づくマークアップ言語で、XML 構文規則に従っています。  
  
 XAML 構文エラーのよくある原因は次のとおりです。  
  
- キーワードのスペルまたは大文字の表記に誤りがある。  
  
- 属性またはテキスト文字列の両側に引用符がない。  
  
- XAML 要素に終了タグがない。  
  
- XAML 要素が許可されていない場所にある。  
  
  共通 XAML 構文の詳細については、「[Basic XAML syntax guide](https://go.microsoft.com/fwlink/?LinkId=329942)」 (基本的な XAML 構文のガイド) を参照してください。  
  
  また、[!INCLUDE[blend_subs](../includes/blend-subs-md.md)] での単純な分離コード構文エラー、コンパイル エラー、およびランタイム エラーを識別して、解決できます。 ただし、分離コード エラーは Visual Studio で識別して解決する方が簡単です。  
  
### <a name="debugging-sample-xaml-code"></a>サンプル XAML コードのデバッグ  
 次の例では、[!INCLUDE[blend_subs](../includes/blend-subs-md.md)] での単純な XAML デバッグ セッションを実行します。  
  
##### <a name="to-create-a-project"></a>プロジェクトを作成するには  
  
1. [!INCLUDE[blend_subs](../includes/blend-subs-md.md)] で、 **[ファイル]** メニューを開き、 **[新しいプロジェクト]** をクリックします。  
  
    **[新しいプロジェクト]** ダイアログ ボックスの左側に、プロジェクトの種類の一覧が表示されます。 プロジェクトの種類をクリックすると、その種類に関連付けられているプロジェクト テンプレートが右側に表示されます。  
  
2. In the list of project types, click **XAML (Windows Store)** .  
  
3. In the list of project templates, click **Blank App**.  
  
4. In the **Name** text box, type `DebuggingSample`.  
  
5. **[場所]** ボックスでプロジェクトの場所を確認します。  
  
6. **[言語]** ボックスの一覧で、 **[Visual C#]** をクリックし、 **[OK]** をクリックしてプロジェクトを作成します。  
  
7. デザイン サーフェイスを右クリックし、 **[ソースの表示]** をクリックして **[分割]** ビューに切り替えます。  
  
8. コードの右上隅にある **[コピー]** リンクをクリックして、次のコードをコピーします。  
  
   ```  
   <Grid HorizontalAlignment="Left" Height="222" VerticalAlignment="Top>  
        <Button content="Button" x:Mame="Home" HorizontalAlignment="Left" VerticalAlignment="Top"/>  
        <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,38,0,0">  
        <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,75,0,0"/>  
        <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,112,0,0"/>  
        <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top Margin="0,149,0,0"/>  
   </Grid>  
  
   ```  
  
9. 既定の**グリッド**を探し、**Grid** の開始タグと終了タグの間にコードを貼り付けます。 完成したコードは次のようになります。  
  
    ```  
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">  
         <Grid HorizontalAlignment="Left" Height="222" VerticalAlignment="Top>  
              <Button content="Button" x:Mame="Home" HorizontalAlignment="Left" VerticalAlignment="Top"/>  
              <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,38,0,0">  
              <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,75,0,0"/>  
              <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="0,112,0,0"/>  
              <Button Content="Button" HorizontalAlignment="Left" VerticalAlignment="Top Margin="0,149,0,0"/>  
         </Grid>  
    </Grid>  
  
    ```  
  
10. Ctrl キーと Shift キーを押しながら B キーを押してプロジェクトをビルドします。  
  
    プロジェクトをビルドできないことを警告するエラー メッセージが表示され、エラーを一覧表示した **[結果]** パネルがアプリの下部に表示されます。  
  
    ![Blend for Visual Studio 内での XAML のデバッグ](../debugger/media/blend-debugxaml-xaml.png "blend_debugXAML_XAML")  
  
### <a name="resolving-xaml-errors"></a>XAML エラーの解決  
 XAML エラーが検出された場合、プロジェクトに無効なマークアップが含まれているという警告がデザイン サーフェスに表示されます。 エラーを解決すると、 **[結果]** パネルのエラー リストが更新されます。 すべてのエラーを解決すると、デザイン サーフェスが有効になり、アプリがデザイン サーフェスに表示されます。  
  
##### <a name="to-resolve-the-xaml-errors"></a>XAML エラーを解決するには  
  
1. リストの最初のエラーをダブルクリックします。 説明は、"値 '<' は、属性では無効です" となります。 エラーをダブルクリックすると、ポインターがコード内の対応する場所を見つけます。 `<` の前の `Button` は有効で、エラー メッセージで指定された属性ではありません。 コードの前の行を見ると、属性 `Top` の終わりの引用符がないことがわかります。 終わりの引用符を入力します。 **[結果]** パネルのエラー リストが更新されて変更が反映されていることに注意してください。  
  
2. Double-click the description "'0' is not valid at the start of a name." `Margin="0,149,0,0"` appears to be well formed. ただし、`Margin` のカラー コーディングはコードの `Margin` の他のインスタンスと一致しないことに注意してください。 終わりの引用符が前の名前/値ペア (`VerticalAlignment="Top`) にないため、`Margin="` は前の属性の値の一部として読み込まれ、0 が名前/値ペアの先頭として読み込まれます。 `Top` の終わりの引用符を入力します。 **[結果]** パネルのエラー リストが更新されて変更が反映されます。  
  
3. 残りのエラーをダブルクリックします。"終わりの XML タグ 'Button' が一致しません。" ポインターは終わりの **Grid** タグ (`</Grid>`) にあり、エラーが `Grid` オブジェクトの内側にあることを示します。 2 番目の `Button` オブジェクトで終わりのタグがないことに注意してください。 終わりの `/` を追加すると、 **[結果]** パネル リストが更新されます。 これら 2 つの最初のエラーが解決され、さらに 2 つのエラーが識別されました。  
  
4. "メンバー 'content' が認識されないか、アクセスできません。" をダブルクリックします。 `c` の `content` は大文字になります。 小文字の "c" を大文字の "c" に置き換えます。  
  
5. Double-click "The property 'Mame' does not exist in the '<https://schemas.microsoft.com/winfx/2006/xaml>' namespace." "Mame" の "M" は "N" でなければなりません。 "M" を "N" で置き換えます。 これで、XAML が解析でき、アプリがデザイン サーフェスに表示されます。  
  
    ![Debugging XAML in Blend for Visual Studio](../debugger/media/blend-debugartboard-xaml.png "blend_debugArtboard_XAML")  
  
    Ctrl + Shift + B キーを押してプロジェクトをビルドし、残っているエラーがないことを確認します。  
  
## <a name="debugging-in-visual-studio"></a>Visual Studio でのデバッグ  
 アプリ内のコードをさらに簡単にデバッグするために、Visual Studio で [!INCLUDE[blend_subs](../includes/blend-subs-md.md)] プロジェクトを開くことができます。 Visual Studio で [!INCLUDE[blend_subs](../includes/blend-subs-md.md)] プロジェクトを開くには、 **[プロジェクト]** パネルでプロジェクトを右クリックし、次に **[Visual Studio で編集]** をクリックします。 Visual Studio でデバッグ セッションを完了したら、Ctrl + Shift + S キーを押してすべての変更を保存し、[!INCLUDE[blend_subs](../includes/blend-subs-md.md)] に戻ります。 プロジェクトの再読み込みを求めるメッセージが表示されます。 **[すべてはい]** をクリックして [!INCLUDE[blend_subs](../includes/blend-subs-md.md)] での作業を続けます。  
  
 For more information about debugging your app, see [Debug Windows Store apps in Visual Studio](https://go.microsoft.com/fwlink/?LinkId=329944).  
  
## <a name="getting-help"></a>ヘルプ情報の入手  
 If you need more help debugging your [!INCLUDE[blend_subs](../includes/blend-subs-md.md)] app, you can search the [Windows Store app community forums](https://go.microsoft.com/fwlink/?LinkId=280308) for posts related your issue or post a question.

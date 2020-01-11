---
title: コード化された UI テストを使用した SharePoint 2010 アプリケーションのテスト | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 51b53778-469c-4cc9-854c-4e4992d6389b
caps.latest.revision: 32
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b44e921a8e1ba13d3f0786d4633f942f94f3eaaa
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75851285"
---
# <a name="testing-sharepoint-2010-applications-with-coded-ui-tests"></a>コード化された UI テストを使用した SharePoint 2010 アプリケーションのテスト
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コード化された UI テストを SharePoint アプリケーションに含めると、UI コントロールを含むアプリケーション全体が正しく機能していることを検証できます。 コード化された UI テストでは、ユーザー インターフェイスの値とロジックも検証できます。

 **Requirements**

- Visual Studio Enterprise

## <a name="what-else-should-i-know-about-coded-ui-tests"></a>コード化された UI テストについて把握しておくべきこと
 コード化された UI テストを使用する利点の詳細については、「[UI オートメーションを使用してコードをテストする](../test/use-ui-automation-to-test-your-code.md)」と「[Visual Studio 2012 を使用した継続的デリバリーのためのテスト – 第 5 章: システム テストの自動化](https://msdn.microsoft.com/library/jj159335.aspx)」を参照してください。

 **ノート**

- ![Prerequsite](../test/media/prereq.png "前提条件")SharePoint アプリケーションのコード化された UI テストは、SharePoint 2010 でのみサポートされています。

- ![Prerequsite](../test/media/prereq.png "前提条件")SharePoint アプリケーションでの Visio および PowerPoint 2010 コントロールのサポートはサポートされていません。

## <a name="creating-a-coded-ui-test-for-your-sharepoint-app"></a>SharePoint アプリのコード化された UI テストを作成する
 SharePoint 2010 アプリケーションでの[コード化された UI テストの作成](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate) 方法は、他の種類のアプリケーションでのテストの作成方法と同じです。 記録と再生は、Web 編集インターフェイス上のすべてのコントロールでサポートされています。 カテゴリと Web パーツを選択するためのインターフェイスは、すべてが標準 Web コントロールです。

 ![SharePoint web パーツ](../test/media/cuit-sharepoint.png "CUIT_SharePoint")

> [!NOTE]
> 操作を記録している場合は、コードを生成する前に操作を検証します。 マウス ホバーにはいくつかの動作が関連付けられているため、既定で有効になっています。 コード化された UI テストから冗長なホバーを削除するようにしてください。 そのためには、テスト用のコードを編集するか、 [コード化された UI テスト エディター](../test/editing-coded-ui-tests-using-the-coded-ui-test-editor.md)を使用します。

## <a name="including-testing-of-office-2010-controls-within-your-sharepoint-app"></a>SharePoint アプリ内に Office 2010 コントロールのテストを含める
 SharePoint アプリでいくつかの Office 2010 Web パーツの自動化を有効にするには、コードを少し変更する必要があります。

> [!WARNING]
> Visio および PowerPoint 2010 コントロールはサポートされていません。

### <a name="excel-2010-cell-controls"></a>Excel 2010 のセル コントロール
 Excel セル コントロールを含めるには、コード化された UI テストのコードを少し変更する必要があります。

> [!WARNING]
> Excel のセルにテキストを入力してから方向キーを操作すると、正しく記録されません。 セルの選択にはマウスを使用してください。

 空のセルに対する操作を記録している場合は、セルをダブルクリックしてからテキスト設定操作を実行して、コードを変更する必要があります。 そうする必要があるのは、セルをクリックした後、キーボードを操作すると、セル内の `textarea` がアクティブになるためです。 単に空のセルで `setvalue` を記録すると、セルがクリックされるまでは存在しない `editbox` が検索されます。 例:

```csharp
Mouse.DoubliClick(uiItemCell,new Point(31,14));
uiGridKeyboardInputEdit.Text=value;
```

 空でないセルに対する操作を記録している場合は、セルにテキストを追加したときに新しい \<div> コントロールがセルの子として追加されるため、記録はより複雑になります。 新しい \<div> コントロールには、入力したテキストが含まれます。 レコーダーは新しい \<div> コントロールに対する操作を記録する必要がありますが、新しい \<div> コントロールはテキストが入力されるまで存在しないため、記録できません。 この問題に対応するために、手動で次のようにコードを変更する必要があります。

1. セルの初期化に移動して、 `RowIndex` および `ColumnIndex` プライマリ プロパティを作成します。

    ```csharp
    this.mUIItemCell.SearchProperties[HtmlCell.PropertyNames. RowIndex] = "3";
    this.mUIItemCell.SearchProperties[HtmlCell.PropertyNames. ColumnIndex] = "3";
    ```

2. セルの `HtmlDiv` 子を検索します。

    ```csharp
    private UITestControl getControlToDoubleClick(HtmlCell cell)
    {
         if (String.IsNullOrEmpty(cell.InnerText)) return cell;
         HtmlDiv pane = new HtmlDiv(cell);
         pane.FilterProperties[HtmlDiv.PropertyNames.InnerText] = cell.InnerText;
         // Class is an important property in finding pane
         pane.FilterProperties[HtmlDiv.PropertyNames.Class] = "cv-nwr";
         UITestControlCollection panes = pane.FindMatchingControls();
         return panes[0];
    }

    ```

3. `HtmlDiv`にマウスのダブルクリック操作のコードを追加します。

    ```csharp
    Mouse.DoubleClick(uIItemPane, new Point(31, 14)); )
    ```

4. `TextArea`にテキストを設定するコードを追加します。

    ```csharp
    uIGridKeyboardInputEdit.Text = value; }
    ```

## <a name="enabling-coded-ui-testing-of-silverlight-web-parts-in-your-sharepoint-2010-app"></a>SharePoint 2010 アプリで Silverlight Web パーツのコード化された UI テストを有効にする
 Visual Studio 2012 以降では、Silverlight のテストはサポートされていません。 しかし、SharePoint 2010 アプリで Silverlight Web パーツをテストしたい場合は、Visual Studio ギャラリーから個別の Silverlight プラグインをインストールすることができます。

#### <a name="setting-up-your-machine"></a>コンピューターを設定する

1. Visual Studio 2012.1 以降がインストールされていることを確認します。

2. [Microsoft Visual Studio UI Test Plugin for Silverlight](https://marketplace.visualstudio.com/items?itemName=PrachiBoraMSFT.MicrosoftVisualStudioUITestPluginforSilverlight)をインストールします。

3. [Fiddler](http://www.fiddler2.com/fiddler2/)をインストールします。 これは、HTTP トラフィックをキャプチャしてログ記録するだけのツールです。

4. [fiddlerXap プロジェクト](https://40jajy3iyl373v772m19fybm-wpengine.netdna-ssl.com/wp-content/uploads/sites/6/2019/02/FiddlerXapProxy.zip)をダウンロードします。 解凍、ビルド後、"CopySLHelper.bat" スクリプトを実行して、Fiddler ツールで Silverlight Web パーツをテストするときに必要なヘルパー DLL をインストールします。

   コンピューターのセットアップ後、Silverlight Web パーツを使用する SharePoint 2010 アプリのテストを開始するために、次の手順に従います。

#### <a name="testing-silverlight-web-parts"></a>Silverlight Web パーツをテストする

1. Fiddler を起動します。

2. ブラウザーのキャッシュを消去します。 この操作が必要なのは、Silverlight UI オートメーション ヘルパー DLL が含まれている XAP ファイルが、通常はキャッシュされるためです。 変更した XAP ファイルが確実に格納されるようにするために、ブラウザーのキャッシュを消去します。

3. Web ページを開きます。

4. 通常の Web アプリケーション テストと同様に、レコーダーを開始し、コードを生成します。

5. 生成されたコードが、Microsoft.VisualStudio.TestTools.UITest.Extension.Silverlight.dll を参照することを確認する必要があります。

     詳細については、「 [Visual Studio 2012 での SharePoint 2010 の UI テスト](https://devblogs.microsoft.com/devops/ui-testing-sharepoint-2010-with-visual-studio-2012/)」をご覧ください。

## <a name="external-resources"></a>外部リソース

### <a name="blogs"></a>ブログ
 [Visual Studio 2012 での SharePoint 2010 の UI テスト](https://devblogs.microsoft.com/devops/ui-testing-sharepoint-2010-with-visual-studio-2012/)

 [コード化された UI テストでの Silverlight コントロールの検索ロジックを理解する](https://tapas-techsnips.blogspot.com/)

 [Silverlight コントロールのプロパティの取得](https://tapas-techsnips.blogspot.com/)

 [コード化された UI テストのコンテンツ インデックス](https://blogs.msdn.microsoft.com/mathew_aniyan/2013/02/18/content-index-for-coded-ui-test/)

### <a name="guidance"></a>ガイダンス
 [Visual Studio 2012 を使用した継続的デリバリーのためのテスト – 第 5 章: システム テストの自動化](https://msdn.microsoft.com/library/jj159335.aspx)

### <a name="forum"></a>フォーラム
 [Visual Studio ALM + Team Foundation Server のブログ](https://blogs.msdn.com/b/visualstudioalm/)

## <a name="see-also"></a>参照
 [UI オートメーションを使用してコードをテストする](../test/use-ui-automation-to-test-your-code.md) [Web パフォーマンスとロードテスト sharepoint 2010 および2013アプリケーション](https://msdn.microsoft.com/library/20c2e469-0e4e-4296-a739-c0e8fff36e54) [sharepoint ソリューションの作成](https://msdn.microsoft.com/library/4bfb1e59-97c9-4594-93f8-3068b4eb9631)sharepoint のコードの[検証および](https://msdn.microsoft.com/library/b5f3bce2-6a51-41b1-a292-9e384bae420c)デバッグ sharepoint ソリューションの[ビルドと](https://msdn.microsoft.com/library/c9e7c9ab-4eb3-40cd-a9b9-6c2a896f70ae)デバッグ sharepoint[アプリケーションのパフォーマンスのプロファイリング](https://msdn.microsoft.com/library/61ae02e7-3f37-4230-bae1-54a498c2fae8)

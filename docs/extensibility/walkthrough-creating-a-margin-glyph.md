---
title: 'チュートリアル: 余白グリフの作成 |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - margin glyph
ms.assetid: 814185db-24f9-417f-b3b1-7c5aabb42b45
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9588b150dd795fc2bc5e6c55d8f6e2359f609939
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697698"
---
# <a name="walkthrough-create-a-margin-glyph"></a>チュートリアル: 余白グリフを作成する
カスタム エディター拡張機能を使用して、エディターの余白の外観をカスタマイズできます。 このチュートリアルでは、コード コメントに "todo" という単語が表示されるたびに、インジケーターの余白にカスタム グリフを配置します。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-mef-project"></a>MEF プロジェクトを作成する

1. C# VSIX プロジェクトを作成します。 ([**新しいプロジェクト**] ダイアログで、[**ビジュアル C# / 拡張性**] を選択し、次に**VSIX プロジェクト**を選択します)。ソリューションに名前`TodoGlyphTest`を付ける:

2. エディター分類子プロジェクト項目を追加します。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

3. 既存のクラス ファイルを削除します。

## <a name="define-the-glyph"></a>グリフの定義
 インタフェースを実行してグリフを<xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactory>定義します。

### <a name="to-define-the-glyph"></a>グリフを定義するには

1. クラス ファイルを追加し、その名前を `TodoGlyphFactory`にします。

2. 宣言を使用して、次のコードを追加します。

     [!code-csharp[VSSDKTodoGlyphTest#1](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_1.cs)]
     [!code-vb[VSSDKTodoGlyphTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_1.vb)]

3. を実装するという`TodoGlyphFactory`名前のクラス<xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactory>を追加します。

     [!code-csharp[VSSDKTodoGlyphTest#2](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_2.cs)]
     [!code-vb[VSSDKTodoGlyphTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_2.vb)]

4. グリフの寸法を定義するプライベート フィールドを追加します。

     [!code-csharp[VSSDKTodoGlyphTest#3](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_3.cs)]
     [!code-vb[VSSDKTodoGlyphTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_3.vb)]

5. グリフ`GenerateGlyph`のユーザー インターフェイス (UI) 要素を定義することによって実装します。 `TodoTag`このチュートリアルの後半で定義します。

     [!code-csharp[VSSDKTodoGlyphTest#4](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_4.cs)]
     [!code-vb[VSSDKTodoGlyphTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_4.vb)]

6. を実装するという`TodoGlyphFactoryProvider`名前のクラス<xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactoryProvider>を追加します。 このクラスをエクスポートするには<xref:Microsoft.VisualStudio.Utilities.NameAttribute>、"TodoGlyph" の<xref:Microsoft.VisualStudio.Utilities.OrderAttribute>値、VsText マーカーの<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>後、"コード" の<xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>a、および TodoTag の a を指定します。

     [!code-csharp[VSSDKTodoGlyphTest#5](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_5.cs)]
     [!code-vb[VSSDKTodoGlyphTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_5.vb)]

7. をインスタンス<xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactoryProvider.GetGlyphFactory%2A>化してメソッドを実装します`TodoGlyphFactory`。

     [!code-csharp[VSSDKTodoGlyphTest#6](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_6.cs)]
     [!code-vb[VSSDKTodoGlyphTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_6.vb)]

## <a name="define-a-todo-tag-and-tagger"></a>Todo タグとタグ付けの定義
 前の手順で定義した UI 要素とインジケーターの余白との関係を定義します。 タグの種類とタグ付けを作成し、タガー プロバイダーを使用してエクスポートします。

### <a name="to-define-a-todo-tag-and-tagger"></a>todo タグとタグ付けを定義するには

1. 新しいクラス ファイルをプロジェクトに追加し、`TodoTagger`という名前を付けます。

2. 次のインポートを追加します。

     [!code-csharp[VSSDKTodoGlyphTest#7](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_7.cs)]
     [!code-vb[VSSDKTodoGlyphTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_7.vb)]

3. `TodoTag`という名前のクラスを追加します。

     [!code-csharp[VSSDKTodoGlyphTest#8](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_8.cs)]
     [!code-vb[VSSDKTodoGlyphTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_8.vb)]

4. 型を実装する`TodoTagger`クラスを<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>変更します`TodoTag`。

     [!code-csharp[VSSDKTodoGlyphTest#9](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_9.cs)]
     [!code-vb[VSSDKTodoGlyphTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_9.vb)]

5. クラスに`TodoTagger`、分類範囲内で検索する<xref:Microsoft.VisualStudio.Text.Classification.IClassifier>テキストおよび のプライベート フィールドを追加します。

     [!code-csharp[VSSDKTodoGlyphTest#10](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_10.cs)]
     [!code-vb[VSSDKTodoGlyphTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_10.vb)]

6. 分類子を設定するコンストラクターを追加します。

     [!code-csharp[VSSDKTodoGlyphTest#11](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_11.cs)]
     [!code-vb[VSSDKTodoGlyphTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_11.vb)]

7. "comment" という単語を含み、テキストに検索テキストが含まれるすべての分類範囲を検索して<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A>、メソッドを実装します。 検索テキストが見つかった場合は常に、新<xref:Microsoft.VisualStudio.Text.Tagging.TagSpan%601>しいタイプ`TodoTag`を返します。

     [!code-csharp[VSSDKTodoGlyphTest#12](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_12.cs)]
     [!code-vb[VSSDKTodoGlyphTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_12.vb)]

8. イベントを`TagsChanged`宣言します。

     [!code-csharp[VSSDKTodoGlyphTest#13](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_13.cs)]
     [!code-vb[VSSDKTodoGlyphTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_13.vb)]

9. を実装するという`TodoTaggerProvider`名前のクラス<xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider>を追加し、"<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>コード" と TodoTag のを使用して<xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>エクスポートします。

     [!code-csharp[VSSDKTodoGlyphTest#14](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_14.cs)]
     [!code-vb[VSSDKTodoGlyphTest#14](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_14.vb)]

10. をインポート<xref:Microsoft.VisualStudio.Text.Classification.IClassifierAggregatorService>します。

     [!code-csharp[VSSDKTodoGlyphTest#15](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_15.cs)]
     [!code-vb[VSSDKTodoGlyphTest#15](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_15.vb)]

11. をインスタンス<xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider.CreateTagger%2A>化してメソッドを実装します`TodoTagger`。

     [!code-csharp[VSSDKTodoGlyphTest#16](../extensibility/codesnippet/CSharp/walkthrough-creating-a-margin-glyph_16.cs)]
     [!code-vb[VSSDKTodoGlyphTest#16](../extensibility/codesnippet/VisualBasic/walkthrough-creating-a-margin-glyph_16.vb)]

## <a name="build-and-test-the-code"></a>コードのビルドとテスト
 このコードをテストするには、TodoGlyphTest ソリューションをビルドし、実験用インスタンスで実行します。

### <a name="to-build-and-test-the-todoglyphtest-solution"></a>TodoGlyphTest ソリューションをビルドしてテストするには

1. ソリューションをビルドします。

2. **F5**キーを押してプロジェクトを実行します。 2 番目のインスタンスが起動します。

3. インジケーターマージンが表示されていることを確認します。 ([**ツール**] メニューの [**オプション**] をクリックします。 [**テキスト エディター]** ページで、[**インジケーターの余白]** が選択されていることを確認します。

4. コメントのあるコード ファイルを開きます。 コメント セクションの 1 つに "todo" という単語を追加します。

5. コード ウィンドウの左側のインジケーターマージンに、濃い青色の輪郭が表示されます。

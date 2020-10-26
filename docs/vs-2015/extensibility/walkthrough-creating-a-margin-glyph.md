---
title: 'チュートリアル: Margin グリフの作成 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - margin glyph
ms.assetid: 814185db-24f9-417f-b3b1-7c5aabb42b45
caps.latest.revision: 30
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: aa18b900ca44fbb52c646bfdf021beed6e77f504
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148858"
---
# <a name="walkthrough-creating-a-margin-glyph"></a>チュートリアル: 余白のグリフの作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

エディターの余白の外観をカスタマイズするには、カスタムエディター拡張機能を使用します。 このチュートリアルでは、コードコメントに "todo" という語が表示されるたびに、カスタムグリフをインジケーターの余白に配置します。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
## <a name="creating-a-mef-project"></a>MEF プロジェクトの作成  
  
1. C# VSIX プロジェクトを作成します。 ([ **新しいプロジェクト** ] ダイアログで、[Visual C#]、[ **拡張機能**]、[ **VSIX プロジェクト**] の順に選択します)。ソリューションにという名前を指定 `TodoGlyphTest` します。  
  
2. エディター分類子プロジェクト項目を追加します。 詳細については、「 [エディター項目テンプレートを使用した拡張機能の作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。  
  
3. 既存のクラス ファイルを削除します。  
  
## <a name="defining-the-glyph"></a>グリフの定義  
 インターフェイスを実装して、グリフを定義し <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactory> ます。  
  
#### <a name="to-define-the-glyph"></a>グリフを定義するには  
  
1. クラス ファイルを追加し、その名前を `TodoGlyphFactory`にします。  
  
2. 次の using 宣言を追加します。  
  
     [!code-csharp[VSSDKTodoGlyphTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs#1)]
     [!code-vb[VSSDKTodoGlyphTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb#1)]  
  
3. を実装するという名前のクラスを追加 `TodoGlyphFactory` <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactory> します。  
  
     [!code-csharp[VSSDKTodoGlyphTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs#2)]
     [!code-vb[VSSDKTodoGlyphTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb#2)]  
  
4. グリフの大きさを定義するプライベートフィールドを追加します。  
  
     [!code-csharp[VSSDKTodoGlyphTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs#3)]
     [!code-vb[VSSDKTodoGlyphTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb#3)]  
  
5. `GenerateGlyph`グリフのユーザーインターフェイス (UI) 要素を定義してを実装します。 `TodoTag` は、このチュートリアルの後半で定義されています。  
  
     [!code-csharp[VSSDKTodoGlyphTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs#4)]
     [!code-vb[VSSDKTodoGlyphTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb#4)]  
  
6. を実装するという名前のクラスを追加 `TodoGlyphFactoryProvider` <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactoryProvider> します。 このクラスをエクスポートするには、を <xref:Microsoft.VisualStudio.Utilities.NameAttribute> "TodoGlyph"、 <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> After VsTextMarker の、を <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "code"、および <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> TodoTag のを使用します。  
  
     [!code-csharp[VSSDKTodoGlyphTest#5](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs#5)]
     [!code-vb[VSSDKTodoGlyphTest#5](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb#5)]  
  
7. <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactoryProvider.GetGlyphFactory%2A>をインスタンス化して、メソッドを実装し `TodoGlyphFactory` ます。  
  
     [!code-csharp[VSSDKTodoGlyphTest#6](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs#6)]
     [!code-vb[VSSDKTodoGlyphTest#6](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb#6)]  
  
## <a name="defining-a-todo-tag-and-tagger"></a>Todo タグとタグを定義する  
 前の手順で定義した UI 要素とインジケーターマージンの間のリレーションシップを定義します。これには、タグの種類とタグを作成し、タガープロバイダーを使用してエクスポートします。  
  
#### <a name="to-define-a-todo-tag-and-tagger"></a>Todo タグとタガーを定義するには  
  
1. 新しいクラスファイルをプロジェクトに追加し、という名前を指定 `TodoTagger` します。  
  
2. 次のインポートを追加します。  
  
     [!code-csharp[VSSDKTodoGlyphTest#7](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs#7)]
     [!code-vb[VSSDKTodoGlyphTest#7](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb#7)]  
  
3. `TodoTag`という名前のクラスを追加します。  
  
     [!code-csharp[VSSDKTodoGlyphTest#8](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs#8)]
     [!code-vb[VSSDKTodoGlyphTest#8](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb#8)]  
  
4. `TodoTagger`型のを実装するという名前のクラスを変更 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> `TodoTag` します。  
  
     [!code-csharp[VSSDKTodoGlyphTest#9](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs#9)]
     [!code-vb[VSSDKTodoGlyphTest#9](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb#9)]  
  
5. クラスに `TodoTagger` 、 <xref:Microsoft.VisualStudio.Text.Classification.IClassifier> 分類範囲内で検索するテキストのとのプライベートフィールドを追加します。  
  
     [!code-csharp[VSSDKTodoGlyphTest#10](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs#10)]
     [!code-vb[VSSDKTodoGlyphTest#10](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb#10)]  
  
6. 分類子を設定するコンストラクターを追加します。  
  
     [!code-csharp[VSSDKTodoGlyphTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs#11)]
     [!code-vb[VSSDKTodoGlyphTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb#11)]  
  
7. 名前に <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> "comment" という単語が含まれ、そのテキストに検索テキストが含まれているすべての分類範囲を検索して、メソッドを実装します。 検索テキストが見つかるたびに、型の新しいが返され <xref:Microsoft.VisualStudio.Text.Tagging.TagSpan%601> `TodoTag` ます。  
  
     [!code-csharp[VSSDKTodoGlyphTest#12](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs#12)]
     [!code-vb[VSSDKTodoGlyphTest#12](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb#12)]  
  
8. イベントを宣言 `TagsChanged` します。  
  
     [!code-csharp[VSSDKTodoGlyphTest#13](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs#13)]
     [!code-vb[VSSDKTodoGlyphTest#13](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb#13)]  
  
9. を実装するという名前のクラスを追加 `TodoTaggerProvider` <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider> し、 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "Code" と TodoTag のを使用してエクスポートし <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> ます。  
  
     [!code-csharp[VSSDKTodoGlyphTest#14](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs#14)]
     [!code-vb[VSSDKTodoGlyphTest#14](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb#14)]  
  
10. をインポート <xref:Microsoft.VisualStudio.Text.Classification.IClassifierAggregatorService> します。  
  
     [!code-csharp[VSSDKTodoGlyphTest#15](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs#15)]
     [!code-vb[VSSDKTodoGlyphTest#15](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb#15)]  
  
11. <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider.CreateTagger%2A>をインスタンス化して、メソッドを実装し `TodoTagger` ます。  
  
     [!code-csharp[VSSDKTodoGlyphTest#16](../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs#16)]
     [!code-vb[VSSDKTodoGlyphTest#16](../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb#16)]  
  
## <a name="building-and-testing-the-code"></a>コードのビルドとテスト  
 このコードをテストするには、TodoGlyphTest ソリューションをビルドし、実験用インスタンスで実行します。  
  
#### <a name="to-build-and-test-the-todoglyphtest-solution"></a>TodoGlyphTest ソリューションをビルドしてテストするには  
  
1. ソリューションをビルドします。  
  
2. F5 キーを押して、プロジェクトを実行します。 Visual Studio の2番目のインスタンスがインスタンス化されます。  
  
3. インジケーターマージンが表示されていることを確認します。 ([ **ツール** ] メニューの [ **オプション**] をクリックします。 [ **テキストエディター** ] ページで、[ **インジケーターマージン** ] が選択されていることを確認します。)  
  
4. コメントが含まれているコードファイルを開きます。 コメントセクションのいずれかに "todo" という単語を追加します。  
  
5. 濃い青の枠線が付いた薄い青の円が、コードウィンドウの左側のインジケーターマージンに表示されます。

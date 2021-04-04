---
title: 'チュートリアル: Margin グリフの作成 |Microsoft Docs'
description: このチュートリアルを使用して、カスタムエディター拡張機能を使用してエディターの余白の外観をカスタマイズする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - margin glyph
ms.assetid: 814185db-24f9-417f-b3b1-7c5aabb42b45
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ec5eecef40220c2cf2d4e3f1ece8eb5eb763bdeb
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217412"
---
# <a name="walkthrough-create-a-margin-glyph"></a>チュートリアル: 余白のグリフの作成
エディターの余白の外観をカスタマイズするには、カスタムエディター拡張機能を使用します。 このチュートリアルでは、コードコメントに "todo" という語が表示されるたびに、カスタムグリフをインジケーターの余白に配置します。

## <a name="prerequisites"></a>前提条件
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-mef-project"></a>MEF プロジェクトを作成する

1. C# VSIX プロジェクトを作成します。 ([ **新しいプロジェクト** ] ダイアログで、[Visual C#]、[ **拡張機能**]、[ **VSIX プロジェクト**] の順に選択します)。ソリューションにという名前を指定 `TodoGlyphTest` します。

2. エディター分類子プロジェクト項目を追加します。 詳細については、「 [エディター項目テンプレートを使用して拡張機能を作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)する」を参照してください。

3. 既存のクラス ファイルを削除します。

## <a name="define-the-glyph"></a>グリフを定義する
 インターフェイスを実行して、グリフを定義し <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactory> ます。

### <a name="to-define-the-glyph"></a>グリフを定義するには

1. クラス ファイルを追加し、その名前を `TodoGlyphFactory`にします。

2. 宣言を使用して、次のコードを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs" id="Snippet1":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb" id="Snippet1":::

3. を実装するという名前のクラスを追加 `TodoGlyphFactory` <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactory> します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb" id="Snippet2":::

4. グリフの大きさを定義するプライベートフィールドを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb" id="Snippet3":::

5. `GenerateGlyph`グリフのユーザーインターフェイス (UI) 要素を定義してを実装します。 `TodoTag` は、このチュートリアルの後半で定義されています。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs" id="Snippet4":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb" id="Snippet4":::

6. を実装するという名前のクラスを追加 `TodoGlyphFactoryProvider` <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactoryProvider> します。 このクラスをエクスポートするには、を <xref:Microsoft.VisualStudio.Utilities.NameAttribute> "TodoGlyph"、 <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> After VsTextMarker の、を <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "code"、および <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> TodoTag のを使用します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs" id="Snippet5":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb" id="Snippet5":::

7. <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactoryProvider.GetGlyphFactory%2A>をインスタンス化して、メソッドを実装し `TodoGlyphFactory` ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs" id="Snippet6":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb" id="Snippet6":::

## <a name="define-a-todo-tag-and-tagger"></a>Todo タグとタグを定義する
 前の手順で定義した UI 要素とインジケーターマージンの間のリレーションシップを定義します。 タグの種類とタグを作成し、タガープロバイダーを使用してエクスポートします。

### <a name="to-define-a-todo-tag-and-tagger"></a>Todo タグとタガーを定義するには

1. 新しいクラスファイルをプロジェクトに追加し、という名前を指定 `TodoTagger` します。

2. 次のインポートを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet7":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet7":::

3. `TodoTag`という名前のクラスを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet8":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet8":::

4. `TodoTagger`型のを実装するという名前のクラスを変更 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> `TodoTag` します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet9":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet9":::

5. クラスに `TodoTagger` 、 <xref:Microsoft.VisualStudio.Text.Classification.IClassifier> 分類範囲内で検索するテキストのとのプライベートフィールドを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet10":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet10":::

6. 分類子を設定するコンストラクターを追加します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet11":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet11":::

7. 名前に <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> "comment" という単語が含まれ、そのテキストに検索テキストが含まれているすべての分類範囲を検索して、メソッドを実装します。 検索テキストが見つかるたびに、型の新しいが返され <xref:Microsoft.VisualStudio.Text.Tagging.TagSpan%601> `TodoTag` ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet12":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet12":::

8. イベントを宣言 `TagsChanged` します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet13":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet13":::

9. を実装するという名前のクラスを追加 `TodoTaggerProvider` <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider> し、 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "Code" と TodoTag のを使用してエクスポートし <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet14":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet14":::

10. をインポート <xref:Microsoft.VisualStudio.Text.Classification.IClassifierAggregatorService> します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet15":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet15":::

11. <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider.CreateTagger%2A>をインスタンス化して、メソッドを実装し `TodoTagger` ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet16":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet16":::

## <a name="build-and-test-the-code"></a>コードをビルドしてテストする
 このコードをテストするには、TodoGlyphTest ソリューションをビルドし、実験用インスタンスで実行します。

### <a name="to-build-and-test-the-todoglyphtest-solution"></a>TodoGlyphTest ソリューションをビルドしてテストするには

1. ソリューションをビルドします。

2. **F5** キーを押してプロジェクトを実行します。 Visual Studio の2番目のインスタンスが起動します。

3. インジケーターマージンが表示されていることを確認します。 ([ **ツール** ] メニューの [ **オプション**] をクリックします。 [ **テキストエディター** ] ページで、[ **インジケーターマージン** ] が選択されていることを確認します。)

4. コメントが含まれているコードファイルを開きます。 コメントセクションのいずれかに "todo" という単語を追加します。

5. コードウィンドウの左側のインジケーターマージンに濃い青の輪郭の付いた薄い青の円が表示されます。

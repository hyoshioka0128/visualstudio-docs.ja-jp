---
title: 'チュートリアル: 一致する中かっこを表示する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - brace matching
ms.assetid: 5af08ac7-1d08-4ccf-997e-01aa6cb3d3d7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 107610733ab9b5c8085b3f987fa999250b453d63
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697449"
---
# <a name="walkthrough-display-matching-braces"></a>チュートリアル: 一致する中かっこを表示する
一致させる中かっこを定義し、カレットが中かっこの 1 つに表示されている場合は、対応する中かっこにテキスト マーカー タグを追加することで、中かっこの一致などの言語ベースの機能を実装します。 言語のコンテキストで中かっこを定義し、独自のファイル名拡張子とコンテンツ タイプを定義し、タグをその種類だけに適用したり、タグを既存のコンテンツ タイプ ("text"など) に適用したりできます。 次のチュートリアルでは、"text" コンテンツ タイプにかっこの一致タグを適用する方法を示します。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-managed-extensibility-framework-mef-project"></a>マネージ機能拡張フレームワーク (MEF) プロジェクトを作成する

#### <a name="to-create-a-mef-project"></a>MEF プロジェクトを作成するには

1. エディター分類子プロジェクトを作成します。 ソリューション `BraceMatchingTest`の名前を指定します。

2. エディター分類子項目テンプレートをプロジェクトに追加します。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

3. 既存のクラス ファイルを削除します。

## <a name="implement-a-brace-matching-tagger"></a>ブレースマッチングタガーを実装する
 Visual Studio で使用されているのと似たかっこの強調表示効果を取得するには、型<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>のタガーを実装できます。 次のコードは、入れ子の任意のレベルでかっこのペアのタガーを定義する方法を示しています。 この例では、タガーコンストラクタで定義{}されている[]の中かっこのペアが定義されていますが、完全な言語実装では、関連するブレースのペアは言語仕様で定義されます。

### <a name="to-implement-a-brace-matching-tagger"></a>ブレースに一致するタガーを実装するには

1. クラス ファイルを追加し、BraceMatching という名前を付けます。

2. 次の名前空間をインポートします。

     [!code-csharp[VSSDKBraceMatchingTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_1.cs)]
     [!code-vb[VSSDKBraceMatchingTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_1.vb)]

3. 型から`BraceMatchingTagger`<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>継承するクラスを定義します<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>。

     [!code-csharp[VSSDKBraceMatchingTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_2.cs)]
     [!code-vb[VSSDKBraceMatchingTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_2.vb)]

4. テキスト ビュー、ソース バッファー、現在のスナップショット ポイント、および一連の中かっこのペアのプロパティを追加します。

     [!code-csharp[VSSDKBraceMatchingTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_3.cs)]
     [!code-vb[VSSDKBraceMatchingTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_3.vb)]

5. タガー コンストラクタで、プロパティを設定し、ビュー変更イベント<xref:Microsoft.VisualStudio.Text.Editor.ITextCaret.PositionChanged>と<xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged>を購読します。 この例では、例示の目的で、一致するペアもコンストラクターで定義されています。

     [!code-csharp[VSSDKBraceMatchingTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_4.cs)]
     [!code-vb[VSSDKBraceMatchingTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_4.vb)]

6. 実装の<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>一部として、TagsChanged イベントを宣言します。

     [!code-csharp[VSSDKBraceMatchingTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_5.cs)]
     [!code-vb[VSSDKBraceMatchingTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_5.vb)]

7. イベント ハンドラーは、プロパティの現在のキャレット`CurrentChar`位置を更新し、TagsChanged イベントを発生させます。

     [!code-csharp[VSSDKBraceMatchingTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_6.cs)]
     [!code-vb[VSSDKBraceMatchingTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_6.vb)]

8. 現在の<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A>文字が中かっこの場合、または前の文字が Visual Studio のように近い中かっこである場合に、中かっこを一致させるメソッドを実装します。 一致が見つかると、このメソッドは、左中かっことクローズ中かっこの 2 つのタグをインスタンス化します。

     [!code-csharp[VSSDKBraceMatchingTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_7.cs)]
     [!code-vb[VSSDKBraceMatchingTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_7.vb)]

9. 次のプライベート メソッドは、入れ子の任意のレベルで一致する中かっこを検索します。 最初のメソッドは、開いている文字と一致する close 文字を検索します。

     [!code-csharp[VSSDKBraceMatchingTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_8.cs)]
     [!code-vb[VSSDKBraceMatchingTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_8.vb)]

10. 次のヘルパー メソッドは、終了文字に一致するオープン文字を検索します。

     [!code-csharp[VSSDKBraceMatchingTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_9.cs)]
     [!code-vb[VSSDKBraceMatchingTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_9.vb)]

## <a name="implement-a-brace-matching-tagger-provider"></a>ブレースに一致するタガー プロバイダを実装する
 タガーの実装に加えて、タガープロバイダーを実装およびエクスポートする必要があります。 この場合、プロバイダのコンテンツ タイプは "text" です。 そのため、すべての種類のテキスト ファイルにかっこの一致が表示されますが、より詳細な実装では、特定のコンテンツ タイプにのみ中かっこが適用されます。

### <a name="to-implement-a-brace-matching-tagger-provider"></a>タガー プロバイダに一致するかっこを実装するには

1. から<xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider>継承するタガー プロバイダを宣言し、BraceMatchingTaggerProvider という名前を付け、"text" と<xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute>の<xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag>a<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>を指定してエクスポートします。

     [!code-csharp[VSSDKBraceMatchingTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_10.cs)]
     [!code-vb[VSSDKBraceMatchingTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_10.vb)]

2. 括弧<xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A>一致タガーをインスタンス化するメソッドを実装します。

     [!code-csharp[VSSDKBraceMatchingTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_11.cs)]
     [!code-vb[VSSDKBraceMatchingTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_11.vb)]

## <a name="build-and-test-the-code"></a>コードのビルドとテスト
 このコードをテストするには、BraceMatchingTest ソリューションをビルドし、実験用インスタンスで実行します。

#### <a name="to-build-and-test-bracematchingtest-solution"></a>ブレースマッチングテストソリューションを構築してテストするには

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 番目のインスタンスが起動します。

3. テキスト ファイルを作成し、一致する中かっこを含むテキストを入力します。

    ```
    hello {
    goodbye}

    {}

    {hello}
    ```

4. カレットを左中かっこの前に配置すると、その中かっこと対応する近いかっこの両方が強調表示されます。 カーソルを右中かっこの直後に置くと、その中かっこと対応する左中かっこが強調表示されます。

## <a name="see-also"></a>関連項目
- [チュートリアル: コンテンツ タイプをファイル名拡張子にリンクする](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)

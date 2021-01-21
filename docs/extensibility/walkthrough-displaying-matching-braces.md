---
title: 'チュートリアル: 一致する中かっこの表示 |Microsoft Docs'
description: このチュートリアルを使用して、言語のコンテキストで中かっこを定義し、テキストコンテンツの種類にかっこの一致タグを適用する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - brace matching
ms.assetid: 5af08ac7-1d08-4ccf-997e-01aa6cb3d3d7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ce40f5673a8aba4ab3f7714a3aafdc3de4697cc4
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97877950"
---
# <a name="walkthrough-display-matching-braces"></a>チュートリアル: 一致する中かっこの表示
一致させるかっこを定義することによる中かっこの一致など、言語に基づく機能を実装し、カレットが中かっこのいずれかにある場合は、対応する中かっこにテキストマーカータグを追加します。 言語のコンテキストで中かっこを定義し、独自のファイル名の拡張子とコンテンツの種類を定義し、その種類のタグだけを適用するか、既存のコンテンツの種類 ("text" など) にタグを適用することができます。 次のチュートリアルでは、かっこに一致するタグを "text" コンテンツタイプに適用する方法を示します。

## <a name="prerequisites"></a>前提条件
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-managed-extensibility-framework-mef-project"></a>Managed Extensibility Framework (MEF) プロジェクトを作成する

#### <a name="to-create-a-mef-project"></a>MEF プロジェクトを作成するには

1. エディター分類子プロジェクトを作成します。 ソリューション `BraceMatchingTest`の名前を指定します。

2. エディター分類子項目テンプレートをプロジェクトに追加します。 詳細については、「 [エディター項目テンプレートを使用して拡張機能を作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)する」を参照してください。

3. 既存のクラス ファイルを削除します。

## <a name="implement-a-brace-matching-tagger"></a>かっこに一致するタグを実装する
 Visual Studio で使用されているものに似た中かっこの強調表示効果を取得するには、型のタガーを実装し <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> ます。 次のコードは、任意の入れ子レベルで中かっこのペアのタガーを定義する方法を示しています。 この例では、[] との中かっこのペアが {} タガーコンストラクターで定義されていますが、完全な言語実装では、関連する中かっこのペアが言語仕様で定義されています。

### <a name="to-implement-a-brace-matching-tagger"></a>かっこに一致するタグを実装するには

1. クラスファイルを追加し、BraceMatching という名前を指定します。

2. 次の名前空間をインポートします。

     [!code-csharp[VSSDKBraceMatchingTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_1.cs)]
     [!code-vb[VSSDKBraceMatchingTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_1.vb)]

3. `BraceMatchingTagger`型のから継承するクラスを定義 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> します。

     [!code-csharp[VSSDKBraceMatchingTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_2.cs)]
     [!code-vb[VSSDKBraceMatchingTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_2.vb)]

4. テキストビュー、ソースバッファー、現在のスナップショットポイント、および一連のかっこのペアのプロパティを追加します。

     [!code-csharp[VSSDKBraceMatchingTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_3.cs)]
     [!code-vb[VSSDKBraceMatchingTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_3.vb)]

5. タガーコンストラクターで、プロパティを設定し、ビュー変更イベントおよびをサブスクライブ <xref:Microsoft.VisualStudio.Text.Editor.ITextCaret.PositionChanged> し <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> ます。 この例では、説明を目的として、一致するペアがコンストラクターでも定義されています。

     [!code-csharp[VSSDKBraceMatchingTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_4.cs)]
     [!code-vb[VSSDKBraceMatchingTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_4.vb)]

6. 実装の一部として <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> 、TagsChanged イベントを宣言します。

     [!code-csharp[VSSDKBraceMatchingTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_5.cs)]
     [!code-vb[VSSDKBraceMatchingTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_5.vb)]

7. イベントハンドラーは、プロパティの現在のキャレット位置を更新 `CurrentChar` し、TagsChanged イベントを発生させます。

     [!code-csharp[VSSDKBraceMatchingTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_6.cs)]
     [!code-vb[VSSDKBraceMatchingTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_6.vb)]

8. 現在の <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> 文字が左中かっこの場合、または前の文字が Visual Studio のように終わりかっこである場合に、中かっこに一致するようにメソッドを実装します。 一致が検出されると、このメソッドは2つのタグをインスタンス化します。1つは左中かっこ用で、もう1つは終わりかっこ用です。

     [!code-csharp[VSSDKBraceMatchingTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_7.cs)]
     [!code-vb[VSSDKBraceMatchingTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_7.vb)]

9. 次のプライベートメソッドは、入れ子の任意のレベルで対応する中かっこを検索します。 最初のメソッドは、開いた文字に一致する終わりの文字を検索します。

     [!code-csharp[VSSDKBraceMatchingTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_8.cs)]
     [!code-vb[VSSDKBraceMatchingTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_8.vb)]

10. 次のヘルパーメソッドは、終わりの文字に一致する open 文字を検索します。

     [!code-csharp[VSSDKBraceMatchingTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_9.cs)]
     [!code-vb[VSSDKBraceMatchingTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_9.vb)]

## <a name="implement-a-brace-matching-tagger-provider"></a>かっこに一致するタグプロバイダーを実装します
 タガーを実装するだけでなく、タグプロバイダーを実装してエクスポートする必要もあります。 この場合、プロバイダーのコンテンツの種類は "text" です。 したがって、中かっこの一致はすべての種類のテキストファイルに表示されますが、完全な実装では、特定のコンテンツの種類に対してのみ、中かっこの一致が適用されます。

### <a name="to-implement-a-brace-matching-tagger-provider"></a>かっこに一致するタグプロバイダーを実装するには

1. から継承して BraceMatchingTaggerProvider という名前を付け、を <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider> <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "text" とのでエクスポートするタガーのプロバイダーを宣言し <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> ます。

     [!code-csharp[VSSDKBraceMatchingTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_10.cs)]
     [!code-vb[VSSDKBraceMatchingTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_10.vb)]

2. <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A>BraceMatchingTagger をインスタンス化するメソッドを実装します。

     [!code-csharp[VSSDKBraceMatchingTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-matching-braces_11.cs)]
     [!code-vb[VSSDKBraceMatchingTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-matching-braces_11.vb)]

## <a name="build-and-test-the-code"></a>コードをビルドしてテストする
 このコードをテストするには、BraceMatchingTest ソリューションをビルドし、実験用インスタンスで実行します。

#### <a name="to-build-and-test-bracematchingtest-solution"></a>BraceMatchingTest ソリューションをビルドしてテストするには

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の2番目のインスタンスが開始されます。

3. テキストファイルを作成し、対応する中かっこを含むテキストを入力します。

    ```
    hello {
    goodbye}

    {}

    {hello}
    ```

4. 左中かっこの前にカレットを配置する場合は、その中かっこと一致する終わりかっこの両方を強調表示する必要があります。 終わりかっこの直後にカーソルを置くと、その中かっこと一致する左中かっこの両方が強調表示されます。

## <a name="see-also"></a>関連項目
- [チュートリアル: コンテンツの種類をファイル名拡張子にリンクする](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)

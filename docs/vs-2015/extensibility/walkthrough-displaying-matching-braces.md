---
title: 'チュートリアル: 一致する中かっこの表示 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - brace matching
ms.assetid: 5af08ac7-1d08-4ccf-997e-01aa6cb3d3d7
caps.latest.revision: 28
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: caaafd0143d3b09a51518ee5f54a02b06dbf10aa
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68165789"
---
# <a name="walkthrough-displaying-matching-braces"></a>チュートリアル: 対応するかっこの表示
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

一致させるかっこを定義して、かっこの照合などの言語ベースの機能を実装し、カレットが中かっこのいずれかにある場合は、対応する中かっこにテキストマーカータグを追加できます。 言語のコンテキストで中かっこを定義することも、独自のファイル名の拡張子とコンテンツの種類を定義し、その型にのみタグを適用することもできます。または、既存のコンテンツの種類 ("text" など) にタグを適用することもできます。 次のチュートリアルでは、かっこに一致するタグを "text" コンテンツタイプに適用する方法を示します。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
## <a name="creating-a-managed-extensibility-framework-mef-project"></a>Managed Extensibility Framework (MEF) プロジェクトの作成  
  
#### <a name="to-create-a-mef-project"></a>MEF プロジェクトを作成するには  
  
1. エディター分類子プロジェクトを作成します。 ソリューション `BraceMatchingTest`の名前を指定します。  
  
2. エディター分類子項目テンプレートをプロジェクトに追加します。 詳細については、「 [エディター項目テンプレートを使用した拡張機能の作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。  
  
3. 既存のクラス ファイルを削除します。  
  
## <a name="implementing-a-brace-matching-tagger"></a>かっこに一致するタグを実装する  
 Visual Studio で使用されているものに似た中かっこの強調表示効果を取得するには、型のタガーを実装し <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> ます。 次のコードは、任意の入れ子レベルで中かっこのペアのタガーを定義する方法を示しています。 この例では、かっこのペア [] です。 []、および {} はタガーコンストラクターで定義されていますが、完全な言語実装では、関連する中かっこのペアが言語仕様で定義されます。  
  
#### <a name="to-implement-a-brace-matching-tagger"></a>かっこに一致するタグを実装するには  
  
1. クラスファイルを追加し、BraceMatching という名前を指定します。  
  
2. 次の名前空間をインポートします。  
  
     [!code-csharp[VSSDKBraceMatchingTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#1)]
     [!code-vb[VSSDKBraceMatchingTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#1)]  
  
3. `BraceMatchingTagger`型のから継承するクラスを定義 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> します。  
  
     [!code-csharp[VSSDKBraceMatchingTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#2)]
     [!code-vb[VSSDKBraceMatchingTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#2)]  
  
4. テキストビュー、ソースバッファー、および現在のスナップショットポイントのプロパティと、一連の中かっこのペアを追加します。  
  
     [!code-csharp[VSSDKBraceMatchingTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#3)]
     [!code-vb[VSSDKBraceMatchingTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#3)]  
  
5. タガーコンストラクターで、プロパティを設定し、ビュー変更イベントおよびをサブスクライブ <xref:Microsoft.VisualStudio.Text.Editor.ITextCaret.PositionChanged> し <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> ます。 この例では、説明を目的として、一致するペアがコンストラクターでも定義されています。  
  
     [!code-csharp[VSSDKBraceMatchingTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#4)]
     [!code-vb[VSSDKBraceMatchingTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#4)]  
  
6. 実装の一部として <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> 、TagsChanged イベントを宣言します。  
  
     [!code-csharp[VSSDKBraceMatchingTest#5](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#5)]
     [!code-vb[VSSDKBraceMatchingTest#5](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#5)]  
  
7. イベントハンドラーは、プロパティの現在のキャレット位置を更新 `CurrentChar` し、TagsChanged イベントを発生させます。  
  
     [!code-csharp[VSSDKBraceMatchingTest#6](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#6)]
     [!code-vb[VSSDKBraceMatchingTest#6](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#6)]  
  
8. 現在の <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> 文字が左中かっこの場合、または前の文字が Visual Studio のように終わりかっこである場合に、中かっこに一致するようにメソッドを実装します。 一致が検出されると、このメソッドは2つのタグをインスタンス化します。1つは左中かっこ用で、もう1つは終わりかっこ用です。  
  
     [!code-csharp[VSSDKBraceMatchingTest#7](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#7)]
     [!code-vb[VSSDKBraceMatchingTest#7](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#7)]  
  
9. 次のプライベートメソッドは、入れ子の任意のレベルで対応する中かっこを検索します。 最初のメソッドは、開いた文字に一致する終わりの文字を検索します。  
  
     [!code-csharp[VSSDKBraceMatchingTest#8](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#8)]
     [!code-vb[VSSDKBraceMatchingTest#8](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#8)]  
  
10. 次のヘルパーメソッドは、終わりの文字に一致する open 文字を検索します。  
  
     [!code-csharp[VSSDKBraceMatchingTest#9](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#9)]
     [!code-vb[VSSDKBraceMatchingTest#9](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#9)]  
  
## <a name="implementing-a-brace-matching-tagger-provider"></a>かっこに一致するタグプロバイダーの実装  
 タガーを実装するだけでなく、タグプロバイダーを実装してエクスポートする必要もあります。 この場合、プロバイダーのコンテンツの種類は "text" です。 これは、すべての種類のテキストファイルに中かっこの一致が表示されることを意味しますが、完全な実装では、特定のコンテンツの種類に対してのみ、中かっこの一致が適用されます。  
  
#### <a name="to-implement-a-brace-matching-tagger-provider"></a>かっこに一致するタグプロバイダーを実装するには  
  
1. から継承して BraceMatchingTaggerProvider という名前を付け、を <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider> <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "text" とのでエクスポートするタガーのプロバイダーを宣言し <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> ます。  
  
     [!code-csharp[VSSDKBraceMatchingTest#10](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#10)]
     [!code-vb[VSSDKBraceMatchingTest#10](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#10)]  
  
2. <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A>BraceMatchingTagger をインスタンス化するメソッドを実装します。  
  
     [!code-csharp[VSSDKBraceMatchingTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs#11)]
     [!code-vb[VSSDKBraceMatchingTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb#11)]  
  
## <a name="building-and-testing-the-code"></a>コードのビルドとテスト  
 このコードをテストするには、BraceMatchingTest ソリューションをビルドし、実験用インスタンスで実行します。  
  
#### <a name="to-build-and-test-bracematchingtest-solution"></a>BraceMatchingTest ソリューションをビルドしてテストするには  
  
1. ソリューションをビルドします。  
  
2. デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 つ目のインスタンスがインスタンス化されます。  
  
3. テキストファイルを作成し、対応する中かっこを含むテキストを入力します。  
  
    ```  
    hello {  
    goodbye}  
  
    {}  
  
    {hello}  
    ```  
  
4. 左中かっこの前にカレットを配置する場合は、その中かっこと一致する終わりかっこの両方を強調表示する必要があります。 終わりかっこの直後にカーソルを置くと、その中かっこと一致する左中かっこの両方が強調表示されます。  
  
## <a name="see-also"></a>参照  
 [チュートリアル: コンテンツの種類とファイル名拡張子とをリンクさせる](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)

---
title: 'チュートリアル: アウトライン |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - outlining
ms.assetid: d75a44aa-265a-44d4-9c28-457f59c4ff9f
caps.latest.revision: 31
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7c1dd3d28b9978b52c95b5ff905d57720ed10f5d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68201953"
---
# <a name="walkthrough-outlining"></a>チュートリアル: アウトライン
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

展開または折りたたむテキスト領域の種類を定義することで、アウトラインなどの言語ベースの機能を実装できます。 言語サービスのコンテキストで地域を定義することも、独自のファイル名の拡張子とコンテンツの種類を定義して、その型にのみ領域の定義を適用することもできます。または、領域の定義を既存のコンテンツの種類 ("text" など) に適用することもできます。 このチュートリアルでは、アウトライン領域を定義および表示する方法について説明します。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
## <a name="creating-a-managed-extensibility-framework-mef-project"></a>Managed Extensibility Framework (MEF) プロジェクトの作成  
  
#### <a name="to-create-a-mef-project"></a>MEF プロジェクトを作成するには  
  
1. VSIX プロジェクトを作成します。 ソリューション `OutlineRegionTest`の名前を指定します。  
  
2. エディター分類子項目テンプレートをプロジェクトに追加します。 詳細については、「 [エディター項目テンプレートを使用した拡張機能の作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。  
  
3. 既存のクラス ファイルを削除します。  
  
## <a name="implementing-an-outlining-tagger"></a>アウトラインタグを実装する  
 アウトライン領域は、一種のタグ () でマークされ <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag> ます。 このタグは、標準のアウトライン動作を提供します。 アウトラインされた領域は、展開または折りたたむことができます。 アウトライン表示されている領域は、折りたたまれている場合はプラス記号でマークされます。展開されている場合はマイナス記号が付き、展開された領域は垂直線で demarcated ます。  
  
 次の手順では、"[" および "]" で区切られたすべての領域に対してアウトライン領域を作成するタグを定義する方法を示します。  
  
#### <a name="to-implement-an-outlining-tagger"></a>アウトラインタグを実装するには  
  
1. クラス ファイルを追加し、その名前を `OutliningTagger`にします。  
  
2. 次の名前空間をインポートします。  
  
     [!code-csharp[VSSDKOutlineRegionTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#1)]
     [!code-vb[VSSDKOutlineRegionTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#1)]  
  
3. という名前のクラスを作成 `OutliningTagger` し、を実装し <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> ます。  
  
     [!code-csharp[VSSDKOutlineRegionTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#2)]
     [!code-vb[VSSDKOutlineRegionTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#2)]  
  
4. テキストバッファーとスナップショットを追跡し、アウトライン領域としてタグ付けする必要がある行のセットを累積するために、いくつかのフィールドを追加します。 このコードには、アウトライン領域を表す領域オブジェクト (後で定義する) の一覧が含まれています。  
  
     [!code-csharp[VSSDKOutlineRegionTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#3)]
     [!code-vb[VSSDKOutlineRegionTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#3)]  
  
5. フィールドを初期化し、バッファーを解析し、イベントにイベントハンドラーを追加するタガーコンストラクターを追加し <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> ます。  
  
     [!code-csharp[VSSDKOutlineRegionTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#4)]
     [!code-vb[VSSDKOutlineRegionTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#4)]  
  
6. <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A>タグ範囲をインスタンス化するメソッドを実装します。 この例では、メソッドに渡されたの範囲が連続していることを前提としていますが、常にそうであるとは <xref:Microsoft.VisualStudio.Text.NormalizedSpanCollection> 限りません。 このメソッドは、アウトライン領域ごとに新しいタグスパンをインスタンス化します。  
  
     [!code-csharp[VSSDKOutlineRegionTest#5](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#5)]
     [!code-vb[VSSDKOutlineRegionTest#5](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#5)]  
  
7. `TagsChanged`イベントハンドラーを宣言します。  
  
     [!code-csharp[VSSDKOutlineRegionTest#6](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#6)]
     [!code-vb[VSSDKOutlineRegionTest#6](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#6)]  
  
8. `BufferChanged`テキストバッファーを解析することによって、イベントに応答するイベントハンドラーを追加 <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> します。  
  
     [!code-csharp[VSSDKOutlineRegionTest#7](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#7)]
     [!code-vb[VSSDKOutlineRegionTest#7](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#7)]  
  
9. バッファーを解析するメソッドを追加します。 ここで示す例は、例示のみを目的としています。 バッファーは、入れ子になったアウトライン領域に同期的に解析されます。  
  
     [!code-csharp[VSSDKOutlineRegionTest#8](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#8)]
     [!code-vb[VSSDKOutlineRegionTest#8](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#8)]  
  
10. 次のヘルパーメソッドは、アウトラインのレベルを表す整数を取得します。1は、最も左の中かっこのペアです。  
  
     [!code-csharp[VSSDKOutlineRegionTest#9](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#9)]
     [!code-vb[VSSDKOutlineRegionTest#9](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#9)]  
  
11. 次のヘルパーメソッドは、(このトピックで後述するように定義されている) 領域を SnapshotSpan に変換します。  
  
     [!code-csharp[VSSDKOutlineRegionTest#10](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#10)]
     [!code-vb[VSSDKOutlineRegionTest#10](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#10)]  
  
12. 次のコードは、例示のみを目的としています。 これは、アウトライン領域の開始の行番号とオフセット、および親領域への参照 (存在する場合) を含む PartialRegion クラスを定義します。 これにより、パーサーは入れ子になったアウトライン領域を設定できます。 派生領域クラスには、アウトライン領域の終了位置の行番号への参照が含まれています。  
  
     [!code-csharp[VSSDKOutlineRegionTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#11)]
     [!code-vb[VSSDKOutlineRegionTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#11)]  
  
## <a name="implementing-a-tagger-provider"></a>Tagger プロバイダーの実装  
 タガーのタガープロバイダーをエクスポートする必要があります。 タガープロバイダーは、 `OutliningTagger` "text" コンテンツタイプのバッファー用のを作成します。それ以外の場合は、バッファーに既に存在する場合はを返し `OutliningTagger` ます。  
  
#### <a name="to-implement-a-tagger-provider"></a>タガープロバイダーを実装するには  
  
1. を実装するという名前のクラスを作成 `OutliningTaggerProvider` <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider> し、ContentType 属性と tagtype 属性を使用してエクスポートします。  
  
     [!code-csharp[VSSDKOutlineRegionTest#12](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#12)]
     [!code-vb[VSSDKOutlineRegionTest#12](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#12)]  
  
2. <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider.CreateTagger%2A>バッファーのプロパティにを追加して、メソッドを実装し `OutliningTagger` ます。  
  
     [!code-csharp[VSSDKOutlineRegionTest#13](../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs#13)]
     [!code-vb[VSSDKOutlineRegionTest#13](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb#13)]  
  
## <a name="building-and-testing-the-code"></a>コードのビルドとテスト  
 このコードをテストするには、OutlineRegionTest ソリューションをビルドし、実験用インスタンスで実行します。  
  
#### <a name="to-build-and-test-the-outlineregiontest-solution"></a>OutlineRegionTest ソリューションをビルドしてテストするには  
  
1. ソリューションをビルドします。  
  
2. デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 つ目のインスタンスがインスタンス化されます。  
  
3. テキスト ファイルを作成します。 左中かっこと右中かっこの両方を含むテキストを入力します。  
  
    ```  
    [  
       Hello  
    ]  
    ```  
  
4. 両方の中かっこを含むアウトライン領域が存在する必要があります。 左中かっこの左側にあるマイナス記号をクリックすると、アウトライン領域を折りたたむことができます。 領域が折りたたまれている場合は、折りたたまれた領域の左側に省略記号 (...) が表示され、ポインターを省略記号の上に移動すると、テキストの **ホバーテキスト** を含むポップアップが表示されます。  
  
## <a name="see-also"></a>参照  
 [チュートリアル: コンテンツの種類とファイル名拡張子とをリンクさせる](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)

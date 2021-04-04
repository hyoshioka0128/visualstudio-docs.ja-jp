---
title: 'チュートリアル: アウトライン |Microsoft Docs'
description: 言語サービスのコンテキストで、または独自のファイル名の拡張子とコンテンツタイプを使用して、アウトライン領域を定義および表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - outlining
ms.assetid: d75a44aa-265a-44d4-9c28-457f59c4ff9f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- csharp
- vb
ms.openlocfilehash: 7bf4c0cc8757ea4f034da2ac17d6c76971f86305
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217230"
---
# <a name="walkthrough-outlining"></a>チュートリアル: アウトライン
展開または折りたたむテキスト領域の種類を定義することで、アウトラインなどの言語ベースの機能を設定します。 言語サービスのコンテキストでリージョンを定義することも、独自のファイル名の拡張子とコンテンツの種類を定義して、その型にのみ領域の定義を適用することもできます。また、既存のコンテンツの種類 ("text" など) に領域の定義を適用することもできます。 このチュートリアルでは、アウトライン領域を定義および表示する方法について説明します。

## <a name="prerequisites"></a>前提条件
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-managed-extensibility-framework-mef-project"></a>Managed Extensibility Framework (MEF) プロジェクトを作成する

### <a name="to-create-a-mef-project"></a>MEF プロジェクトを作成するには

1. VSIX プロジェクトを作成する。 ソリューション `OutlineRegionTest`の名前を指定します。

2. エディター分類子項目テンプレートをプロジェクトに追加します。 詳細については、「 [エディター項目テンプレートを使用して拡張機能を作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)する」を参照してください。

3. 既存のクラス ファイルを削除します。

## <a name="implement-an-outlining-tagger"></a>アウトラインタグを実装する
 アウトライン領域は、一種のタグ () でマークされ <xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag> ます。 このタグは、標準のアウトライン動作を提供します。 アウトラインされた領域は、展開または折りたたむことができます。 アウトライン表示された領域は、折りたたまれている場合はプラス記号 () でマークされ **+** ます。展開されている場合はマイナス記号 () が付いて **-** おり、展開された領域は垂直線で demarcated ます。

 次の手順は、角かっこ (**[**,**]**) で区切られたすべての領域のアウトライン領域を作成するタガー定義する方法を示しています。

### <a name="to-implement-an-outlining-tagger"></a>アウトラインタグを実装するには

1. クラス ファイルを追加し、その名前を `OutliningTagger`にします。

2. 次の名前空間をインポートします。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet1":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet1":::

3. という名前のクラスを作成 `OutliningTagger` し、を実装し <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet2":::

4. テキストバッファーとスナップショットを追跡し、アウトライン領域としてタグ付けする必要がある行のセットを累積するために、いくつかのフィールドを追加します。 このコードには、アウトライン領域を表す領域オブジェクト (後で定義する) の一覧が含まれています。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet3":::

5. フィールドを初期化し、バッファーを解析し、イベントにイベントハンドラーを追加するタガーコンストラクターを追加し <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet4":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet4":::

6. <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A>タグ範囲をインスタンス化するメソッドを実装します。 この例では、メソッドに渡されたの範囲が連続していることを前提としていますが、常にそうであるとは <xref:Microsoft.VisualStudio.Text.NormalizedSpanCollection> 限りません。 このメソッドは、アウトライン領域ごとに新しいタグスパンをインスタンス化します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet5":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet5":::

7. `TagsChanged`イベントハンドラーを宣言します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet6":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet6":::

8. `BufferChanged`テキストバッファーを解析することによって、イベントに応答するイベントハンドラーを追加 <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet7":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet7":::

9. バッファーを解析するメソッドを追加します。 ここで示す例は、例示のみを目的としています。 バッファーは、入れ子になったアウトライン領域に同期的に解析されます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet8":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet8":::

10. 次のヘルパーメソッドは、アウトラインのレベルを表す整数を取得します。1は、最も左の中かっこのペアです。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet9":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet9":::

11. 次のヘルパーメソッドは、(この記事で後述するように定義されている) 領域を SnapshotSpan に変換します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet10":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet10":::

12. 次のコードは、例示のみを目的としています。 これは、アウトライン領域の開始の行番号とオフセット、および親領域への参照 (存在する場合) を含む PartialRegion クラスを定義します。 このコードにより、パーサーは入れ子になったアウトライン領域を設定できます。 派生領域クラスには、アウトライン領域の終了位置の行番号への参照が含まれています。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet11":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet11":::

## <a name="implement-a-tagger-provider"></a>タガープロバイダーを実装する
 タガーのプロバイダーをエクスポートします。 タガープロバイダーは、 `OutliningTagger` "text" コンテンツタイプのバッファー用のを作成します。それ以外の場合は、バッファーに既に存在する場合はを返し `OutliningTagger` ます。

### <a name="to-implement-a-tagger-provider"></a>タガープロバイダーを実装するには

1. を実装するという名前のクラスを作成 `OutliningTaggerProvider` <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider> し、ContentType 属性と tagtype 属性を使用してエクスポートします。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet12":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet12":::

2. <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider.CreateTagger%2A>バッファーのプロパティにを追加して、メソッドを実装し `OutliningTagger` ます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkoutlineregiontest/cs/outliningtagger.cs" id="Snippet13":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkoutlineregiontest/vb/outliningtagger.vb" id="Snippet13":::

## <a name="build-and-test-the-code"></a>コードをビルドしてテストする
 このコードをテストするには、OutlineRegionTest ソリューションをビルドし、実験用インスタンスで実行します。

### <a name="to-build-and-test-the-outlineregiontest-solution"></a>OutlineRegionTest ソリューションをビルドしてテストするには

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の2番目のインスタンスが開始されます。

3. テキスト ファイルを作成します。 左角かっこと右角かっこの両方を含むテキストを入力します。

    ```
    [
       Hello
    ]
    ```

4. 両方の角かっこを含むアウトライン領域が存在する必要があります。 開いている角かっこの左側にあるマイナス記号をクリックすると、アウトライン領域を折りたたむことができます。 領域が折りたたまれている場合は、折りたたまれた領域の左側に省略記号 (*...*) が表示され、ポインターを省略記号の上に移動すると、テキストの **ホバーテキスト** を含むポップアップが表示されます。

## <a name="see-also"></a>関連項目
- [チュートリアル: コンテンツの種類をファイル名拡張子にリンクする](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)

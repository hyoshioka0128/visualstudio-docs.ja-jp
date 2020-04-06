---
title: 'チュートリアル: アウトライン |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - outlining
ms.assetid: d75a44aa-265a-44d4-9c28-457f59c4ff9f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 97b9dcbb2a24f1a3ed336a4a6bb7de4a15e907b4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697212"
---
# <a name="walkthrough-outlining"></a>チュートリアル: アウトライン
展開または折りたたみを行うテキスト領域の種類を定義して、アウトラインなどの言語ベースの機能を設定します。 言語サービスのコンテキストで領域を定義するか、独自のファイル名拡張子とコンテンツ タイプを定義し、その種類にのみ領域定義を適用するか、領域定義を既存のコンテンツ タイプ ("text"など) に適用できます。 このチュートリアルでは、アウトライン領域を定義して表示する方法を示します。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-managed-extensibility-framework-mef-project"></a>マネージ機能拡張フレームワーク (MEF) プロジェクトを作成する

### <a name="to-create-a-mef-project"></a>MEF プロジェクトを作成するには

1. VSIX プロジェクトを作成する。 ソリューション `OutlineRegionTest`の名前を指定します。

2. エディター分類子項目テンプレートをプロジェクトに追加します。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

3. 既存のクラス ファイルを削除します。

## <a name="implement-an-outlining-tagger"></a>アウトライン タガーを実装する
 アウトライン領域は、一種のタグ ( )<xref:Microsoft.VisualStudio.Text.Tagging.OutliningRegionTag>でマークされます。 このタグは、標準的なアウトライン動作を提供します。 アウトライン領域は、展開または折りたたむことができます。 輪郭を描いた領域は、折りたた**+** まれている場合はプラス記号 ( ) でマーク**-** され、展開された領域が縦線で区切られた場合はマイナス記号 ( ) で囲まれます。

 次の手順では、括弧 (**[**]**)** で区切られたすべての領域のアウトライン領域を作成するタガーを定義する方法を示します。

### <a name="to-implement-an-outlining-tagger"></a>アウトライン タガーを実装するには

1. クラス ファイルを追加し、その名前を `OutliningTagger`にします。

2. 次の名前空間をインポートします。

     [!code-csharp[VSSDKOutlineRegionTest#1](../extensibility/codesnippet/CSharp/walkthrough-outlining_1.cs)]
     [!code-vb[VSSDKOutlineRegionTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_1.vb)]

3. という名前`OutliningTagger`のクラスを作成し、<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601>を実装します。

     [!code-csharp[VSSDKOutlineRegionTest#2](../extensibility/codesnippet/CSharp/walkthrough-outlining_2.cs)]
     [!code-vb[VSSDKOutlineRegionTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_2.vb)]

4. テキスト バッファーとスナップショットを追跡し、アウトライン領域としてタグ付けする行のセットを蓄積するフィールドをいくつか追加します。 このコードには、アウトライン領域を表す Region オブジェクト (後で定義する) の一覧が含まれています。

     [!code-csharp[VSSDKOutlineRegionTest#3](../extensibility/codesnippet/CSharp/walkthrough-outlining_3.cs)]
     [!code-vb[VSSDKOutlineRegionTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_3.vb)]

5. フィールドを初期化し、バッファーを解析し、イベントハンドラーをイベントに追加するタガー コンストラクターを追加<xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed>します。

     [!code-csharp[VSSDKOutlineRegionTest#4](../extensibility/codesnippet/CSharp/walkthrough-outlining_4.cs)]
     [!code-vb[VSSDKOutlineRegionTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_4.vb)]

6. タグ範囲<xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A>をインスタンス化するメソッドを実装します。 この例では、メソッドに渡された<xref:Microsoft.VisualStudio.Text.NormalizedSpanCollection>範囲が連続していると仮定していますが、必ずしも当てはまるとは限りません。 このメソッドは、アウトライン領域ごとに新しいタグ範囲をインスタンス化します。

     [!code-csharp[VSSDKOutlineRegionTest#5](../extensibility/codesnippet/CSharp/walkthrough-outlining_5.cs)]
     [!code-vb[VSSDKOutlineRegionTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_5.vb)]

7. イベント`TagsChanged`ハンドラーを宣言します。

     [!code-csharp[VSSDKOutlineRegionTest#6](../extensibility/codesnippet/CSharp/walkthrough-outlining_6.cs)]
     [!code-vb[VSSDKOutlineRegionTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_6.vb)]

8. テキスト`BufferChanged`バッファーを解析することによってイベントに<xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed>応答するイベント ハンドラーを追加します。

     [!code-csharp[VSSDKOutlineRegionTest#7](../extensibility/codesnippet/CSharp/walkthrough-outlining_7.cs)]
     [!code-vb[VSSDKOutlineRegionTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_7.vb)]

9. バッファーを解析するメソッドを追加します。 ここで示す例は、説明のためだけにあります。 バッファーを同期的に解析して、入れ子になったアウトライン領域にします。

     [!code-csharp[VSSDKOutlineRegionTest#8](../extensibility/codesnippet/CSharp/walkthrough-outlining_8.cs)]
     [!code-vb[VSSDKOutlineRegionTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_8.vb)]

10. 次のヘルパー メソッドは、アウトラインのレベルを表す整数を取得し、1 が一番左のかっこのペアになります。

     [!code-csharp[VSSDKOutlineRegionTest#9](../extensibility/codesnippet/CSharp/walkthrough-outlining_9.cs)]
     [!code-vb[VSSDKOutlineRegionTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_9.vb)]

11. 次のヘルパー メソッドは、リージョン (この記事の後半で定義) を SnapshotSpan に変換します。

     [!code-csharp[VSSDKOutlineRegionTest#10](../extensibility/codesnippet/CSharp/walkthrough-outlining_10.cs)]
     [!code-vb[VSSDKOutlineRegionTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_10.vb)]

12. 次のコードは、説明のためだけに使用できます。 アウトライン領域の開始位置の行番号とオフセット、および親領域への参照 (存在する場合) を含む PartialRegion クラスを定義します。 このコードにより、パーサーは入れ子になったアウトライン領域を設定できます。 派生領域クラスには、アウトライン領域の終了の行番号への参照が含まれています。

     [!code-csharp[VSSDKOutlineRegionTest#11](../extensibility/codesnippet/CSharp/walkthrough-outlining_11.cs)]
     [!code-vb[VSSDKOutlineRegionTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_11.vb)]

## <a name="implement-a-tagger-provider"></a>タガー プロバイダーの実装
 タガーのタガープロバイダをエクスポートします。 タガー プロバイダーは、"text" コンテンツ タイプのバッファー`OutliningTagger`用を作成します。 `OutliningTagger`

### <a name="to-implement-a-tagger-provider"></a>タガー プロバイダーを実装するには

1. を実装するという`OutliningTaggerProvider`名前のクラス<xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider>を作成し、コンテンツ タイプ属性と TagType 属性を使用してエクスポートします。

     [!code-csharp[VSSDKOutlineRegionTest#12](../extensibility/codesnippet/CSharp/walkthrough-outlining_12.cs)]
     [!code-vb[VSSDKOutlineRegionTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_12.vb)]

2. バッファーの<xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider.CreateTagger%2A>プロパティに を`OutliningTagger`追加してメソッドを実装します。

     [!code-csharp[VSSDKOutlineRegionTest#13](../extensibility/codesnippet/CSharp/walkthrough-outlining_13.cs)]
     [!code-vb[VSSDKOutlineRegionTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-outlining_13.vb)]

## <a name="build-and-test-the-code"></a>コードのビルドとテスト
 このコードをテストするには、OutlineRegionTest ソリューションをビルドし、実験用インスタンスで実行します。

### <a name="to-build-and-test-the-outlineregiontest-solution"></a>アウトライン領域テスト ソリューションをビルドしてテストするには

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 番目のインスタンスが起動します。

3. テキスト ファイルを作成します。 角かっこと右かっこの両方を含むテキストを入力します。

    ```
    [
       Hello
    ]
    ```

4. 両方のブラケットを含むアウトライン領域が存在する必要があります。 アウトライン領域を折りたたむには、左括弧の左側にあるマイナス記号をクリックできます。 領域が折りたたまれると、省略記号 *(.)* が折りたたまれた領域の左側に表示され、テキスト**のホバー テキスト**を含むポップアップが、省略記号の上にポインタを移動したときに表示されます。

## <a name="see-also"></a>関連項目
- [チュートリアル: コンテンツ タイプをファイル名拡張子にリンクする](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)

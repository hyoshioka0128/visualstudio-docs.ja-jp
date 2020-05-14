---
title: 'チュートリアル: クイックヒントツールチップの表示 |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - QuickInfo
ms.assetid: 23fb8384-4f12-446f-977f-ce7910347947
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- csharp
- vb
ms.openlocfilehash: 47a14ca0692ad0338b56fd1d372307fb0e2ccc4c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697438"
---
# <a name="walkthrough-display-quickinfo-tooltips"></a>チュートリアル: クイック ヒントヒントを表示する
クイック ヒントは、ユーザーがポインターをメソッド名の上に移動したときにメソッドのシグネチャと説明を表示する IntelliSense 機能です。 クイック ヒントなどの言語ベースの機能を実装するには、クイック ヒントの説明を提供する識別子を定義し、コンテンツを表示するためのツールヒントを作成します。 言語サービスのコンテキストでクイック ヒントを定義するか、独自のファイル名拡張子とコンテンツ タイプを定義して、その種類のクイック ヒントを表示するか、または既存のコンテンツ タイプ ("text" など) のクイック ヒントを表示することができます。 このチュートリアルでは、"テキスト" コンテンツ タイプのクイック ヒントを表示する方法を示します。

 このチュートリアルの QuickInfo の例では、ユーザーがポインターをメソッド名の上に移動したときにツールヒントを表示します。 この設計では、次の 4 つのインターフェイスを実装する必要があります。

- ソース インターフェイス

- ソース プロバイダー インターフェイス

- コントローラ インターフェイス

- コントローラ プロバイダ インターフェイス

  ソース プロバイダーとコントローラー プロバイダーはマネージ機能拡張フレームワーク (MEF) コンポーネントの一部であり、ソースとコント ローラークラスをエクスポートし、ツールヒントテキスト バッファー<xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService>を作成する、および<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker>などのサービスとブローカーをインポートする役割を果たすクイック ヒント セッションをトリガーします。

  この例では、QuickInfo ソースはメソッド名と説明のハードコーディングされたリストを使用しますが、完全な実装では、言語サービスと言語ドキュメントがそのコンテンツを提供する役割を担います。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールする必要はありません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-mef-project"></a>MEF プロジェクトを作成する

### <a name="to-create-a-mef-project"></a>MEF プロジェクトを作成するには

1. C# VSIX プロジェクトを作成します。 ([**新しいプロジェクト**] ダイアログで、[**ビジュアル C# / 拡張性**] を選択し、次に**VSIX プロジェクト**を選択します)。ソリューションに名前`QuickInfoTest`を付ける:

2. エディター分類子項目テンプレートをプロジェクトに追加します。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

3. 既存のクラス ファイルを削除します。

## <a name="implement-the-quickinfo-source"></a>クイック ヒント ソースの実装
 QuickInfo ソースは、識別子のセットとその説明を収集し、識別子のいずれかが検出されたときにツールヒント テキスト バッファーにコンテンツを追加します。 この例では、識別子とその説明がソース コンストラクターに追加されただけです。

#### <a name="to-implement-the-quickinfo-source"></a>クイック ヒント ソースを実装するには

1. クラス ファイルを追加し、その名前を `TestQuickInfoSource`にします。

2. *への参照*を追加します。

3. 次のインポートを追加します。

     [!code-vb[VSSDKQuickInfoTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_1.vb)]
     [!code-csharp[VSSDKQuickInfoTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_1.cs)]

4. を実装するクラスを<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource>宣言し、 という`TestQuickInfoSource`名前を付けます。

     [!code-vb[VSSDKQuickInfoTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_2.vb)]
     [!code-csharp[VSSDKQuickInfoTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_2.cs)]

5. QuickInfo ソース プロバイダー、テキスト バッファー、およびメソッド名とメソッド シグネチャのセットのフィールドを追加します。 この例では、メソッド名とシグネチャが`TestQuickInfoSource`コンストラクターで初期化されます。

     [!code-vb[VSSDKQuickInfoTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_3.vb)]
     [!code-csharp[VSSDKQuickInfoTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_3.cs)]

6. QuickInfo ソース プロバイダーとテキスト バッファーを設定し、メソッド名のセット、およびメソッドのシグネチャと説明を設定するコンストラクターを追加します。

     [!code-vb[VSSDKQuickInfoTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_4.vb)]
     [!code-csharp[VSSDKQuickInfoTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_4.cs)]

7. <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource.AugmentQuickInfoSession%2A> メソッドを実装します。 この例では、カーソルが行またはテキスト バッファーの末尾にある場合は、現在の単語、または前の単語を検索します。 単語がメソッド名の 1 つである場合、そのメソッド名の説明が QuickInfo コンテンツに追加されます。

     [!code-vb[VSSDKQuickInfoTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_5.vb)]
     [!code-csharp[VSSDKQuickInfoTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_5.cs)]

8. また、次のメソッドを実装しているため<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource>、Dispose()<xref:System.IDisposable>メソッドも実装する必要があります。

     [!code-vb[VSSDKQuickInfoTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_6.vb)]
     [!code-csharp[VSSDKQuickInfoTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_6.cs)]

## <a name="implement-a-quickinfo-source-provider"></a>クイック ヒント ソース プロバイダーを実装する
 クイック ヒント ソースのプロバイダーは、主に MEF コンポーネント パーツとして自身をエクスポートし、クイック ヒント ソースをインスタンス化する役割を果たします。 MEF コンポーネントパーツなので、他の MEF コンポーネントパーツをインポートできます。

#### <a name="to-implement-a-quickinfo-source-provider"></a>クイック ヒント ソース プロバイダーを実装するには

1. <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider>を実装するという名前<xref:Microsoft.VisualStudio.Utilities.NameAttribute>の<xref:Microsoft.VisualStudio.Utilities.OrderAttribute><xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>`TestQuickInfoSourceProvider`QuickInfo ソース プロバイダを宣言し、"ツールヒント クイックヒント ソース" の "Before="default" と "text" の名前を指定してエクスポートします。

     [!code-vb[VSSDKQuickInfoTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_7.vb)]
     [!code-csharp[VSSDKQuickInfoTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_7.cs)]

2. のプロパティとして 2 <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> <xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService>つのエディター サービス`TestQuickInfoSourceProvider`と をインポートします。

     [!code-vb[VSSDKQuickInfoTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_8.vb)]
     [!code-csharp[VSSDKQuickInfoTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_8.cs)]

3. 新<xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider.TryCreateQuickInfoSource%2A>しい`TestQuickInfoSource`を返すを実装します。

     [!code-vb[VSSDKQuickInfoTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_9.vb)]
     [!code-csharp[VSSDKQuickInfoTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_9.cs)]

## <a name="implement-a-quickinfo-controller"></a>クイック ヒント コントローラーを実装する
 クイック ヒント コントローラは、クイック ヒントが表示されるタイミングを決定します。 この例では、メソッド名のいずれかに対応する単語の上にポインタが置かれたときに、クイック ヒントが表示されます。 クイック ヒント コントローラーは、クイック ヒント セッションをトリガーするマウス ホバー イベント ハンドラーを実装します。

### <a name="to-implement-a-quickinfo-controller"></a>クイック ヒント コントローラーを実装するには

1. を実装するクラスを<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController>宣言し、 という`TestQuickInfoController`名前を付けます。

     [!code-vb[VSSDKQuickInfoTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_10.vb)]
     [!code-csharp[VSSDKQuickInfoTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_10.cs)]

2. テキスト ビューのプライベート フィールド、テキスト ビューで表されるテキスト バッファー、クイック ヒント セッション、およびクイック ヒント コントローラー プロバイダーを追加します。

     [!code-vb[VSSDKQuickInfoTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_11.vb)]
     [!code-csharp[VSSDKQuickInfoTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_11.cs)]

3. フィールドを設定し、マウス ホバー イベント ハンドラーを追加するコンストラクターを追加します。

     [!code-vb[VSSDKQuickInfoTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_12.vb)]
     [!code-csharp[VSSDKQuickInfoTest#12](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_12.cs)]

4. クイック ヒント セッションをトリガーするマウス ホバー イベント ハンドラーを追加します。

     [!code-vb[VSSDKQuickInfoTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_13.vb)]
     [!code-csharp[VSSDKQuickInfoTest#13](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_13.cs)]

5. コントローラーが<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.Detach%2A>テキスト ビューからデタッチされたときにマウス ホバー イベント ハンドラーを削除するようにメソッドを実装します。

     [!code-vb[VSSDKQuickInfoTest#14](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_14.vb)]
     [!code-csharp[VSSDKQuickInfoTest#14](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_14.cs)]

6. この例<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.ConnectSubjectBuffer%2A>では、メソッド<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.DisconnectSubjectBuffer%2A>とメソッドを空のメソッドとして実装します。

     [!code-vb[VSSDKQuickInfoTest#15](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_15.vb)]
     [!code-csharp[VSSDKQuickInfoTest#15](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_15.cs)]

## <a name="implementing-the-quickinfo-controller-provider"></a>クイック ヒント コントローラー プロバイダーの実装
 クイック ヒント コント ローラーのプロバイダーは、主に MEF コンポーネントの部分として自身をエクスポートし、クイック ヒント コント ローラーをインスタンス化する機能します。 MEF コンポーネントパーツなので、他の MEF コンポーネントパーツをインポートできます。

### <a name="to-implement-the-quickinfo-controller-provider"></a>クイック ヒント コントローラー プロバイダーを実装するには

1. を実装するという`TestQuickInfoControllerProvider`名前のクラス<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseControllerProvider>を宣言し、それを<xref:Microsoft.VisualStudio.Utilities.NameAttribute>"ツールヒント クイックヒント コントローラー"<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>と "text" の名前でエクスポートします。

     [!code-vb[VSSDKQuickInfoTest#16](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_16.vb)]
     [!code-csharp[VSSDKQuickInfoTest#16](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_16.cs)]

2. <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker> をプロパティとしてインポートします。

     [!code-vb[VSSDKQuickInfoTest#17](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_17.vb)]
     [!code-csharp[VSSDKQuickInfoTest#17](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_17.cs)]

3. クイック<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseControllerProvider.TryCreateIntellisenseController%2A>ヒント コントローラーをインスタンス化してメソッドを実装します。

     [!code-vb[VSSDKQuickInfoTest#18](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-quickinfo-tooltips_18.vb)]
     [!code-csharp[VSSDKQuickInfoTest#18](../extensibility/codesnippet/CSharp/walkthrough-displaying-quickinfo-tooltips_18.cs)]

## <a name="build-and-test-the-code"></a>コードのビルドとテスト
 このコードをテストするには、QuickInfoTest ソリューションをビルドし、実験用インスタンスで実行します。

### <a name="to-build-and-test-the-quickinfotest-solution"></a>クイックヒント ソリューションをビルドしてテストするには

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 番目のインスタンスが起動します。

3. テキスト ファイルを作成し、"add" と "subtract" という単語を含むテキストを入力します。

4. 「追加」の出現箇所の上にポインタを移動します。 メソッドのシグネチャと説明が`add`表示されます。

## <a name="see-also"></a>関連項目
- [チュートリアル: コンテンツ タイプをファイル名拡張子にリンクする](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)

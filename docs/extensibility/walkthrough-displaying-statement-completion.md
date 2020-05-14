---
title: 'チュートリアル: ステートメント補完の表示 |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - statement completion
ms.assetid: f3152c4e-7673-4047-a079-2326941d1c83
author: acangialosi
ms.author: anthc
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- vssdk
ms.openlocfilehash: 1d2f5499511c9dc0bbb6711d0da630315384f8e7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697415"
---
# <a name="walkthrough-display-statement-completion"></a>チュートリアル: 入力候補の表示
言語ベースのステートメント入力候補を実装するには、完了を提供する識別子を定義し、完了セッションをトリガーします。 言語サービスのコンテキストでステートメント入力候補を定義し、独自のファイル名拡張子とコンテンツ タイプを定義し、その種類の完了のみを表示できます。 または、既存のコンテンツ タイプ ("プレーンテキスト" など) の完了をトリガーできます。 このチュートリアルでは、テキスト ファイルのコンテンツ タイプである "プレーンテキスト" コンテンツ タイプのステートメント補完をトリガーする方法を示します。 "text" コンテンツ タイプは、コードファイルや XML ファイルを含む、その他すべてのコンテンツ タイプの祖先です。

 通常、ステートメント入力候補は、たとえば"using" などの識別子の先頭を入力して特定の文字を入力することによってトリガーされます。 通常、**スペースバー**、**タブ**、または**Enter**キーを押して選択を確定すると、このオプションは消去されます。 キーストローク (<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>インターフェイス) のコマンド ハンドラーと、インターフェイスを実装するハンドラー プロバイダーを使用して、文字を入力するときにトリガーする IntelliSense<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>機能を実装できます。 完了に関与する識別子のリストである完了ソースを作成するには、<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>インターフェイスと完了ソース プロバイダー (インターフェイス) を<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider>実装します。 プロバイダーは、マネージ機能拡張フレームワーク (MEF) コンポーネントの部分です。 ソースクラスとコントローラクラスのエクスポート、サービスとブローカー<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService><xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>のインポートを担当します。

 このチュートリアルでは、ハードコーディングされた識別子のセットに対してステートメント補完を実装する方法を示します。 完全な実装では、言語サービスと言語ドキュメントがそのコンテンツを提供する責任があります。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-mef-project"></a>MEF プロジェクトの作成

#### <a name="to-create-a-mef-project"></a>MEF プロジェクトを作成するには

1. C# VSIX プロジェクトを作成します。 ([**新しいプロジェクト**] ダイアログで、[**ビジュアル C# / 拡張性**] を選択し、次に**VSIX プロジェクト**を選択します)。ソリューションに名前`CompletionTest`を付ける:

2. エディター分類子項目テンプレートをプロジェクトに追加します。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

3. 既存のクラス ファイルを削除します。

4. プロジェクトに次の参照を追加し **、CopyLocal**が に`false`設定されていることを確認します。

     エディター

     Microsoft.VisualStudio.Language.Intellisense

     Microsoft.VisualStudio.OLE.Interop

     シェル.15.0

     をクリックします。

     相互運用機能

## <a name="implement-the-completion-source"></a>完了ソースの実装
 完了ソースは、識別子の最初の文字など、ユーザーが完了トリガーを入力したときに、識別子のセットを収集し、完了ウィンドウにコンテンツを追加します。 この例では、<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A>識別子とその説明がメソッド内でハードコーディングされています。 ほとんどの実際の使用では、入力候補リストを設定するトークンを取得するのに、言語のパーサーを使用します。

### <a name="to-implement-the-completion-source"></a>完了ソースを実装するには

1. クラス ファイルを追加し、その名前を `TestCompletionSource`にします。

2. 次のインポートを追加します。

     [!code-csharp[VSSDKCompletionTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_1.cs)]
     [!code-vb[VSSDKCompletionTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_1.vb)]

3. クラス宣言を変更`TestCompletionSource`して、 を実装します<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>。

     [!code-csharp[VSSDKCompletionTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_2.cs)]
     [!code-vb[VSSDKCompletionTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_2.vb)]

4. ソース プロバイダー、テキスト バッファー、およびオブジェクトのリスト (完了セッション<xref:Microsoft.VisualStudio.Language.Intellisense.Completion>に参加する識別子に対応する) のプライベート フィールドを追加します。

     [!code-csharp[VSSDKCompletionTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_3.cs)]
     [!code-vb[VSSDKCompletionTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_3.vb)]

5. ソース プロバイダーとバッファーを設定するコンストラクターを追加します。 この`TestCompletionSourceProvider`クラスは、後の手順で定義されます。

     [!code-csharp[VSSDKCompletionTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_4.cs)]
     [!code-vb[VSSDKCompletionTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_4.vb)]

6. コンテキストで<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A>指定する完了を含む完了セットを追加して、メソッドを実装します。 各完了セットには、完了の<xref:Microsoft.VisualStudio.Language.Intellisense.Completion>セットが含まれ、完了ウィンドウのタブに対応します。 Visual Basic プロジェクトでは、完了ウィンドウのタブは **[共通]** と [**すべて]** と呼ばれます。メソッド`FindTokenSpanAtPosition`は次の手順で定義します。

     [!code-csharp[VSSDKCompletionTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_5.cs)]
     [!code-vb[VSSDKCompletionTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_5.vb)]

7. カーソル位置から現在の単語を検索するには、次のメソッドを使用します。

     [!code-csharp[VSSDKCompletionTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_6.cs)]
     [!code-vb[VSSDKCompletionTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_6.vb)]

8. メソッドを`Dispose()`実装します。

     [!code-csharp[VSSDKCompletionTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_7.cs)]
     [!code-vb[VSSDKCompletionTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_7.vb)]

## <a name="implement-the-completion-source-provider"></a>完了ソース プロバイダーを実装する
 完了ソース プロバイダーは、完了ソースをインスタンス化する MEF コンポーネント部分です。

### <a name="to-implement-the-completion-source-provider"></a>完了ソース プロバイダーを実装するには

1. を実装するという`TestCompletionSourceProvider`名前のクラス<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider>を追加します。 このクラスを<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>「プレーンテキスト」と「テスト完了」<xref:Microsoft.VisualStudio.Utilities.NameAttribute>のクラスをエクスポートします。

     [!code-csharp[VSSDKCompletionTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_8.cs)]
     [!code-vb[VSSDKCompletionTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_8.vb)]

2. のインポート<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>: 完了ソース内の現在の単語を検索します。

     [!code-csharp[VSSDKCompletionTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_9.cs)]
     [!code-vb[VSSDKCompletionTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_9.vb)]

3. 完了ソース<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider.TryCreateCompletionSource%2A>をインスタンス化するメソッドを実装します。

     [!code-csharp[VSSDKCompletionTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_10.cs)]
     [!code-vb[VSSDKCompletionTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_10.vb)]

## <a name="implement-the-completion-command-handler-provider"></a>完了コマンド ハンドラー プロバイダーを実装します。
 完了コマンド ハンドラー プロバイダーは<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>、 から派生し、テキスト ビューの作成イベントをリッスンし、Visual <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>Studio シェルのコマンド チェーンにコマンドを追加できるビューから に変換<xref:Microsoft.VisualStudio.Text.Editor.ITextView>します。 このクラスは MEF エクスポートであるため、コマンド ハンドラー自体が必要とするサービスをインポートするために使用することもできます。

#### <a name="to-implement-the-completion-command-handler-provider"></a>完了コマンド ハンドラー プロバイダーを実装するには

1. という名前`TestCompletionCommandHandler`のファイルを追加します。

2. 次の using ディレクティブを追加します。

     [!code-csharp[VSSDKCompletionTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_11.cs)]
     [!code-vb[VSSDKCompletionTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_11.vb)]

3. を実装するという`TestCompletionHandlerProvider`名前のクラス<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>を追加します。 <xref:Microsoft.VisualStudio.Utilities.NameAttribute>このクラスを"トークン完了ハンドラ"、<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>プレーンテキストの、および のを使用して<xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>エクスポート<xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Editable>します。

     [!code-csharp[VSSDKCompletionTest#12](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_12.cs)]
     [!code-vb[VSSDKCompletionTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_12.vb)]

4. <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>をインポートすると、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>から<xref:Microsoft.VisualStudio.Text.Editor.ITextView>、 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>、および 標準の<xref:Microsoft.VisualStudio.Shell.SVsServiceProvider>Visual Studio サービスへのアクセスを可能にする 、 への変換が可能になります。

     [!code-csharp[VSSDKCompletionTest#13](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_13.cs)]
     [!code-vb[VSSDKCompletionTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_13.vb)]

5. コマンド<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A>ハンドラーをインスタンス化するメソッドを実装します。

     [!code-csharp[VSSDKCompletionTest#14](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_14.cs)]
     [!code-vb[VSSDKCompletionTest#14](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_14.vb)]

## <a name="implement-the-completion-command-handler"></a>完了コマンド ハンドラーを実装する
 ステートメント入力候補はキーストロークによってトリガーされるため、完了セッションを<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>トリガー、コミット、および終了するキーストロークを受信および処理するインターフェイスを実装する必要があります。

#### <a name="to-implement-the-completion-command-handler"></a>完了コマンド ハンドラーを実装するには

1. を実装するという`TestCompletionCommandHandler`名前のクラス<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>を追加します。

    [!code-csharp[VSSDKCompletionTest#15](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_15.cs)]
    [!code-vb[VSSDKCompletionTest#15](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_15.vb)]

2. 次のコマンド ハンドラー (コマンドを渡す) のプライベート フィールド、テキスト ビュー、コマンド ハンドラー プロバイダー (さまざまなサービスへのアクセスを可能にする)、および完了セッションを追加します。

    [!code-csharp[VSSDKCompletionTest#16](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_16.cs)]
    [!code-vb[VSSDKCompletionTest#16](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_16.vb)]

3. テキスト ビューとプロバイダー フィールドを設定するコンストラクターを追加し、コマンド チェーンにコマンドを追加します。

    [!code-csharp[VSSDKCompletionTest#17](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_17.cs)]
    [!code-vb[VSSDKCompletionTest#17](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_17.vb)]

4. コマンドを<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>渡してメソッドを実装します。

    [!code-csharp[VSSDKCompletionTest#18](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_18.cs)]
    [!code-vb[VSSDKCompletionTest#18](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_18.vb)]

5. <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> メソッドを実装します。 このメソッドは、キーストロークを受け取るときに、次のいずれかを行う必要があります。

   - 文字をバッファーに書き込み、トリガーまたはフィルターの完了を許可します。 (文字の印刷は、これを行います。

   - 完了をコミットしますが、文字をバッファーに書き込まないようにします。 (空白、**タブ**、および**Enter**は、完了セッションが表示されたときにこれを行います。

   - コマンドを次のハンドラーに渡すことを許可します。 (その他のすべてのコマンド。

     このメソッドは UI を表示<xref:Microsoft.VisualStudio.Shell.VsShellUtilities.IsInAutomationFunction%2A>する可能性があるため、オートメーション コンテキストで呼び出されないように呼び出します。

     [!code-csharp[VSSDKCompletionTest#19](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_19.cs)]
     [!code-vb[VSSDKCompletionTest#19](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_19.vb)]

6. このコードは、完了セッションをトリガーするプライベート メソッドです。

    [!code-csharp[VSSDKCompletionTest#20](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_20.cs)]
    [!code-vb[VSSDKCompletionTest#20](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_20.vb)]

7. 次の例は、イベントのサブスクライブを解除するプライベート<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSession.Dismissed>メソッドです。

    [!code-csharp[VSSDKCompletionTest#21](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_21.cs)]
    [!code-vb[VSSDKCompletionTest#21](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_21.vb)]

## <a name="build-and-test-the-code"></a>コードのビルドとテスト
 このコードをテストするには、CompletionTest ソリューションをビルドし、実験用インスタンスで実行します。

#### <a name="to-build-and-test-the-completiontest-solution"></a>完了テスト ソリューションをビルドしてテストするには

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 番目のインスタンスが起動します。

3. テキスト ファイルを作成し、"add" という単語を含むテキストを入力します。

4. 最初に「a」と「d」と入力すると、「追加」と「適合」を含むリストが表示されます。 [追加] が選択されていることに注意してください。 別の "d" を入力すると、リストには "加算" のみが含まれ、現在選択されている必要があります。 **スペースバー**、**タブ**、または**Enter**キーを押して「追加」をコミットするか、Esc キーなどのキーを押してリストを閉じてください。

## <a name="see-also"></a>関連項目
- [チュートリアル: コンテンツ タイプをファイル名拡張子にリンクする](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)

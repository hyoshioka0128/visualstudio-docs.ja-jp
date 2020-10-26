---
title: 'チュートリアル: ステートメント入力候補の表示 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - statement completion
ms.assetid: f3152c4e-7673-4047-a079-2326941d1c83
caps.latest.revision: 37
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: db4e63beb1e3d4ff53e547492ae9eae7ee8001e8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202005"
---
# <a name="walkthrough-displaying-statement-completion"></a>チュートリアル: 入力候補の表示
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

入力候補を提供する識別子を定義し、完了セッションをトリガーすることによって、言語ベースのステートメント入力候補を実装できます。 言語サービスのコンテキストでステートメント入力候補を定義し、独自のファイル名の拡張子とコンテンツの種類を定義して、その型の入力候補だけを表示するか、既存のコンテンツの種類 ("プレーンテキスト" など) の完了をトリガーすることができます。 このチュートリアルでは、テキストファイルのコンテンツタイプである "プレーンテキスト" コンテンツタイプに対してステートメント入力候補をトリガーする方法について説明します。 "Text" コンテンツタイプは、コードファイルや XML ファイルなど、他のすべてのコンテンツタイプの先祖です。  
  
 通常、ステートメント入力候補は特定の文字を入力することによってトリガーされます。たとえば、"using" などの識別子の先頭を入力します。 通常、Space、Tab、または Enter キーを押すと、選択範囲がコミットされます。 キー入力によってトリガーされる IntelliSense 機能を実装できます。これには、キーストローク (インターフェイス) のコマンドハンドラー <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> と、インターフェイスを実装するハンドラープロバイダーを使用し <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> ます。 完了に参加する識別子の一覧である完了ソースを作成するには、 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource> インターフェイスと完了ソースプロバイダー (インターフェイス) を実装し <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider> ます。 プロバイダーは、Managed Extensibility Framework (MEF) コンポーネントのパートです。 ソースとコントローラーのクラスをエクスポートし、サービスとブローカーをインポートする役割を担い <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> ます。たとえば、テキストバッファー内の移動を可能にするや、 <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker> 完了セッションをトリガーするなどです。  
  
 このチュートリアルでは、ハードコーディングされた識別子のセットに対してステートメント入力候補を実装する方法について説明します。 完全な実装では、言語サービスと言語ドキュメントにそのコンテンツを提供する役割があります。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
## <a name="creating-a-mef-project"></a>MEF プロジェクトの作成  
  
#### <a name="to-create-a-mef-project"></a>MEF プロジェクトを作成するには  
  
1. C# VSIX プロジェクトを作成します。 ([ **新しいプロジェクト** ] ダイアログで、[Visual C#]、[ **拡張機能**]、[ **VSIX プロジェクト**] の順に選択します)。ソリューションにという名前を指定 `CompletionTest` します。  
  
2. エディター分類子項目テンプレートをプロジェクトに追加します。 詳細については、「 [エディター項目テンプレートを使用した拡張機能の作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。  
  
3. 既存のクラス ファイルを削除します。  
  
4. 次の参照をプロジェクトに追加し、 **CopyLocal** がに設定されていることを確認し `false` ます。  
  
     VisualStudio  
  
     Microsoft.VisualStudio.Language.Intellisense  
  
     Microsoft.VisualStudio.OLE.Interop  
  
     VisualStudio. 14.0  
  
     VisualStudio (変更不可)  
  
     VisualStudio。相互運用  
  
## <a name="implementing-the-completion-source"></a>完了ソースの実装  
 入力候補は、識別子の最初の文字などの入力候補のトリガーをユーザーが入力したときに、一連の識別子を収集し、その内容を完了ウィンドウに追加する役割を担います。 この例では、識別子とその説明は、メソッドでハードコーディングされてい <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A> ます。 ほとんどの実際の使用では、言語のパーサーを使用してトークンを取得し、入力候補一覧に入力します。  
  
#### <a name="to-implement-the-completion-source"></a>完了ソースを実装するには  
  
1. クラス ファイルを追加し、その名前を `TestCompletionSource`にします。  
  
2. 次のインポートを追加します。  
  
     [!code-csharp[VSSDKCompletionTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs#1)]
     [!code-vb[VSSDKCompletionTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb#1)]  
  
3. を実装するように、クラス宣言を変更し `TestCompletionSource` <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource> ます。  
  
     [!code-csharp[VSSDKCompletionTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs#2)]
     [!code-vb[VSSDKCompletionTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb#2)]  
  
4. ソースプロバイダー、テキストバッファー、およびオブジェクトの一覧 <xref:Microsoft.VisualStudio.Language.Intellisense.Completion> (完了セッションに参加する識別子に対応する) のプライベートフィールドを追加します。  
  
     [!code-csharp[VSSDKCompletionTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs#3)]
     [!code-vb[VSSDKCompletionTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb#3)]  
  
5. ソースプロバイダーとバッファーを設定するコンストラクターを追加します。 `TestCompletionSourceProvider`クラスは、後の手順で定義します。  
  
     [!code-csharp[VSSDKCompletionTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs#4)]
     [!code-vb[VSSDKCompletionTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb#4)]  
  
6. <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A>コンテキストで指定する入力候補を含む完了セットを追加して、メソッドを実装します。 各入力候補セットには入力候補のセットが含まれて <xref:Microsoft.VisualStudio.Language.Intellisense.Completion> おり、完了ウィンドウのタブに対応しています。 (Visual Basic プロジェクトでは、[完了] ウィンドウのタブの名前は " **共通** " と " **すべて**" になります)。FindTokenSpanAtPosition メソッドは、次の手順で定義します。  
  
     [!code-csharp[VSSDKCompletionTest#5](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs#5)]
     [!code-vb[VSSDKCompletionTest#5](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb#5)]  
  
7. カーソルの位置から現在の単語を検索するには、次のメソッドを使用します。  
  
     [!code-csharp[VSSDKCompletionTest#6](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs#6)]
     [!code-vb[VSSDKCompletionTest#6](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb#6)]  
  
8. メソッドを実装し `Dispose()` ます。  
  
     [!code-csharp[VSSDKCompletionTest#7](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs#7)]
     [!code-vb[VSSDKCompletionTest#7](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb#7)]  
  
## <a name="implementing-the-completion-source-provider"></a>完了ソースプロバイダーの実装  
 完了ソースプロバイダーは、完了ソースをインスタンス化する MEF コンポーネント部分です。  
  
#### <a name="to-implement-the-completion-source-provider"></a>完了ソースプロバイダーを実装するには  
  
1. を実装するという名前のクラスを追加 `TestCompletionSourceProvider` <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider> します。 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>"Plaintext" と "test completion" のを使用して、このクラスをエクスポート <xref:Microsoft.VisualStudio.Utilities.NameAttribute> します。  
  
     [!code-csharp[VSSDKCompletionTest#8](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs#8)]
     [!code-vb[VSSDKCompletionTest#8](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb#8)]  
  
2. をインポートし <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> ます。これは、完了ソース内の現在の単語を検索するために使用されます。  
  
     [!code-csharp[VSSDKCompletionTest#9](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs#9)]
     [!code-vb[VSSDKCompletionTest#9](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb#9)]  
  
3. メソッドを実装して <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider.TryCreateCompletionSource%2A> 、完了ソースをインスタンス化します。  
  
     [!code-csharp[VSSDKCompletionTest#10](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletionsource.cs#10)]
     [!code-vb[VSSDKCompletionTest#10](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletionsource.vb#10)]  
  
## <a name="implementing-the-completion-command-handler-provider"></a>完了コマンドハンドラープロバイダーの実装  
 完了コマンドハンドラープロバイダーは、から派生します。このクラスは、 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> テキストビュー作成イベントをリッスンし、から、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> Visual Studio シェルのコマンドチェーンにコマンドを追加できるように、そのビューをに変換し <xref:Microsoft.VisualStudio.Text.Editor.ITextView> ます。 このクラスは MEF エクスポートであるため、このクラスを使用して、コマンドハンドラー自体が必要とするサービスをインポートすることもできます。  
  
#### <a name="to-implement-the-completion-command-handler-provider"></a>完了コマンドハンドラープロバイダーを実装するには  
  
1. という名前のファイルを追加 `TestCompletionCommandHandler` します。  
  
2. 次の using ステートメントを追加します。  
  
     [!code-csharp[VSSDKCompletionTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#11)]
     [!code-vb[VSSDKCompletionTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#11)]  
  
3. を実装するという名前のクラスを追加 `TestCompletionHandlerProvider` <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> します。 <xref:Microsoft.VisualStudio.Utilities.NameAttribute>"トークンの完了ハンドラー"、 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "プレーンテキスト"、およびのを使用して、このクラスをエクスポートし <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Editable> ます。  
  
     [!code-csharp[VSSDKCompletionTest#12](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#12)]
     [!code-vb[VSSDKCompletionTest#12](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#12)]  
  
4. をインポートします <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> 。これにより、からへの変換 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> と、標準の <xref:Microsoft.VisualStudio.Text.Editor.ITextView> <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker> <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> Visual Studio サービスへのアクセスを可能にするへの変換が可能になります。  
  
     [!code-csharp[VSSDKCompletionTest#13](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#13)]
     [!code-vb[VSSDKCompletionTest#13](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#13)]  
  
5. <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A>コマンドハンドラーをインスタンス化するメソッドを実装します。  
  
     [!code-csharp[VSSDKCompletionTest#14](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#14)]
     [!code-vb[VSSDKCompletionTest#14](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#14)]  
  
## <a name="implementing-the-completion-command-handler"></a>完了コマンドハンドラーの実装  
 ステートメント入力候補はキーストロークによってトリガーされるため、このインターフェイスを実装して、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 完了セッションをトリガー、コミット、および破棄するキーストロークを受信して処理する必要があります。  
  
#### <a name="to-implement-the-completion-command-handler"></a>完了コマンドハンドラーを実装するには  
  
1. を実装するという名前のクラスを追加し `TestCompletionCommandHandler` <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ます。  
  
    [!code-csharp[VSSDKCompletionTest#15](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#15)]
    [!code-vb[VSSDKCompletionTest#15](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#15)]  
  
2. 次のコマンドハンドラー (コマンドの渡し先)、テキストビュー、コマンドハンドラープロバイダー (さまざまなサービスへのアクセスを可能にする)、および完了セッションのプライベートフィールドを追加します。  
  
    [!code-csharp[VSSDKCompletionTest#16](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#16)]
    [!code-vb[VSSDKCompletionTest#16](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#16)]  
  
3. テキストビューとプロバイダーフィールドを設定するコンストラクターを追加し、コマンドチェーンにコマンドを追加します。  
  
    [!code-csharp[VSSDKCompletionTest#17](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#17)]
    [!code-vb[VSSDKCompletionTest#17](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#17)]  
  
4. <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>次のコマンドを渡すことによって、メソッドを実装します。  
  
    [!code-csharp[VSSDKCompletionTest#18](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#18)]
    [!code-vb[VSSDKCompletionTest#18](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#18)]  
  
5. <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> メソッドを実装します。 このメソッドがキーストロークを受け取ると、次のいずれかの操作を行う必要があります。  
  
   - 文字がバッファーに書き込まれることを許可し、その後、完了をトリガーまたはフィルター処理します。 (印刷文字はこれを行います)。  
  
   - 完了をコミットしますが、バッファーへの文字の書き込みは許可しません。 (空白、タブ、Enter キーを押したときに入力します。  
  
   - コマンドを次のハンドラーに渡すことを許可します。 (その他のすべてのコマンド)。  
  
     このメソッドは UI を表示する可能性があるため、を呼び出して、 <xref:Microsoft.VisualStudio.Shell.VsShellUtilities.IsInAutomationFunction%2A> オートメーションコンテキストで呼び出されないようにします。  
  
     [!code-csharp[VSSDKCompletionTest#19](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#19)]
     [!code-vb[VSSDKCompletionTest#19](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#19)]  
  
6. このコードは、完了セッションをトリガーするプライベートメソッドです。  
  
    [!code-csharp[VSSDKCompletionTest#20](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#20)]
    [!code-vb[VSSDKCompletionTest#20](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#20)]  
  
7. 次の例は、イベントからアンサブスクライブするプライベートメソッドです <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSession.Dismissed> 。  
  
    [!code-csharp[VSSDKCompletionTest#21](../snippets/csharp/VS_Snippets_VSSDK/vssdkcompletiontest/cs/testcompletioncommandhandler.cs#21)]
    [!code-vb[VSSDKCompletionTest#21](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkcompletiontest/vb/testcompletioncommandhandler.vb#21)]  
  
## <a name="building-and-testing-the-code"></a>コードのビルドとテスト  
 このコードをテストするには、実行テストソリューションをビルドし、実験用インスタンスで実行します。  
  
#### <a name="to-build-and-test-the-completiontest-solution"></a>補完テストソリューションをビルドしてテストするには  
  
1. ソリューションをビルドします。  
  
2. デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 つ目のインスタンスがインスタンス化されます。  
  
3. テキストファイルを作成し、"add" という単語を含むテキストを入力します。  
  
4. 最初の "a" と "d" を入力すると、"加算" と "アダプテーション" を含む一覧が表示されます。 追加が選択されていることを確認します。 別の "d" と入力した場合、一覧には [追加] のみが表示されます。これは現在選択されています。 "追加" をコミットするには、Space キー、Tab キー、または Enter キーを押すか、Esc キーまたは他のキーを入力して一覧を閉じます。  
  
## <a name="see-also"></a>参照  
 [チュートリアル: コンテンツの種類とファイル名拡張子とをリンクさせる](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)

---
title: 'チュートリアル: ステートメント入力候補の表示 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - statement completion
ms.assetid: f3152c4e-7673-4047-a079-2326941d1c83
author: madskristensen
ms.author: madsk
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- vssdk
ms.openlocfilehash: 78cbcc9b2efd37aa99906d7ed7708621ec213b2e
ms.sourcegitcommit: e3c3d2b185b689c5e32ab4e595abc1ac60b6b9a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/18/2020
ms.locfileid: "76269079"
---
# <a name="walkthrough-display-statement-completion"></a>チュートリアル: ステートメント入力候補の表示
入力候補を提供する識別子を定義し、完了セッションをトリガーすることによって、言語ベースのステートメント入力候補を実装できます。 言語サービスのコンテキストでステートメント入力候補を定義し、独自のファイル名の拡張子とコンテンツの種類を定義して、その型の入力候補だけを表示することができます。 または、既存のコンテンツの種類 ("プレーンテキスト" など) の完了をトリガーすることもできます。 このチュートリアルでは、テキストファイルのコンテンツタイプである "プレーンテキスト" コンテンツタイプに対してステートメント入力候補をトリガーする方法について説明します。 "Text" コンテンツタイプは、コードファイルや XML ファイルなど、他のすべてのコンテンツタイプの先祖です。

 通常、ステートメント入力候補は特定の文字を入力することによってトリガーされます。たとえば、"using" などの識別子の先頭を入力します。 通常、 **space**、 **Tab**、または**enter**キーを押すと、選択範囲がコミットされます。 キーストロークのコマンドハンドラー (<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイス) と、<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> インターフェイスを実装するハンドラープロバイダーを使用して、文字を入力するときにトリガーされる IntelliSense 機能を実装できます。 完了に参加する識別子の一覧である完了ソースを作成するには、<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource> インターフェイスと完了ソースプロバイダー (<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider> インターフェイス) を実装します。 プロバイダーは、Managed Extensibility Framework (MEF) コンポーネントのパートです。 ソースとコントローラークラスをエクスポートし、サービスとブローカー (たとえば、テキストバッファー内の移動を可能にする <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>や、完了セッションをトリガーする <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>) をインポートする責任があります。

 このチュートリアルでは、ハードコーディングされた識別子のセットに対してステートメント入力候補を実装する方法について説明します。 完全な実装では、言語サービスと言語ドキュメントにそのコンテンツを提供する役割があります。

## <a name="prerequisites"></a>Prerequisites
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 また、後から VS SDK をインストールすることもできます。 詳細については、"[Visual Studio SDK をインストール](../extensibility/installing-the-visual-studio-sdk.md)"を参照してください。

## <a name="create-a-mef-project"></a>MEF プロジェクトを作成する

#### <a name="to-create-a-mef-project"></a>MEF プロジェクトを作成するには

1. VSIX プロジェクトC#を作成します。 ( **[新しいプロジェクト]** ダイアログで、 **[ C#ビジュアル/機能拡張**]、 **[VSIX プロジェクト]** の順に選択します)。ソリューションに `CompletionTest`という名前を指定します。

2. エディター分類子項目テンプレートをプロジェクトに追加します。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)する」を参照してください。

3. 既存のクラス ファイルを削除します。

4. 次の参照をプロジェクトに追加し、 **CopyLocal**が `false`に設定されていることを確認します。

     VisualStudio

     Microsoft.VisualStudio.Language.Intellisense

     Microsoft.VisualStudio.OLE.Interop

     VisualStudio. 15.0

     Microsoft.VisualStudio.Shell.Immutable.10.0

     Microsoft.VisualStudio.TextManager.Interop

## <a name="implement-the-completion-source"></a>完了ソースの実装
 入力候補は、識別子の最初の文字などの入力候補のトリガーをユーザーが入力したときに、一連の識別子を収集し、その内容を完了ウィンドウに追加する役割を担います。 この例では、<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A> メソッドで識別子とその説明をハードコーディングしています。 ほとんどの実際の使用では、言語のパーサーを使用してトークンを取得し、入力候補一覧に入力します。

### <a name="to-implement-the-completion-source"></a>完了ソースを実装するには

1. クラス ファイルを追加し、その名前を `TestCompletionSource`にします。

2. 次のインポートを追加します。

     [!code-csharp[VSSDKCompletionTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_1.cs)]
     [!code-vb[VSSDKCompletionTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_1.vb)]

3. <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource>を実装するように、`TestCompletionSource` のクラス宣言を変更します。

     [!code-csharp[VSSDKCompletionTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_2.cs)]
     [!code-vb[VSSDKCompletionTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_2.vb)]

4. ソースプロバイダー、テキストバッファー、および <xref:Microsoft.VisualStudio.Language.Intellisense.Completion> オブジェクトの一覧 (完了セッションに参加する識別子に対応する) のプライベートフィールドを追加します。

     [!code-csharp[VSSDKCompletionTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_3.cs)]
     [!code-vb[VSSDKCompletionTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_3.vb)]

5. ソースプロバイダーとバッファーを設定するコンストラクターを追加します。 `TestCompletionSourceProvider` クラスは、後の手順で定義します。

     [!code-csharp[VSSDKCompletionTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_4.cs)]
     [!code-vb[VSSDKCompletionTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_4.vb)]

6. コンテキストで指定する入力候補を含む完了セットを追加することによって、<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSource.AugmentCompletionSession%2A> メソッドを実装します。 各入力候補セットには <xref:Microsoft.VisualStudio.Language.Intellisense.Completion> 入力候補のセットが含まれており、[完了] ウィンドウのタブに対応しています。 (Visual Basic プロジェクトでは、[完了] ウィンドウのタブの名前は "**共通**" と "**すべて**" になります)。`FindTokenSpanAtPosition` メソッドは、次の手順で定義します。

     [!code-csharp[VSSDKCompletionTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_5.cs)]
     [!code-vb[VSSDKCompletionTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_5.vb)]

7. カーソルの位置から現在の単語を検索するには、次のメソッドを使用します。

     [!code-csharp[VSSDKCompletionTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_6.cs)]
     [!code-vb[VSSDKCompletionTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_6.vb)]

8. `Dispose()` メソッドを実装します。

     [!code-csharp[VSSDKCompletionTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_7.cs)]
     [!code-vb[VSSDKCompletionTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_7.vb)]

## <a name="implement-the-completion-source-provider"></a>完了ソースプロバイダーを実装する
 完了ソースプロバイダーは、完了ソースをインスタンス化する MEF コンポーネント部分です。

### <a name="to-implement-the-completion-source-provider"></a>完了ソースプロバイダーを実装するには

1. <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider>を実装する `TestCompletionSourceProvider` という名前のクラスを追加します。 "Plaintext" の <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> と "test completion" の <xref:Microsoft.VisualStudio.Utilities.NameAttribute> を使用して、このクラスをエクスポートします。

     [!code-csharp[VSSDKCompletionTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_8.cs)]
     [!code-vb[VSSDKCompletionTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_8.vb)]

2. <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>をインポートします。これにより、完了ソース内の現在の単語が検索されます。

     [!code-csharp[VSSDKCompletionTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_9.cs)]
     [!code-vb[VSSDKCompletionTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_9.vb)]

3. <xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionSourceProvider.TryCreateCompletionSource%2A> メソッドを実装して、完了ソースをインスタンス化します。

     [!code-csharp[VSSDKCompletionTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_10.cs)]
     [!code-vb[VSSDKCompletionTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_10.vb)]

## <a name="implement-the-completion-command-handler-provider"></a>完了コマンドハンドラープロバイダーを実装する
 完了コマンドハンドラープロバイダーは <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>から派生します。このクラスは、テキストビュー作成イベントをリッスンし、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>からビューを変換します。これにより、Visual Studio シェルのコマンドチェーンにコマンドを追加できるようになり、<xref:Microsoft.VisualStudio.Text.Editor.ITextView>になります。 このクラスは MEF エクスポートであるため、このクラスを使用して、コマンドハンドラー自体が必要とするサービスをインポートすることもできます。

#### <a name="to-implement-the-completion-command-handler-provider"></a>完了コマンドハンドラープロバイダーを実装するには

1. `TestCompletionCommandHandler`という名前のファイルを追加します。

2. 次の using ディレクティブを追加します。

     [!code-csharp[VSSDKCompletionTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_11.cs)]
     [!code-vb[VSSDKCompletionTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_11.vb)]

3. <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>を実装する `TestCompletionHandlerProvider` という名前のクラスを追加します。 このクラスを、"token completion handler" の <xref:Microsoft.VisualStudio.Utilities.NameAttribute>、"plaintext" の <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>、および <xref:Microsoft.VisualStudio.Text.Editor.PredefinedTextViewRoles.Editable>の <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> を使用してエクスポートします。

     [!code-csharp[VSSDKCompletionTest#12](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_12.cs)]
     [!code-vb[VSSDKCompletionTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_12.vb)]

4. <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>をインポートします。これにより、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> から <xref:Microsoft.VisualStudio.Text.Editor.ITextView>、<xref:Microsoft.VisualStudio.Language.Intellisense.ICompletionBroker>、および標準の Visual Studio サービスへのアクセスを可能にする <xref:Microsoft.VisualStudio.Shell.SVsServiceProvider> に変換できるようになります。

     [!code-csharp[VSSDKCompletionTest#13](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_13.cs)]
     [!code-vb[VSSDKCompletionTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_13.vb)]

5. コマンドハンドラーをインスタンス化するには、<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A> メソッドを実装します。

     [!code-csharp[VSSDKCompletionTest#14](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_14.cs)]
     [!code-vb[VSSDKCompletionTest#14](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_14.vb)]

## <a name="implement-the-completion-command-handler"></a>完了コマンドハンドラーの実装
 ステートメント入力候補はキーストロークによってトリガーされるため、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスを実装して、完了セッションをトリガー、コミット、および破棄するキーストロークを受信および処理する必要があります。

#### <a name="to-implement-the-completion-command-handler"></a>完了コマンドハンドラーを実装するには

1. <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>を実装する `TestCompletionCommandHandler` という名前のクラスを追加します。

    [!code-csharp[VSSDKCompletionTest#15](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_15.cs)]
    [!code-vb[VSSDKCompletionTest#15](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_15.vb)]

2. 次のコマンドハンドラー (コマンドの渡し先)、テキストビュー、コマンドハンドラープロバイダー (さまざまなサービスへのアクセスを可能にする)、および完了セッションのプライベートフィールドを追加します。

    [!code-csharp[VSSDKCompletionTest#16](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_16.cs)]
    [!code-vb[VSSDKCompletionTest#16](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_16.vb)]

3. テキストビューとプロバイダーフィールドを設定するコンストラクターを追加し、コマンドチェーンにコマンドを追加します。

    [!code-csharp[VSSDKCompletionTest#17](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_17.cs)]
    [!code-vb[VSSDKCompletionTest#17](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_17.vb)]

4. 次のコマンドを渡して、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> メソッドを実装します。

    [!code-csharp[VSSDKCompletionTest#18](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_18.cs)]
    [!code-vb[VSSDKCompletionTest#18](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_18.vb)]

5. <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> メソッドを実装します。 このメソッドがキーストロークを受け取ると、次のいずれかの操作を行う必要があります。

   - 文字がバッファーに書き込まれることを許可し、その後、完了をトリガーまたはフィルター処理します。 (印刷文字はこれを行います)。

   - 完了をコミットしますが、バッファーへの文字の書き込みは許可しません。 (空白、**タブ**、 **Enter キー**を押したときに入力します。

   - コマンドを次のハンドラーに渡すことを許可します。 (その他のすべてのコマンド)。

     このメソッドは UI を表示する可能性があるため、<xref:Microsoft.VisualStudio.Shell.VsShellUtilities.IsInAutomationFunction%2A> を呼び出して、オートメーションコンテキストで呼び出されないようにします。

     [!code-csharp[VSSDKCompletionTest#19](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_19.cs)]
     [!code-vb[VSSDKCompletionTest#19](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_19.vb)]

6. このコードは、完了セッションをトリガーするプライベートメソッドです。

    [!code-csharp[VSSDKCompletionTest#20](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_20.cs)]
    [!code-vb[VSSDKCompletionTest#20](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_20.vb)]

7. 次の例は、<xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseSession.Dismissed> イベントからアンサブスクライブするプライベートメソッドです。

    [!code-csharp[VSSDKCompletionTest#21](../extensibility/codesnippet/CSharp/walkthrough-displaying-statement-completion_21.cs)]
    [!code-vb[VSSDKCompletionTest#21](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-statement-completion_21.vb)]

## <a name="build-and-test-the-code"></a>コードをビルドしてテストする
 このコードをテストするには、実行テストソリューションをビルドし、実験用インスタンスで実行します。

#### <a name="to-build-and-test-the-completiontest-solution"></a>補完テストソリューションをビルドしてテストするには

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の2番目のインスタンスが開始されます。

3. テキストファイルを作成し、"add" という単語を含むテキストを入力します。

4. 最初の "a" と "d" を入力すると、"加算" と "アダプテーション" を含む一覧が表示されます。 追加が選択されていることを確認します。 別の "d" と入力した場合、一覧には [追加] のみが表示されます。これは現在選択されています。 "追加" をコミットするには、 **space**キー、 **tab**キー、または**enter**キーを押すか、Esc キーまたは他のキーを入力して一覧を閉じます。

## <a name="see-also"></a>関連項目
- [チュートリアル: コンテンツの種類をファイル名拡張子にリンクする](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)

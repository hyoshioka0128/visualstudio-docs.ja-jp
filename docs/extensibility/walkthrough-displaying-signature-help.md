---
title: 'チュートリアル: 署名ヘルプを表示する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - signature help/parameter info
ms.assetid: 4a6a884b-5730-4b54-9264-99684f5b523c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f85d7eb3959064468e7583ec0c8a927f3e139daf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697430"
---
# <a name="walkthrough-display-signature-help"></a>チュートリアル: 署名ヘルプの表示
シグネチャ ヘルプ (*パラメーター ヒント*とも呼ばれます) は、ユーザーがパラメーター リストの開始文字 (通常は左かっこ) を入力したときに、ツールヒントにメソッドのシグネチャを表示します。 パラメーターとパラメーターの区切り記号 (通常はコンマ) が入力されると、ツールヒントが更新され、次のパラメーターが太字で表示されます。 シグネチャ ヘルプは、言語サービスのコンテキストで、独自のファイル名拡張子とコンテンツ タイプを定義し、その種類の署名ヘルプを表示したり、既存のコンテンツ タイプ ("text" など) の Signature ヘルプを表示したりできます。 このチュートリアルでは、"text" コンテンツ タイプの署名ヘルプを表示する方法を示します。

 シグネチャ ヘルプは通常、特定の文字 ("(" (左かっこ) など) を入力して起動し、別の文字 (")" (右かっこ) などの文字を入力すると、その文字は閉じられます。 文字を入力してトリガーされる IntelliSense 機能は、キーストローク (<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>インターフェイス) のコマンド ハンドラーと<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>、インターフェイスを実装するハンドラー プロバイダーを使用して実装できます。 署名ヘルプに含まれるシグネチャの一覧である署名ヘルプ ソースを作成するには、インターフェイスと、インターフェイス<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource>を実行するソース プロバイダーを実装<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider>します。 プロバイダはマネージ機能拡張フレームワーク (MEF) コンポーネントの一部であり、ソース クラスとコントローラ クラスのエクスポート、およびサービスとブローカーの<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService><xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker>インポートを担当します。

 このチュートリアルでは、ハードコーディングされた識別子のセットに対してシグネチャ ヘルプを設定する方法を示します。 完全な実装では、言語がそのコンテンツを提供する責任があります。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="creating-a-mef-project"></a>MEF プロジェクトの作成

#### <a name="to-create-a-mef-project"></a>MEF プロジェクトを作成するには

1. C# VSIX プロジェクトを作成します。 ([**新しいプロジェクト**] ダイアログで、[**ビジュアル C# / 拡張性**] を選択し、次に**VSIX プロジェクト**を選択します)。ソリューションに名前`SignatureHelpTest`を付ける:

2. エディター分類子項目テンプレートをプロジェクトに追加します。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

3. 既存のクラス ファイルを削除します。

4. プロジェクトに次の参照を追加し **、CopyLocal**が に`false`設定されていることを確認します。

     エディター

     Microsoft.VisualStudio.Language.Intellisense

     Microsoft.VisualStudio.OLE.Interop

     シェル.14.0

     相互運用機能

## <a name="implement-signature-help-signatures-and-parameters"></a>署名ヘルプのシグネチャとパラメータを実装する
 Signature ヘルプ ソースは、 を実装する<xref:Microsoft.VisualStudio.Language.Intellisense.ISignature>シグネチャに基づいており、各<xref:Microsoft.VisualStudio.Language.Intellisense.IParameter>シグネチャには を実装するパラメータが含まれています。 完全な実装では、この情報は言語ドキュメントから取得されますが、この例では署名はハードコーディングされています。

#### <a name="to-implement-the-signature-help-signatures-and-parameters"></a>署名ヘルプのシグネチャとパラメータを実装するには

1. クラス ファイルを追加し、その名前を `SignatureHelpSource`にします。

2. 次のインポートを追加します。

     [!code-vb[VSSDKSignatureHelpTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_1.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_1.cs)]

3. を実装するという`TestParameter`名前のクラス<xref:Microsoft.VisualStudio.Language.Intellisense.IParameter>を追加します。

     [!code-vb[VSSDKSignatureHelpTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_2.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_2.cs)]

4. すべてのプロパティを設定するコンストラクターを追加します。

     [!code-vb[VSSDKSignatureHelpTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_3.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_3.cs)]

5. のプロパティを<xref:Microsoft.VisualStudio.Language.Intellisense.IParameter>追加します。

     [!code-vb[VSSDKSignatureHelpTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_4.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_4.cs)]

6. を実装するという`TestSignature`名前のクラス<xref:Microsoft.VisualStudio.Language.Intellisense.ISignature>を追加します。

     [!code-vb[VSSDKSignatureHelpTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_5.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_5.cs)]

7. いくつかのプライベート フィールドを追加します。

     [!code-vb[VSSDKSignatureHelpTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_6.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_6.cs)]

8. フィールドを設定し、イベントをサブスクライブするコンストラクターを<xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed>追加します。

     [!code-vb[VSSDKSignatureHelpTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_7.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_7.cs)]

9. イベントを`CurrentParameterChanged`宣言します。 このイベントは、ユーザーが署名のパラメーターの 1 つを入力したときに発生します。

     [!code-vb[VSSDKSignatureHelpTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_8.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_8.cs)]

10. プロパティ値<xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.CurrentParameter%2A>が変更されたときにイベントが`CurrentParameterChanged`発生するように、プロパティを実装します。

     [!code-vb[VSSDKSignatureHelpTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_9.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_9.cs)]

11. イベントを発生させるメソッドを追加`CurrentParameterChanged`します。

     [!code-vb[VSSDKSignatureHelpTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_10.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_10.cs)]

12. のコンマの数とシグネチャのコンマの数<xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A>を比較して、現在のパラメーターを計算するメソッドを追加します。

     [!code-vb[VSSDKSignatureHelpTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_11.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_11.cs)]

13. メソッドを呼び出す<xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed>イベントのイベント`ComputeCurrentParameter()`ハンドラーを追加します。

     [!code-vb[VSSDKSignatureHelpTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_12.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#12](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_12.cs)]

14. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> プロパティを実装します。 このプロパティは<xref:Microsoft.VisualStudio.Text.ITrackingSpan>、署名が適用されるバッファー内のテキストの範囲に対応する を保持します。

     [!code-vb[VSSDKSignatureHelpTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_13.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#13](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_13.cs)]

15. 他のパラメーターを実装します。

     [!code-vb[VSSDKSignatureHelpTest#14](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_14.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#14](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_14.cs)]

## <a name="implement-the-signature-help-source"></a>署名ヘルプ ソースの実装
 署名ヘルプ ソースは、情報を提供する署名のセットです。

#### <a name="to-implement-the-signature-help-source"></a>署名ヘルプ ソースを実装するには

1. を実装するという`TestSignatureHelpSource`名前のクラス<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource>を追加します。

     [!code-vb[VSSDKSignatureHelpTest#15](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_15.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#15](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_15.cs)]

2. テキスト バッファーへの参照を追加します。

     [!code-vb[VSSDKSignatureHelpTest#16](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_16.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#16](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_16.cs)]

3. テキスト バッファーと署名ヘルプソース プロバイダーを設定するコンストラクターを追加します。

     [!code-vb[VSSDKSignatureHelpTest#17](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_17.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#17](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_17.cs)]

4. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.AugmentSignatureHelpSession%2A> メソッドを実装します。 この例では、署名はハードコーディングされていますが、完全な実装では、言語ドキュメントからこの情報を取得します。

     [!code-vb[VSSDKSignatureHelpTest#18](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_18.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#18](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_18.cs)]

5. このヘルパー`CreateSignature()`メソッドは、説明用に用意されています。

     [!code-vb[VSSDKSignatureHelpTest#19](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_19.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#19](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_19.cs)]

6. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.GetBestMatch%2A> メソッドを実装します。 この例では、2 つのシグネチャがあり、それぞれに 2 つのパラメーターがあります。 したがって、このメソッドは必要ありません。 複数の Signature ヘルプ ソースを使用できる完全な実装では、このメソッドを使用して、最も優先度の高い署名ヘルプ ソースが一致するシグネチャを提供できるかどうかを判断します。 それができない場合、メソッドは null を返し、次に優先順位の高いソースが一致を指定するように求められます。

     [!code-vb[VSSDKSignatureHelpTest#20](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_20.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#20](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_20.cs)]

7. メソッドを`Dispose()`実装します。

     [!code-vb[VSSDKSignatureHelpTest#21](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_21.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#21](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_21.cs)]

## <a name="implement-the-signature-help-source-provider"></a>署名ヘルプ ソース プロバイダーを実装する
 署名ヘルプ ソース プロバイダーは、マネージ機能拡張フレームワーク (MEF) コンポーネントの部分をエクスポートし、署名のヘルプ ソースをインスタンス化します。

#### <a name="to-implement-the-signature-help-source-provider"></a>署名ヘルプ ソース プロバイダーを実装するには

1. を実装するという`TestSignatureHelpSourceProvider`名前のクラス<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider>を追加し、それを<xref:Microsoft.VisualStudio.Utilities.NameAttribute>「text」の a<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>と<xref:Microsoft.VisualStudio.Utilities.OrderAttribute>Before="default の a と共にエクスポートします。

     [!code-vb[VSSDKSignatureHelpTest#22](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_22.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#22](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_22.cs)]

2. を<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider.TryCreateSignatureHelpSource%2A>インスタンス化して実装します`TestSignatureHelpSource`。

     [!code-vb[VSSDKSignatureHelpTest#23](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_23.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#23](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_23.cs)]

## <a name="implement-the-command-handler"></a>コマンド ハンドラーを実装する
 シグネチャ ヘルプは通常、左かっこ "(" 文字によってトリガされ、右かっこ ")" 文字で閉じます。 これらのキーストロークを処理するには、 を<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>実行して、既知のメソッド名が付いた左かっこを受け取ったときにシグネチャ ヘルプ セッションをトリガーし、閉じかっこを受け取ったときにセッションを閉じます。

#### <a name="to-implement-the-command-handler"></a>コマンド ハンドラーを実装するには

1. を実装するという`TestSignatureHelpCommand`名前のクラス<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>を追加します。

     [!code-vb[VSSDKSignatureHelpTest#24](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_24.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#24](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_24.cs)]

2. アダプタの<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>プライベート フィールド (コマンド ハンドラのチェーンにコマンド ハンドラを追加できます)、テキスト ビュー、シグネチャ ヘルプ ブローカとセッション<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator>、、、および<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>次の フィールドを追加します。

     [!code-vb[VSSDKSignatureHelpTest#25](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_25.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#25](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_25.cs)]

3. これらのフィールドを初期化し、コマンド フィルターのチェーンにコマンド フィルターを追加するコンストラクターを追加します。

     [!code-vb[VSSDKSignatureHelpTest#26](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_26.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#26](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_26.cs)]

4. コマンド<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A>フィルタが既知のメソッド名の後に左かっこ "(" 文字を受け取ったときにシグネチャ ヘルプ セッションをトリガーし、セッションがアクティブな状態で閉じかっこ ")" 文字を受け取ったときにセッションを終了するメソッドを実装します。 いずれの場合も、コマンドは転送されます。

     [!code-vb[VSSDKSignatureHelpTest#27](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_27.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#27](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_27.cs)]

5. 常に<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>コマンドを転送するようにメソッドを実装します。

     [!code-vb[VSSDKSignatureHelpTest#28](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_28.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#28](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_28.cs)]

## <a name="implement-the-signature-help-command-provider"></a>署名ヘルプ コマンド プロバイダーを実装する
 署名ヘルプ コマンドを指定するには、テキスト<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>ビューの作成時にコマンド ハンドラーをインスタンス化する を実装します。

### <a name="to-implement-the-signature-help-command-provider"></a>署名ヘルプ コマンド プロバイダーを実装するには

1. を実装`TestSignatureHelpController`<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener>し、 、<xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>および<xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>を使用してエクスポート<xref:Microsoft.VisualStudio.Utilities.NameAttribute>するという名前のクラスを追加します。

     [!code-vb[VSSDKSignatureHelpTest#29](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_29.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#29](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_29.cs)]

2. <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> <xref:Microsoft.VisualStudio.Text.Editor.ITextView>(<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>オブジェクトを指定してを取得するために使用<xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService>)、(現在の単語を検索するために使用)、および<xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker>(署名ヘルプセッションをトリガするために)をインポートします。

     [!code-vb[VSSDKSignatureHelpTest#30](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_30.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#30](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_30.cs)]

3. をインスタンス<xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A>化してメソッドを実装します`TestSignatureCommandHandler`。

     [!code-vb[VSSDKSignatureHelpTest#31](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_31.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#31](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_31.cs)]

## <a name="build-and-test-the-code"></a>コードのビルドとテスト
 このコードをテストするには、SignatureHelpTest ソリューションをビルドし、実験用インスタンスで実行します。

#### <a name="to-build-and-test-the-signaturehelptest-solution"></a>署名ヘルプテスト ソリューションをビルドしてテストするには

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 番目のインスタンスが起動します。

3. テキスト ファイルを作成し、"add" と左かっこを含むテキストを入力します。

4. 左かっこを入力すると、メソッドの 2 つのシグネチャの一覧を表示するツールヒントが表示されます`add()`。

## <a name="see-also"></a>関連項目
- [チュートリアル: コンテンツ タイプをファイル名拡張子にリンクする](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)

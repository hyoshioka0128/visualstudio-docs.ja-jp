---
title: 'チュートリアル: シグネチャのヘルプを表示する |Microsoft Docs'
description: このチュートリアルを使用して、テキストコンテンツタイプの署名のヘルプを表示する方法について説明します。 シグネチャヘルプは、メソッドのシグネチャをツールヒントに表示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - signature help/parameter info
ms.assetid: 4a6a884b-5730-4b54-9264-99684f5b523c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1a9aedc6324eb1d4a57517a10b80348841fa72df
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078501"
---
# <a name="walkthrough-display-signature-help"></a>チュートリアル: 署名のヘルプを表示する
シグネチャヘルプ ( *パラメーターヒント* とも呼ばれます) は、ユーザーがパラメーターリストの開始文字 (通常は始めかっこ) を入力したときに、ツールヒントにメソッドの署名を表示します。 パラメーターとパラメーターの区切り記号 (通常はコンマ) が入力されると、ツールヒントが更新され、次のパラメーターが太字で表示されます。 シグネチャヘルプは、次の方法で定義できます。言語サービスのコンテキストでは、独自のファイル名の拡張子とコンテンツの種類を定義し、その種類の署名のヘルプを表示します。または、既存のコンテンツの種類 (たとえば、"text") の署名のヘルプを表示します。 このチュートリアルでは、"text" コンテンツタイプのシグネチャヘルプを表示する方法について説明します。

 シグネチャヘルプは、通常、特定の文字 (左かっこ) を入力することによってトリガーされ、別の文字 (")" (右かっこ) を入力することによって無視されます。 文字の入力によってトリガーされる IntelliSense 機能を実装するには、キーストローク (インターフェイス) のコマンドハンドラー <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> と、インターフェイスを実装するハンドラープロバイダーを使用し <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> ます。 シグネチャヘルプに参加する署名の一覧である Signature ヘルプソースを作成するには、インターフェイス <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource> と、インターフェイスを実行するソースプロバイダーを実装し <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider> ます。 プロバイダーは Managed Extensibility Framework (MEF) コンポーネントのパーツであり、ソースとコントローラーのクラスをエクスポートし、サービスとブローカーをインポートし <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> ます。たとえば、テキストバッファー内を移動できるようにしたり、 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker> 署名ヘルプセッションをトリガーするを使用したりします。

 このチュートリアルでは、ハードコーディングされた識別子のセットの署名のヘルプを設定する方法について説明します。 完全な実装では、言語がそのコンテンツを提供する必要があります。

## <a name="prerequisites"></a>前提条件
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="creating-a-mef-project"></a>MEF プロジェクトの作成

#### <a name="to-create-a-mef-project"></a>MEF プロジェクトを作成するには

1. C# VSIX プロジェクトを作成します。 ([ **新しいプロジェクト** ] ダイアログで、[Visual C#]、[ **拡張機能**]、[ **VSIX プロジェクト**] の順に選択します)。ソリューションにという名前を指定 `SignatureHelpTest` します。

2. エディター分類子項目テンプレートをプロジェクトに追加します。 詳細については、「 [エディター項目テンプレートを使用して拡張機能を作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)する」を参照してください。

3. 既存のクラス ファイルを削除します。

4. 次の参照をプロジェクトに追加し、 **CopyLocal** がに設定されていることを確認し `false` ます。

     VisualStudio

     Microsoft.VisualStudio.Language.Intellisense

     Microsoft.VisualStudio.OLE.Interop

     VisualStudio. 14.0

     VisualStudio。相互運用

## <a name="implement-signature-help-signatures-and-parameters"></a>署名のヘルプ署名とパラメーターを実装する
 シグネチャヘルプソースはを実装する署名に基づいて <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature> おり、それぞれにを実装するパラメーターが含まれてい <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> ます。 完全な実装では、この情報は言語ドキュメントから取得されますが、この例では、署名はハードコーディングされています。

#### <a name="to-implement-the-signature-help-signatures-and-parameters"></a>署名のヘルプ署名とパラメーターを実装するには

1. クラス ファイルを追加し、その名前を `SignatureHelpSource`にします。

2. 次のインポートを追加します。

     [!code-vb[VSSDKSignatureHelpTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_1.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#1](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_1.cs)]

3. を実装するという名前のクラスを追加 `TestParameter` <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> します。

     [!code-vb[VSSDKSignatureHelpTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_2.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#2](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_2.cs)]

4. すべてのプロパティを設定するコンストラクターを追加します。

     [!code-vb[VSSDKSignatureHelpTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_3.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#3](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_3.cs)]

5. のプロパティを追加 <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> します。

     [!code-vb[VSSDKSignatureHelpTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_4.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#4](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_4.cs)]

6. を実装するという名前のクラスを追加 `TestSignature` <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature> します。

     [!code-vb[VSSDKSignatureHelpTest#5](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_5.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#5](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_5.cs)]

7. いくつかのプライベートフィールドを追加します。

     [!code-vb[VSSDKSignatureHelpTest#6](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_6.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#6](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_6.cs)]

8. フィールドを設定し、イベントをサブスクライブするコンストラクターを追加し <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> ます。

     [!code-vb[VSSDKSignatureHelpTest#7](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_7.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#7](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_7.cs)]

9. イベントを宣言 `CurrentParameterChanged` します。 このイベントは、ユーザーが署名のパラメーターの1つを入力したときに発生します。

     [!code-vb[VSSDKSignatureHelpTest#8](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_8.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#8](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_8.cs)]

10. プロパティ <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.CurrentParameter%2A> 値が変更されたときにイベントを発生させるように、プロパティを実装し `CurrentParameterChanged` ます。

     [!code-vb[VSSDKSignatureHelpTest#9](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_9.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#9](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_9.cs)]

11. イベントを発生させるメソッドを追加 `CurrentParameterChanged` します。

     [!code-vb[VSSDKSignatureHelpTest#10](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_10.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#10](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_10.cs)]

12. のコンマの数をシグネチャのコンマの数と比較して、現在のパラメーターを計算するメソッドを追加し <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> ます。

     [!code-vb[VSSDKSignatureHelpTest#11](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_11.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#11](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_11.cs)]

13. メソッドを呼び出すイベントのイベントハンドラーを追加 <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> `ComputeCurrentParameter()` します。

     [!code-vb[VSSDKSignatureHelpTest#12](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_12.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#12](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_12.cs)]

14. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> プロパティを実装します。 このプロパティは、 <xref:Microsoft.VisualStudio.Text.ITrackingSpan> 署名が適用されるバッファー内のテキストの範囲に対応するを保持します。

     [!code-vb[VSSDKSignatureHelpTest#13](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_13.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#13](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_13.cs)]

15. 他のパラメーターを実装します。

     [!code-vb[VSSDKSignatureHelpTest#14](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_14.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#14](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_14.cs)]

## <a name="implement-the-signature-help-source"></a>署名ヘルプソースを実装する
 署名ヘルプソースは、情報を提供するための一連の署名です。

#### <a name="to-implement-the-signature-help-source"></a>シグネチャヘルプソースを実装するには

1. を実装するという名前のクラスを追加 `TestSignatureHelpSource` <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource> します。

     [!code-vb[VSSDKSignatureHelpTest#15](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_15.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#15](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_15.cs)]

2. テキストバッファーへの参照を追加します。

     [!code-vb[VSSDKSignatureHelpTest#16](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_16.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#16](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_16.cs)]

3. テキストバッファーとシグネチャヘルプソースプロバイダーを設定するコンストラクターを追加します。

     [!code-vb[VSSDKSignatureHelpTest#17](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_17.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#17](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_17.cs)]

4. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.AugmentSignatureHelpSession%2A> メソッドを実装します。 この例では、署名はハードコーディングされていますが、完全な実装では、言語ドキュメントからこの情報を取得します。

     [!code-vb[VSSDKSignatureHelpTest#18](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_18.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#18](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_18.cs)]

5. ヘルパーメソッド `CreateSignature()` は、説明のためだけに用意されています。

     [!code-vb[VSSDKSignatureHelpTest#19](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_19.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#19](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_19.cs)]

6. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.GetBestMatch%2A> メソッドを実装します。 この例では、2つのシグネチャがあり、それぞれに2つのパラメーターがあります。 したがって、このメソッドは必要ありません。 複数のシグネチャヘルプソースを使用できる完全な実装では、このメソッドを使用して、優先順位の高いシグネチャのヘルプソースが一致する署名を提供できるかどうかを判断します。 そうでない場合、メソッドは null を返し、優先度の高い次のソースが一致を指定するように求められます。

     [!code-vb[VSSDKSignatureHelpTest#20](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_20.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#20](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_20.cs)]

7. メソッドを実装し `Dispose()` ます。

     [!code-vb[VSSDKSignatureHelpTest#21](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_21.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#21](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_21.cs)]

## <a name="implement-the-signature-help-source-provider"></a>シグネチャヘルプソースプロバイダーを実装する
 シグネチャヘルプソースプロバイダーは、Managed Extensibility Framework (MEF) コンポーネントのエクスポートと、シグネチャヘルプソースのインスタンス化を担当します。

#### <a name="to-implement-the-signature-help-source-provider"></a>シグネチャヘルプソースプロバイダーを実装するには

1. を実装するという名前のクラスを追加 `TestSignatureHelpSourceProvider` <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider> し、 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> 、、 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "Text"、および <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> Before = "default" を使用してエクスポートします。

     [!code-vb[VSSDKSignatureHelpTest#22](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_22.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#22](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_22.cs)]

2. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider.TryCreateSignatureHelpSource%2A>をインスタンス化することによってを実装し `TestSignatureHelpSource` ます。

     [!code-vb[VSSDKSignatureHelpTest#23](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_23.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#23](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_23.cs)]

## <a name="implement-the-command-handler"></a>コマンドハンドラーを実装する
 シグネチャヘルプは、通常、始めかっこ "(" 文字によってトリガーされ、閉じかっこ ")" で終了します。 これらのキーストロークは、を実行することで処理できます。これにより、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 既知のメソッド名の前に始めかっこ文字を受け取ったときに署名ヘルプセッションがトリガーされ、閉じかっこ文字を受け取ったときにセッションが終了します。

#### <a name="to-implement-the-command-handler"></a>コマンドハンドラーを実装するには

1. を実装するという名前のクラスを追加 `TestSignatureHelpCommand` <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> します。

     [!code-vb[VSSDKSignatureHelpTest#24](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_24.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#24](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_24.cs)]

2. アダプターのプライベートフィールドを追加します <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> (コマンドハンドラーをコマンドハンドラーのチェーンに追加することができます)、テキストビュー、署名ヘルプブローカーとセッション、、、およびを追加し <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ます。

     [!code-vb[VSSDKSignatureHelpTest#25](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_25.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#25](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_25.cs)]

3. これらのフィールドを初期化するコンストラクターを追加し、コマンドフィルターをコマンドフィルターのチェーンに追加します。

     [!code-vb[VSSDKSignatureHelpTest#26](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_26.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#26](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_26.cs)]

4. メソッドを実装して、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> コマンドフィルターが開始かっこ "(" 既知のメソッド名の1つの後にある ") を受信したときに、セッションがアクティブな状態のままである場合にセッションを終了します。 いずれの場合も、コマンドは転送されます。

     [!code-vb[VSSDKSignatureHelpTest#27](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_27.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#27](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_27.cs)]

5. メソッドを実装して、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 常にコマンドを転送するようにします。

     [!code-vb[VSSDKSignatureHelpTest#28](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_28.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#28](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_28.cs)]

## <a name="implement-the-signature-help-command-provider"></a>Signature Help command プロバイダーを実装します。
 署名のヘルプコマンドを提供するには、 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> テキストビューが作成されたときにコマンドハンドラーをインスタンス化するを実装します。

### <a name="to-implement-the-signature-help-command-provider"></a>Signature Help command プロバイダーを実装するには

1. を実装し、、、 `TestSignatureHelpController` およびと共にエクスポートするという名前のクラスを追加し <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> <xref:Microsoft.VisualStudio.Utilities.NameAttribute> <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> ます。

     [!code-vb[VSSDKSignatureHelpTest#29](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_29.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#29](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_29.cs)]

2. (オブジェクトを取得するために使用される)、( <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 現在の単語を検索するために <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> 使用される)、および <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker> (シグネチャヘルプセッションをトリガーする) をインポートします。

     [!code-vb[VSSDKSignatureHelpTest#30](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_30.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#30](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_30.cs)]

3. <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A>をインスタンス化して、メソッドを実装し `TestSignatureCommandHandler` ます。

     [!code-vb[VSSDKSignatureHelpTest#31](../extensibility/codesnippet/VisualBasic/walkthrough-displaying-signature-help_31.vb)]
     [!code-csharp[VSSDKSignatureHelpTest#31](../extensibility/codesnippet/CSharp/walkthrough-displaying-signature-help_31.cs)]

## <a name="build-and-test-the-code"></a>コードをビルドしてテストする
 このコードをテストするには、SignatureHelpTest ソリューションをビルドし、実験用インスタンスで実行します。

#### <a name="to-build-and-test-the-signaturehelptest-solution"></a>SignatureHelpTest ソリューションをビルドしてテストするには

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の2番目のインスタンスが開始されます。

3. テキストファイルを作成し、"add" という語と左かっこを含むテキストを入力します。

4. 始めかっこを入力すると、メソッドの2つのシグネチャの一覧を示すツールヒントが表示され `add()` ます。

## <a name="see-also"></a>こちらもご覧ください
- [チュートリアル: コンテンツの種類をファイル名拡張子にリンクする](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)

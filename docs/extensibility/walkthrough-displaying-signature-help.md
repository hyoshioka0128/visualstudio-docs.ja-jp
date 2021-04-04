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
ms.openlocfilehash: d6ffa2a0e646c11cb56d08ef91e3d7a4b9af7572
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217503"
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

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet1":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet1":::

3. を実装するという名前のクラスを追加 `TestParameter` <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet2":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet2":::

4. すべてのプロパティを設定するコンストラクターを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet3":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet3":::

5. のプロパティを追加 <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet4":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet4":::

6. を実装するという名前のクラスを追加 `TestSignature` <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature> します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet5":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet5":::

7. いくつかのプライベートフィールドを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet6":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet6":::

8. フィールドを設定し、イベントをサブスクライブするコンストラクターを追加し <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> ます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet7":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet7":::

9. イベントを宣言 `CurrentParameterChanged` します。 このイベントは、ユーザーが署名のパラメーターの1つを入力したときに発生します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet8":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet8":::

10. プロパティ <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.CurrentParameter%2A> 値が変更されたときにイベントを発生させるように、プロパティを実装し `CurrentParameterChanged` ます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet9":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet9":::

11. イベントを発生させるメソッドを追加 `CurrentParameterChanged` します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet10":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet10":::

12. のコンマの数をシグネチャのコンマの数と比較して、現在のパラメーターを計算するメソッドを追加し <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> ます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet11":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet11":::

13. メソッドを呼び出すイベントのイベントハンドラーを追加 <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> `ComputeCurrentParameter()` します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet12":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet12":::

14. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> プロパティを実装します。 このプロパティは、 <xref:Microsoft.VisualStudio.Text.ITrackingSpan> 署名が適用されるバッファー内のテキストの範囲に対応するを保持します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet13":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet13":::

15. 他のパラメーターを実装します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet14":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet14":::

## <a name="implement-the-signature-help-source"></a>署名ヘルプソースを実装する
 署名ヘルプソースは、情報を提供するための一連の署名です。

#### <a name="to-implement-the-signature-help-source"></a>シグネチャヘルプソースを実装するには

1. を実装するという名前のクラスを追加 `TestSignatureHelpSource` <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource> します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet15":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet15":::

2. テキストバッファーへの参照を追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet16":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet16":::

3. テキストバッファーとシグネチャヘルプソースプロバイダーを設定するコンストラクターを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet17":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet17":::

4. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.AugmentSignatureHelpSession%2A> メソッドを実装します。 この例では、署名はハードコーディングされていますが、完全な実装では、言語ドキュメントからこの情報を取得します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet18":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet18":::

5. ヘルパーメソッド `CreateSignature()` は、説明のためだけに用意されています。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet19":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet19":::

6. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.GetBestMatch%2A> メソッドを実装します。 この例では、2つのシグネチャがあり、それぞれに2つのパラメーターがあります。 したがって、このメソッドは必要ありません。 複数のシグネチャヘルプソースを使用できる完全な実装では、このメソッドを使用して、優先順位の高いシグネチャのヘルプソースが一致する署名を提供できるかどうかを判断します。 そうでない場合、メソッドは null を返し、優先度の高い次のソースが一致を指定するように求められます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet20":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet20":::

7. メソッドを実装し `Dispose()` ます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet21":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet21":::

## <a name="implement-the-signature-help-source-provider"></a>シグネチャヘルプソースプロバイダーを実装する
 シグネチャヘルプソースプロバイダーは、Managed Extensibility Framework (MEF) コンポーネントのエクスポートと、シグネチャヘルプソースのインスタンス化を担当します。

#### <a name="to-implement-the-signature-help-source-provider"></a>シグネチャヘルプソースプロバイダーを実装するには

1. を実装するという名前のクラスを追加 `TestSignatureHelpSourceProvider` <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider> し、 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> 、、 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "Text"、および <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> Before = "default" を使用してエクスポートします。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet22":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet22":::

2. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider.TryCreateSignatureHelpSource%2A>をインスタンス化することによってを実装し `TestSignatureHelpSource` ます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet23":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet23":::

## <a name="implement-the-command-handler"></a>コマンドハンドラーを実装する
 シグネチャヘルプは、通常、始めかっこ "(" 文字によってトリガーされ、閉じかっこ ")" で終了します。 これらのキーストロークは、を実行することで処理できます。これにより、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 既知のメソッド名の前に始めかっこ文字を受け取ったときに署名ヘルプセッションがトリガーされ、閉じかっこ文字を受け取ったときにセッションが終了します。

#### <a name="to-implement-the-command-handler"></a>コマンドハンドラーを実装するには

1. を実装するという名前のクラスを追加 `TestSignatureHelpCommand` <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet24":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet24":::

2. アダプターのプライベートフィールドを追加します <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> (コマンドハンドラーをコマンドハンドラーのチェーンに追加することができます)、テキストビュー、署名ヘルプブローカーとセッション、、、およびを追加し <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet25":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet25":::

3. これらのフィールドを初期化するコンストラクターを追加し、コマンドフィルターをコマンドフィルターのチェーンに追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet26":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet26":::

4. メソッドを実装して、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> コマンドフィルターが開始かっこ "(" 既知のメソッド名の1つの後にある ") を受信したときに、セッションがアクティブな状態のままである場合にセッションを終了します。 いずれの場合も、コマンドは転送されます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet27":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet27":::

5. メソッドを実装して、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 常にコマンドを転送するようにします。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet28":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet28":::

## <a name="implement-the-signature-help-command-provider"></a>Signature Help command プロバイダーを実装します。
 署名のヘルプコマンドを提供するには、 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> テキストビューが作成されたときにコマンドハンドラーをインスタンス化するを実装します。

### <a name="to-implement-the-signature-help-command-provider"></a>Signature Help command プロバイダーを実装するには

1. を実装し、、、 `TestSignatureHelpController` およびと共にエクスポートするという名前のクラスを追加し <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> <xref:Microsoft.VisualStudio.Utilities.NameAttribute> <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> ます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet29":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet29":::

2. (オブジェクトを取得するために使用される)、( <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 現在の単語を検索するために <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> 使用される)、および <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker> (シグネチャヘルプセッションをトリガーする) をインポートします。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet30":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet30":::

3. <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A>をインスタンス化して、メソッドを実装し `TestSignatureCommandHandler` ます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb" id="Snippet31":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs" id="Snippet31":::

## <a name="build-and-test-the-code"></a>コードをビルドしてテストする
 このコードをテストするには、SignatureHelpTest ソリューションをビルドし、実験用インスタンスで実行します。

#### <a name="to-build-and-test-the-signaturehelptest-solution"></a>SignatureHelpTest ソリューションをビルドしてテストするには

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の2番目のインスタンスが開始されます。

3. テキストファイルを作成し、"add" という語と左かっこを含むテキストを入力します。

4. 始めかっこを入力すると、メソッドの2つのシグネチャの一覧を示すツールヒントが表示され `add()` ます。

## <a name="see-also"></a>関連項目
- [チュートリアル: コンテンツの種類をファイル名拡張子にリンクする](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)

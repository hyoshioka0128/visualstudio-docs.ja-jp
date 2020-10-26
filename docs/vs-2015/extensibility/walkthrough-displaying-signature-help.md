---
title: 'チュートリアル: シグネチャのヘルプを表示する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - signature help/parameter info
ms.assetid: 4a6a884b-5730-4b54-9264-99684f5b523c
caps.latest.revision: 29
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 280b5b517089ad9e5b38cb00dc9b14c68253d1e6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202044"
---
# <a name="walkthrough-displaying-signature-help"></a>チュートリアル: シグネチャ ヘルプの表示
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

シグネチャヘルプ ( *パラメーターヒント*とも呼ばれます) は、ユーザーがパラメーターリストの開始文字 (通常は始めかっこ) を入力したときに、ツールヒントにメソッドの署名を表示します。 パラメーターとパラメーターの区切り記号 (通常はコンマ) が入力されると、ツールヒントが更新され、次のパラメーターが太字で表示されます。 言語サービスのコンテキストでシグネチャのヘルプを定義することも、独自のファイル名の拡張子とコンテンツの種類を定義し、その種類の署名のヘルプを表示することもできます。また、既存のコンテンツの種類 (たとえば、"text") のシグネチャヘルプを表示することもできます。 このチュートリアルでは、"text" コンテンツタイプのシグネチャヘルプを表示する方法について説明します。  
  
 シグネチャヘルプは、通常、特定の文字 (左かっこ) を入力することによってトリガーされ、別の文字 (")" (右かっこ) を入力することによって無視されます。 文字の入力によってトリガーされる IntelliSense 機能を実装するには、キーストローク (インターフェイス) のコマンドハンドラー <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> と、インターフェイスを実装するハンドラープロバイダーを使用し <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> ます。 シグネチャヘルプに参加する署名の一覧である Signature ヘルプソースを作成するには、インターフェイス <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource> と、インターフェイスを実装するソースプロバイダーを実装し <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider> ます。 プロバイダーは Managed Extensibility Framework (MEF) コンポーネントのパーツであり、ソースとコントローラーのクラスをエクスポートし、サービスとブローカーをインポートし <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> ます。たとえば、テキストバッファー内を移動できるようにしたり、 <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker> 署名ヘルプセッションをトリガーするを使用したりします。  
  
 このチュートリアルでは、ハードコーディングされた識別子のセットのシグネチャヘルプを実装する方法について説明します。 完全な実装では、言語がそのコンテンツを提供する必要があります。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
## <a name="creating-a-mef-project"></a>MEF プロジェクトの作成  
  
#### <a name="to-create-a-mef-project"></a>MEF プロジェクトを作成するには  
  
1. C# VSIX プロジェクトを作成します。 ([ **新しいプロジェクト** ] ダイアログで、[Visual C#]、[ **拡張機能**]、[ **VSIX プロジェクト**] の順に選択します)。ソリューションにという名前を指定 `SignatureHelpTest` します。  
  
2. エディター分類子項目テンプレートをプロジェクトに追加します。 詳細については、「 [エディター項目テンプレートを使用した拡張機能の作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。  
  
3. 既存のクラス ファイルを削除します。  
  
4. 次の参照をプロジェクトに追加し、 **CopyLocal** がに設定されていることを確認し `false` ます。  
  
     VisualStudio  
  
     Microsoft.VisualStudio.Language.Intellisense  
  
     Microsoft.VisualStudio.OLE.Interop  
  
     VisualStudio. 14.0  
  
     VisualStudio。相互運用  
  
## <a name="implementing-signature-help-signatures-and-parameters"></a>シグネチャのヘルプ署名とパラメーターの実装  
 シグネチャヘルプソースはを実装する署名に基づいて <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature> おり、それぞれにを実装するパラメーターが含まれてい <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> ます。 完全な実装では、この情報は言語ドキュメントから取得されますが、この例では、署名はハードコーディングされています。  
  
#### <a name="to-implement-the-signature-help-signatures-and-parameters"></a>署名のヘルプ署名とパラメーターを実装するには  
  
1. クラス ファイルを追加し、その名前を `SignatureHelpSource`にします。  
  
2. 次のインポートを追加します。  
  
     [!code-csharp[VSSDKSignatureHelpTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#1)]
     [!code-vb[VSSDKSignatureHelpTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#1)]  
  
3. を実装するという名前のクラスを追加 `TestParameter` <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> します。  
  
     [!code-csharp[VSSDKSignatureHelpTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#2)]
     [!code-vb[VSSDKSignatureHelpTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#2)]  
  
4. すべてのプロパティを設定するコンストラクターを追加します。  
  
     [!code-csharp[VSSDKSignatureHelpTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#3)]
     [!code-vb[VSSDKSignatureHelpTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#3)]  
  
5. のプロパティを追加 <xref:Microsoft.VisualStudio.Language.Intellisense.IParameter> します。  
  
     [!code-csharp[VSSDKSignatureHelpTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#4)]
     [!code-vb[VSSDKSignatureHelpTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#4)]  
  
6. を実装するという名前のクラスを追加 `TestSignature` <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature> します。  
  
     [!code-csharp[VSSDKSignatureHelpTest#5](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#5)]
     [!code-vb[VSSDKSignatureHelpTest#5](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#5)]  
  
7. いくつかのプライベートフィールドを追加します。  
  
     [!code-csharp[VSSDKSignatureHelpTest#6](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#6)]
     [!code-vb[VSSDKSignatureHelpTest#6](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#6)]  
  
8. フィールドを設定し、イベントをサブスクライブするコンストラクターを追加し <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> ます。  
  
     [!code-csharp[VSSDKSignatureHelpTest#7](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#7)]
     [!code-vb[VSSDKSignatureHelpTest#7](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#7)]  
  
9. イベントを宣言 `CurrentParameterChanged` します。 このイベントは、ユーザーが署名のパラメーターの1つを入力したときに発生します。  
  
     [!code-csharp[VSSDKSignatureHelpTest#8](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#8)]
     [!code-vb[VSSDKSignatureHelpTest#8](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#8)]  
  
10. プロパティ <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.CurrentParameter%2A> 値が変更されたときにイベントを発生させるように、プロパティを実装し `CurrentParameterChanged` ます。  
  
     [!code-csharp[VSSDKSignatureHelpTest#9](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#9)]
     [!code-vb[VSSDKSignatureHelpTest#9](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#9)]  
  
11. イベントを発生させるメソッドを追加 `CurrentParameterChanged` します。  
  
     [!code-csharp[VSSDKSignatureHelpTest#10](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#10)]
     [!code-vb[VSSDKSignatureHelpTest#10](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#10)]  
  
12. のコンマの数をシグネチャのコンマの数と比較して、現在のパラメーターを計算するメソッドを追加し <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> ます。  
  
     [!code-csharp[VSSDKSignatureHelpTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#11)]
     [!code-vb[VSSDKSignatureHelpTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#11)]  
  
13. メソッドを呼び出すイベントのイベントハンドラーを追加 <xref:Microsoft.VisualStudio.Text.ITextBuffer.Changed> `ComputeCurrentParameter()` します。  
  
     [!code-csharp[VSSDKSignatureHelpTest#12](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#12)]
     [!code-vb[VSSDKSignatureHelpTest#12](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#12)]  
  
14. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignature.ApplicableToSpan%2A> プロパティを実装します。 このプロパティは、 <xref:Microsoft.VisualStudio.Text.ITrackingSpan> 署名が適用されるバッファー内のテキストの範囲に対応するを保持します。  
  
     [!code-csharp[VSSDKSignatureHelpTest#13](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#13)]
     [!code-vb[VSSDKSignatureHelpTest#13](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#13)]  
  
15. 他のパラメーターを実装します。  
  
     [!code-csharp[VSSDKSignatureHelpTest#14](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#14)]
     [!code-vb[VSSDKSignatureHelpTest#14](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#14)]  
  
## <a name="implementing-the-signature-help-source"></a>シグネチャヘルプソースの実装  
 署名ヘルプソースは、情報を提供するための一連の署名です。  
  
#### <a name="to-implement-the-signature-help-source"></a>シグネチャヘルプソースを実装するには  
  
1. を実装するという名前のクラスを追加 `TestSignatureHelpSource` <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource> します。  
  
     [!code-csharp[VSSDKSignatureHelpTest#15](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#15)]
     [!code-vb[VSSDKSignatureHelpTest#15](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#15)]  
  
2. テキストバッファーへの参照を追加します。  
  
     [!code-csharp[VSSDKSignatureHelpTest#16](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#16)]
     [!code-vb[VSSDKSignatureHelpTest#16](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#16)]  
  
3. テキストバッファーとシグネチャヘルプソースプロバイダーを設定するコンストラクターを追加します。  
  
     [!code-csharp[VSSDKSignatureHelpTest#17](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#17)]
     [!code-vb[VSSDKSignatureHelpTest#17](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#17)]  
  
4. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.AugmentSignatureHelpSession%2A> メソッドを実装します。 この例では、署名はハードコーディングされていますが、完全な実装では、言語ドキュメントからこの情報を取得します。  
  
     [!code-csharp[VSSDKSignatureHelpTest#18](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#18)]
     [!code-vb[VSSDKSignatureHelpTest#18](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#18)]  
  
5. ヘルパーメソッド `CreateSignature()` は、説明のためだけに用意されています。  
  
     [!code-csharp[VSSDKSignatureHelpTest#19](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#19)]
     [!code-vb[VSSDKSignatureHelpTest#19](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#19)]  
  
6. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSource.GetBestMatch%2A> メソッドを実装します。 この例では、2つのシグネチャがあり、それぞれに2つのパラメーターがあります。 したがって、このメソッドは必要ありません。 複数のシグネチャヘルプソースを使用できる完全な実装では、このメソッドを使用して、優先順位の高いシグネチャのヘルプソースが一致する署名を提供できるかどうかを判断します。 そうでない場合、メソッドは null を返し、優先度の高い次のソースが一致を指定するように求められます。  
  
     [!code-csharp[VSSDKSignatureHelpTest#20](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#20)]
     [!code-vb[VSSDKSignatureHelpTest#20](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#20)]  
  
7. Dispose () メソッドを実装します。  
  
     [!code-csharp[VSSDKSignatureHelpTest#21](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#21)]
     [!code-vb[VSSDKSignatureHelpTest#21](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#21)]  
  
## <a name="implementing-the-signature-help-source-provider"></a>シグネチャヘルプソースプロバイダーの実装  
 シグネチャヘルプソースプロバイダーは、Managed Extensibility Framework (MEF) コンポーネントのエクスポートと、シグネチャヘルプソースのインスタンス化を担当します。  
  
#### <a name="to-implement-the-signature-help-source-provider"></a>シグネチャヘルプソースプロバイダーを実装するには  
  
1. を実装するという名前のクラスを追加 `TestSignatureHelpSourceProvider` <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider> し、 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> 、、 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "Text"、および <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> Before = "default" を使用してエクスポートします。  
  
     [!code-csharp[VSSDKSignatureHelpTest#22](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#22)]
     [!code-vb[VSSDKSignatureHelpTest#22](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#22)]  
  
2. <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpSourceProvider.TryCreateSignatureHelpSource%2A>をインスタンス化することによってを実装し `TestSignatureHelpSource` ます。  
  
     [!code-csharp[VSSDKSignatureHelpTest#23](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#23)]
     [!code-vb[VSSDKSignatureHelpTest#23](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#23)]  
  
## <a name="implementing-the-command-handler"></a>コマンドハンドラーの実装  
 シグネチャヘルプは、通常、(文字によって) 文字によってトリガーされます。 これらのキーストロークは、を実装することによって処理でき <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ます。これにより、(前に知られたメソッド名の前にある文字の前にある文字) を受け取ったときに署名ヘルプセッションがトリガーされ、文字を受け取ったときにセッションが破棄されます。  
  
#### <a name="to-implement-the-command-handler"></a>コマンドハンドラーを実装するには  
  
1. を実装するという名前のクラスを追加 `TestSignatureHelpCommand` <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> します。  
  
     [!code-csharp[VSSDKSignatureHelpTest#24](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#24)]
     [!code-vb[VSSDKSignatureHelpTest#24](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#24)]  
  
2. アダプターのプライベートフィールドを追加します <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> (コマンドハンドラーをコマンドハンドラーのチェーンに追加することができます)、テキストビュー、署名ヘルプブローカーとセッション、、、およびを追加し <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigator> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> ます。  
  
     [!code-csharp[VSSDKSignatureHelpTest#25](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#25)]
     [!code-vb[VSSDKSignatureHelpTest#25](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#25)]  
  
3. これらのフィールドを初期化するコンストラクターを追加し、コマンドフィルターをコマンドフィルターのチェーンに追加します。  
  
     [!code-csharp[VSSDKSignatureHelpTest#26](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#26)]
     [!code-vb[VSSDKSignatureHelpTest#26](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#26)]  
  
4. メソッドを実装して、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> コマンドフィルターが (既知のメソッド名の1つの後の文字) を受け取ったときに、セッションがアクティブな状態のままであることを確認するために、署名ヘルプセッションを開始します。 いずれの場合も、コマンドは転送されます。  
  
     [!code-csharp[VSSDKSignatureHelpTest#27](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#27)]
     [!code-vb[VSSDKSignatureHelpTest#27](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#27)]  
  
5. メソッドを実装して、 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 常にコマンドを転送するようにします。  
  
     [!code-csharp[VSSDKSignatureHelpTest#28](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#28)]
     [!code-vb[VSSDKSignatureHelpTest#28](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#28)]  
  
## <a name="implementing-the-signature-help-command-provider"></a>Signature Help Command プロバイダーの実装  
 署名のヘルプコマンドを提供するには、 <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> テキストビューが作成されたときにコマンドハンドラーをインスタンス化するを実装します。  
  
#### <a name="to-implement-the-signature-help-command-provider"></a>Signature Help command プロバイダーを実装するには  
  
1. を実装し、、、 `TestSignatureHelpController` およびと共にエクスポートするという名前のクラスを追加し <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> <xref:Microsoft.VisualStudio.Utilities.NameAttribute> <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> ます。  
  
     [!code-csharp[VSSDKSignatureHelpTest#29](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#29)]
     [!code-vb[VSSDKSignatureHelpTest#29](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#29)]  
  
2. (オブジェクトを取得するために使用される)、( <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> <xref:Microsoft.VisualStudio.Text.Editor.ITextView> 現在の単語を検索するために <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> 使用される)、および <xref:Microsoft.VisualStudio.Language.Intellisense.ISignatureHelpBroker> (シグネチャヘルプセッションをトリガーする) をインポートします。  
  
     [!code-csharp[VSSDKSignatureHelpTest#30](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#30)]
     [!code-vb[VSSDKSignatureHelpTest#30](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#30)]  
  
3. <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener.VsTextViewCreated%2A>をインスタンス化して、メソッドを実装し `TestSignatureCommandHandler` ます。  
  
     [!code-csharp[VSSDKSignatureHelpTest#31](../snippets/csharp/VS_Snippets_VSSDK/vssdksignaturehelptest/cs/signaturehelpsource.cs#31)]
     [!code-vb[VSSDKSignatureHelpTest#31](../snippets/visualbasic/VS_Snippets_VSSDK/vssdksignaturehelptest/vb/signaturehelpsource.vb#31)]  
  
## <a name="building-and-testing-the-code"></a>コードのビルドとテスト  
 このコードをテストするには、SignatureHelpTest ソリューションをビルドし、実験用インスタンスで実行します。  
  
#### <a name="to-build-and-test-the-signaturehelptest-solution"></a>SignatureHelpTest ソリューションをビルドしてテストするには  
  
1. ソリューションをビルドします。  
  
2. デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 つ目のインスタンスがインスタンス化されます。  
  
3. テキストファイルを作成し、"add" という語と左かっこを含むテキストを入力します。  
  
4. 始めかっこを入力すると、メソッドの2つのシグネチャの一覧を示すツールヒントが表示され `add()` ます。  
  
## <a name="see-also"></a>参照  
 [チュートリアル: コンテンツの種類とファイル名拡張子とをリンクさせる](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)

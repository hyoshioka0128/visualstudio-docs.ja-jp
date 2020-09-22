---
title: 'チュートリアル: QuickInfo ツールヒントの表示 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - QuickInfo
ms.assetid: 23fb8384-4f12-446f-977f-ce7910347947
caps.latest.revision: 28
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3b349f0293071dfa30677b7558ca93985d16d55e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841833"
---
# <a name="walkthrough-displaying-quickinfo-tooltips"></a>チュートリアル: クイック ヒントの表示
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

QuickInfo は、ユーザーがメソッド名の上にポインターを移動したときに、メソッドのシグネチャと説明を表示する IntelliSense 機能です。 Quickinfo などの言語ベースの機能を実装するには、QuickInfo の説明を提供する識別子を定義した後、コンテンツを表示するためのツールヒントを作成します。 言語サービスのコンテキストで QuickInfo を定義することも、独自のファイル名の拡張子とコンテンツの種類を定義し、その種類のクイックヒントを表示することもできます。または、既存のコンテンツの種類 ("text" など) の QuickInfo を表示することもできます。 このチュートリアルでは、"text" コンテンツタイプの QuickInfo を表示する方法について説明します。  
  
 このチュートリアルの QuickInfo の例では、ユーザーがポインターをメソッド名の上に移動したときにツールヒントを表示します。 この設計では、次の4つのインターフェイスを実装する必要があります。  
  
- ソースインターフェイス  
  
- ソースプロバイダーインターフェイス  
  
- コントローラーインターフェイス  
  
- コントローラープロバイダーインターフェイス  
  
  ソースプロバイダーとコントローラープロバイダーは、Managed Extensibility Framework (MEF) コンポーネントのパーツであり、ソースとコントローラーのクラスのエクスポートと、ツールヒントテキストバッファーを作成するなどのサービスおよびブローカーのインポート、 <xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService> および QuickInfo セッションを開始するの役割を担い <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker> ます。  
  
  この例では、QuickInfo ソースはメソッド名と説明のハードコーディングされたリストを使用しますが、完全な実装では、言語サービスと言語ドキュメントがそのコンテンツを提供する役割を担います。  
  
## <a name="prerequisites"></a>前提条件  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
## <a name="creating-a-mef-project"></a>MEF プロジェクトの作成  
  
#### <a name="to-create-a-mef-project"></a>MEF プロジェクトを作成するには  
  
1. C# VSIX プロジェクトを作成します。 ([ **新しいプロジェクト** ] ダイアログで、[Visual C#]、[ **拡張機能**]、[ **VSIX プロジェクト**] の順に選択します)。ソリューションにという名前を指定 `QuickInfoTest` します。  
  
2. エディター分類子項目テンプレートをプロジェクトに追加します。 詳細については、「 [エディター項目テンプレートを使用した拡張機能の作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。  
  
3. 既存のクラス ファイルを削除します。  
  
## <a name="implementing-the-quickinfo-source"></a>QuickInfo ソースの実装  
 QuickInfo ソースは、識別子とその説明のセットを収集し、いずれかの識別子が検出されたときに、ツールヒントテキストバッファーにコンテンツを追加します。 この例では、識別子とその説明がソースコンストラクターに追加されています。  
  
#### <a name="to-implement-the-quickinfo-source"></a>QuickInfo ソースを実装するには  
  
1. クラス ファイルを追加し、その名前を `TestQuickInfoSource`にします。  
  
2. VisualStudio への参照を追加します。  
  
3. 次のインポートを追加します。  
  
     [!code-csharp[VSSDKQuickInfoTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#1)]
     [!code-vb[VSSDKQuickInfoTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#1)]  
  
4. を実装するクラスを宣言 <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource> し、という名前を指定 `TestQuickInfoSource` します。  
  
     [!code-csharp[VSSDKQuickInfoTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#2)]
     [!code-vb[VSSDKQuickInfoTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#2)]  
  
5. QuickInfo ソースプロバイダー、テキストバッファー、および一連のメソッド名とメソッドシグネチャのフィールドを追加します。 この例では、メソッド名とシグネチャがコンストラクターで初期化され `TestQuickInfoSource` ます。  
  
     [!code-csharp[VSSDKQuickInfoTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#3)]
     [!code-vb[VSSDKQuickInfoTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#3)]  
  
6. QuickInfo ソースプロバイダーとテキストバッファーを設定するコンストラクターを追加し、メソッド名、メソッドのシグネチャ、および説明を設定します。  
  
     [!code-csharp[VSSDKQuickInfoTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#4)]
     [!code-vb[VSSDKQuickInfoTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#4)]  
  
7. <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource.AugmentQuickInfoSession%2A> メソッドを実装します。 この例では、メソッドは、現在の単語を検索します。カーソルが行またはテキストバッファーの末尾にある場合は、前の単語を検索します。 Word がメソッド名の1つである場合、そのメソッド名の説明は QuickInfo コンテンツに追加されます。  
  
     [!code-csharp[VSSDKQuickInfoTest#5](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#5)]
     [!code-vb[VSSDKQuickInfoTest#5](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#5)]  
  
8. でを実装するため、Dispose () メソッドも実装する必要があり <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource> <xref:System.IDisposable> ます。  
  
     [!code-csharp[VSSDKQuickInfoTest#6](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#6)]
     [!code-vb[VSSDKQuickInfoTest#6](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#6)]  
  
## <a name="implementing-a-quickinfo-source-provider"></a>QuickInfo ソースプロバイダーの実装  
 QuickInfo ソースのプロバイダーは、主に MEF コンポーネントパーツとしてエクスポートし、QuickInfo ソースをインスタンス化します。 MEF コンポーネント部分であるため、他の MEF コンポーネントパーツをインポートできます。  
  
#### <a name="to-implement-a-quickinfo-source-provider"></a>QuickInfo ソースプロバイダーを実装するには  
  
1. を実装するという名前の QuickInfo ソースプロバイダーを宣言 `TestQuickInfoSourceProvider` <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider> し、 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> "ToolTip quickinfo Source"、 <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> Before = "default"、および "text" のを使用してエクスポートし <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> ます。  
  
     [!code-csharp[VSSDKQuickInfoTest#7](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#7)]
     [!code-vb[VSSDKQuickInfoTest#7](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#7)]  
  
2. 2つのエディターサービス ( <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> と <xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService> ) をのプロパティとしてインポートし `TestQuickInfoSourceProvider` ます。  
  
     [!code-csharp[VSSDKQuickInfoTest#8](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#8)]
     [!code-vb[VSSDKQuickInfoTest#8](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#8)]  
  
3. を実装して <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider.TryCreateQuickInfoSource%2A> 、新しいを返し `TestQuickInfoSource` ます。  
  
     [!code-csharp[VSSDKQuickInfoTest#9](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#9)]
     [!code-vb[VSSDKQuickInfoTest#9](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#9)]  
  
## <a name="implementing-a-quickinfo-controller"></a>QuickInfo コントローラーの実装  
 Quickinfo コントローラーは、QuickInfo をいつ表示するかを決定します。 この例では、メソッド名のいずれかに対応する単語の上にポインターを置いたときに、QuickInfo が表示されます。 QuickInfo コントローラーは、QuickInfo セッションをトリガーするマウスホバーイベントハンドラーを実装します。  
  
#### <a name="to-implement-a-quickinfo-controller"></a>QuickInfo コントローラーを実装するには  
  
1. を実装するクラスを宣言 <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController> し、という名前を指定 `TestQuickInfoController` します。  
  
     [!code-csharp[VSSDKQuickInfoTest#10](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#10)]
     [!code-vb[VSSDKQuickInfoTest#10](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#10)]  
  
2. テキストビューのプライベートフィールド、テキストビューで表されるテキストバッファー、QuickInfo セッション、および QuickInfo コントローラープロバイダーを追加します。  
  
     [!code-csharp[VSSDKQuickInfoTest#11](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#11)]
     [!code-vb[VSSDKQuickInfoTest#11](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#11)]  
  
3. フィールドを設定し、マウスのホバーイベントハンドラーを追加するコンストラクターを追加します。  
  
     [!code-csharp[VSSDKQuickInfoTest#12](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#12)]
     [!code-vb[VSSDKQuickInfoTest#12](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#12)]  
  
4. QuickInfo セッションを開始するマウスホバーイベントハンドラーを追加します。  
  
     [!code-csharp[VSSDKQuickInfoTest#13](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#13)]
     [!code-vb[VSSDKQuickInfoTest#13](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#13)]  
  
5. <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.Detach%2A>コントロールがテキストビューからデタッチされたときにマウスホバーイベントハンドラーが削除されるように、メソッドを実装します。  
  
     [!code-csharp[VSSDKQuickInfoTest#14](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#14)]
     [!code-vb[VSSDKQuickInfoTest#14](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#14)]  
  
6. <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.ConnectSubjectBuffer%2A>この例では、メソッドと <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.DisconnectSubjectBuffer%2A> メソッドを空のメソッドとして実装します。  
  
     [!code-csharp[VSSDKQuickInfoTest#15](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#15)]
     [!code-vb[VSSDKQuickInfoTest#15](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#15)]  
  
## <a name="implementing-the-quickinfo-controller-provider"></a>QuickInfo コントローラープロバイダーの実装  
 QuickInfo コントローラーのプロバイダーは、主に MEF コンポーネントパーツとしてエクスポートし、QuickInfo コントローラーをインスタンス化します。 MEF コンポーネント部分であるため、他の MEF コンポーネントパーツをインポートできます。  
  
#### <a name="to-implement-the-quickinfo-controller-provider"></a>QuickInfo コントローラープロバイダーを実装するには  
  
1. を実装するという名前のクラスを宣言 `TestQuickInfoControllerProvider` <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseControllerProvider> し、 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> "ToolTip quickinfo Controller" と "text" のを使用してエクスポートし <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> ます。  
  
     [!code-csharp[VSSDKQuickInfoTest#16](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#16)]
     [!code-vb[VSSDKQuickInfoTest#16](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#16)]  
  
2. <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker> をプロパティとしてインポートします。  
  
     [!code-csharp[VSSDKQuickInfoTest#17](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#17)]
     [!code-vb[VSSDKQuickInfoTest#17](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#17)]  
  
3. QuickInfo コントローラーをインスタンス化して、メソッドを実装し <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseControllerProvider.TryCreateIntellisenseController%2A> ます。  
  
     [!code-csharp[VSSDKQuickInfoTest#18](../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs#18)]
     [!code-vb[VSSDKQuickInfoTest#18](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb#18)]  
  
## <a name="building-and-testing-the-code"></a>コードのビルドとテスト  
 このコードをテストするには、QuickInfoTest ソリューションをビルドし、実験用インスタンスで実行します。  
  
#### <a name="to-build-and-test-the-quickinfotest-solution"></a>QuickInfoTest ソリューションをビルドしてテストするには  
  
1. ソリューションをビルドします。  
  
2. デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 つ目のインスタンスがインスタンス化されます。  
  
3. テキストファイルを作成し、"add" と "減算" という単語を含むテキストを入力します。  
  
4. "Add" のいずれかの位置にポインターを移動します。 メソッドの署名と説明が `add` 表示されます。  
  
## <a name="see-also"></a>参照  
 [チュートリアル: コンテンツの種類とファイル名拡張子とをリンクさせる](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)

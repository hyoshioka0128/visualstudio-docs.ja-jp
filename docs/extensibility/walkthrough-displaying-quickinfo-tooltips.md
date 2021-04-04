---
title: 'チュートリアル: QuickInfo ツールヒントの表示 |Microsoft Docs'
description: このチュートリアルを使用して、テキストコンテンツの QuickInfo を表示する方法について説明します。 [QuickInfo] メソッド名のメソッドシグネチャと説明を表示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - QuickInfo
ms.assetid: 23fb8384-4f12-446f-977f-ce7910347947
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- csharp
- vb
ms.openlocfilehash: d374aa41d85b1d64b6623cb99f6183787a2afc53
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217256"
---
# <a name="walkthrough-display-quickinfo-tooltips"></a>チュートリアル: QuickInfo ツールヒントの表示
QuickInfo は、ユーザーがメソッド名の上にポインターを移動したときに、メソッドのシグネチャと説明を表示する IntelliSense 機能です。 Quickinfo などの言語ベースの機能を実装するには、QuickInfo の説明を提供する識別子を定義した後、コンテンツを表示するためのツールヒントを作成します。 言語サービスのコンテキストで QuickInfo を定義することも、独自のファイル名の拡張子とコンテンツの種類を定義し、その種類のクイックヒントを表示することもできます。または、既存のコンテンツの種類 ("text" など) の QuickInfo を表示することもできます。 このチュートリアルでは、"text" コンテンツタイプの QuickInfo を表示する方法について説明します。

 このチュートリアルの QuickInfo の例では、ユーザーがポインターをメソッド名の上に移動したときにツールヒントを表示します。 この設計では、次の4つのインターフェイスを実装する必要があります。

- ソースインターフェイス

- ソースプロバイダーインターフェイス

- コントローラーインターフェイス

- コントローラープロバイダーインターフェイス

  ソースプロバイダーとコントローラープロバイダーは、Managed Extensibility Framework (MEF) コンポーネントのパーツであり、ソースとコントローラーのクラスのエクスポートと、ツールヒントテキストバッファーを作成するなどのサービスおよびブローカーのインポート、 <xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService> および QuickInfo セッションを開始するの役割を担い <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker> ます。

  この例では、QuickInfo ソースはメソッド名と説明のハードコーディングされたリストを使用しますが、完全な実装では、言語サービスと言語ドキュメントがそのコンテンツを提供する役割を担います。

## <a name="prerequisites"></a>前提条件
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールする必要はありません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-mef-project"></a>MEF プロジェクトを作成する

### <a name="to-create-a-mef-project"></a>MEF プロジェクトを作成するには

1. C# VSIX プロジェクトを作成します。 ([ **新しいプロジェクト** ] ダイアログで、[Visual C#]、[ **拡張機能**]、[ **VSIX プロジェクト**] の順に選択します)。ソリューションにという名前を指定 `QuickInfoTest` します。

2. エディター分類子項目テンプレートをプロジェクトに追加します。 詳細については、「 [エディター項目テンプレートを使用して拡張機能を作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)する」を参照してください。

3. 既存のクラス ファイルを削除します。

## <a name="implement-the-quickinfo-source"></a>QuickInfo ソースを実装する
 QuickInfo ソースは、識別子とその説明のセットを収集し、いずれかの識別子が検出されたときに、ツールヒントテキストバッファーにコンテンツを追加します。 この例では、識別子とその説明がソースコンストラクターに追加されています。

#### <a name="to-implement-the-quickinfo-source"></a>QuickInfo ソースを実装するには

1. クラス ファイルを追加し、その名前を `TestQuickInfoSource`にします。

2. *VisualStudio* への参照を追加します。

3. 次のインポートを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet1":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet1":::

4. を実装するクラスを宣言 <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource> し、という名前を指定 `TestQuickInfoSource` します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet2":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet2":::

5. QuickInfo ソースプロバイダー、テキストバッファー、および一連のメソッド名とメソッドシグネチャのフィールドを追加します。 この例では、メソッド名とシグネチャがコンストラクターで初期化され `TestQuickInfoSource` ます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet3":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet3":::

6. QuickInfo ソースプロバイダーとテキストバッファーを設定するコンストラクターを追加し、メソッド名、メソッドのシグネチャ、および説明を設定します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet4":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet4":::

7. <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource.AugmentQuickInfoSession%2A> メソッドを実装します。 この例では、メソッドは、現在の単語を検索します。カーソルが行またはテキストバッファーの末尾にある場合は、前の単語を検索します。 Word がメソッド名の1つである場合、そのメソッド名の説明は QuickInfo コンテンツに追加されます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet5":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet5":::

8. でを実装するため、Dispose () メソッドも実装する必要があり <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSource> <xref:System.IDisposable> ます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet6":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet6":::

## <a name="implement-a-quickinfo-source-provider"></a>QuickInfo ソースプロバイダーを実装する
 QuickInfo ソースのプロバイダーは、主に MEF コンポーネントパーツとしてエクスポートし、QuickInfo ソースをインスタンス化します。 MEF コンポーネント部分であるため、他の MEF コンポーネントパーツをインポートできます。

#### <a name="to-implement-a-quickinfo-source-provider"></a>QuickInfo ソースプロバイダーを実装するには

1. を実装するという名前の QuickInfo ソースプロバイダーを宣言 `TestQuickInfoSourceProvider` <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider> し、 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> "ToolTip quickinfo Source"、 <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> Before = "default"、および "text" のを使用してエクスポートし <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> ます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet7":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet7":::

2. 2つのエディターサービス ( <xref:Microsoft.VisualStudio.Text.Operations.ITextStructureNavigatorSelectorService> と <xref:Microsoft.VisualStudio.Text.ITextBufferFactoryService> ) をのプロパティとしてインポートし `TestQuickInfoSourceProvider` ます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet8":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet8":::

3. を実装して <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoSourceProvider.TryCreateQuickInfoSource%2A> 、新しいを返し `TestQuickInfoSource` ます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet9":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet9":::

## <a name="implement-a-quickinfo-controller"></a>QuickInfo コントローラーを実装する
 Quickinfo コントローラーは、QuickInfo がいつ表示されるかを決定します。 この例では、メソッド名のいずれかに対応する単語の上にポインターを置いたときに、QuickInfo と表示されます。 QuickInfo コントローラーは、QuickInfo セッションをトリガーするマウスホバーイベントハンドラーを実装します。

### <a name="to-implement-a-quickinfo-controller"></a>QuickInfo コントローラーを実装するには

1. を実装するクラスを宣言 <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController> し、という名前を指定 `TestQuickInfoController` します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet10":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet10":::

2. テキストビューのプライベートフィールド、テキストビューで表されるテキストバッファー、QuickInfo セッション、および QuickInfo コントローラープロバイダーを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet11":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet11":::

3. フィールドを設定し、マウスのホバーイベントハンドラーを追加するコンストラクターを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet12":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet12":::

4. QuickInfo セッションを開始するマウスホバーイベントハンドラーを追加します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet13":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet13":::

5. <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.Detach%2A>コントロールがテキストビューからデタッチされたときにマウスホバーイベントハンドラーが削除されるように、メソッドを実装します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet14":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet14":::

6. <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.ConnectSubjectBuffer%2A>この例では、メソッドと <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseController.DisconnectSubjectBuffer%2A> メソッドを空のメソッドとして実装します。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet15":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet15":::

## <a name="implementing-the-quickinfo-controller-provider"></a>QuickInfo コントローラープロバイダーの実装
 QuickInfo コントローラーのプロバイダーは、主に MEF コンポーネントパーツとしてエクスポートし、QuickInfo コントローラーをインスタンス化します。 MEF コンポーネント部分であるため、他の MEF コンポーネントパーツをインポートできます。

### <a name="to-implement-the-quickinfo-controller-provider"></a>QuickInfo コントローラープロバイダーを実装するには

1. を実装するという名前のクラスを宣言 `TestQuickInfoControllerProvider` <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseControllerProvider> し、 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> "ToolTip quickinfo Controller" と "text" のを使用してエクスポートし <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> ます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet16":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet16":::

2. <xref:Microsoft.VisualStudio.Language.Intellisense.IQuickInfoBroker> をプロパティとしてインポートします。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet17":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet17":::

3. QuickInfo コントローラーをインスタンス化して、メソッドを実装し <xref:Microsoft.VisualStudio.Language.Intellisense.IIntellisenseControllerProvider.TryCreateIntellisenseController%2A> ます。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkquickinfotest/vb/testquickinfosource.vb" id="Snippet18":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkquickinfotest/cs/testquickinfosource.cs" id="Snippet18":::

## <a name="build-and-test-the-code"></a>コードをビルドしてテストする
 このコードをテストするには、QuickInfoTest ソリューションをビルドし、実験用インスタンスで実行します。

### <a name="to-build-and-test-the-quickinfotest-solution"></a>QuickInfoTest ソリューションをビルドしてテストするには

1. ソリューションをビルドします。

2. デバッガーでこのプロジェクトを実行すると、Visual Studio の2番目のインスタンスが開始されます。

3. テキストファイルを作成し、"add" と "減算" という単語を含むテキストを入力します。

4. "Add" のいずれかの位置にポインターを移動します。 メソッドの署名と説明が `add` 表示されます。

## <a name="see-also"></a>関連項目
- [チュートリアル: コンテンツの種類をファイル名拡張子にリンクする](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)

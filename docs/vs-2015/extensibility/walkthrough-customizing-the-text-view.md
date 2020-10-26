---
title: 'チュートリアル: テキストビューのカスタマイズ |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - customizing the view
ms.assetid: 32d32ac8-22ff-4de7-af69-bd46ec4ad9bf
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e96bb177d3cfa90b2c80304eabfd93d1bea76d5b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202025"
---
# <a name="walkthrough-customizing-the-text-view"></a>チュートリアル: テキスト ビューのカスタマイズ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

テキストビューをカスタマイズするには、エディターで次のいずれかのプロパティを変更します。  
  
- インジケーター マージン  
  
- 挿入キャレット  
  
- キャレットの上書き  
  
- 選択されたテキスト  
  
- アクティブでない選択されたテキスト (フォーカスが失われたテキスト)  
  
- 参照可能な空白  
  
## <a name="prerequisites"></a>必須コンポーネント  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
## <a name="creating-a-mef-project"></a>MEF プロジェクトの作成  
  
1. C# VSIX プロジェクトを作成します。 ([ **新しいプロジェクト** ] ダイアログで、[Visual C#]、[ **拡張機能**]、[ **VSIX プロジェクト**] の順に選択します)。ソリューションにという名前を指定 `ViewPropertyTest` します。  
  
2. エディター分類子項目テンプレートをプロジェクトに追加します。 詳細については、「 [エディター項目テンプレートを使用した拡張機能の作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。  
  
3. 既存のクラス ファイルを削除します。  
  
## <a name="defining-the-content-type"></a>コンテンツの種類の定義  
  
1. クラス ファイルを追加し、その名前を `ViewPropertyModifier`にします。  
  
2. 次の `using` ディレクティブを追加します。  
  
    [!code-csharp[VSSDKViewPropertyTest#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkviewpropertytest/cs/viewpropertymodifier.cs#1)]
    [!code-vb[VSSDKViewPropertyTest#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkviewpropertytest/vb/viewpropertymodifier.vb#1)]  
  
3. を継承するという名前のクラスを宣言 `TestViewCreationListener` <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener> します。 次の属性を使用して、このクラスをエクスポートします。  
  
   - <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> このリスナーが適用されるコンテンツの種類を指定します。  
  
   - <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> このリスナーのロールを指定します。  
  
     [!code-csharp[VSSDKViewPropertyTest#2](../snippets/csharp/VS_Snippets_VSSDK/vssdkviewpropertytest/cs/viewpropertymodifier.cs#2)]
     [!code-vb[VSSDKViewPropertyTest#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkviewpropertytest/vb/viewpropertymodifier.vb#2)]  
  
4. このクラスで、をインポートし <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService> ます。  
  
    [!code-csharp[VSSDKViewPropertyTest#3](../snippets/csharp/VS_Snippets_VSSDK/vssdkviewpropertytest/cs/viewpropertymodifier.cs#3)]
    [!code-vb[VSSDKViewPropertyTest#3](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkviewpropertytest/vb/viewpropertymodifier.vb#3)]  
  
## <a name="changing-the-view-properties"></a>ビューのプロパティの変更  
  
1. ビューを <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> 開いたときにビューのプロパティが変更されるように、メソッドを実装します。 この変更を行うには、まず、 <xref:System.Windows.ResourceDictionary> 検索するビューの側面に対応するを見つけます。 次に、リソースディクショナリで適切なプロパティを変更し、プロパティを設定します。 <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.SetProperties%2A>プロパティを設定する前にメソッドを呼び出し、プロパティを設定した後にを呼び出すことによって、メソッドへの呼び出しをバッチ処理し <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.BeginBatchUpdate%2A> <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.EndBatchUpdate%2A> ます。  
  
     [!code-csharp[VSSDKViewPropertyTest#4](../snippets/csharp/VS_Snippets_VSSDK/vssdkviewpropertytest/cs/viewpropertymodifier.cs#4)]
     [!code-vb[VSSDKViewPropertyTest#4](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkviewpropertytest/vb/viewpropertymodifier.vb#4)]  
  
## <a name="building-and-testing-the-code"></a>コードのビルドとテスト  
  
1. ソリューションをビルドします。  
  
     デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 つ目のインスタンスがインスタンス化されます。  
  
2. テキスト ファイルを作成し、いくつかのテキストを入力します。  
  
    - 挿入キャレットはマゼンタで、上書きキャレットは水色である必要があります。  
  
    - インジケーターマージン (テキストビューの左側) は明るい緑にする必要があります。  
  
3. 入力したテキストを選択します。 選択したテキストの色は薄いピンクにする必要があります。  
  
4. テキストが選択された状態で、テキストウィンドウの外側の任意の場所をクリックします。 選択したテキストの色は濃いピンクにする必要があります。  
  
5. 参照可能な空白を有効にします。 ([ **編集** ] メニューの [ **詳細設定** ] をポイントし、[ **空白の表示**] をクリックします)。 テキストにいくつかのタブを入力します。 タブを表す赤色の矢印が表示されます。  
  
## <a name="see-also"></a>参照  
 [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)

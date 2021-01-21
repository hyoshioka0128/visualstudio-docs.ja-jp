---
title: 'チュートリアル: テキストビューのカスタマイズ |Microsoft Docs'
description: このチュートリアルを使用して、エディターでいくつかのプロパティを変更し、テキストビューをカスタマイズする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - customizing the view
ms.assetid: 32d32ac8-22ff-4de7-af69-bd46ec4ad9bf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 057e2a68e1d9a130f69441d8aec4b6a7fe0249e9
ms.sourcegitcommit: dd96a95d87a039525aac86abe689c30e2073ae87
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2021
ms.locfileid: "97862967"
---
# <a name="walkthrough-customize-the-text-view"></a>チュートリアル: テキストビューのカスタマイズ
テキストビューをカスタマイズするには、エディターで次のいずれかのプロパティを変更します。

- インジケーター マージン

- 挿入キャレット

- キャレットの上書き

- 選択されたテキスト

- アクティブでない選択されたテキスト (フォーカスが失われたテキスト)

- 参照可能な空白

## <a name="prerequisites"></a>前提条件
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-mef-project"></a>MEF プロジェクトを作成する

1. C# VSIX プロジェクトを作成します。 ([ **新しいプロジェクト** ] ダイアログで、[Visual C#]、[ **拡張機能**]、[ **VSIX プロジェクト**] の順に選択します)。ソリューションにという名前を指定 `ViewPropertyTest` します。

2. エディター分類子項目テンプレートをプロジェクトに追加します。 詳細については、「 [エディター項目テンプレートを使用して拡張機能を作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)する」を参照してください。

3. 既存のクラス ファイルを削除します。

## <a name="define-the-content-type"></a>コンテンツの種類を定義する

1. クラス ファイルを追加し、その名前を `ViewPropertyModifier`にします。

2. 次の `using` ディレクティブを追加します。

    [!code-csharp[VSSDKViewPropertyTest#1](../extensibility/codesnippet/CSharp/walkthrough-customizing-the-text-view_1.cs)]
    [!code-vb[VSSDKViewPropertyTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-customizing-the-text-view_1.vb)]

3. を継承するという名前のクラスを宣言 `TestViewCreationListener` <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener> します。 次の属性を使用して、このクラスをエクスポートします。

   - <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> このリスナーが適用されるコンテンツの種類を指定します。

   - <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> このリスナーのロールを指定します。

     [!code-csharp[VSSDKViewPropertyTest#2](../extensibility/codesnippet/CSharp/walkthrough-customizing-the-text-view_2.cs)]
     [!code-vb[VSSDKViewPropertyTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-customizing-the-text-view_2.vb)]

4. このクラスで、をインポートし <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService> ます。

    [!code-csharp[VSSDKViewPropertyTest#3](../extensibility/codesnippet/CSharp/walkthrough-customizing-the-text-view_3.cs)]
    [!code-vb[VSSDKViewPropertyTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-customizing-the-text-view_3.vb)]

## <a name="change-the-view-properties"></a>ビューのプロパティを変更する

1. ビューを <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> 開いたときにビューのプロパティが変更されるように、メソッドを設定します。 この変更を行うには、まず、 <xref:System.Windows.ResourceDictionary> 検索するビューの側面に対応するを見つけます。 次に、リソースディクショナリで適切なプロパティを変更し、プロパティを設定します。 <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.SetProperties%2A>プロパティを設定する前にメソッドを呼び出し、プロパティを設定した後にを呼び出すことによって、メソッドへの呼び出しをバッチ処理し <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.BeginBatchUpdate%2A> <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.EndBatchUpdate%2A> ます。

     [!code-csharp[VSSDKViewPropertyTest#4](../extensibility/codesnippet/CSharp/walkthrough-customizing-the-text-view_4.cs)]
     [!code-vb[VSSDKViewPropertyTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-customizing-the-text-view_4.vb)]

## <a name="build-and-test-the-code"></a>コードをビルドしてテストする

1. ソリューションをビルドします。

     デバッガーでこのプロジェクトを実行すると、Visual Studio の2番目のインスタンスが開始されます。

2. テキスト ファイルを作成し、いくつかのテキストを入力します。

    - 挿入キャレットはマゼンタで、上書きキャレットは水色である必要があります。

    - インジケーターマージン (テキストビューの左側) は明るい緑にする必要があります。

3. 入力したテキストを選択します。 選択したテキストの色は薄いピンクにする必要があります。

4. テキストが選択された状態で、テキストウィンドウの外側の任意の場所をクリックします。 選択したテキストの色は濃いピンクにする必要があります。

5. 参照可能な空白を有効にします。 ([ **編集** ] メニューの [ **詳細設定** ] をポイントし、[ **空白の表示**] をクリックします)。 テキストにいくつかのタブを入力します。 タブを表す赤色の矢印が表示されます。

## <a name="see-also"></a>関連項目
- [言語サービスとエディターの拡張点](../extensibility/language-service-and-editor-extension-points.md)

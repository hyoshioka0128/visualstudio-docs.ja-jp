---
title: 'チュートリアル: テキスト ビューをカスタマイズする |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - customizing the view
ms.assetid: 32d32ac8-22ff-4de7-af69-bd46ec4ad9bf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9d99f9201761bbe079c34ccf61339158863509dd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697466"
---
# <a name="walkthrough-customize-the-text-view"></a>チュートリアル: テキスト ビューをカスタマイズする
テキスト ビューをカスタマイズするには、エディタ形式マップで次のプロパティのいずれかを変更します。

- インジケーター マージン

- 挿入カレット

- カレットの上書き

- 選択したテキスト

- 選択したテキスト (フォーカスが失われた選択したテキスト) が無効になっています。

- 可視空白

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-mef-project"></a>MEF プロジェクトを作成する

1. C# VSIX プロジェクトを作成します。 ([**新しいプロジェクト**] ダイアログで、[**ビジュアル C# / 拡張性**] を選択し、次に**VSIX プロジェクト**を選択します)。ソリューションに名前`ViewPropertyTest`を付ける:

2. エディター分類子項目テンプレートをプロジェクトに追加します。 詳細については、「[エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)」を参照してください。

3. 既存のクラス ファイルを削除します。

## <a name="define-the-content-type"></a>コンテンツ タイプの定義

1. クラス ファイルを追加し、その名前を `ViewPropertyModifier`にします。

2. 次の `using` ディレクティブを追加します。

    [!code-csharp[VSSDKViewPropertyTest#1](../extensibility/codesnippet/CSharp/walkthrough-customizing-the-text-view_1.cs)]
    [!code-vb[VSSDKViewPropertyTest#1](../extensibility/codesnippet/VisualBasic/walkthrough-customizing-the-text-view_1.vb)]

3. から<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener>継承するクラス`TestViewCreationListener`を宣言します。 このクラスを次の属性でエクスポートします。

   - <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute>をクリックして、このリスナーが適用されるコンテンツの種類を指定します。

   - <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute>をクリックして、このリスナーのロールを指定します。

     [!code-csharp[VSSDKViewPropertyTest#2](../extensibility/codesnippet/CSharp/walkthrough-customizing-the-text-view_2.cs)]
     [!code-vb[VSSDKViewPropertyTest#2](../extensibility/codesnippet/VisualBasic/walkthrough-customizing-the-text-view_2.vb)]

4. このクラスでは、 を<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService>インポートします。

    [!code-csharp[VSSDKViewPropertyTest#3](../extensibility/codesnippet/CSharp/walkthrough-customizing-the-text-view_3.cs)]
    [!code-vb[VSSDKViewPropertyTest#3](../extensibility/codesnippet/VisualBasic/walkthrough-customizing-the-text-view_3.vb)]

## <a name="change-the-view-properties"></a>ビューのプロパティを変更する

1. ビューを<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A>開いたときにビュープロパティが変更されるようにメソッドを設定します。 変更を行う場合は、まず<xref:System.Windows.ResourceDictionary>、検索するビューの側面に対応する を見つけます。 次に、リソース ディクショナリの適切なプロパティを変更し、プロパティを設定します。 プロパティを設定する前<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.SetProperties%2A>にメソッドを<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.BeginBatchUpdate%2A>呼び出し、プロパティを設定した後<xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.EndBatchUpdate%2A>で、メソッドの呼び出しをバッチ処理します。

     [!code-csharp[VSSDKViewPropertyTest#4](../extensibility/codesnippet/CSharp/walkthrough-customizing-the-text-view_4.cs)]
     [!code-vb[VSSDKViewPropertyTest#4](../extensibility/codesnippet/VisualBasic/walkthrough-customizing-the-text-view_4.vb)]

## <a name="build-and-test-the-code"></a>コードのビルドとテスト

1. ソリューションをビルドします。

     デバッガーでこのプロジェクトを実行すると、Visual Studio の 2 番目のインスタンスが起動します。

2. テキスト ファイルを作成し、いくつかのテキストを入力します。

    - 挿入キャレットはマゼンタにする必要があり、上書きキャレットはターコイズでなければなりません。

    - インジケーターの余白 (テキスト ビューの左側) は明るい緑色にする必要があります。

3. 入力したテキストを選択します。 選択したテキストの色は薄いピンク色にする必要があります。

4. テキストが選択されているときに、テキスト ウィンドウの外側の任意の場所をクリックします。 選択したテキストの色は濃いピンク色にする必要があります。

5. 表示される空白をオンにします。 ([**編集**] メニューの [**詳細設定]** をポイントし、[**ホワイト スペースの表示**] をクリックします。 テキストにタブをいくつか入力します。 タブを表す赤い矢印が表示されます。

## <a name="see-also"></a>関連項目
- [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)

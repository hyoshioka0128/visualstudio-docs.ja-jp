---
title: エディター項目テンプレートを使用した拡張機能の作成 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: fa3b993b-ab95-47fa-a38b-b788f3a5b2d8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7ac19d99bf75c79ad011bfd0d5a56ecf3880b100
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739506"
---
# <a name="create-an-extension-with-an-editor-item-template"></a>エディター項目テンプレートを使用して拡張機能を作成する
Visual Studio SDK に含まれている項目テンプレートを使用して、分類子、表示要素、およびマージンをエディターに追加する基本的なエディター拡張機能を作成できます。 エディター項目テンプレートは、Visual C# または Visual Basic VSIX プロジェクトで使用できます。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-classifier-extension"></a>分類子拡張の作成
 エディター分類子項目テンプレートは、任意のテキスト ファイル内の適切なテキスト (この場合は、すべて) を色分けするエディター分類子を作成します。

1. [**新しいプロジェクト**] ダイアログ ボックスで **、[Visual C#** ] または **[Visual Basic]** を展開し、[**機能拡張**] をクリックします。 [**テンプレート]** ペインで **、[VSIX プロジェクト**] を選択します。 **[名前]** ボックスに「`TestClassifier`」と入力します。 **[OK]** をクリックします。

2. ソリューション**エクスプローラ**で、プロジェクト ノードを右クリックし、[**Add** > **新しい項目**の追加] を選択します。 [Visual C#**拡張機能**] ノードに移動し、[**エディター分類子**] を選択します。 既定のファイル名 (*EditorClassifier1.cs*) のままにします。

3. 次の 4 つのコード ファイルがあります。

    - *EditorClassifier1.cs*クラスが`EditorClassifier1`含まれています。

    - *EditorClassifier1ClassificationDefinition.cs*クラスが`EditorClassifier1ClassificationDefinition`含まれています。

    - *EditorClassifier1Format.cs*クラスが`EditorClassifier1Format`含まれています。

    - *EditorClassifier1Provider.cs*クラスが`EditorClassifier1Provider`含まれています。

4. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。

     テキスト ファイルを開くと、すべてのテキストに紫色の背景が下線が付きます。

## <a name="create-a-text-relative-adornment-extension"></a>テキスト相対表示要素の拡張を作成する
 エディタ テキスト表示要素テンプレートは、赤いアウトラインと青の背景を持つボックスを使用してテキスト文字 'a' のすべてのインスタンスを装飾するテキスト相対表示要素を作成します。 このテキストは、移動または再フォーマットされた場合でも、ボックスが常に 'a' 文字を重ねるので、テキスト相対です。

1. [**新しいプロジェクト**] ダイアログ ボックスで **、[Visual C#** ] または **[Visual Basic]** を展開し、[**機能拡張**] をクリックします。 [**テンプレート]** ペインで **、[VSIX プロジェクト**] を選択します。 **[名前]** ボックスに「`TestAdornment`」と入力します。 **[OK]** をクリックします。

2. ソリューション**エクスプローラ**で、プロジェクト ノードを右クリックし、[**Add** > **新しい項目**の追加] を選択します。 [Visual C#**拡張機能**] ノードに移動し、[**エディター テキスト表示要素]** を選択します。 既定のファイル名 (*TextAdornment1.cs/vb*) のままにします。

3. 次の 2 つのコード ファイルがあります。

    - *TextAdornment1.cs*クラスが`TextAdornment1`含まれています。

    - *TextAdornment1TextViewCreationListener.cs*クラスが`TextAdornment1TextViewCreationListener`含まれています。

4. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。 テキスト ファイルを開くと、テキスト内のすべての 'a' 文字が青い背景に赤で囲まれます。

## <a name="create-a-viewport-relative-adornment-extension"></a>ビューポート相対表示要素の拡張を作成する
 エディタ ビューポート表示要素テンプレートは、ビューポートの右上隅に赤いアウトラインを持つ紫色のボックスを追加するビューポート相対表示要素を作成します。

> [!NOTE]
> **ビューポート**は、現在表示されているテキスト ビューの領域です。

### <a name="to-create-a-viewport-adornment-extension-by-using-the-editor-viewport-adornment-template"></a>エディタ ビューポート表示要素テンプレートを使用してビューポート表示要素の拡張機能を作成するには

1. [**新しいプロジェクト**] ダイアログ ボックスで **、[Visual C#** ] または **[Visual Basic]** を展開し、[**機能拡張**] をクリックします。 [**テンプレート]** ペインで **、[VSIX プロジェクト**] を選択します。 **[名前]** ボックスに「`ViewportAdornment`」と入力します。 **[OK]** をクリックします。

2. ソリューション**エクスプローラ**で、プロジェクト ノードを右クリックし、[**Add** > **新しい項目**の追加] を選択します。 [Visual C#**拡張機能**] ノードに移動し、[**エディター ビューポート表示要素]** を選択します。 既定のファイル名 (*ViewportAdornment1.cs/vb*) のままにします。

3. 次の 2 つのコード ファイルがあります。

    - *ViewportAdornment1.cs*クラスが`ViewportAdornment1`含まれています。

    - *ViewportAdornment1TextViewCreationListener.cs*クラスを`ViewportAdornment1TextViewCreationListener`含む

4. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。 新しいテキスト ファイルを作成すると、ビューポートの右上隅に赤いアウトラインの紫色のボックスが表示されます。

## <a name="create-a-margin-extension"></a>余白の拡張機能を作成する
 エディタマージンテンプレートは、*こんにちは世界という言葉と一緒に表示される緑のマージンを作成*します!* 水平スクロール バーの下に移動します。

### <a name="to-create-a-margin-extension-by-using-the-editor-margin-template"></a>[エディター余白] テンプレートを使用して余白の拡張機能を作成するには

1. [**新しいプロジェクト**] ダイアログ ボックスで **、[Visual C#** ] または **[Visual Basic]** を展開し、[**機能拡張**] をクリックします。 [**テンプレート]** ペインで **、[VSIX プロジェクト**] を選択します。 **[名前]** ボックスに「`MarginExtension`」と入力します。 **[OK]** をクリックします。

2. ソリューション**エクスプローラ**で、プロジェクト ノードを右クリックし、[**Add** > **新しい項目**の追加] を選択します。 [Visual C#**拡張機能**] ノードに移動し、[**エディターの余白**] を選択します。 既定のファイル名 (EditorMargin1.cs/vb) のままにします。

3. 次の 2 つのコード ファイルがあります。

    - *EditorMargin1.cs*にはクラス`EditorMargin1`が含まれています。

    - *EditorMargin1Factory.cs*クラスが`EditorMargin1Factory`含まれています。

4. このプロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。 テキスト ファイルを開くと、水平スクロール バーの下に **"Hello EditorMargin1"** という単語が表示される緑色の余白が表示されます。

## <a name="see-also"></a>関連項目
- [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)

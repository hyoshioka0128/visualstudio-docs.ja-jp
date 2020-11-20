---
title: エディター項目テンプレートを使用して拡張機能を作成する |Microsoft Docs
description: Visual Studio SDK の項目テンプレートを使用して、分類子、装飾、および余白をエディターに追加する基本的なエディター拡張機能を作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: fa3b993b-ab95-47fa-a38b-b788f3a5b2d8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e6264cb35e404d69900094513875fc7b79310a4d
ms.sourcegitcommit: 5027eb5c95e1d2da6d08d208fd6883819ef52d05
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2020
ms.locfileid: "94973746"
---
# <a name="create-an-extension-with-an-editor-item-template"></a>エディター項目テンプレートを使用して拡張機能を作成する
Visual Studio SDK に含まれている項目テンプレートを使用して、エディターに分類子、装飾、および余白を追加する基本的なエディター拡張機能を作成できます。 エディター項目テンプレートは、Visual C# または Visual Basic VSIX プロジェクトで使用できます。

## <a name="prerequisites"></a>前提条件
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-classifier-extension"></a>分類子拡張機能を作成する
 エディター分類子項目テンプレートは、任意のテキストファイル内の適切なテキスト (この場合はすべて) に色を色付けするエディター分類子を作成します。

1. [ **新しいプロジェクト** ] ダイアログボックスで、 **[Visual C#** ] または [ **Visual Basic** を展開し、[ **機能拡張**] をクリックします。 [ **テンプレート** ] ペインで、[ **VSIX プロジェクト**] を選択します。 **[名前]** ボックスに「 `TestClassifier`」と入力します。 **[OK]** をクリックします。

2. **ソリューションエクスプローラー** で、プロジェクトノードを右クリックし、[新しい項目の **追加**] を選択し  >  **New Item** ます。 Visual C# の **機能拡張** ノードにアクセスし、[ **エディター分類子**] を選択します。 既定のファイル名 (*EditorClassifier1.cs*) をそのまま使用します。

3. 次の4つのコードファイルがあります。

    - *EditorClassifier1.cs* にはクラスが含まれてい `EditorClassifier1` ます。

    - *EditorClassifier1ClassificationDefinition.cs* にはクラスが含まれてい `EditorClassifier1ClassificationDefinition` ます。

    - *EditorClassifier1Format.cs* にはクラスが含まれてい `EditorClassifier1Format`  ます。

    - *EditorClassifier1Provider.cs* にはクラスが含まれてい `EditorClassifier1Provider` ます。

4. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。

     テキストファイルを開くと、すべてのテキストに紫色の背景が下線付きで表示されます。

## <a name="create-a-text-relative-adornment-extension"></a>テキスト相対の表示要素の拡張機能を作成する
 エディターのテキストの表示要素テンプレートでは、赤いアウトラインと青の背景を持つボックスを使用して、テキスト文字 "a" のすべてのインスタンスを装飾するテキスト相対の表示要素を作成します。 ボックスは、移動または再フォーマットされるときでも、常に ' a ' 文字をオーバーレイするので、テキスト相対です。

1. [ **新しいプロジェクト** ] ダイアログボックスで、 **[Visual C#** ] または [ **Visual Basic** を展開し、[ **機能拡張**] をクリックします。 [ **テンプレート** ] ペインで、[ **VSIX プロジェクト**] を選択します。 **[名前]** ボックスに「 `TestAdornment`」と入力します。 **[OK]** をクリックします。

2. **ソリューションエクスプローラー** で、プロジェクトノードを右クリックし、[新しい項目の **追加**] を選択し  >  **New Item** ます。 Visual C# の **機能拡張** ノードにアクセスし、[ **エディターテキスト** の表示要素] を選択します。 既定のファイル名 (*TextAdornment1.cs/vb*) をそのまま使用します。

3. 次の2つのコードファイルがあります。

    - *TextAdornment1.cs* にはクラスが含まれてい `TextAdornment1` ます。

    - *TextAdornment1TextViewCreationListener.cs* にはクラスが含まれてい `TextAdornment1TextViewCreationListener` ます。

4. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。 テキストファイルを開くと、テキスト内のすべての ' a ' 文字が青い背景に対して赤で囲まれて表示されます。

## <a name="create-a-viewport-relative-adornment-extension"></a>ビューポート相対装飾拡張機能を作成する
 エディタービューポートの参照要素テンプレートによって、ビューポートの相対参照ポイントが作成されます。これにより、ビューポートの右上隅に赤いアウトラインの紫色のボックスが追加されます。

> [!NOTE]
> **ビューポート** は、現在表示されているテキストビューの領域です。

### <a name="to-create-a-viewport-adornment-extension-by-using-the-editor-viewport-adornment-template"></a>エディタービューポートの装飾テンプレートを使用してビューポートの装飾拡張機能を作成するには

1. [ **新しいプロジェクト** ] ダイアログボックスで、 **[Visual C#** ] または [ **Visual Basic** を展開し、[ **機能拡張**] をクリックします。 [ **テンプレート** ] ペインで、[ **VSIX プロジェクト**] を選択します。 **[名前]** ボックスに「 `ViewportAdornment`」と入力します。 **[OK]** をクリックします。

2. **ソリューションエクスプローラー** で、プロジェクトノードを右クリックし、[新しい項目の **追加**] を選択し  >  **New Item** ます。 Visual C# の **機能拡張** ノードにアクセスし、[ **エディタービューポート**] 表示要素を選択します。 既定のファイル名 (*ViewportAdornment1.cs/vb*) をそのまま使用します。

3. 次の2つのコードファイルがあります。

    - *ViewportAdornment1.cs* にはクラスが含まれてい `ViewportAdornment1` ます。

    - *ViewportAdornment1TextViewCreationListener.cs* クラスを含む `ViewportAdornment1TextViewCreationListener`

4. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。 新しいテキストファイルを作成すると、ビューポートの右上隅に赤色の枠線が表示されます。

## <a name="create-a-margin-extension"></a>余白拡張機能を作成する
 エディターの余白テンプレートによって、"*Hello world!* " という単語と共に表示される緑の余白が作成されます。 水平スクロールバーの下。

### <a name="to-create-a-margin-extension-by-using-the-editor-margin-template"></a>[エディターの余白テンプレートを使用して余白の拡張機能を作成するには

1. [ **新しいプロジェクト** ] ダイアログボックスで、 **[Visual C#** ] または [ **Visual Basic** を展開し、[ **機能拡張**] をクリックします。 [ **テンプレート** ] ペインで、[ **VSIX プロジェクト**] を選択します。 **[名前]** ボックスに「 `MarginExtension`」と入力します。 **[OK]** をクリックします。

2. **ソリューションエクスプローラー** で、プロジェクトノードを右クリックし、[新しい項目の **追加**] を選択し  >  **New Item** ます。 Visual C# の **機能拡張** ノードにアクセスし、[ **エディターの余白**] を選択します。 既定のファイル名 (EditorMargin1.cs/vb) をそのまま使用します。

3. 次の2つのコードファイルがあります。

    - *EditorMargin1.cs* にはクラスが含まれてい `EditorMargin1` ます。

    - *EditorMargin1Factory.cs* にはクラスが含まれてい `EditorMargin1Factory` ます。

4. このプロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。 テキストファイルを開いた場合、水平スクロールバーの下に " **Hello EditorMargin1** " という単語がある緑の余白が表示されます。

## <a name="see-also"></a>関連項目
- [言語サービスとエディターの拡張点](../extensibility/language-service-and-editor-extension-points.md)

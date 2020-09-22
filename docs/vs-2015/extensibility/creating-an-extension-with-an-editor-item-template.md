---
title: エディター項目テンプレートを使用して拡張機能を作成する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: fa3b993b-ab95-47fa-a38b-b788f3a5b2d8
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 46ccdd87d44ee90c925992f4d7b997c9bbe09684
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842253"
---
# <a name="creating-an-extension-with-an-editor-item-template"></a>エディターの項目テンプレートを使用した拡張機能の作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio SDK に含まれている項目テンプレートを使用して、エディターに分類子、装飾、および余白を追加する基本的なエディター拡張機能を作成できます。 エディター項目テンプレートは、Visual C# または Visual Basic VSIX プロジェクトで使用できます。  
  
## <a name="prerequisites"></a>前提条件  
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
## <a name="creating-a-classifier-extension"></a>分類子拡張機能の作成  
 エディター分類子項目テンプレートは、任意のテキストファイル内の適切なテキスト (この場合はすべて) に色を色付けするエディター分類子を作成します。  
  
1. [ **新しいプロジェクト** ] ダイアログボックスで、 **[Visual C#** ] または [ **Visual Basic** を展開し、[ **機能拡張**] をクリックします。 [ **テンプレート** ] ペインで、[ **VSIX プロジェクト**] を選択します。 **[名前]** ボックスに「 `TestClassifier`」と入力します。 **[OK]** をクリックします。  
  
2. **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[追加]、[**新しい項目**] の順に選択します。 Visual C# の **機能拡張** ノードにアクセスし、[ **エディター分類子**] を選択します。 既定のファイル名 (EditorClassifier1.cs) をそのまま使用します。  
  
3. 次の3つのコードファイルがあります。  
  
    - EditorClassifier1.cs にはクラスが含まれてい `EditorClassifier1` ます。  
  
    - EditorClassifier1ClassificationDefinition.cs にはクラスが含まれてい `OEditorClassifier1ClassificationDefinition` ます。  
  
    - EditorClassifier1Format.cs にはクラスが含まれてい `EditorClassifier1Format`  ます。  
  
    - EditorClassifier1Provider.cs にはクラスが含まれてい `EditorClassifier1Provider` ます。  
  
4. プロジェクトをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されます。  
  
     テキストファイルを開くと、すべてのテキストに紫色の背景が下線付きで表示されます。  
  
## <a name="creating-a-text-relative-adornment-extension"></a>テキストを基準とした表示要素の拡張機能の作成  
 エディターのテキストの表示要素テンプレートでは、赤いアウトラインと青の背景を持つボックスを使用して、テキスト文字 "a" のすべてのインスタンスを装飾するテキスト相対の表示要素を作成します。 ボックスは、移動または再フォーマットされるときでも、常に ' a ' 文字をオーバーレイするので、テキスト相対です。  
  
1. [ **新しいプロジェクト** ] ダイアログボックスで、 **[Visual C#** ] または [ **Visual Basic** を展開し、[ **機能拡張**] をクリックします。 [ **テンプレート** ] ペインで、[ **VSIX プロジェクト**] を選択します。 **[名前]** ボックスに「 `TestAdornment`」と入力します。 **[OK]** をクリックします。  
  
2. **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[追加]、[**新しい項目**] の順に選択します。 Visual C# の **機能拡張** ノードにアクセスし、[ **エディターテキスト**の表示要素] を選択します。 既定のファイル名 (TextAdornment1.cs/vb) をそのまま使用します。  
  
3. 次の2つのコードファイルがあります。  
  
    - TextAdornment1.cs にはクラスが含まれてい `TextAdornment1` ます。  
  
    - extAdornment1TextViewCreationListener.cs にはクラスが含まれてい `TextAdornment1TextViewCreationListener` ます。  
  
4. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。 テキストファイルを開くと、テキスト内のすべての ' a ' 文字が青い背景に対して赤で囲まれて表示されます。  
  
## <a name="creating-a-viewport-relative-adornment-extension"></a>ビューポート相対参照要素拡張の作成  
 エディタービューポートの参照要素テンプレートによって、ビューポートの相対参照ポイントが作成されます。これにより、ビューポートの右上隅に赤いアウトラインの紫色のボックスが追加されます。  
  
> [!NOTE]
> *ビューポート*は、現在表示されているテキストビューの領域です。  
  
#### <a name="to-create-a-viewport-adornment-extension-by-using-the-editor-viewport-adornment-template"></a>エディタービューポートの装飾テンプレートを使用してビューポートの装飾拡張機能を作成するには  
  
1. [ **新しいプロジェクト** ] ダイアログボックスで、 **[Visual C#** ] または [ **Visual Basic** を展開し、[ **機能拡張**] をクリックします。 [ **テンプレート** ] ペインで、[ **VSIX プロジェクト**] を選択します。 **[名前]** ボックスに「 `ViewportAdornment`」と入力します。 **[OK]** をクリックします。  
  
2. **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[追加]、[**新しい項目**] の順に選択します。 Visual C# の **機能拡張** ノードにアクセスし、[ **エディタービューポート**] 表示要素を選択します。 既定のファイル名 (ViewportAdornment1.cs/vb) をそのまま使用します。  
  
3. 次の2つのコードファイルがあります。  
  
    - ViewportAdornment1.cs にはクラスが含まれてい `ViewportAdornment1` ます。  
  
    - ViewportAdornment1TextViewCreationListener.cs クラスを含む `ViewportAdornment1TextViewCreationListener`  
  
4. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。 新しいテキストファイルを作成すると、ビューポートの右上隅に赤色の枠線が表示されます。  
  
## <a name="creating-a-margin-extension"></a>余白拡張機能の作成  
 エディターの余白テンプレートによって、"Hello world!" という単語と共に表示される緑色の余白が作成されます。 水平スクロールバーの下。  
  
#### <a name="to-create-a-margin-extension-by-using-the-editor-margin-template"></a>[エディターの余白テンプレートを使用して余白の拡張機能を作成するには  
  
1. [ **新しいプロジェクト** ] ダイアログボックスで、 **[Visual C#** ] または [ **Visual Basic** を展開し、[ **機能拡張**] をクリックします。 [ **テンプレート** ] ペインで、[ **VSIX プロジェクト**] を選択します。 **[名前]** ボックスに「 `MarginExtension`」と入力します。 **[OK]** をクリックします。  
  
2. **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[追加]、[**新しい項目**] の順に選択します。 Visual C# の **機能拡張** ノードにアクセスし、[ **エディタービューポート**] 表示要素を選択します。 既定のファイル名 (EditorMargin1.cs/vb) をそのまま使用します。  
  
3. 次の2つのコードファイルがあります。  
  
    - EditorMargin1.cs にはクラスが含まれてい `EditorMargin1` ます。  
  
    - EditorMargin1Factory.cs にはクラスが含まれてい `EditorMargin1Factory` ます。  
  
4. このプロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。 テキストファイルを開くと、水平スクロールバーの下に "Hello EditorMargin1" という単語を含む緑色の余白が表示されます。  
  
## <a name="see-also"></a>参照  
 [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)

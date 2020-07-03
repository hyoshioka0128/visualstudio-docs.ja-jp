---
title: ツールウィンドウを使用した拡張機能の作成 |Microsoft Docs
ms.date: 3/16/2019
ms.topic: how-to
ms.assetid: 585b0a3a-f85b-4f92-81bb-9ca499bb8a89
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 597b84854dd398abee9dc21090e085273bc94c75
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903893"
---
# <a name="create-an-extension-with-a-tool-window"></a>ツールウィンドウで拡張機能を作成する

この手順では、VSIX プロジェクトテンプレートと**カスタムツールウィンドウ**項目テンプレートを使用して、ツールウィンドウで拡張機能を作成する方法について説明します。

## <a name="prerequisites"></a>必須コンポーネント

 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

### <a name="create-a-tool-window"></a>ツールウィンドウを作成する

1. **Firstwindow**という名前の VSIX プロジェクトを作成します。 VSIX プロジェクトテンプレートは、"vsix" を検索することで、[**新しいプロジェクト**] ダイアログで見つけることができます。

2. プロジェクトが開いたら、 **Mywindow**という名前のツールウィンドウ項目テンプレートを追加します。 **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[新しい項目の**追加**] を選択し  >  **New Item**ます。 [**新しい項目の追加**] ダイアログで、[ **Visual C#** の機能拡張] にアクセスし、  >  **Extensibility** [**カスタムツールウィンドウ**] を選択します。 ウィンドウの下部にある [**名前**] フィールドで、ツールウィンドウのファイル名を*MyWindow.cs*に変更します。

3. プロジェクトをビルドし、デバッグを開始します。

   Visual Studio の実験用インスタンスが表示されます。 実験用インスタンスの詳細については、[実験用インスタンス](../extensibility/the-experimental-instance.md)を参照してください。

4. 実験用インスタンスで、[ **View**  >  **他のウィンドウの**表示] にアクセスします。

   **Mywindow**のメニュー項目が表示するはずです。 このボタンをクリックします。

   **Mywindow**というタイトルのツールウィンドウと、 **[click Me!** ] ボタンが表示されます。

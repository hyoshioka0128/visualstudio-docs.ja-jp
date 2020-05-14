---
title: ツール ウィンドウを使用した拡張機能の作成 |マイクロソフトドキュメント
ms.date: 3/16/2019
ms.topic: conceptual
ms.assetid: 585b0a3a-f85b-4f92-81bb-9ca499bb8a89
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 17f72cf130c5ff0f2d6d03ca8c460aa98ea39111
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739543"
---
# <a name="create-an-extension-with-a-tool-window"></a>ツール ウィンドウを使用して拡張機能を作成する

この手順では、VSIX プロジェクト テンプレートと**カスタム ツール ウィンドウ**項目テンプレートを使用して、ツール ウィンドウを使用して拡張機能を作成する方法について説明します。

## <a name="prerequisites"></a>必須コンポーネント

 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

### <a name="create-a-tool-window"></a>ツール ウィンドウを作成する

1. **"FirstWindow"** という名前の VSIX プロジェクトを作成します。 VSIX プロジェクト テンプレートは、"vsix" を検索して **[新しいプロジェクト**] ダイアログで見つけることができます。

2. プロジェクトが開いたら **、MyWindow**という名前のツール ウィンドウ項目テンプレートを追加します。 ソリューション**エクスプローラ**で、プロジェクト ノードを右クリックし、[**Add** > **新しい項目**の追加] を選択します。 [**新しい項目の追加]** ダイアログで **、[Visual C#** > **の機能拡張**] に移動し、[**カスタム ツール ウィンドウ**] をクリックします。 ウィンドウの下部にある [**名前]** フィールドで、ツール ウィンドウのファイル名を*MyWindow.cs*に変更します。

3. プロジェクトをビルドし、デバッグを開始します。

   Visual Studio の実験用インスタンスが表示されます。 実験インスタンスの詳細については、「[実験インスタンス](../extensibility/the-experimental-instance.md)」を参照してください。

4. 実験用の例では、**他のウィンドウ**を**表示** > に移動します。

   **MyWindow**のメニュー項目が表示されます。 このボタンをクリックします。

   MyWindow というタイトルのツール ウィンドウ**MyWindow**と **、[クリックミー]** というボタンが表示されます。

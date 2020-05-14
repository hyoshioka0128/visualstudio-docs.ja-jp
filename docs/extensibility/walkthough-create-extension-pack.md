---
title: 拡張パック項目テンプレートを使用して拡張パックを作成する |マイクロソフトドキュメント
ms.date: 07/27/2018
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: 5388EEBA-211D-4114-8CD9-70C899919F7E
author: acangialosi
ms.author: anthc
manager: Meng
ms.workload:
- vssdk
ms.openlocfilehash: fa1c141e18a3870eaad4b155d816e30ee207f45d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697751"
---
# <a name="walkthrough-create-an-extension-pack"></a>チュートリアル: 拡張機能パックを作成する

拡張パックは、一緒にインストールできる拡張機能のセットです。 エクステンション パックを使用すると、お気に入りの拡張機能を他のユーザーと簡単に共有したり、特定のシナリオで一緒に拡張機能のセットをバンドルしたりできます。

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio 2015 以降、Visual Studio SDK は、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

拡張機能パック機能は、Visual Studio 15.8 プレビュー 2 以降で使用できます。

## <a name="create-an-extension-with-an-extension-pack-item-template"></a>拡張機能パック項目テンプレートを使用して拡張機能を作成する

拡張機能パック項目テンプレートは、一緒にインストールできる一連の拡張機能を含む拡張機能パックを作成します。

1. [**新しいプロジェクト**] ダイアログで、"vsix" を検索し **、[VSIX プロジェクト**] を選択します。 **[プロジェクト名**] に「拡張パックのテスト」と入力します。 **［作成］** を選択します

2. ソリューション**エクスプローラ**で、プロジェクト ノードを右クリックし、[**Add** > **新しい項目**の追加] を選択します。 [Visual C#**拡張機能**] ノードに移動し、[**拡張機能パック**] を選択します。 既定のファイル名 (ExtensionPack1.cs) のままにします。

3. 次のコードを含む拡張パック1.vsextファイルが追加されました

   ```json
   {
    "id": "ExtensionPack1",
    "name": "ExtensionPack1",
    "description": "Read about creating extension packs at https://aka.ms/vsextpack",
    "version": "1.0.0.0",
    "extensions": [  // List of extensions that are included in the Extension Pack.
      {
        "vsixId": "41858b2d-ff0b-4a43-80b0-f1b2d6084935", // The vsix id of the extension you want to   include.
        "name": "AlignAssignments"
      },
      {
          "vsixId": "42374550-426a-400e-96f9-237682e8dea6",
        "name": "CopyAsHtml"
      }
    ]
   }
   ```

4. 拡張機能パックに含める拡張機能の vsixid は[、Visual Studio マーケットプレース](https://marketplace.visualstudio.com/)で見つけることができます。 含める拡張子を探し、[ ID**のコピー**] をクリックします。 上記のファイルの既存の**vsixId**を更新するか、または別の拡張子をリストに追加できます。

    ![マーケットプレースから VsixId をコピーする](media/vsixid-marketplace.png)

5. プロジェクトをビルドし、マーケットプレースに拡張機能をアップロードします。 [「Visual Studio 拡張機能の発行](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)」を参照してください。

> [!NOTE]
> 拡張機能パックは[、Visual Studio マーケットプレース](https://marketplace.visualstudio.com/)または[プライベート ギャラリー](../extensibility/how-to-create-an-atom-feed-for-a-private-gallery.md)で利用可能な拡張機能のみをインストールできます。

## <a name="install-the-extension-pack-from-the-visual-studio-marketplace"></a>拡張機能パックを Visual Studio マーケットプレースからインストールする

拡張機能が発行された後、Visual Studio にインストールして、そこでテストします。

::: moniker range="vs-2017"

1. Visual Studio の [**ツール**] メニューの [**拡張機能と更新プログラム**] をクリックします。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio の [**拡張機能**] メニューの [**マネージ拡張**] をクリックします。

::: moniker-end

2. [**オンライン**] をクリックし、[テスト拡張機能パック] を検索します。

3. **[Download]** をクリックします。 拡張機能パックに含まれる拡張機能とその拡張機能の一覧は、インストールのスケジュールが設定されます。

4. 以下は、[拡張機能の管理] ダイアログのエクステンション パックのダウンロード ビューの例**です**。 拡張パックに含まれている拡張機能の一部のみをインストールする場合は、**インストールのスケジュール済み**で拡張機能の一覧を変更できます。

    ![マーケットプレースからエクステンションパックをダウンロード](media/vside-extensionpack.png)

5. インストールを完了するには、Visual Studio のすべてのインスタンスを閉じます。

## <a name="remove-the-extension"></a>拡張機能を削除する

コンピュータから拡張機能を削除するには、次の手順を実行します。

::: moniker range="vs-2017"

1. Visual Studio の [**ツール**] メニューの [**拡張機能と更新プログラム**] をクリックします。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio の [**拡張機能**] メニューの [**マネージ拡張**] をクリックします。

::: moniker-end

2. [**拡張パックのテスト**] を選択し、[**アンインストール**] をクリックします。 拡張機能パックに含まれる拡張機能とその拡張機能の一覧は、アンインストールのスケジュールが設定されます。

3. アンインストールを完了するには、Visual Studio のすべてのインスタンスを閉じます。

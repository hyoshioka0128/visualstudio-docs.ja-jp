---
title: 拡張パック項目テンプレートを使用して拡張パックを作成する |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80697751"
---
# <a name="walkthrough-create-an-extension-pack"></a>チュートリアル: 拡張機能パックを作成する

拡張パックは、まとめてインストールできる一連の拡張機能です。 拡張パックを使用すると、お気に入りの拡張機能を他のユーザーと簡単に共有したり、特定のシナリオに合わせて一連の拡張機能をバンドルしたりすることができます。

## <a name="prerequisites"></a>前提条件

Visual studio 2015 以降では、visual studio SDK は visual studio セットアップのオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

拡張機能パック機能は、Visual Studio 15.8 Preview 2 以降で使用できます。

## <a name="create-an-extension-with-an-extension-pack-item-template"></a>拡張機能パック項目テンプレートを使用して拡張機能を作成する

拡張パック項目テンプレートは、一連の拡張機能を一緒にインストールできる拡張パックを作成します。

1. [ **新しいプロジェクト** ] ダイアログで、"vsix" を検索し、[ **vsix プロジェクト**] を選択します。 [ **プロジェクト名**] に「Test Extension Pack」と入力します。 **［作成］** を選択します

2. **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[新しい項目の**追加**] を選択し  >  **New Item**ます。 Visual C# の **機能拡張** ノードにアクセスし、[ **拡張機能パック**] を選択します。 既定のファイル名 (ExtensionPack1.cs) をそのまま使用します。

3. 次のコードを含む ExtensionPack1 vsext ファイルが追加されます。

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

4. 拡張パックに含める拡張機能の vsixid は、 [Visual Studio Marketplace](https://marketplace.visualstudio.com/)にあります。 追加する拡張機能を見つけて、[ **コピー ID**] をクリックします。 上記のファイルの既存の **vsixId** を更新することも、一覧に別の拡張子を追加することもできます。

    ![Marketplace から VsixId をコピーする](media/vsixid-marketplace.png)

5. プロジェクトをビルドし、拡張機能を Marketplace にアップロードします。 「 [Visual Studio 拡張機能の発行」を](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)参照してください。

> [!NOTE]
> 拡張パックは、 [Visual Studio Marketplace](https://marketplace.visualstudio.com/) または [プライベートギャラリー](../extensibility/how-to-create-an-atom-feed-for-a-private-gallery.md)で利用できる拡張機能のみをインストールできます。

## <a name="install-the-extension-pack-from-the-visual-studio-marketplace"></a>Visual Studio Marketplace から拡張機能パックをインストールします。

拡張機能が公開されたので、それを Visual Studio にインストールしてテストします。

::: moniker range="vs-2017"

1. Visual Studio の [ **ツール** ] メニューで、[ **拡張機能と更新プログラム**] をクリックします。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio の [ **拡張** 機能] メニューで、[ **マネージ拡張**] をクリックします。

::: moniker-end

2. [ **オンライン** ] をクリックし、"Test Extension Pack" を検索します。

3. **[Download]** をクリックします。 拡張機能と拡張機能パックに含まれている拡張機能の一覧は、インストールのスケジュールが設定されます。

4. 次に、[ **拡張機能の管理** ] ダイアログの拡張機能パックのダウンロードビューの例を示します。 拡張パックに含まれている拡張機能の一部のみをインストールする場合は、[ **インストールのスケジュール**] で拡張機能の一覧を変更できます。

    ![Marketplace から拡張機能パックをダウンロードする](media/vside-extensionpack.png)

5. インストールを完了するには、Visual Studio のすべてのインスタンスを閉じます。

## <a name="remove-the-extension"></a>拡張機能を削除する

コンピューターから拡張機能を削除するには、次のようにします。

::: moniker range="vs-2017"

1. Visual Studio の [ **ツール** ] メニューで、[ **拡張機能と更新プログラム**] をクリックします。

::: moniker-end

::: moniker range=">=vs-2019"

1. Visual Studio の [ **拡張** 機能] メニューで、[ **マネージ拡張**] をクリックします。

::: moniker-end

2. [ **テスト拡張パック** ] を選択し、[ **アンインストール**] をクリックします。 拡張機能と拡張機能パックに含まれている拡張機能の一覧は、アンインストールのスケジュールが設定されます。

3. アンインストールを完了するには、Visual Studio のすべてのインスタンスを閉じます。

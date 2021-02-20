---
title: フォルダーに発行する
ms.date: 01/22/2019
helpviewer_keywords:
- deployment, website
ms.assetid: e963fb4b-6d32-4d45-86bb-ef7e4d3028b0
author: sayedihashimi
ms.author: sayedha
manager: unniravindranathan
ms.prod: visual-studio-mac
ms.topic: how-to
ms.openlocfilehash: 98831768dac9f7e57c1bd5f19f0dc088951a6af4
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2021
ms.locfileid: "98719787"
---
# <a name="publish-a-web-app-to-a-folder-using-visual-studio-for-mac"></a>Visual Studio for Mac を使用してフォルダーに Web アプリを発行する

発行ツールを使用することで、フォルダーに ASP.NET Core アプリを発行することができます。

## <a name="prerequisites"></a>必須コンポーネント

- ASP.NET Core を有効にしてインストールされた [Visual Studio 2017 for Mac](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs4mac2017)。
- ASP.NET Core プロジェクト。 プロジェクトをまだ用意していない場合は、[新しいプロジェクトを作成](./create-new-projects.md?view=vsmac-2017&preserve-view=true)することができます。

## <a name="publish-to-folder"></a>フォルダーに発行する

Visual Studio for Mac では、発行ツールを使用してフォルダーにご利用の ASP.NET Core プロジェクトを発行することができます。 フォルダーに発行したら、ファイルをご利用の Web サーバーに転送して異なる環境に取り込むことができます。 フォルダーに発行するには、次の手順を行います。

 1. Solution Pad で、プロジェクトを右クリックして、 **[発行]** を選択します。

    ![[発行] コンテキスト メニュー](media/publish-context-menu.png)

 2. このプロジェクトが既に発行されている場合は、メニューに発行プロファイルが表示されます。 その発行プロファイルを選択して、発行プロセスを開始します。

 3. このプロジェクトをフォルダーに初めて発行する場合は、 **[Publish to Folder]\(フォルダーに発行する\)** を選択します。

    ![[Publish to Folder]\(フォルダーに発行する\) コンテキスト メニュー](media/publish-to-folder-context-menu.png)

 4. **[Publish to Folder]\(フォルダーに発行する\)** ダイアログが表示されます。 このダイアログでは、プロジェクトの発行先のフォルダーをカスタマイズできます。 **[参照]** ボタンを使用してこれを行うことも、パスに貼り付けることもできます。

 5. **[発行]** をクリックすると、いくつかのことが行われます。 まず、発行プロファイルが作成されます。 発行プロファイルは、発行プロセス中にプロジェクトにインポートされる MSBuild ファイルです。 これには、発行プロセス中に使用されるプロパティが含まれています。 これらのファイルは、`Properties/PublishProfiles` に格納され、拡張子 `.pubxml` が付けられます。 次に、発行プロセスが開始されます。 Visual Studio for Mac のステータス バーを注視することで、進行状況を監視できます。

    ![発行状態が表示されている IDE ステータス バー](media/publish-to-folder-status-bar.png)

 6. 発行が正常に完了すると、発行フォルダーに対して Finder ウィンドウが開きます。 発行プロファイルが作成されたので、[発行] コンテキスト メニューにそれが表示されるようになります。

    ![フォルダー プロファイルを含む [発行] コンテキスト メニュー](media/publish-context-menu-with-folder-profile.png)

 7. 同じ設定を使用してプロジェクトを再び発行するには、[発行] コンテキスト メニューでそのプロファイルをクリックしてください。

## <a name="customize-publish-options"></a>発行オプションのカスタマイズ

発行プロファイル ([発行] コンテキスト メニューに表示される) の名前を変更するには、発行プロファイル ファイルの名前を変更します。 ファイルの拡張子 (`.puxbml`) は決して変更しないでください。

発行フォルダーのパスを変更するには、発行プロファイルを開き、`publishUrl` 値を編集します。

使用されるビルド構成を変更するには、発行プロファイル内の `LastUsedBuildConfiguration` プロパティを変更します。
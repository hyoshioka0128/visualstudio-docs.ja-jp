---
title: Web サイトに発行する
ms.date: 01/29/2019
ms.topic: quickstart
helpviewer_keywords:
- deployment, website
ms.assetid: fc82b1f1-d342-4b82-9a44-590479f0a895
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1236c3057cd209bd5c7c81304a2168704927c506
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "71127930"
---
# <a name="publish-a-web-app-to-a-web-site-using-visual-studio"></a>Visual Studio を使用して Web サイトに Web アプリを発行する

Visual Studio から Web サイトに ASP.NET、ASP.NET Core、.NET Core、および Python アプリを発行するには、 **[発行]** ツールを使用します。 Node.js では、この手順はサポートされていますが、ユーザー インターフェイスが異なります。

[!INCLUDE [quickstart-prereqs](includes/quickstart-prereqs.md)]

> [!NOTE]
> ネットワーク ファイル共有に Windows デスクトップ アプリケーションを発行する必要がある場合、[ClickOnce を使用したデスクトップ アプリの配置](how-to-publish-a-clickonce-application-using-the-publish-wizard.md)に関するページ (C# または Visual Basic) を参照してください。 C++/CLI については、[ClickOnce を使用したネイティブ アプリの配置](/cpp/windows/clickonce-deployment-for-visual-cpp-applications)に関するページを、C/C++ については、[セットアップ プロジェクトを使用したネイティブ アプリの配置](/cpp/windows/walkthrough-deploying-a-visual-cpp-application-by-using-a-setup-project)に関するページを参照してください。

## <a name="publish-to-a-web-site"></a>Web サイトに発行する

1. ソリューション エクスプローラーで、プロジェクトを右クリックして、 **[発行]** を選択します (または **[ビルド]**  >  **[発行]** メニュー項目を使用します)。

    ![ソリューション エクスプローラーのプロジェクト コンテキスト メニューにある [発行] コマンド](../deployment/media/quickstart-publish.png "[発行] を選択する")

1. 以前に発行プロファイルを構成してある場合、 **[発行]** ウィンドウが表示されます。 **[新しいプロファイルの作成]** を選択します。

1. **[発行先を選択]** ダイアログ ボックスで **[IIS、FTP、その他]** を選択します。

    ![IIS や FTP などを選択します。](../deployment/media/quickstart-publish-iis-ftp.png "IIS や FTP などを選択します。")

1. **[発行]** を選びます。 プロファイルの発行設定ダイアログ ボックスが開きます。

    ![フォルダーの選択](../deployment/media/quickstart-publish-settings-web.png "フォルダーの選択")

1. **[発行方法]** フィールドで **[Web 配置]** や **[FTP]** などの方法を選択します。 次に表示される設定は発行方法に対応しています。 Web 配置を使用すると、Web アプリケーションと Web サイトを IIS サーバーの配置が簡単になります。Web 配置はアプリケーションとしてサーバーにインストールする必要があります。 インストールには [Web プラットフォーム インストーラー](https://www.microsoft.com/web/downloads/platform.aspx)を使用します。

1. 発行方法に必要な設定を構成し、 **[接続の検証]** を選択します。 サーバーまたはターゲットを使用可能で、設定が正しい場合、接続が有効であることを示すメッセージが表示されたら、発行することができます。

    ![接続を検証する](../deployment/media/quickstart-publish-web-deploy.png "接続を検証する")

1. **[設定]** を選択して、デバッグまたはリリースの構成を配置するかどうかなどの他の配置設定を構成し、次に **[保存]** を選択します。 リモートでデバッグしている場合は、デバッグ構成が必要です。

1. 発行するには、 **[発行]** を選択します。 [出力] ウィンドウに配置の進行状況と結果が表示されます。

## <a name="next-steps"></a>次の手順

このクイック スタートでは、Visual Studio を使用して発行プロファイルを作成する方法を学習しました。 発行設定をインポートして、発行プロファイルを構成することもできます。

> [!div class="nextstepaction"]
> [発行設定のインポートと IIS へのデプロイ](tutorial-import-publish-settings-iis.md)

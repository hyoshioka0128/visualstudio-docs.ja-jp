---
ms.openlocfilehash: a292b37a50bbf667fa5b23f18879cd79c3f76805
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85292194"
---
ホスティング サーバーの Web 配置 3.6 では、UI から発行設定ファイルの作成を有効にする追加の構成機能を提供しています。

1. Windows Server に Web 配置を既にインストールしている場合は、 **[コントロール パネル]**  >  **[プログラム]**  >  **[プログラムのアンインストール]** を使用してアンインストールします。

2. 次に、Windows Server にホスティング サーバーの Web 配置 3.6 をインストールします。

    ホスティング サーバーの Web 配置をインストールするには、Web Platform Installer (WebPI) を使用します。 (IIS で Web Platform Installer のリンクを見つけるには、サーバー マネージャーの左側のウィンドウで **[IIS]** を選択します。 サーバー ウィンドウで、サーバーを右クリックして **[インターネット インフォメーション サービス (IIS) マネージャー]** を選択します。 次に、 **[アクション]** ウィンドウの **[Get New Web Platform Components] (新しい Web Platform コンポーネントの取得)** リンクをクリックします)。Web Platform Installer (WebPI) は[ダウンロード](https://www.microsoft.com/web/downloads/platform.aspx)から入手することもできます。

    Web Platform Installer の [アプリケーション] タブで、 **[Web Deploy 3.6 for Hosting Servers]\(ホスティング サーバーの Web 配置 3.6\)** を見つけます。

3. **[IIS 管理スクリプトおよびツール]** をまだインストールしていない場合は、今すぐインストールします。

    **[サーバーの役割の選択]**  >  **[Web Server (IIS)]**  >  **[管理ツール]** の順に移動して、 **[IIS 管理スクリプトおよびツール]** の役割を選択し、 **[次へ]** をクリックしてその役割をインストールします。

    ![IIS 管理スクリプトおよびツールのインストール](../../deployment/media/tutorial-iis-management-scripts-and-tools.png)

    発行設定ファイルの作成を有効にするには、このスクリプトとツールが必要です。

4. (省略可能) **[コントロール パネル] > [システムとセキュリティ] > [管理ツール] > [サービス]** を開くことで、Web 配置が正常に実行されていることを確認した後、以下を確認します。

    * **Web Deployment Agent Service** が実行されている (古いバージョンではサービス名が異なります)。

    * **Web 管理サービス**が実行されている。

    いずれかのエージェント サービスが実行されていない場合は、**Web Deployment Agent サービス**を再起動します。

    Web Deployment Agent サービスがまったく表示されない場合は、 **[コントロール パネル] > [プログラム] > [プログラムのアンインストール]** の順に移動し、 **[Microsoft Web Deploy \<version>]** を見つけます。 インストールの **[変更]** を選び、Web 配置コンポーネントに **[Will be installed to the local hard drive]\(ローカル ハード ドライブにインストール\)** を選択していることを確認します。 インストールの変更手順を完了します。
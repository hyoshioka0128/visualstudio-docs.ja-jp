---
ms.openlocfilehash: 0fc18fab56f5b46ef097cdf699e4f0569dc190c9
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "68143518"
---
ホスティング サーバーの Web 配置 3.6 では、UI から発行設定ファイルの作成を有効にする追加の構成機能を提供しています。

1. Windows Server に Web 配置 3.6 が既にインストールされている場合は、**[コントロール パネル]** > **[プログラム]** > **[プログラムのアンインストール]** を使用してアンインストールします。

2. 次に、Windows Server にホスティング サーバーの Web 配置 3.6 をインストールします。

    ホスティング サーバーの Web 配置をインストールするには、[Web Platform Installer (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx) を使用します。 (IIS で Web Platform Installer のリンクを見つけるには、サーバー マネージャーの左側のウィンドウで **[IIS]** を選択します。 サーバーを右クリックして **[インターネット インフォメーション サービス (IIS) マネージャー]** を選択します。)

    Web Platform Installer の [アプリケーション] タブで、**[Web Deploy for Hosting Servers]\(ホスティング サーバーの Web 配置\)** を見つけます。

3. **[IIS 管理スクリプトおよびツール]** をまだインストールしていない場合は、今すぐインストールします。

    **[サーバーの役割の選択]** > **[Web Server (IIS)]** > **[管理ツール]** の順に移動して、**[IIS 管理スクリプトおよびツール]** の役割を選択し、**[次へ]** をクリックしてその役割をインストールします。

    ![IIS 管理スクリプトおよびツールのインストール](../../deployment/media/tutorial-iis-management-scripts-and-tools.png)

    発行設定ファイルの作成を有効にするには、このスクリプトとツールが必要です。

4. (省略可能) **[コントロール パネル]、[システムとセキュリティ]、[管理ツール]、[サービス]** の順に開くことで、Web 配置が正常に実行されていることを確認し、**Web Deployment Agent Service** が実行されていることを確認します (より古いバージョンでは、サービス名が異なります)。

    エージェント サービスが実行されていない場合は、サービスを開始します。 何も表示されない場合は、**[コントロール パネル]、[プログラム]、[プログラムのアンインストール]** の順に移動して、**Microsoft Web Deploy \<バージョン>** を見つけます。 インストールの **[変更]** を選び、Web 配置コンポーネントに **[Will be installed to the local hard drive]\(ローカル ハード ドライブにインストール\)** を選択していることを確認します。 インストールの変更手順を完了します。
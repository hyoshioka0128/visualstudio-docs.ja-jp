---
title: Docker のコンテナー ログ、環境変数、ファイル システム アクセス
description: Visual Studio でツール ウィンドウを使用してアプリをホストしているコンテナー内の状況を表示することにより、コンテナーベースのアプリをデバッグおよび診断する機能を向上させる方法について説明します。
author: ghogen
ms.author: ghogen
ms.topic: conceptual
ms.date: 01/20/2020
ms.technology: vs-azure
monikerRange: vs-2019
ms.openlocfilehash: b4670c003c06f8d16979589a4dce5abf33d5e27d
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "77027304"
---
# <a name="how-to-view-and-diagnose-containers-and-images-in-visual-studio"></a>Visual Studio でコンテナーおよびイメージを表示および診断する方法

**[コンテナー]** ウィンドウを使用すると、アプリをホストしているコンテナー内の状況を表示できます。 コマンド プロンプトを使用して Docker コマンドを実行し、コンテナーの状況を表示および診断することに慣れている場合、このウィンドウには Visual Studio IDE を離れることなくコンテナーを監視できるさらに便利な方法が用意されています。

## <a name="prerequisites"></a>必須コンポーネント

- [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
- [Visual Studio 2019 バージョン 16.4 Preview 2](https://visualstudio.microsoft.com/downloads) 以降、または以前のバージョンの Visual Studio 2019 を使用している場合は[コンテナー ウィンドウ拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vs-containers-tools-extensions)をインストールします。

## <a name="view-information-about-your-containers"></a>コンテナーに関する情報を表示する

コンテナー化された .NET プロジェクトを開始すると、 **[コンテナー]** ウィンドウが自動的に開きます。 いつでも Visual Studio でコンテナーを表示するには、**Ctrl**+**Q** キーを使用して Visual Studio の [検索] ボックスをアクティブにし、「`Containers`」と入力して最初の項目を選択します。 メイン メニューから **[コンテナー]** ウィンドウを開くこともできます。 メニュー パス **[表示]**  >  **[その他のウィンドウ]**  >  **[コンテナー]** を使用します。  

![[コンテナー] ウィンドウの [環境] タブのスクリーンショット](media/view-and-diagnose-containers/container-window.png)

左側にはローカル コンピューター上のコンテナーの一覧が表示されます。 ソリューションに関連付けられているコンテナーは **[ソリューション コンテナー]** に表示されます。 右側には、 **[環境]** 、 **[ポート]** 、 **[ログ]** 、および **[ファイル]** のタブがあるウィンドウが表示されます。

> [!TIP]
> **[コンテナー]** ツール ウィンドウをドッキングする場所は Visual Studio で簡単にカスタマイズすることができます。 「[Visual Studio のウィンドウ レイアウトをカスタマイズする](../ide/customizing-window-layouts-in-visual-studio.md)」を参照してください。 デバッガーが実行されているときに、既定で **[コンテナー]** ウィンドウは **[ウォッチ]** ウィンドウにドッキングされます。

## <a name="view-environment-variables"></a>環境変数を表示する

**[環境]** タブには、コンテナーの環境変数が表示されます。 アプリのコンテナーでは、これらの変数をさまざまな方法で設定できます。たとえば、Dockerfile、.env ファイル、または Docker コマンドを使用してコンテナーを起動するときに -e オプションを使用します。

![[コンテナー] ウィンドウの [環境] タブのスクリーンショット](media/view-and-diagnose-containers/containers-environment-vars.png)

> [!NOTE]
> 環境変数の変更は、リアルタイムでは反映されません。 また、このタブの環境変数はコンテナーのシステム環境変数であり、アプリにローカルなユーザー環境変数は反映されません。

## <a name="view-port-mappings"></a>ポート マッピングを表示する

**[ポート]** タブで、お使いのコンテナーに有効なポート マッピングを確認できます。

![[コンテナー] ウィンドウの [ポート] タブのスクリーンショット](media/view-and-diagnose-containers/containers-ports.png)

既知のポートがリンクされているため、ポートに使用できるコンテンツがある場合は、リンクをクリックしてブラウザーを開くことができます。

## <a name="view-logs"></a>ログを表示する

**[ログ]** タブには、`docker logs` コマンドの結果が表示されます。 既定では、タブにはコンテナー上の stdout と stderr のストリームが表示されますが、出力を構成することができます。 詳細については、[Docker のログ記録](https://docs.docker.com/config/containers/logging/)に関する記事を参照してください。  既定では、 **[ログ]** タブにはログがストリームされますが、これを無効にするには、タブの **[停止]** ボタンをクリックします。

![[コンテナー] ウィンドウの [ログ] タブのスクリーンショット](media/view-and-diagnose-containers/containers-logs.png)

ログを消去するには、 **[ログ]** タブの **[クリア]** ボタンを使用します。すべてのログを取得するには、 **[更新]** ボタンを使用します。

> [!NOTE]
> Windows コンテナーでデバッグを使用しないで実行すると、Visual Studio により stdout と stderr が **[出力]** ウィンドウに自動的にリダイレクトされるため、**Ctrl**+**F5** キーを使用して Visual Studio から開始されたコンテナーでは、このタブにログが表示されません。代わりに **[出力]** ウィンドウを使用します。

## <a name="view-the-filesystem"></a>ファイルシステムを表示する

**[ファイル]** タブでは、プロジェクトを含むアプリ フォルダーを含め、コンテナーのファイルシステムを確認できます。

![[コンテナー] ウィンドウの [ファイル] タブのスクリーンショット](media/view-and-diagnose-containers/container-filesystem.png)

Visual Studio でファイルを開くには、ファイルを参照してダブルクリックするか、右クリックして **[開く]** を選択します。 Visual Studio で、読み取り専用モードでファイルを開きます。

![Visual Studio で表示するために開いたファイルのスクリーンショット](media/view-and-diagnose-containers/container-file-open.png)

**[ファイル]** タブを使用すると、コンテナーのファイルシステムの IIS ログ、構成ファイル、その他のコンテンツ ファイルなどのアプリケーション ログを確認できます。

## <a name="start-stop-and-remove-containers"></a>コンテナーの開始、停止、および削除

既定では、Docker で管理されているコンピューター上のすべてのコンテナーが **[コンテナー]** ウィンドウに表示されます。 ツール バーのボタンを使用して、コンテナーの開始、停止、または不要になったコンテナーの削除を行うことができます。  この一覧は、コンテナーが作成または削除されると動的に更新されます。

## <a name="open-a-terminal-window-in-a-running-container"></a>実行中のコンテナーでターミナル ウィンドウを開く

**[コンテナー]** ウィンドウの **[ターミナル ウィンドウを開く]** ボタンを使用して、コンテナーでターミナル ウィンドウ (コマンド プロンプトまたは対話型シェル) を開くことができます。

![[コンテナー] ウィンドウの [ターミナル ウィンドウを開く] のスクリーンショット](media/view-and-diagnose-containers/containers-open-terminal-window.png)

Windows コンテナーの場合は、Windows のコマンド プロンプトが開きます。 Linux コンテナーの場合は、Bash シェルを使用してウィンドウが開きます。

![Bash ウィンドウのスクリーンショット](media/view-and-diagnose-containers/container-bash-window.png)

通常、ターミナル ウィンドウは、Visual Studio の外部に別のウィンドウとして開かれます。 ドッキング可能なツール ウィンドウとしてコマンドライン環境を Visual Studio IDE に統合する場合は、[Whack Whack Terminal](https://marketplace.visualstudio.com/items?itemName=DanielGriffen.WhackWhackTerminal) をインストールします。

## <a name="attach-the-debugger-to-a-process"></a>デバッガーをプロセスにアタッチする

[コンテナー] ウィンドウのツール バーにある **[プロセスにアタッチ]** ボタンを使用して、コンテナーで実行されているプロセスにデバッガーをアタッチできます。 このボタンを使用すると **[プロセスにアタッチ]** ダイアログが表示され、コンテナーで実行されている使用可能なプロセスが表示されます。  

![[プロセスにアタッチ] ダイアログ ボックスのスクリーンショット](media/view-and-diagnose-containers/containers-attach-to-process.jpg)

コンテナー内のマネージド プロセスにアタッチすることができます。 別のコンテナーでプロセスを探すには、 **[検索]** ボタンを使用し、 **[Docker コンテナーの選択]** ダイアログで別のコンテナーを選択します。

## <a name="viewing-images"></a>イメージを表示する

**[コンテナー]** ウィンドウの **[イメージ]** タブを使用して、ローカル コンピューター上のイメージを表示することもできます。 外部リポジトリから取得されたイメージは、ツリー ビューでまとめられています。 イメージを選択して、イメージの詳細を調べます。

イメージを削除するには、ツリー ビューでイメージを右クリックして **[削除]** を選択するか、イメージを選択してツール バーの **[削除]** ボタンを使用します。

## <a name="next-steps"></a>次の手順

Visual Studio で使用できるコンテナー ツールの詳細については、[コンテナー ツールの概要](overview.md)に関する記事を参照してください。

## <a name="see-also"></a>関連項目

[Visual Studio でのコンテナーの開発](/visualstudio/containers)

[Visual Studio 用の拡張機能のマーケットプレース](https://marketplace.visualstudio.com/)

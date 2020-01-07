---
title: オフライン インストールを作成する | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-install
ms.topic: conceptual
f1_keywords:
- offline installation
- offline install
- ISO
ms.assetid: 85d65709-42be-449f-9663-914bf1045089
caps.latest.revision: 22
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 197ae2a168f7f14f7d0ea3d9b82b5943c1af82f4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68186014"
---
# <a name="create-an-offline-installation-of-visual-studio"></a>Visual Studio のオフライン インストールを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio に関する最新のドキュメントについては、「[Visual Studio のオフライン インストールを作成する](/visualstudio/install/create-an-offline-installation-of-visual-studio)」または「[Visual Studio のネットワーク インストールを作成する](/visualstudio/install/create-a-network-installation-of-visual-studio)」をご覧ください。

このページでは、インターネットに接続していない場合に Visual Studio 2015 をインストールする方法について説明します。 ただし、"接続なし" でインストールを実行するには、インターネットに接続したマシンを使って、最初にオフライン インストール レイアウトを作成する必要があります。 これを行う方法を次に示します。

> [!IMPORTANT]
> オフラインのコンピューターが Windows 7 SP1 または Windows Server 2008 R2 を稼働している場合は、このトピックの「[オフライン インストールのトラブルシューティング](#BKMK_tshoot)」セクションにある特別な手順を参照してください。  Visual Studio 2015 をインストールする "*前に*" これらの手順に従う必要があります。

## <a name="BKMK_Offline"></a> オフライン インストールの作成によるインストール

#### <a name="to-create-an-offline-installation-layout"></a>オフライン インストール レイアウトを作成するには

1. [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20Enterprise%202015) のダウンロード ページから、インストールする Visual Studio のエディションを選択します。

2. ファイル システム上の場所にインストーラーをダウンロードした後、"\<実行可能ファイル名> /layout" を実行します。

     たとえば、`vs_enterprise.exe /layout D:\VisualStudio2015` を実行します

     `/layout` スイッチを使用すると、ダウンロード先のマシンに適用するものだけでなく、ほとんどすべてのインストール パッケージをダウンロードできます。 この方法では、任意の場所でこのインストーラーを実行するために必要なファイルを入手できます。これは、元はインストールしていなかったコンポーネントをインストールしたい場合に役立つことがあります。

3. このコマンドを実行すると、ダイアログ ボックスが表示されます。これを使って、オフライン インストール レイアウトを置くフォルダーを変更できます。   次に、 **[ダウンロード]** ボタンをクリックします。

     パッケージのダウンロードが成功すると、次のメッセージが表示されます: **セットアップが正常に完了しました。指定したコンポーネントがすべて正常に取得されました。**

4. 前に指定したフォルダーを探します。 (たとえば、D:\VisualStudio2015 を探します。)このフォルダーには、共有の場所またはインストール メディアにコピーする必要があるものがすべて含まれています。

    > [!CAUTION]
    > 現在、Android SDK はオフライン インストール エクスペリエンスをサポートしていません。 Android SDK セットアップ項目をインターネットに接続されていないコンピューターにインストールする場合、インストールが失敗する可能性があります。 詳細については、このトピックの「オフライン インストールのトラブルシューティング」セクションをご覧ください。

5. ファイルの場所、またはインストール メディアからインストールを実行します。

## <a name="updating-an-offline-installation"></a>オフライン インストールの更新
 Microsoft は Visual Studio 2015 の更新プログラムをいくつかリリースしています。 ご自分の Visual Studio のインストールを更新するには、単に [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20Enterprise%202015) のダウンロード ページから必要なエディションをダウンロードします。 次に、このトピックで説明されている手順に従って新しいオフライン インストール レイアウトを作成してから、それを使って自分の Visual Studio 2015 のコピーを更新します。

## <a name="BKMK_tshoot"></a> オフライン インストールのトラブルシューティング
 オフライン インストール キャッシュからオフラインでインストールする際に、一部のコンポーネントとパッケージをインストールできないことを示す警告メッセージが表示される場合があります。 そのようなシナリオで使用可能なソリューションを以下の表に示します。

| コンポーネントまたはパッケージ | ソリューション |
|-|-|
| Dotfuscator および Analytics Community Edition 5.19.1 (**Windows 7 SP1** や **Windows Server 2008 R2** にインストールされているような、Community、Professional、および Enterprise エディションの Visual Studio の場合) | オフラインのマシンで **Windows 7 SP1** または **Windows Server 2008 R2** を稼働している場合は、Visual Studio 2015 をインストールする前に次の手順を実行する必要があります。<br /><br /> 1.CTL ファイルをダウンロードするファイルまたは Web サーバーを構成します。<br /><br /> 2.  接続なしの環境の Microsoft 自動更新の URL をリダイレクトします。<br /><br /> 詳細については、Microsoft TechNet サイトの「[Configure Trusted Roots and Disallowed Certificates (信頼されたルートおよび許可されない証明書を構成する)](https://technet.microsoft.com/library/dn265983.aspx)」ページをご覧ください。 |
| Android SDK セットアップ (API レベル) | Android SDK (API レベル) パッケージをインストールするには、インターネットに接続する必要があります。 制限付きネットワークを使用している場合は、Visual Studio のインストール時に次の URL へのアクセスを許可する必要があります。<br /><br /> -   http://dl.google.com:443<br />-   http://dl-ssl.google.com:443<br />-   https://dl-ssl.google.com/android/repository/*<br /> <br />プロキシ設定で考えられる問題を解決する方法の詳細については、ブログ投稿の「[Visual Studio 2015 install failures (Android SDK Setup) behind a Proxy](https://blogs.msdn.microsoft.com/peterhauge/2016/09/22/visual-studio-2015-install-failures-android-sdk-setup-behind-a-proxy/)」(プロキシ経由で Visual Studio 2015 をインストールできない (Android SDK セットアップ)) を参照してください。 |
| Visual Studio 機能拡張の項目テンプレート<br /><br /> Visual Studio 向け GitHub 拡張<br /><br /> PowerShell Tools for Visual Studio | Visual Studio 2015 をインストールする際にインターネットに接続出来ない場合は、特別なオフライン フィードを使ってオフライン インストール レイアウトを生成することができます。 **注:** この特別なフィードには、Visual Studio 2015 に対する最新の更新プログラムが含まれています。 <br /><br /> 特別なオフライン フィードを作成するには、次のコマンドを実行します: /layout *Drive:* \VisualStudio2015 /overridefeeduri *URL-to-feed-xml*<br /><br /> たとえば、英語版の Visual Studio 2015 Enterprise の特別なオフライン フィードについては、次を実行します。<br /><br /> `vs_enterprise_ENU.exe /layout D:\VisualStudio2015 /overridefeeduri "http://go.microsoft.com/fwlink/?LinkID=785882&clcid0x409"`<br /><br /> 任意の言語の特別なオフライン フィードを作成するために使える URL の完全な一覧については、次の表をご覧ください。 |

 上記の表に示すように、次の URL を使って、言語固有の特別なオフライン フィードを作成します。

|       言語        |                            URL                            |
|-----------------------|-----------------------------------------------------------|
| 簡体中国語  | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x804 |
| 繁体中国語 | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x404 |
|         チェコ語         | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x405 |
|        ドイツ語         | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x407 |
|        英語        | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x409 |
|        スペイン語        | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0xC0A |
|        フランス語         | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x40C |
|        イタリア語        | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x410 |
|       日本語        | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x411 |
|        韓国語         | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x412 |
|        ポーランド語         | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x415 |
|      ポルトガル語       | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x416 |
|        ロシア語        | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x419 |
|        トルコ語        | http://go.microsoft.com/fwlink/?LinkID=785882&clcid=0x41F |

## <a name="see-also"></a>関連項目

- [Visual Studio のインストール](install-visual-studio-2015.md)
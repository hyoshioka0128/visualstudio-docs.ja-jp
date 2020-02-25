---
title: iOS を使用してビルドするためのツールのインストールおよび構成 | Microsoft Docs
ms.custom: ''
ms.date: 10/17/2019
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: d0c311c9-9eb9-42c5-ba07-25604362cd28
author: corob-msft
ms.author: corob
manager: jillfra
ms.workload:
- xplat-cplusplus
ms.openlocfilehash: 37ef83cc968276fb29ae5380544ee9c27ffd485d
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2020
ms.locfileid: "77272288"
---
# <a name="install-and-configure-tools-to-build-using-ios"></a>iOS を使用してビルドするためのツールのインストールおよび構成

Visual Studio でクロスプラットフォームの **C++ によるモバイル開発**ツールを使用して、iOS Simulator または iOS デバイス用の iOS コードを編集、デバッグ、配置することができます。 ただし、ライセンスの制限により、コードのビルドと実行はリモート環境の Mac で行う必要があります。 Visual Studio を使用して iOS アプリをビルドおよび実行するには、Mac 上にリモート エージェント [vcremote](https://www.npmjs.com/package/vcremote)をセットアップして構成する必要があります。 このリモート エージェントが、Visual Studio からのビルド要求を処理し、Mac に接続された iOS デバイスまたは Mac 上の iOS シミュレーターでアプリを実行します。

> [!NOTE]
> Mac ではなくクラウド ホスト型 Mac サービスを使用する場合の詳細については、「[Visual Studio をクラウドでホストされた Mac に接続するよう構成する](/visualstudio/cross-platform/tools-for-cordova/tips-workarounds/host-a-mac-in-the-cloud?view=toolsforcordova-2017#configure-visual-studio-to-connect-to-your-cloud-hosted-mac)」をご覧ください。 ここでは、Visual Studio Tools for Apache Cordova を使用してビルドする場合の手順を説明します。 C++ を使用してビルドする場合は、`remotebuild` を `vcremote` に置き換えます。

iOS を使用してビルドするためのツールをインストールしたら、この記事を参照して、Visual Studio および Mac で iOS 開発用のリモート エージェントを素早く構成して更新する方法を確認してください。

## <a name="prerequisites"></a>必須コンポーネント

iOS のコードを開発するためのリモート エージェントをインストールして使用するには、まず、次の前提条件を満たす必要があります。

- macOS Mojave バージョン 10.14 以降を実行する Mac コンピューター

- [Apple ID](https://appleid.apple.com/)

- アクティブな [Apple Developer Program](https://developer.apple.com/programs/) アカウント

   配布ではなくテスト目的でのみ iOS デバイスにアプリをサイドロードすることを可能にする無料アカウントを取得できます。

- [Xcode](https://developer.apple.com/xcode/downloads/) バージョン 10.2.1 以降

   Xcode は、App Store からダウンロードできます。

- Xcode コマンドライン ツール

   Xcode コマンドライン ツールをインストールするには、Mac 上でターミナル アプリを開き、次のコマンドを入力します。

   `xcode-select --install`

- アプリに署名する他の署名 ID として Xcode で構成された Apple ID アカウント

   Xcode で署名 ID を表示または設定するには、 **[Xcode]** メニューを開き、 **[環境設定]** を選択します。 **[アカウント]** を選択し、自分の Apple ID を選択してから、 **[詳細の表示]** ボタンを選択します。 詳しい手順については、「[Add your Apple ID account](https://help.apple.com/xcode/mac/current/#/devaf282080a)」 (Apple ID アカウントを追加する) を参照してください。
   
   署名要件の詳細については、「[What is app signing](https://help.apple.com/xcode/mac/current/#/dev3a05256b8)」 (アプリの署名とは何か) を参照してください。 

- 開発用の iOS デバイスを使用している場合、デバイスのプロビジョニング プロファイルを Xcode で構成します。

   Xcode には自動署名機能があり、必要に応じて署名証明書が作成されます。 Xcode の自動署名に関する詳細については、「[automatic signing](https://help.apple.com/xcode/mac/current/#/dev80cc24546)」 (自動署名) を参照してください。

   手動で署名する場合、アプリのプロビジョニング プロファイルを作成する必要があります。 プロビジョニング プロファイルを作成する方法の詳細については、「[Create a development provisioning profile](https://help.apple.com/developer-account/#/devf2eb157f8)」 (プロビジョニング プロファイルの作成) を参照してください。 

- [Node.js](https://nodejs.org/) バージョン 12.14.1 と npm バージョン 6.13.4

   バージョン 12.14.1 の Node.js を Mac にインストールします。 Node.js パッケージをインストールする場合、それは npm バージョン 6.13.4 に付属しているはずです。 他のバージョンの Node.js と npm は、リモート エージェント `vcremote` で使用されている一部のモジュールに対応していない場合があり、`vcremote` のインストールが失敗する可能性があります。 Node.js は、[Node Version Manager](https://nodejs.org/en/download/package-manager/#nvm) などのパッケージ マネージャーを使用してインストールすることをお勧めします。 `sudo` を使用すると、一部のモジュールがインストールに失敗する可能性があるため、Node.js のインストールにはコマンド `sudo` を使用しないようにしてください。

## <a name="Install"></a> iOS 用リモート エージェントをインストールする

C++ によるモバイル開発ワークロードをインストールすると、Visual Studio は、Mac 上で実行されているリモート エージェント [vcremote](https://www.npmjs.com/package/vcremote) と通信して、ファイルを転送したり、iOS アプリをビルドして実行したり、デバッグ コマンドを送信したりできます。

リモート エージェントをインストールする前に、[前提条件](#prerequisites)を満たしていること、および「[C++ によるクロスプラットフォーム モバイル開発をインストールする](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md#install-the-tools)」のインストール手順が完了していることを確認してください。

### <a name="DownloadInstall"></a> リモート エージェントをダウンロードしてインストールするには

- Mac 上のターミナル アプリから、現在使用されている Node.js のバージョンが、必須バージョン 12.14.1 であることを確認します。 バージョンを確認するには、次のコマンドを実行します。

  `node -v`
  
  適切なバージョンでない場合は、「必須コンポーネント」の Node.js のインストール手順に従う必要があります。 次に Node.js を再起動します。

- 必須の Node.js が使用されていることを確認した後、次のコマンドを実行して、その Node.js バージョンで vcremote をインストールします。

   `npm install -g --unsafe-perm vcremote`

   グローバル インストール ( **-g**) スイッチが推奨されますが、必須ではありません。 グローバル インストール スイッチを使用しない場合、vcremote は、ターミナル アプリの現在のアクティブなパスの下にインストールされます。

   インストールの間に、Mac に `vcremote` がインストールされて、開発者モードがアクティブ化されます。 [Homebrew](https://brew.sh/) および 2 つの npm パッケージ `vcremote-lib` と `vcremote-utils` もインストールされます。 インストールが完了したら、スキップしたオプションの依存関係に関する警告は無視しても安全です。

   > [!NOTE]
   > Homebrew をインストールするには、sudo (管理者) のアクセス許可が必要です。 sudo 以外で `vcremote` をインストールする必要がある場合は、Homebrew を手動で usr/local の場所にインストールして、その bin フォルダーをパスに追加します。 詳細については、 [Homebrew のドキュメント](https://github.com/Homebrew/homebrew/wiki/Installation)を参照してください。 開発者モードを手動で有効にするには、ターミナル アプリでコマンド `DevToolsSecurity -enable`を入力します。

Visual Studio を新しいバージョンに更新した場合は、リモート エージェントも現在のバージョンに更新する必要があります。 リモート エージェントを更新するには、リモート エージェントをダウンロードしてインストールする手順を繰り返します。

## <a name="Start"></a> リモート エージェントを起動する

Visual Studio で iOS コードをビルドして実行するには、リモート エージェントが実行されている必要があります。 Visual Studio がリモート エージェントとペアリングされていないと、Visual Studio はリモート エージェントと通信できません。 既定では、リモート エージェントはセキュリティで保護された接続モードで実行されます。この場合、PIN を使用して Visual Studio とペアリングする必要があります。

### <a name="RemoteAgentStartServer"></a> リモート エージェントを起動するには

- Mac 上のターミナル アプリから、次のように入力します。

   `vcremote`

   このコマンドにより、既定のビルド ディレクトリ `~/vcremote` でエージェントが起動されます。 追加の構成オプションについては、「 [Configure the remote agent on the Mac](#ConfigureMac)」を参照してください。

エージェントを初めて起動するとき、および新しいクライアント証明書を作成するたびに、そのエージェントを Visual Studio で構成するために必要な情報 (ホスト名、ポート、PIN など) が提供されます。

![vcremote を使用したセキュリテ暗証番号 (PIN) の生成](../cross-platform/media/cppmdd_vcremote_generateclientcert.png "CPPMDD_vcremote_generateClientCert")

ホスト名を使用して Visual Studio にリモート エージェントを構成する場合は、Windows からホスト名を使用して Mac を ping し、到達可能であることを確認してください。 そうでない場合は、代わりに IP アドレスを使用する必要があります。

生成される PIN は 1 回限りの使い捨て PIN であり、有効期間は限られています。 Visual Studio とリモート エージェントをペアリングする前に期限が切れた場合は、新しい PIN を生成する必要があります。 詳細については、「 [Generate a new security PIN](#GeneratePIN)」を参照してください。

リモート エージェントは、セキュリティで保護されていないモードでも使用できます。 セキュリティで保護されていないモードでは、PIN なしでリモート エージェントと Visual Studio をペアリングすることができます。

#### <a name="to-disable-secured-connection-mode"></a>セキュリティで保護された接続モードを無効にするには

- `vcremote` のセキュリティ保護接続モードを無効にするには、Mac 上のターミナル アプリで次のコマンドを入力します。

   `vcremote --secure false`

#### <a name="to-enable-secured-connection-mode"></a>セキュリティで保護された接続モードを有効にするには

- セキュリティで保護された接続モードを有効にするには、次のコマンドを入力します。

   `vcremote --secure true`

リモート エージェントを起動した後は停止するまで、Visual Studio からリモート エージェントを使用できます。

#### <a name="to-stop-the-remote-agent"></a>リモート エージェントを停止するには

- `vcremote` が実行されているターミナル ウィンドウで、**Control**+**C** キーを押します。

## <a name="ConfigureVS"></a> Visual Studio でリモート エージェントを構成する

Visual Studio からリモート エージェントに接続するには、Visual Studio のオプションで、リモート構成を指定する必要があります。

### <a name="to-configure-the-remote-agent-from-visual-studio"></a>Visual Studio でリモート エージェントを構成するには

1. エージェントが Mac 上でまだ実行されていない場合は、「 [リモート エージェントを起動する](#Start)」の手順に従います。 Visual Studio をリモート エージェントと正常にペアリングして接続し、プロジェクトをビルドするには、Mac で `vcremote` が実行されている必要があります。

1. Mac 上で、Mac のホスト名または IP アドレスを取得します。

   IP アドレスを取得するには、ターミナル ウィンドウで **ifconfig** コマンドを使用します。 アクティブなネットワーク インターフェイスの下に表示される inet アドレスを使用します。

1. Visual Studio のメニュー バーで、 **[ツール]** 、 **[オプション]** の順に選択します。

1. **[オプション]** ダイアログ ボックスで、 **[クロス プラットフォーム]** 、 **[C++]** 、 **[iOS]** の順に展開します。

1. **[ホスト名]** フィールドと **[ポート]** フィールドに、リモート エージェントの起動時に示された値を入力します。 ホスト名には、Mac の DNS 名または IP アドレスを使用できます。 既定のポートは 3030 です。

   > [!NOTE]
   > ホスト名で Mac を ping できない場合は、IP アドレスを使用する必要があります。

1. 既定のセキュリティで保護された接続モードでリモート エージェントを使用する場合は、 **[セキュア]** チェック ボックスをオンにしてから、リモート エージェントから示された PIN の値を **[PIN]** フィールドに入力します。 セキュリティで保護されていない接続モードでリモート エージェントを使用する場合は、 **[セキュア]** チェック ボックスをオフにして、 **[PIN]** フィールドを空白のままにします。

1. **[ペアリングする]** を選択してペアリングを有効にします。

   ![iOS のビルドにおける vcremote 接続の構成](../cross-platform/media/cppmdd_options_ios.PNG "CPPMDD_Options_iOS")

   ペアリングは、ホスト名またはポートを変更するまで維持されます。 **[オプション]** ダイアログ ボックスでホスト名またはポートを変更した場合にその変更を元に戻すには、 **[元に戻す]** ボタンを選択して前のペアリングに戻します。

   ペアリングが成功しなかった場合は、「 [Start the remote agent](#Start)」の手順に従って、リモート エージェントが実行されていることを確認します。 リモート エージェントの PIN が生成されてから経過した時間が長すぎる場合は、Mac 上で「 [Generate a new security PIN](#GeneratePIN) 」の手順に従ってからもう一度実行します。 Mac のホスト名を使用している場合は、代わりに IP アドレスを **[ホスト名]** に使用してみてください。

1. **[リモート ルート]** フィールドのフォルダー名を更新して、Mac のホーム ( *~* ) ディレクトリ内のリモート エージェントで使用されるフォルダーを指定します。 既定の場合、リモート エージェントではリモート ルートとして `/Users/<username>/vcremote` が使用されます。

1. **[OK]** を選択して、リモート ペアリング接続設定を保存します。

リモート エージェントを使用するたびに、Visual Studio は、この同じ情報を使用して Mac 上のリモート エージェントに接続します。 Visual Studio を再度リモート エージェントにペアリングさせる必要はありません。それが必要になるのは、Mac 上で新しいセキュリティ証明書を生成した場合、あるいは Mac のホスト名または IP アドレスが変更された場合のみです。

## <a name="GeneratePIN"></a> Generate a new security PIN

初めてリモート エージェントを起動すると、生成された PIN が期間限定で有効になります (既定では 10 分)。 Visual Studio とリモート エージェントをペアリングする前に期限切れになった場合は、新しい PIN を生成する必要があります。

### <a name="to-generate-a-new-pin"></a>新しい PIN を生成するには

1. エージェントを停止するか、Mac 上で 2 つ目のターミナル アプリ ウィンドウを開き、それを使用してコマンドを入力します。

1. ターミナル アプリで、次のコマンドを入力します。

   `vcremote generateClientCert`

   リモート エージェントが新しい一時 PIN を生成します。 新しい PIN を使用して Visual Studio をペアリングするには、「 [Visual Studio でリモート エージェントを構成する](#ConfigureVS)」の手順を繰り返します。

## <a name="GenerateCert"></a> 新しいサーバー証明書を生成する

セキュリティ上の目的で、Visual Studio とリモート エージェントをペアリングするサーバー証明書は、Mac の IP アドレスまたはホスト名と関連付けられています。 これらの値が変更された場合、新しいサーバー証明書を生成し、新しい値で Visual Studio を再構成する必要があります。

### <a name="to-generate-a-new-server-certificate"></a>新しいサーバー証明書を生成するには

1. `vcremote` エージェントを停止します。

1. ターミナル アプリで、次のコマンドを入力します。

   `vcremote resetServerCert`

1. 確認を求めるプロンプトが表示されたら、「 `Y`」と入力します。

1. ターミナル アプリで、次のコマンドを入力します。

   `vcremote generateClientCert`

   このコマンドでは、新しい一時 PIN が生成されます。

1. 新しい PIN を使用して Visual Studio をペアリングするには、「 [Visual Studio でリモート エージェントを構成する](#ConfigureVS)」の手順を繰り返します。

## <a name="ConfigureMac"></a> Configure the remote agent on the Mac

さまざまなコマンドライン オプションを使用して、リモート エージェントを構成することができます。 たとえば、ビルド要求をリッスンするポートを指定したり、ファイル システムに保持するビルドの最大数を指定したりできます。 既定では、10 個のビルドに制限されます。 最大数を超えたビルドは、リモート エージェントによってシャットダウン時に削除されます。

### <a name="to-configure-the-remote-agent"></a>リモート エージェントを構成するには

- リモート エージェントの完全なコマンド一覧を表示するには、ターミナル アプリで次のように入力します。

   `vcremote --help`

- セキュリティ保護モードを無効にして、単純な HTTP ベースの接続を有効にするには、次のように入力します。

   `vcremote --secure false`

   このオプションを使用する場合、Visual Studio でエージェントを構成する際に、 **[セキュア]** チェック ボックスをオフにして、 **[PIN]** フィールドを空白のままにします。

- リモート エージェント ファイルの場所を指定するには、次のように入力します。

   `vcremote --serverDir directory_path`

   ここで *directory_path* は、ログ ファイル、ビルド、サーバー証明書を配置する Mac 上の場所です。 既定では、この場所は `/Users/<username>/vcremote` です。 ビルドはこの場所でビルド番号順に編成されます。

- バックグラウンド プロセスを使用して、server.log という名前のファイルに `stdout` と `stderr` をキャプチャするには、次のように入力します。

   `vcremote > server.log 2>&1 &`

   server.log ファイルは、ビルドの問題のトラブルシューティングに役立ちます。

- コマンド ライン パラメーターではなく、構成ファイルを使用してエージェントを実行するには、次のように入力します。

   `vcremote --config config_file_path`

   ここで *config_file_path* は JSON 形式の構成ファイルのパスです。 スタートアップ オプションとその値にダッシュを含めることはできません。

## <a name="troubleshoot-the-remote-agent"></a>リモート エージェントの問題を解決する

### <a name="debugging-on-an-ios-device"></a>iOS デバイスでのデバッグ

iOS デバイスでのデバッグがうまくいかない場合、[ideviceinstaller](https://github.com/libimobiledevice/ideviceinstaller) というツールに問題がある可能性があります。これは、iOS デバイスとの通信に使用されるツールです。 このツールは通常、`vcremote` のインストールの間に、Homebrew からインストールされます。 回避策としては以下の手順を行います。

ターミナル アプリを開き、次のコマンドを順番に実行することで、`ideviceinstaller` とその依存関係を更新します。

1. Homebrew が確実に更新されるようにする

   `brew update`

1. `libimobiledevice` と `usbmuxd` をアンインストールします

   `brew uninstall --ignore-dependencies libimobiledevice`

   `brew uninstall --ignore-dependencies usbmuxd`

1. 最新バージョンの `libimobiledevice` と `usbmuxd` をインストールします

   `brew install --HEAD usbmuxd`

   `brew unlink usbmuxd`

   `brew link usbmuxd`

   `brew install --HEAD libimobiledevice`

1. `ideviceinstaller` をアンインストールして再インストールします

   `brew uninstall ideviceinstaller`

   `brew install ideviceinstaller`

デバイスにインストールされているアプリを一覧表示してみることで、`ideviceinstaller` でデバイスと通信できることを確認します。

`ideviceinstaller -l`

フォルダー `/var/db/lockdown` にアクセスできないというエラーが `ideviceinstaller` で発生する場合は、次のようにしてフォルダーの権限を変更します。

`sudo chmod 777 /var/db/lockdown`
    
その後、`ideviceinstaller` でデバイスと通信できるかどうか、再度確認します。

## <a name="see-also"></a>関連項目

- [C++ によるクロスプラットフォーム モバイル開発をインストールする](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md)

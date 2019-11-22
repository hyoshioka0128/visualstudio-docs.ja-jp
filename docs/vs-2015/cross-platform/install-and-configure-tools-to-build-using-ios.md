---
title: iOS を使用してビルドするためのツールのインストールおよび構成 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: tgt-pltfrm-cross-plat
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: d0c311c9-9eb9-42c5-ba07-25604362cd28
caps.latest.revision: 13
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: 695cbeaba5a108c61b5e81078a9651c0df9237f5
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299812"
---
# <a name="install-and-configure-tools-to-build-using-ios"></a>Install and Configure Tools to Build using iOS
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual C++ for Cross-Platform Mobile Development を使用して、iOS コードを編集およびデバッグし、iOS シミュレーターまたは iOS デバイスに配置することができます。ただし、ライセンスの制限により、コードのビルドと実行は、リモートの Mac 上で行わなければなりません。 Visual Studio を使用して iOS アプリをビルドおよび実行するには、Mac 上にリモート エージェント [vcremote](https://go.microsoft.com/fwlink/p/?LinkId=534988)をセットアップして構成する必要があります。 このリモート エージェントが、Visual Studio からのビルド要求を処理し、Mac に接続された iOS デバイスまたは Mac 上の iOS シミュレーターでアプリを実行します。  
  
> [!NOTE]
> Mac ではなくクラウド ホスト型 Mac サービスを使用する場合の詳細については、「 [Build and Simulate iOS in the Cloud](https://taco.visualstudio.com/docs/build_ios_cloud/)」を参照してください。 ここでは、Visual Studio Tools for Apache Cordova を使用してビルドする場合の手順を説明します。 Visual C++ for Cross-Platform Mobile Development を使用してビルドする場合は、vcremote を vs-mda-remote に置き換えて手順に従ってください。  
  
 iOS を使用してビルドするためのツールをインストールしたら、このトピックを参照して、Visual Studio と Mac で iOS 開発を行うためにリモート エージェントを素早く構成して更新する方法を確認してください。  
  
 [必須コンポーネント](#Prerequisites)  
  
 [iOS 用リモート エージェントをインストールする](#Install)  
  
 [リモート エージェントを起動する](#Start)  
  
 [Visual Studio でリモート エージェントを構成する](#ConfigureVS)  
  
 [Generate a new security PIN](#GeneratePIN)  
  
 [新しいサーバー証明書を生成する](#GenerateCert)  
  
 [Configure the remote agent on the Mac](#ConfigureMac)  
  
## <a name="Prerequisites"></a> 必要条件  
 iOS のコードを開発するためのリモート エージェントをインストールして使用するには、まず、次の前提条件を満たす必要があります。  
  
- OS X Mavericks 以降を実行する Mac コンピューター  
  
- [Apple ID](https://appleid.apple.com/)  
  
- Apple のアクティブな [iOS Developer Program](https://developer.apple.com/programs/ios/) アカウント  
  
- [Xcode 6](https://developer.apple.com/xcode/downloads/)  
  
     Xcode 6 は、App Store からダウンロードできます。  
  
- Xcode コマンド ライン ツール  
  
     Xcode コマンド ライン ツールをインストールするには、Mac 上でターミナル アプリを開き、次のコマンドを入力します。  
  
     `xcode-select --install`  
  
- Xcode で構成されている iOS 署名 ID  
  
     iOS 署名 ID を取得する方法の詳細については、iOS Developer Library の「 [Maintaining Your Signing Identities and Certificates (署名 ID と証明書の管理)](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html) 」を参照してください。 Xcode で署名 ID を表示または設定するには、 **[Xcode]** メニューを開き、 **[環境設定]** を選択します。 **[アカウント]** を選択し、自分の Apple ID を選択してから、 **[詳細の表示]** ボタンを選択します。  
  
- 開発用の iOS デバイスを使用している場合、デバイスのプロビジョニング プロファイルを Xcode で構成します。  
  
     プロビジョニング プロファイルを作成する方法の詳細については、iOS Developer Library の「 [Creating Provisioning Profiles Using Member Center (メンバー センターを使用したプロビジョニング プロファイルの作成)](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW24) 」を参照してください。  
  
- [Node.js](https://nodejs.org/en/)  
  
- npm の更新バージョン  
  
     Node.js に付属している npm のバージョンは、vcremote をインストールするには古い可能性があります。 npm を更新するには、Mac 上でターミナル アプリを開き、次のコマンドを入力します。  
  
     `sudo npm install -g npm@latest`  
  
## <a name="Install"></a> iOS 用リモート エージェントをインストールする  
 Visual C++ for Cross-Platform Mobile Development をインストールすると、Visual Studio は、Mac 上で実行されているリモート エージェント [vcremote](https://go.microsoft.com/fwlink/p/?LinkId=534988)と通信して、ファイルを転送したり、iOS アプリをビルドして実行したり、デバッグ コマンドを送信したりできます。  
  
 リモート エージェントをインストールする前に、 [前提条件](#Prerequisites) を満たしていること、 [Visual C++ for Cross-Platform Mobile Development](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md#InstallTheTools)をインストール済みであることを確認してください。  
  
### <a name="DownloadInstall"></a> リモート エージェントをダウンロードしてインストールするには  
  
- Mac 上のターミナル アプリから、次のように入力します。  
  
   `sudo npm install -g --unsafe-perm vcremote`  
  
   グローバル インストール ( **-g**) スイッチが推奨されますが、必須ではありません。  
  
   インストール中、Mac に vcremote がインストールされて、開発者モードがアクティブ化されます。 [Homebrew](https://brew.sh/) と 2 つのパッケージ (vcremote-lib および vcremote-utils) もインストールされます。  
  
  > [!NOTE]
  > Homebrew をインストールするには、sudo (管理者) のアクセス許可が必要です。 sudo 以外で vcremote をインストールする必要がある場合には、Homebrew を手動で usr/local の場所にインストールして、その bin フォルダーをパスに追加します。 詳細については、 [Homebrew のドキュメント](https://github.com/Homebrew/homebrew/wiki/Installation)を参照してください。 開発者モードを手動で有効にするには、ターミナル アプリでコマンド `DevToolsSecurity –enable` を入力します。  
  
  Visual Studio を新しいバージョンに更新した場合は、リモート エージェントも現在のバージョンに更新する必要があります。 リモート エージェントを更新するには、リモート エージェントをダウンロードしてインストールする手順を繰り返します。  
  
## <a name="Start"></a> リモート エージェントを起動する  
 Visual Studio で iOS コードをビルドして実行するには、リモート エージェントが実行されている必要があります。 Visual Studio がリモート エージェントとペアリングされていないと、Visual Studio はリモート エージェントと通信できません。 既定では、リモート エージェントはセキュリティで保護された接続モードで実行されます。この場合、PIN を使用して Visual Studio とペアリングする必要があります。  
  
### <a name="RemoteAgentStartServer"></a> リモート エージェントを起動するには  
  
- Mac 上のターミナル アプリから、次のように入力します。  
  
   `vcremote`  
  
   これにより、既定のビルド ディレクトリである ~/vcremote でエージェントが起動します。 追加の構成オプションについては、「 [Configure the remote agent on the Mac](#ConfigureMac)」を参照してください。  
  
  エージェントを初めて起動するとき、また、新しいクライアント証明書を作成するときは必ず、そのエージェントを Visual Studio に構成するために必要な情報 (ホスト名、ポート、PIN など) が提供されます。  
  
  ![vcremote を使用したセキュリテ暗証番号 (PIN) の生成](../cross-platform/media/cppmdd-vcremote-generateclientcert.png "CPPMDD_vcremote_generateClientCert")  
  
  ホスト名を使用して Visual Studio にリモート エージェントを構成する場合は、Windows からホスト名を使用して Mac を ping し、到達可能であることを確認してください。 そうでない場合は、代わりに IP アドレスを使用する必要があります。  
  
  生成される PIN は 1 回限りの使い捨て PIN であり、有効期間は限られています。 Visual Studio とリモート エージェントをペアリングする前に期限が切れた場合は、新しい PIN を生成する必要があります。 詳細については、「 [Generate a new security PIN](#GeneratePIN)」を参照してください。  
  
  リモート エージェントは、セキュリティで保護されていないモードでも使用できます。 セキュリティで保護されていないモードでは、PIN なしでリモート エージェントと Visual Studio をペアリングすることができます。  
  
#### <a name="to-disable-secured-connection-mode"></a>セキュリティで保護された接続モードを無効にするには  
  
- vcremote のセキュリティで保護された接続モードを無効にするには、Mac 上のターミナル アプリで次のコマンドを入力します。  
  
     `vcremote --secure false`  
  
#### <a name="to-enable-secured-connection-mode"></a>セキュリティで保護された接続モードを有効にするには  
  
- セキュリティで保護された接続モードを有効にするには、次のコマンドを入力します。  
  
   `vcremote --secure true`  
  
  リモート エージェントを起動した後は停止するまで、Visual Studio からリモート エージェントを使用できます。  
  
#### <a name="to-stop-the-remote-agent"></a>リモート エージェントを停止するには  
  
- vcremote が実行されているターミナル ウィンドウで、 `Control+C`を押します。  
  
## <a name="ConfigureVS"></a> Visual Studio でリモート エージェントを構成する  
 Visual Studio からリモート エージェントに接続するには、Visual Studio のオプションで、リモート構成を指定する必要があります。  
  
#### <a name="to-configure-the-remote-agent-from-visual-studio"></a>Visual Studio でリモート エージェントを構成するには  
  
1. エージェントが Mac 上でまだ実行されていない場合は、「 [リモート エージェントを起動する](#Start)」の手順に従います。 Visual Studio をリモート エージェントと正常にペアリングして接続し、プロジェクトをビルドするためには、Mac が vcremote を実行している必要があります。  
  
2. Mac 上で、Mac のホスト名または IP アドレスを取得します。  
  
    IP アドレスを取得するには、ターミナル ウィンドウで **ifconfig** コマンドを使用します。 アクティブなネットワーク インターフェイスの下に表示される inet アドレスを使用します。  
  
3. Visual Studio のメニュー バーで、 **[ツール]** 、 **[オプション]** の順に選択します。  
  
4. **[オプション]** ダイアログ ボックスで、 **[クロス プラットフォーム]** 、 **[C++]** 、 **[iOS]** の順に展開します。  
  
5. **[ホスト名]** フィールドと **[ポート]** フィールドに、リモート エージェントの起動時に示された値を入力します。 ホスト名には、Mac の DNS 名または IP アドレスを使用できます。 既定のポートは 3030 です。  
  
   > [!NOTE]
   > ホスト名で Mac を ping できない場合は、IP アドレスを使用する必要があります。  
  
6. 既定のセキュリティで保護された接続モードでリモート エージェントを使用する場合は、 **[セキュア]** チェック ボックスをオンにしてから、リモート エージェントから示された PIN の値を **[PIN]** フィールドに入力します。 セキュリティで保護されていない接続モードでリモート エージェントを使用する場合は、 **[セキュア]** チェック ボックスをオフにして、 **[PIN]** フィールドを空白のままにします。  
  
7. **[ペアリングする]** を選択してペアリングを有効にします。  
  
    ![iOS のビルドにおける vcremote 接続の構成](../cross-platform/media/cppmdd-options-ios.PNG "CPPMDD_Options_iOS")  
  
    ペアリングは、ホスト名またはポートを変更するまで維持されます。 **[オプション]** ダイアログ ボックスでホスト名またはポートを変更した場合にその変更を元に戻すには、 **[元に戻す]** ボタンを選択して前のペアリングに戻します。  
  
    ペアリングが成功しなかった場合は、「 [Start the remote agent](#Start)」の手順に従って、リモート エージェントが実行されていることを確認します。 リモート エージェントの PIN が生成されてから経過した時間が長すぎる場合は、Mac 上で「 [Generate a new security PIN](#GeneratePIN) 」の手順に従ってからもう一度実行します。 Mac のホスト名を使用している場合は、代わりに IP アドレスを **[ホスト名]** に使用してみてください。  
  
8. **[リモート ルート]** フィールドのフォルダー名を更新して、Mac のホーム (~) ディレクトリ内の リモート エージェントで使用されるフォルダーを指定します。 既定では、リモート エージェントはリモート ルートとして /Users/`username`/vcremote を使用します。  
  
9. **[OK]** を選択して、リモート ペアリング接続設定を保存します。  
  
   リモート エージェントを使用するたびに、Visual Studio は、この同じ情報を使用して Mac 上のリモート エージェントに接続します。 Visual Studio を再度リモート エージェントにペアリングさせる必要はありません。それが必要になるのは、Mac 上で新しいセキュリティ証明書を生成した場合、あるいは Mac のホスト名または IP アドレスが変更された場合のみです。  
  
## <a name="GeneratePIN"></a> Generate a new security PIN  
 初めてリモート エージェントを起動すると、生成された PIN が期間限定で有効になります (既定では 10 分)。 Visual Studio とリモート エージェントをペアリングする前に期限切れになった場合は、新しい PIN を生成する必要があります。  
  
#### <a name="to-generate-a-new-pin"></a>新しい PIN を生成するには  
  
1. エージェントを停止するか、Mac 上で 2 つ目のターミナル アプリ ウィンドウを開き、それを使用してコマンドを入力します。  
  
2. ターミナル アプリで、次のコマンドを入力します。  
  
     `vcremote generateClientCert`  
  
     リモート エージェントが新しい一時 PIN を生成します。 新しい PIN を使用して Visual Studio をペアリングするには、「 [Visual Studio でリモート エージェントを構成する](#ConfigureVS)」の手順を繰り返します。  
  
## <a name="GenerateCert"></a> 新しいサーバー証明書を生成する  
 セキュリティ上の目的で、Visual Studio とリモート エージェントをペアリングするサーバー証明書は、Mac の IP アドレスまたはホスト名と関連付けられています。 これらの値が変更された場合、新しいサーバー証明書を生成し、新しい値で Visual Studio を再構成する必要があります。  
  
#### <a name="to-generate-a-new-server-certificate"></a>新しいサーバー証明書を生成するには  
  
1. vcremote エージェントを停止します。  
  
2. ターミナル アプリで、次のコマンドを入力します。  
  
     `vcremote resetServerCert`  
  
3. 確認を求めるプロンプトが表示されたら、「 `Y`」と入力します。  
  
4. ターミナル アプリで、次のコマンドを入力します。  
  
     `vcremote generateClientCert`  
  
     これにより、新しい一時 PIN が生成されます。  
  
5. 新しい PIN を使用して Visual Studio をペアリングするには、「 [Visual Studio でリモート エージェントを構成する](#ConfigureVS)」の手順を繰り返します。  
  
## <a name="ConfigureMac"></a> Configure the remote agent on the Mac  
 さまざまなコマンド ライン オプションを使用して、リモート エージェントを構成することができます。 たとえば、ビルド要求をリッスンするポートを指定したり、ファイル システムに保持するビルドの最大数を指定したりできます。 既定では、10 個のビルドに制限されます。 最大数を超えたビルドは、リモート エージェントによってシャットダウン時に削除されます。  
  
#### <a name="to-configure-the-remote-agent"></a>リモート エージェントを構成するには  
  
- リモート エージェントの完全なコマンド一覧を表示するには、ターミナル アプリで次のように入力します。  
  
     `vcremote --help`  
  
- セキュリティで保護されたモードを無効にして、単純な HTTP ベースの接続を有効にするには、次のように入力します。  
  
     `vcremote --secure false`  
  
     このオプションを使用する場合、Visual Studio でエージェントを構成する際に、 **[セキュア]** チェック ボックスをオフにして、 **[PIN]** フィールドを空白のままにします。  
  
- リモート エージェント ファイルの場所を指定するには、次のように入力します。  
  
     `vcremote --serverDir directory_path`  
  
     ここで *directory_path* は、ログ ファイル、ビルド、サーバー証明書を配置する Mac 上の場所です。 既定では、この場所は /Users/*username*/vcremote です。 ビルドはこの場所でビルド番号順に編成されます。  
  
- バックグラウンド プロセスを使用して、server.log という名前のファイルに `stdout` と `stderr` をキャプチャするには、次のように入力します。  
  
     `vcremote > server.log 2>&1 &`  
  
     server.log ファイルは、ビルドの問題のトラブルシューティングに役立ちます。  
  
- コマンド ライン パラメーターではなく、構成ファイルを使用してエージェントを実行するには、次のように入力します。  
  
     `vcremote --config config_file_path`  
  
     ここで *config_file_path* は JSON 形式の構成ファイルのパスです。 スタートアップ オプションとその値にダッシュを含めることはできません。  
  
## <a name="see-also"></a>参照  
 [Visual C++ for Cross-Platform Mobile Development のインストール](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md)

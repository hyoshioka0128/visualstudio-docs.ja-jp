---
title: リモート デバッグ モニターに接続できません |マイクロソフトドキュメント
ms.date: 04/14/2020
ms.topic: reference
f1_keywords:
- vs.debug.error.remote_debug
- vs.debug.error.firewall.remotemachine
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d6173d6b3525a1bd723bc859d34b889b3796d295
ms.sourcegitcommit: c3b92a9912a5816f16c6059d1738dbc833851346
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2020
ms.locfileid: "81397377"
---
# <a name="unable-to-connect-to-the-microsoft-visual-studio-remote-debugging-monitor"></a>Microsoft Visual Studio リモート デバッグ モニターに接続できません。
このメッセージは、リモート デバッグ モニタがリモート コンピュータで正しく設定されていないか、ネットワークの問題またはファイアウォールの存在のためにリモート コンピュータにアクセスできない場合に発生することがあります。

> [!IMPORTANT]
> 製品の不具合によりこのメッセージが表示された場合は、[この問題](../ide/how-to-report-a-problem-with-visual-studio.md)を Visual Studio に報告してください。 その他の支援が必要な場合は、Microsoft へのお問い合わせ方法について、「 [Talk to Us](../ide/feedback-options.md) 」を参照してください。

## <a name="what-is-the-detailed-error-message"></a><a name="specificerrors"></a>詳細なエラー メッセージは何ですか。

メッセージ`Unable to Connect to the Microsoft Visual Studio Remote Debugging Monitor`は汎用的です。 通常、より具体的なメッセージがエラー文字列に含まれており、問題の原因を特定したり、より正確な修正を検索したりする場合があります。 メイン エラー メッセージに追加される、一般的なエラー メッセージの一部を次に示します。

- [デバッガはリモート コンピュータに接続できません。デバッガは指定されたコンピュータ名を解決できませんでした](#cannot_connect)
- [リモート デバッガーによって接続要求が拒否されました](#rejected)
- [リモート エンドポイントとの接続が終了しました](#connection_terminated)
- [メモリロケーションへの不正アクセス](#invalid_access)
- [リモート コンピュータ上で実行されている指定された名前のサーバーがありません](#no_server)
- [要求された名前は有効ですが、要求された型のデータが見つかりませんでした](#valid_name)
- [ターゲット コンピューター上の Visual Studio リモート デバッガーは、このコンピューターに接続できません。](#cant_connect_back)
- [アクセスが拒否されました](#access_denied)
- [セキュリティ パッケージ固有のエラーが発生しました](#security_package)

## <a name="the-debugger-cannot-connect-to-the-remote-computer-the-debugger-was-unable-to-resolve-the-specified-computer-name"></a><a name="cannot_connect"></a>デバッガはリモート コンピュータに接続できません。 デバッガは指定されたコンピュータ名を解決できませんでした

以下の手順を試してみてください。

1. [**プロセスにアタッチ**] ダイアログ ボックスまたはプロジェクトのプロパティに、有効なコンピュータ名とポート番号を入力してください (プロパティを設定するには、[次の手順](#server_incorrect)を参照してください)。 コンピュータ名は次の形式である必要があります。

    `computername:port`

    > [!NOTE]
    > ポート番号は、ターゲット マシンで*実行する必要がある*リモート デバッガー の[ポート番号](../debugger/remote-debugger-port-assignments.md)と一致する必要があります。

2. コンピュータ名が機能しない場合は、IP アドレスとポート番号を試してください。

3. ターゲット コンピューターで実行されているリモート デバッガーのバージョンが Visual Studio のバージョンと一致していることを確認します。 リモート デバッガの正しいバージョンを取得するには、「[リモート デバッグ](../debugger/remote-debugging.md)」を参照してください。

    > [!TIP]
    > プロセスにアタッチしていて、正常に接続しても必要なプロセスが表示されない場合は、[**すべてのユーザーからプロセスを表示する] チェック ボックスをオン**にします。 別のユーザー アカウントで接続している場合は、プロセスが表示されます。

4. これらの手順でこのエラーが解決しない場合[は、「リモート コンピュータに到達できません](#dns)」を参照してください。

## <a name="connection-request-was-rejected-by-the-remote-debugger"></a><a name="rejected"></a>リモート デバッガーによって接続要求が拒否されました

[**プロセスにアタッチ**] ダイアログ ボックスまたはプロジェクトのプロパティで、リモート コンピュータ名とポート番号が、リモート デバッガ ウィンドウに表示される名前とポート番号と一致していることを確認します。 間違っている場合は、修正してやり直してください。

これらの値が正しく、メッセージに**Windows 認証**モードが示されている場合は、リモート デバッガが正しい認証モード **([ツール> オプション)]** であることを確認します。

## <a name="connection-with-the-remote-endpoint-was-terminated"></a><a name="connection_terminated"></a>リモート エンドポイントとの接続が終了しました

Azure App Service アプリをデバッグする場合は、クラウド エクスプローラーまたはサーバー エクスプローラーから [**プロセスにアタッチ]** ではなく[[デバッガーのアタッチ](../debugger/remote-debugging-azure.md#remote_debug_azure_app_service)] コマンドを使用してみてください。

**[プロセスにアタッチ] を使用して**デバッグする場合は、次の手順を実行します。

- [**プロセスにアタッチ**] ダイアログ ボックスまたはプロジェクトのプロパティで、リモート コンピュータ名とポート番号が、リモート デバッガ ウィンドウに表示される名前とポート番号と一致していることを確認します。 間違っている場合は、修正してやり直してください。

- ホスト名を使用して接続する場合は、代わりに IP アドレスを試してください。

- 問題の解決に役立つ詳細情報については、サーバー (Windows のイベント ビューア) のアプリケーション ログを確認してください。

- それ以外の場合は、管理者特権で Visual Studio を再起動してから、もう一度やり直してください。

## <a name="invalid-access-to-memory-location"></a><a name="invalid_access"></a>メモリロケーションへの不正アクセス

An internal error occurred. Visual Studio を再起動し、操作をもう一度実行します。

## <a name="there-is-no-server-by-the-specified-name-running-on-the-remote-computer"></a><a name="no_server"></a>リモート コンピュータ上で実行されている指定された名前のサーバーがありません

リモート デバッガーに接続できませんでした。 このメッセージは、次のような理由で発生することがあります。

- リモート デバッガーが別のユーザー アカウントで実行されている可能性があります。 [これらの手順を](#user_accounts)参照してください。

- ポートはファイアウォールでブロックされています。 特にサードパーティ製のファイアウォールを使用している場合は、[ファイアウォールによって要求がブロックされないこと](#firewall)を確認します。

- リモート デバッガーのバージョンが Visual Studio と一致しません。 リモート デバッガの正しいバージョンを取得するには、「[リモート デバッグ](../debugger/remote-debugging.md)」を参照してください。

## <a name="the-requested-name-was-valid-but-no-data-of-the-requested-type-was-found"></a><a name="valid_name"></a>要求された名前は有効ですが、要求された型のデータが見つかりませんでした

リモート コンピューターが存在しますが、Visual Studio はリモート デバッガーに接続できませんでした。 このメッセージは、次のような理由で発生することがあります。

- DNS の問題により接続が妨げられます。 [これらの手順](#dns)を参照してください。

- リモート デバッガーが別のユーザー アカウントで実行されている可能性があります。 次[の手順に従います](#user_accounts)。

- ポートはファイアウォールでブロックされています。 特にサードパーティ製のファイアウォールを使用している場合は、[ファイアウォールによって要求がブロックされないこと](#firewall)を確認します。

- リモート デバッガーのバージョンが Visual Studio と一致しません。 リモート デバッガの正しいバージョンを取得するには、「[リモート デバッグ](../debugger/remote-debugging.md)」を参照してください。

## <a name="the-visual-studio-remote-debugger-on-the-target-computer-cannot-connect-back-to-this-computer"></a><a name="cant_connect_back"></a>ターゲット コンピューター上の Visual Studio リモート デバッガーは、このコンピューターに接続できません。

リモート デバッガーが別のユーザー アカウントで実行されている可能性があります。 リモート デバッガーで、[**ツール] >アクセス許可を**開き、ユーザーをリモート デバッガーのアクセス許可に追加します。 詳細については、「[リモート デバッガーが別のユーザー アカウントで実行されている](#user_accounts)」を参照してください。

エラー メッセージにファイアウォールも記載されている場合は、ローカル コンピュータのファイアウォールによって、リモート コンピュータから Visual Studio への通信が妨げられている可能性があります。 [これらの手順](#firewall)を参照してください。

## <a name="access-denied"></a><a name="access_denied"></a>アクセスが拒否されました

このエラーは、32 ビット コンピューター (サポートされていない) から 64 ビットのリモート コンピューターでデバッグしようとすると表示されることがあります。

## <a name="a-security-package-specific-error-occurred"></a><a name="security_package"></a>セキュリティ パッケージ固有のエラーが発生しました

これは、Windows XP と Windows 7 に固有の従来の問題である可能性があります。 この[情報](https://stackoverflow.com/questions/4786016/unable-to-connect-to-the-microsoft-remote-debugging-monitor-a-security-package)を参照してください。

## <a name="causes-and-recommendations"></a>原因と推奨事項

### <a name="the-remote-machine-is-not-reachable"></a><a name="dns"></a> リモート コンピューターに到達できません

リモート コンピュータ名を使用して接続できない場合は、代わりに IP アドレスを使用してみます。 リモート コンピュータ`ipconfig`のコマンド ラインで IPv4 アドレスを取得できます。 HOSTS ファイルを使用している場合は、正しく設定されていることを確認します。

失敗した場合は、リモート コンピュータがネットワーク上でアクセス可能であることを確認します (リモート コンピュータに ping を[実行](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee624059(v=ws.10))します)。 一部の Microsoft Azure シナリオを除き、インターネット経由のリモート デバッグはサポートされていません。

### <a name="the-server-name-is-incorrect-or-third-party-software-is-interfering-with-the-remote-debugger"></a><a name="server_incorrect"></a>サーバー名が正しくないか、サードパーティ製ソフトウェアがリモート デバッガに干渉している

Visual Studio で、プロジェクトのプロパティを確認し、サーバー名が正しいことを確認します。 [C# および Visual Basic および](../debugger/remote-debugging-csharp.md#remote_csharp) [C++](../debugger/remote-debugging-cpp.md#remote_cplusplus)のトピックを参照してください。 ASP.NETの場合は、プロジェクトの種類に応じて **[プロパティ] / [Web/ サーバー** ] または **[プロパティ] / [デバッグ]** を開きます。

> [!NOTE]
> プロセスにアタッチする場合、プロジェクトプロパティのリモート設定は使用されません。

サーバー名が正しい場合は、ウイルス対策ソフトウェアまたはサードパーティ製のファイアウォールによってリモート デバッガがブロックされている可能性があります。 ローカルでデバッグする場合、Visual Studio は 32 ビット アプリケーションであるため、64 ビット アプリケーションをデバッグするのには、リモート デバッガーの 64 ビット バージョンを使用するため、この問題が発生する可能性があります。 32 ビットおよび 64 ビットのプロセスは、ローカル コンピューター内のローカル ネットワークを使用して通信します。 コンピューターからネットワーク トラフィックが送信されることはありませんが、サード パーティのセキュリティ ソフトウェアが通信を妨げる可能性があります。

### <a name="the-remote-debugger-is-running-under-a-different-user-account"></a><a name="user_accounts"></a>リモート デバッガーが別のユーザー アカウントで実行されている

リモート デバッガーは、既定では、リモート デバッガーを起動したユーザーと Administrators グループのメンバーからの接続のみを受け入れます。 追加のユーザーにアクセス許可を明示的に付与する必要があります。

これは、次のいずれかの方法で解消できます。

- リモート デバッガーのアクセス許可に Visual Studio ユーザーを追加します (リモート デバッガー ウィンドウで、[**ツール>アクセス許可**] を選択します)。

- リモート コンピューターで、Visual Studio コンピューターで使用しているのと同じユーザー アカウントとパスワードでリモート デバッガーを再起動します。

    > [!NOTE]
    > リモート サーバーでリモート デバッガーを実行している場合は、リモート デバッガー アプリを右クリックし、[**管理者として実行**] を選択します (または、リモート デバッガーをサービスとして実行できます)。 リモート サーバーで実行していない場合は、通常どおりに起動します。

- コマンド ラインで **/allow \<username** パラメーターに `msvsmon /allow <username@computer>` を指定してリモート デバッガーを開始します。

- または、任意のユーザーにリモート デバッグを許可することもできます。 リモート デバッガー ウィンドウで、**[ツール] > [オプション]** ダイアログに移動します。 **[認証なし]** を選択すると、 **[すべてのユーザーにデバッグを許可する]** をチェックできるようになります。 ただし、このオプションは、他のオプションが失敗した場合、またはプライベート ネットワーク上にある場合にのみ実行してください。

### <a name="the-firewall-on-the-remote-machine-doesnt-allow-incoming-connections-to-the-remote-debugger"></a><a name="firewall"></a>リモート コンピュータのファイアウォールでは、リモート デバッガへの着信接続が許可されていません
 Visual Studio とリモート デバッガーの間の通信を許可するように、Visual Studio のコンピューター上のファイアウォールとリモート コンピューター上のファイアウォールを構成する必要があります。 リモート デバッガーが使用するポートについては、「 [Remote Debugger Port Assignments](../debugger/remote-debugger-port-assignments.md)」を参照してください。 Windows ファイアウォールを構成する方法については、「 [Configure the Windows Firewall for Remote Debugging](../debugger/configure-the-windows-firewall-for-remote-debugging.md)」を参照してください。

### <a name="the-version-of-the-remote-debugger-doesnt-match-the-version-of-visual-studio"></a>リモート デバッガーのバージョンが Visual Studio のバージョンと一致していない
 ローカルで実行している Visual Studio のバージョンは、リモート コンピューターで実行されているリモート デバッグ モニターのバージョンと一致している必要があります。 これを解決するには、リモート デバッグ モニターの一致するバージョンをダウンロードして、インストールします。 リモート デバッガの正しいバージョンを取得するには、「[リモート デバッグ](../debugger/remote-debugging.md)」を参照してください。

### <a name="the-local-and-remote-machines-have-different-authentication-modes"></a>ローカル コンピューターとリモート コンピューターの認証モードが異なる
 ローカル コンピューターとリモート コンピューターで、同じ認証モードを使用する必要があります。 これを解決するには、両方のマシンで同じ認証モードを使用するようにします。 認証モードを変更できます。 リモート デバッガー ウィンドウで、[**ツール] >オプション**] ダイアログ ボックスに移動します。

 認証モードの詳細については、「 [Windows 認証の概要](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831472(v=ws.11))」を参照してください。

### <a name="anti-virus-software-is-blocking-the-connections"></a>ウイルス対策ソフトウェアが接続をブロックしている
 Windows のウイルス対策ソフトウェアがリモート デバッガーの接続を許可しても、その他のサード パーティ製のウイルス対策ソフトウェアがそれらの接続をブロックする可能性があります。 これらの接続を許可する方法については、ウイルス対策ソフトウェアのマニュアルを参照してください。

### <a name="network-security-policy-is-blocking-communication-between-the-remote-machine-and-visual-studio"></a>ネットワーク セキュリティ ポリシーによってリモート コンピューターと Visual Studio の間の通信がブロックされる
 ネットワーク セキュリティを調べ、通信をブロックしていないことを確認します。 Windows ネットワーク セキュリティ ポリシーの詳細については、「[セキュリティ ポリシーの設定](/windows/device-security/security-policy-settings/security-policy-settings)」を参照してください。

### <a name="the-network-is-too-busy-to-support-remote-debugging"></a>ネットワークがビジー状態でリモート デバッグをサポートできない
 リモート デバッグを別の時点で実行するか、ネットワークでの作業を別の時点にスケジュールし直す必要がある場合があります。

## <a name="more-help"></a>その他のヘルプ
 リモート デバッガーのヘルプを表示するには、リモート デバッガーのヘルプ ページ (ヘルプ > リモート デバッガーで**の使用法**) を開きます。

## <a name="see-also"></a>関連項目
- [リモート デバッグ](../debugger/remote-debugging.md)

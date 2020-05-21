---
title: Microsoft Visual Studio リモート デバッグ モニターに接続できません | Microsoft Docs
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
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2020
ms.locfileid: "81397377"
---
# <a name="unable-to-connect-to-the-microsoft-visual-studio-remote-debugging-monitor"></a>Microsoft Visual Studio リモート デバッグ モニターに接続できません。
このメッセージは、リモート デバッグ モニターがリモート マシンで正しく設定されていないか、ネットワークの問題やファイアウォールの存在が原因でリモート マシンにアクセスできないために発生することがあります。

> [!IMPORTANT]
> 製品のバグによりこのメッセージが表示されていると思われる場合は、Visual Studio に[この問題を報告](../ide/how-to-report-a-problem-with-visual-studio.md)してください。 その他の支援が必要な場合は、Microsoft へのお問い合わせ方法について、「 [Talk to Us](../ide/feedback-options.md) 」を参照してください。

## <a name="what-is-the-detailed-error-message"></a><a name="specificerrors"></a>詳細なエラー メッセージは何ですか?

`Unable to Connect to the Microsoft Visual Studio Remote Debugging Monitor` メッセージは汎用です。 通常、より具体的なメッセージがエラー文字列に含まれており、そこから問題の原因を特定することや、より適切な修正プログラムを検索することができます。 メイン エラー メッセージに付加される一般的なエラー メッセージの一部を次に示します。

- [デバッガーがリモート コンピューターに接続できません。指定されたコンピューター名を解決できませんでした](#cannot_connect)
- [接続要求がリモート デバッガーによって拒否されました](#rejected)
- [リモート エンドポイントとの接続が終了しました](#connection_terminated)
- [メモリの場所へのアクセスが無効です](#invalid_access)
- [指定された名前でリモート コンピューターで実行中のサーバーはありません](#no_server)
- [要求した名前は有効ですが、要求された種類のデータは見つかりませんでした](#valid_name)
- [対象コンピューター上の Visual Studio リモート デバッガーが、このコンピューターに接続できません](#cant_connect_back)
- [アクセスが拒否されました](#access_denied)
- [セキュリティ パッケージ固有エラーが発生しました](#security_package)

## <a name="the-debugger-cannot-connect-to-the-remote-computer-the-debugger-was-unable-to-resolve-the-specified-computer-name"></a><a name="cannot_connect"></a> デバッガーがリモート コンピューターに接続できません。 指定されたコンピューター名を解決できませんでした

以下の手順を試してみてください。

1. **[プロセスにアタッチ]** ダイアログ ボックスまたはプロジェクトのプロパティに有効なコンピューター名とポート番号を入力していることを確認します (プロパティを設定するには、[こちら手順](#server_incorrect)を参照してください)。 コンピューター名は、次の形式である必要があります。

    `computername:port`

    > [!NOTE]
    > ポート番号は、[リモート デバッガー (ターゲット マシン上で*実行されている必要があります*) のポート番号](../debugger/remote-debugger-port-assignments.md)と一致する必要があります。

2. コンピューター名が機能しない場合は、代わりに IP アドレスとポート番号を試します。

3. ターゲット マシン上で実行されているリモート デバッガーのバージョンが Visual Studio のバージョンと一致していることを確認します。 リモート デバッガーの正しいバージョンを取得するには、「[リモート デバッグ](../debugger/remote-debugging.md)」を参照してください。

    > [!TIP]
    > プロセスにアタッチし、正常に接続しても、目的のプロセスが表示されない場合は、 **[全ユーザーのプロセスを表示する] チェック ボックス**をオンにします。 これで、別のユーザー アカウントで接続している場合にプロセスが表示されるようになります。

4. これらの手順でこのエラーが解決しない場合は、「[リモート コンピューターに到達できません](#dns)」を参照してください。

## <a name="connection-request-was-rejected-by-the-remote-debugger"></a><a name="rejected"></a> 接続要求がリモート デバッガーによって拒否されました

**[プロセスにアタッチ]** ダイアログ ボックスまたはプロジェクトのプロパティで、リモート コンピューター名とポート番号が、リモート デバッガー ウィンドウに表示される名前とポート番号と一致していることを確認します。 正しくない場合は、修正してもう一度やり直してください。

これらの値が正しく、メッセージで **Windows 認証**モードについて触れられている場合は、リモート デバッガーが正しい認証モードであることを確認します ( **[ツール] > [オプション]** )。

## <a name="connection-with-the-remote-endpoint-was-terminated"></a><a name="connection_terminated"></a> リモート エンドポイントとの接続が終了しました

Azure App Service アプリをデバッグする場合は、 **[プロセスにアタッチ]** ではなく、Cloud Explorer またはサーバー エクスプローラーから [[デバッガーのアタッチ]](../debugger/remote-debugging-azure.md#remote_debug_azure_app_service) コマンドを使用してみてください。

**[プロセスにアタッチ]** を使用してデバッグする場合:

- **[プロセスにアタッチ]** ダイアログ ボックスまたはプロジェクトのプロパティで、リモート コンピューター名とポート番号が、リモート デバッガー ウィンドウに表示される名前とポート番号と一致していることを確認します。 正しくない場合は、修正してもう一度やり直してください。

- ホスト名を使用して接続する場合は、代わりに IP アドレスを試します。

- 問題の解決に役立つ詳細情報については、サーバー上のアプリケーション ログ (Windows 上のイベント ビューアー) を確認します。

- それ以外の場合は、管理者特権で Visual Studio を再起動してから再試行します。

## <a name="invalid-access-to-memory-location"></a><a name="invalid_access"></a> メモリの場所へのアクセスが無効です

内部エラーが発生しました。 Visual Studio を再起動し、操作をもう一度実行します。

## <a name="there-is-no-server-by-the-specified-name-running-on-the-remote-computer"></a><a name="no_server"></a> 指定された名前でリモート コンピューターで実行中のサーバーはありません

Visual Studio でリモート デバッガーに接続できませんでした。 このメッセージは、いくつかの理由で発生する可能性があります。

- 異なるユーザー アカウントを使用してリモート デバッガーを実行しています。 [こちらの手順](#user_accounts)を参照してください。

- ファイアウォールでポートがブロックされています。 特にサードパーティのファイアウォールを使用している場合は、ファイアウォールで[要求がブロックされていない](#firewall)ことを確認します。

- リモート デバッガーのバージョンが Visual Studio と一致しません。 リモート デバッガーの正しいバージョンを取得するには、「[リモート デバッグ](../debugger/remote-debugging.md)」を参照してください。

## <a name="the-requested-name-was-valid-but-no-data-of-the-requested-type-was-found"></a><a name="valid_name"></a> 要求した名前は有効ですが、要求された種類のデータは見つかりませんでした

リモート コンピューターは存在しますが、Visual Studio からリモート デバッガーに接続できませんでした。 このメッセージは、いくつかの理由で発生する可能性があります。

- DNS の問題が原因で接続できません。 [こちらの手順](#dns)を参照してください。

- 異なるユーザー アカウントを使用してリモート デバッガーを実行しています。 [以下の手順](#user_accounts)に従ってください。

- ファイアウォールでポートがブロックされています。 特にサードパーティのファイアウォールを使用している場合は、ファイアウォールで[要求がブロックされていない](#firewall)ことを確認します。

- リモート デバッガーのバージョンが Visual Studio と一致しません。 リモート デバッガーの正しいバージョンを取得するには、「[リモート デバッグ](../debugger/remote-debugging.md)」を参照してください。

## <a name="the-visual-studio-remote-debugger-on-the-target-computer-cannot-connect-back-to-this-computer"></a><a name="cant_connect_back"></a> 対象コンピューター上の Visual Studio リモート デバッガーが、このコンピューターに接続できません

異なるユーザー アカウントを使用してリモート デバッガーを実行しています。 リモート デバッガーで **[ツール] > [アクセス許可]** を開き、ユーザーをリモート デバッガーのアクセス許可に追加します。 詳細については、「[異なるユーザー アカウントを使用してリモート デバッガーを実行している](#user_accounts)」を参照してください。

エラー メッセージでファイアウォールについても触れられている場合は、ローカル コンピューター上のファイアウォールが原因で、リモート コンピューターから Visual Studio に通信できない可能性があります。 [こちらの手順](#firewall)を参照してください。

## <a name="access-denied"></a><a name="access_denied"></a> アクセスが拒否されました

(サポートされていない) 32 ビット コンピューターから 64 ビット リモート コンピューター上でデバッグしようとすると、このエラーが表示されることがあります。

## <a name="a-security-package-specific-error-occurred"></a><a name="security_package"></a> セキュリティ パッケージ固有エラーが発生しました

これは、Windows XP および Windows 7 に固有の従来の問題である可能性があります。 こちらの[情報](https://stackoverflow.com/questions/4786016/unable-to-connect-to-the-microsoft-remote-debugging-monitor-a-security-package)を参照してください。

## <a name="causes-and-recommendations"></a>原因と推奨事項

### <a name="the-remote-machine-is-not-reachable"></a><a name="dns"></a> リモート コンピューターに到達できません

リモート コンピューター名を使用して接続できない場合は、代わりに IP アドレスを使用してみてください。 リモート コンピューターのコマンド ラインで `ipconfig` を使用して、IPv4 アドレスを取得することができます。 HOSTS ファイルを使用している場合は、正しく構成されていることを確認します。

それでも失敗する場合は、ネットワーク上でリモート コンピューターにアクセスできることを確認します (リモート マシンの [ping](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee624059(v=ws.10)))。 一部の Microsoft Azure シナリオを除き、インターネット経由のリモート デバッグはサポートされていません。

### <a name="the-server-name-is-incorrect-or-third-party-software-is-interfering-with-the-remote-debugger"></a><a name="server_incorrect"></a> サーバー名が正しくないか、サードパーティ製ソフトウェアがリモート デバッガーに干渉している

Visual Studio でプロジェクトのプロパティを調べて、サーバー名が正しいことを確認します。 [C# および Visual Basic](../debugger/remote-debugging-csharp.md#remote_csharp) と [C++ ](../debugger/remote-debugging-cpp.md#remote_cplusplus) のトピックを参照してください。 ASP.NET の場合は、プロジェクトの種類に応じて、 **[プロパティ] / [Web] / [サーバー]** または **[プロパティ] / [デバッグ]** を開きます。

> [!NOTE]
> プロセスにアタッチする場合、プロジェクトのプロパティのリモート設定は使用されません。

サーバー名が正しい場合は、ウイルス対策ソフトウェアまたはサードパーティのファイアウォールによってリモート デバッガーがブロックされている可能性があります。 ローカルでデバッグしている場合、Visual Studio が 32 ビット アプリケーションであり、64 ビット アプリケーションのデバッグには 64 ビット バージョンのリモート デバッガーが使用されるためにこれが発生する可能性があります。 32 ビットおよび 64 ビット プロセスは、ローカル コンピューター内のローカル ネットワークを使用して通信します。 コンピューターからネットワーク トラフィックが送信されることはありませんが、サード パーティのセキュリティ ソフトウェアが通信を妨げる可能性があります。

### <a name="the-remote-debugger-is-running-under-a-different-user-account"></a><a name="user_accounts"></a> 異なるユーザー アカウントを使用してリモート デバッガーを実行している

リモート デバッガーは、既定では、リモート デバッガーを起動したユーザーと Administrators グループのメンバーからの接続のみを受け入れます。 その他のユーザーには、アクセス許可を明示的に付与する必要があります。

これは、次のいずれかの方法で解消できます。

- Visual Studio ユーザーをリモート デバッガーのアクセス許可に追加します (リモート デバッガー ウィンドウで、 **[ツール] > [アクセス許可]** を選択します)。

- リモート コンピューター上で、Visual Studio コンピューター上で使用しているものと同じユーザー アカウントとパスワードを使用してリモート デバッガーを再起動します。

    > [!NOTE]
    > リモート サーバー上でリモート デバッガーを実行している場合は、リモート デバッガー アプリを右クリックし、 **[管理者として実行]** を選択します (または、リモート デバッガーをサービスとして実行できます)。 リモート サーバー上で実行していない場合は、通常どおり起動します。

- コマンド ラインで **/allow \<username** パラメーターに `msvsmon /allow <username@computer>` を指定してリモート デバッガーを開始します。

- または、任意のユーザーがリモート デバッグを実行できるようにすることもできます。 リモート デバッガー ウィンドウで、 **[ツール] > [オプション]** ダイアログに移動します。 **[認証なし]** を選択すると、 **[すべてのユーザーにデバッグを許可する]** をチェックできるようになります。 ただし、他のオプションが失敗した場合、またはプライベート ネットワーク上の場合にのみ、このオプションを試します。

### <a name="the-firewall-on-the-remote-machine-doesnt-allow-incoming-connections-to-the-remote-debugger"></a><a name="firewall"></a> リモート コンピューター上のファイアウォールがリモート デバッガーへの着信接続を許可しない
 Visual Studio とリモート デバッガーの間の通信を許可するように、Visual Studio のコンピューター上のファイアウォールとリモート コンピューター上のファイアウォールを構成する必要があります。 リモート デバッガーが使用するポートについては、「 [Remote Debugger Port Assignments](../debugger/remote-debugger-port-assignments.md)」を参照してください。 Windows ファイアウォールを構成する方法については、「 [Configure the Windows Firewall for Remote Debugging](../debugger/configure-the-windows-firewall-for-remote-debugging.md)」を参照してください。

### <a name="the-version-of-the-remote-debugger-doesnt-match-the-version-of-visual-studio"></a>リモート デバッガーのバージョンが Visual Studio のバージョンと一致していない
 ローカルで実行している Visual Studio のバージョンは、リモート コンピューターで実行されているリモート デバッグ モニターのバージョンと一致している必要があります。 これを解決するには、リモート デバッグ モニターの一致するバージョンをダウンロードして、インストールします。 リモート デバッガーの正しいバージョンを取得するには、「[リモート デバッグ](../debugger/remote-debugging.md)」を参照してください。

### <a name="the-local-and-remote-machines-have-different-authentication-modes"></a>ローカル コンピューターとリモート コンピューターの認証モードが異なる
 ローカル コンピューターとリモート コンピューターで、同じ認証モードを使用する必要があります。 これを解決するには、両方のマシンで同じ認証モードを使用するようにします。 認証モードを変更することができます。 リモート デバッガー ウィンドウで、 **[ツール] > [オプション]** ダイアログ ボックスに移動します。

 認証モードの詳細については、「 [Windows 認証の概要](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831472(v=ws.11))」を参照してください。

### <a name="anti-virus-software-is-blocking-the-connections"></a>ウイルス対策ソフトウェアが接続をブロックしている
 Windows のウイルス対策ソフトウェアがリモート デバッガーの接続を許可しても、その他のサード パーティ製のウイルス対策ソフトウェアがそれらの接続をブロックする可能性があります。 これらの接続を許可する方法については、ウイルス対策ソフトウェアのマニュアルを参照してください。

### <a name="network-security-policy-is-blocking-communication-between-the-remote-machine-and-visual-studio"></a>ネットワーク セキュリティ ポリシーによってリモート コンピューターと Visual Studio の間の通信がブロックされる
 ネットワーク セキュリティを調べ、通信をブロックしていないことを確認します。 Windows ネットワーク セキュリティ ポリシーの詳細については、「[セキュリティ ポリシー設定](/windows/device-security/security-policy-settings/security-policy-settings)」を参照してください。

### <a name="the-network-is-too-busy-to-support-remote-debugging"></a>ネットワークがビジー状態でリモート デバッグをサポートできない
 リモート デバッグを別の時点で実行するか、ネットワークでの作業を別の時点にスケジュールし直す必要がある場合があります。

## <a name="more-help"></a>その他のヘルプ
 リモート デバッガーのヘルプをさらに表示するには、リモート デバッガーの [ヘルプ] ページを開きます (リモート デバッガーの **[ヘルプ] > [使用法]** )。

## <a name="see-also"></a>関連項目
- [Remote Debugging](../debugger/remote-debugging.md)

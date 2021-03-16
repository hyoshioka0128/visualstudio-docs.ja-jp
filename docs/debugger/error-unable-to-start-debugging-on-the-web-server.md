---
description: Web サーバーで実行されている ASP.NET アプリケーションをデバッグしようとする場合、"Web サーバーでデバッグを開始できません" というエラー メッセージが表示されることがあります。
title: Web サーバー上でデバッグを開始できません | Microsoft Docs
ms.date: 05/23/2018
ms.topic: error-reference
f1_keywords:
- vs.debug.error.http
- vwd.nonadmin.error.
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- IIS, debugging DLLs
- debugger, Web application errors
- unable to start debugging error
- security [debugger], Web applications
- debugging [Visual Studio], errors
- HTTP servers, debugging error
- security settings, checking for default Web sites
- errors [debugger], unable to start debugging
- debugging ASP.NET Web applications, unable to start debugging error
- remote debugging, errors
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 91fa3f74c5dd0f5f6a036d5da7a779e68462c426
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102146367"
---
# <a name="error-unable-to-start-debugging-on-the-web-server"></a>エラー :Web サーバー上でデバッグを開始できません

Web サーバーで実行している ASP.NET アプリケーションのデバッグを試行すると、`Unable to start debugging on the Web server` というエラー メッセージが表示される場合があります。

多くの場合、このエラーが発生するのは、アプリケーション プールの更新または IIS のリセット (あるいは両方) を必要とするエラーまたは構成変更が発生した場合です。 IIS は、管理者特権でのコマンド プロンプトを開いて `iisreset` と入力すると、リセットできます。

## <a name="what-is-the-detailed-error-message"></a><a name="specificerrors"></a>詳細なエラー メッセージは何ですか?

`Unable to start debugging on the Web server` メッセージは汎用です。 通常、より具体的なメッセージがエラー文字列に含まれており、そこから問題の原因を特定することや、より適切な修正プログラムを検索することができます。 メイン エラー メッセージに付加される一般的なエラー メッセージの一部を次に示します。

- [IIS does not list a website that matches the launch url\(起動 URL と一致する Web サイトが IIS によって一覧表示されません\)](#IISlist)
- [Web サーバーは正しく構成されていません](#web_server_config)
- [Web サーバーに接続できません](#unabletoconnect)
- [Web サーバーが時間内に応答を返しませんでした](#webservertimeout)
- [Microsoft Visual Studio リモート デバッグ モニター (msvsmon.exe) は、リモート コンピューター上では実行されていません。](#msvsmon)
- [リモート サーバーがエラーを返しました](#server_error)
- [ASP.NET のデバッグを開始できませんでした](#aspnet)
- [デバッガーがリモート コンピューターに接続できません](#cannot_connect)
- [一般的な構成エラーについてはヘルプを参照してください。Web ページをデバッガーの外で実行することによって、これ以外の情報を得られる場合があります。](#see_help)
- [操作はサポートされていません。不明なエラー: "*エラー番号*" のようなエラー メッセージが表示されます。](#operation_not_supported)

## <a name="iis-does-not-list-a-website-that-matches-the-launch-url"></a><a name="IISlist"></a> IIS does not list a website that matches the launch url\(起動 URL と一致する Web サイトが IIS によって一覧表示されません\)

- 管理者として Visual Studio を起動し、デバッグを再試行します。 (一部の ASP.NET のデバッグ シナリオでは、昇格された特権が必要です。)

    Visual Studio を常に管理者として実行するように構成するには、Visual Studio のショートカット アイコンを右クリックし、 **[プロパティ] > [詳細設定]** を選択し、常に管理者として実行することを選択します。

## <a name="the-web-server-is-not-configured-correctly"></a><a name="web_server_config"></a> Web サーバーは正しく構成されていません

- 各デプロイ シナリオの回避策については、サポート フォーラムで、[エラー:Web サーバーは正しく構成されていません](../debugger/error-the-web-server-is-not-configured-correctly.md)」を参照してください。

## <a name="unable-to-connect-to-the-webserver"></a><a name="unabletoconnect"></a> Web サーバーに接続できません

- Visual Studio と Web サーバーを同じコンピューターで実行しており、**F5** キー ( **[プロセスにアタッチ]** ではなく) を使用してデバッグしていませんか。 プロジェクトのプロパティを開いて、適切な Web サーバーと起動 URL に接続するようにプロジェクトが構成されていることを確認します。 (プロジェクトの種類に応じて、 **[プロパティ] > [Web] > [サーバー]** または **[プロパティ] > [デバッグ]** を開きます。 Web Forms プロジェクトの場合は、 **[プロパティ ページ] > [開始オプション] > [サーバー]** を開きます。)

- それ以外の場合は、アプリケーション プールを再起動し、IIS をリセットします。 詳細については、「[IIS 構成を確認する](#vxtbshttpservererrorsthingstocheck)」を参照してください。

## <a name="the-web-server-did-not-respond-in-a-timely-manner"></a><a name="webservertimeout"></a>Web サーバーが時間内に応答を返しませんでした

- IIS をリセットして、デバッグを再試行します。 複数のデバッガー インスタンスを IIS プロセスにアタッチすることができます。リセットによってこれが終了します。 詳細については、「[IIS 構成を確認する](#vxtbshttpservererrorsthingstocheck)」を参照してください。

## <a name="the-microsoft-visual-studio-remote-debugging-monitormsvsmonexe-does-not-appear-to-be-running-on-the-remote-computer"></a><a name="msvsmon"></a> Microsoft Visual Studio リモート デバッグ モニター (msvsmon.exe) は、リモート コンピューター上では実行されていません。

- リモート コンピューターでデバッグしている場合は、[リモート デバッガーをインストールして実行している](../debugger/remote-debugging.md)ことを確認します。 ファイアウォールに関する内容がメッセージに含まれている場合は、[ファイアウォールの正しいポート](../debugger/remote-debugger-port-assignments.md)が開いていることを確認します (特にサードパーティのファイアウォールを使用している場合)。
- HOSTS ファイルを使用している場合は、正しく構成されていることを確認します。 たとえば、**F5** キー ( **[プロセスにアタッチ]** ではなく) を使用してデバッグしている場合、HOSTS ファイルに、プロジェクトのプロパティと同じプロジェクト URL (プロジェクトの種類に応じて、 **[プロパティ] > [Web] > [サーバー]** または **[プロパティ] > [デバッグ]** ) が含まれる必要があります。

## <a name="the-remote-server-returned-an-error"></a><a name="server_error"></a> リモート サーバーがエラーを返しました

[IIS ログ ファイル](https://support.microsoft.com/help/943891/the-http-status-code-in-iis-7-0--iis-7-5--and-iis-8-0)でエラー サブコードおよびその他の情報を調べ、この IIS 7 の[ブログ記事](https://blogs.iis.net/tomkmvp/troubleshoot-a-403)を参照してください。

また、ここで一般的なエラー コードといくつかの推奨事項についても説明します。
- (403) 禁止。 このエラーには多くの原因が考えられます。そのため、ログ ファイルと Web サイトの IIS セキュリティ設定を確認してください。 サーバーの web.config で、コンパイル要素に `debug=true` が含まれていることを確認します。 Web アプリケーション フォルダーに適切なアクセス許可があり、アプリケーション プール構成が正しいことを確認します (パスワードが変更された可能性があります)。 「[IIS 構成を確認する](#vxtbshttpservererrorsthingstocheck)」を参照してください。 これらの設定が既に正しく、ローカルでデバッグしている場合は、適切なサーバーの種類と URL に接続していることも確認します(プロジェクトの種類に応じて、 **[プロパティ] > [Web] > [サーバー]** または **[プロパティ] > [デバッグ]** )。
- (503) サーバーは使用できません。 エラーまたは構成の変更のために、アプリケーション プールが停止した可能性があります。 アプリケーション プールを再起動します。
- (404) 見つかりません。 アプリケーション プールが正しいバージョンの ASP.NET に構成されていることを確認してください。

## <a name="could-not-start-aspnet-debugging"></a><a name="aspnet"></a> ASP.NET のデバッグを開始できませんでした

- アプリケーション プールを再起動し、IIS をリセットします。 詳細については、「[IIS 構成を確認する](#vxtbshttpservererrorsthingstocheck)」を参照してください。
- URL の書き換えを行っている場合は、URL の書き換えなしの基本的な web.config をテストします。 「[IIS 構成を確認する](#vxtbshttpservererrorsthingstocheck)」で URL Rewrite Module に関する「**注意**」を参照してください。

## <a name="the-debugger-cannot-connect-to-the-remote-computer"></a><a name="cannot_connect"></a> デバッガーがリモート コンピューターに接続できません

ローカルでデバッグしている場合は、Visual Studio でプロジェクトのプロパティを開いて、適切な Web サーバーと URL に接続するようにプロジェクトが構成されていることを確認します。 (プロジェクトの種類に応じて、 **[プロパティ] > [Web] > [サーバー]** または **[プロパティ] > [デバッグ]** を開きます。)

このエラーはローカルでデバッグしている場合に発生する可能性があります。Visual Studio が 32 ビット アプリケーションであり、64 ビット アプリケーションのデバッグには 64 ビット バージョンのリモート デバッガーが使用されるためです。 IIS のアプリケーション プールを調べて、 **[32 ビット アプリケーションの有効化]** が `true` に設定されていることを確認し、IIS を再起動して、再び実行します。

また、HOSTS ファイルを使用している場合は、正しく構成されていることを確認します。 たとえば、HOSTS ファイルに、プロジェクトのプロパティと同じプロジェクト URL (プロジェクトの種類に応じて、 **[プロパティ] > [Web] > [サーバー]** または **[プロパティ] > [デバッグ]** ) が含まれる必要があります。

## <a name="see-help-for-common-configuration-errors-running-the-webpage-outside-of-the-debugger-may-provide-further-information"></a><a name="see_help"></a> 一般的な構成エラーについてはヘルプを参照してください。 Web ページをデバッガーの外で実行することによって、これ以外の情報を得られる場合があります。

- 同じコンピューターで Visual Studio と Web サーバーを実行していますか。 プロジェクトのプロパティを開いて、適切な Web サーバーと起動 URL に接続するようにプロジェクトが構成されていることを確認します。 (プロジェクトの種類に応じて、 **[プロパティ] > [Web] > [サーバー]** または **[プロパティ] > [デバッグ]** を開きます。)

- これが機能しない場合、またはリモートでデバッグしている場合は、「[IIS 構成を確認する](#vxtbshttpservererrorsthingstocheck)」のステップに従います。

## <a name="operation-not-supported-unknown-error-errornumber"></a><a name="operation_not_supported"></a> 操作はサポートされていません。 不明なエラー: "*エラー番号*" のようなエラー メッセージが表示されます。

URL の書き換えを行っている場合は、URL の書き換えなしの基本的な web.config をテストします。 「[IIS 構成を確認する](#vxtbshttpservererrorsthingstocheck)」で URL Rewrite Module に関する「**注意**」を参照してください。

## <a name="check-your-iis-configuration"></a><a name="vxtbshttpservererrorsthingstocheck"></a> IIS 構成を確認する

ここで詳しく説明するステップを実行して問題を解決した後で、再びデバッグを開始する前に、場合によっては IIS をリセットする必要もあります。 これを行うには、管理者特権でのコマンド プロンプトを開いて「`iisreset`」と入力します。

* IIS アプリケーション プールを停止して再起動してから、もう一度やり直します。

    エラーのため、アプリケーション プールが停止している可能性があります。 また、別の構成を変更したことで、アプリケーション プールの停止と再起動が必要になる場合があります。

    > [!NOTE]
    > アプリケーション プールが停止したままの場合、[コントロール パネル] から URL Rewrite Module をアンインストールする必要がある場合があります。 Web Platform Installer (WebPI) を使用して再インストールできます。 この問題は、システムの大規模なアップグレード後に発生する可能性があります。

* アプリケーション プールの構成を確認し、必要に応じて修正してから、やり直します。

    アプリケーション プールが、Visual Studio プロジェクトと一致しないバージョンの ASP.NET 用に構成されている可能性があります。 アプリケーション プールの ASP.NET バージョンを更新して、再起動します。 詳細については、「[ASP.NET 3.5 と ASP.NET 4.5 を使用する IIS 8.0](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45)」を参照してください。

    また、パスワードの資格情報が変更されている場合は、アプリケーション プールまたは Web サイトでそれらを更新する必要があります。  アプリケーション プールで、 **[詳細設定] > [プロセス モデル] > [ID]** で資格情報を更新します。 Web サイトの場合は **[基本設定] > [ユーザー名を指定して接続]** で資格情報を更新します。アプリケーション プールを再起動します。

* Web アプリケーション フォルダーに適切なアクセス許可があることを確認します。

    IIS_IUSRS、IUSR、または[アプリケーション プール](/iis/manage/configuring-security/application-pool-identities)に関連付けた特定のユーザーに、Web アプリケーション フォルダーの読み取り権限と実行権限を付与していることを確認します。 問題を解決し、アプリケーション プールを再起動します。

* ASP.NET の正しいバージョンが IIS にインストールされていることを確認します。

    ASP.NET の IIS 上のバージョンと Visual Studio プロジェクト内のバージョンの不一致によって、この問題が発生することがあります。 web.config 内にフレームワークのバージョンの設定が必要な可能性があります。IIS に ASP.NET をインストールするには、[Web Platform Installer (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx) を使用します。 「[ASP.NET 3.5 と ASP.NET 4.5 を使用する IIS 8.0](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45)」も参照してください。ASP.NET Core の場合は、「[IIS を使用して Windows でホストする](https://docs.asp.net/en/latest/publishing/iis.html)」を参照してください。

* IP アドレスのみを使用している場合は、認証エラーを解決します

     既定では、IP アドレスはインターネットの一部と見なされ、インターネット上では NTLM 認証が行われません。 Web サイトが認証を要求するように IIS で構成されている場合、この認証は失敗します。 この問題を解決するには、IP アドレスではなくリモート コンピューターの名前を指定することができます。

## <a name="other-causes"></a>その他の原因

IIS 構成が問題の原因になっていない場合は、次のステップを試してください。

- 管理者特権で Visual Studio を起動し、やり直します。

    Web 配置の使用など、一部の ASP.NET デバッグ シナリオでは、Visual Studio の昇格された特権が必要です。

- Visual Studio の複数のインスタンスが実行されている場合は、(管理者特権を持つ) Visual Studio の 1 つのインスタンスでプロジェクトを再度開いて、もう一度やり直してください。

- ローカル アドレスを含む HOSTS ファイルを使用している場合は、コンピューターの IP アドレスの代わりにループバック アドレスを使用してみてください。

    ローカル アドレスを使用していない場合は、HOSTS ファイルに、プロジェクトのプロパティと同じプロジェクト URL (プロジェクトの種類に応じて、 **[プロパティ] > [Web] > [サーバー]** または **[プロパティ] > [デバッグ]** ) が含まれることを確認します。

## <a name="more-troubleshooting-steps"></a>その他のトラブルシューティングの手順

* サーバーでブラウザーに localhost ページを表示します

     IIS が正しくインストールされていない場合、ブラウザーに `http://localhost` を入力するとエラーが表示されます。

     IIS の展開の詳細については、「[ASP.NET 3.5 および ASP.NET 4.5 を使用する IIS 8.0](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45)」、ASP.NET Core については、「[IIS による Windows 上のホスト](https://docs.asp.net/en/latest/publishing/iis.html)」を参照してください。

* サーバー上に基本的な ASP.NET アプリケーションを作成します (または、基本の web.config ファイルを使用します)。

    アプリとデバッガーを連携できない場合は、基本の ASP.NET アプリケーションをサーバー上にローカルに作成してみて、基本のアプリのデバッグを試してください。 (既定の ASP.NET MVC テンプレートを使用することもできます。)基本のアプリをデバッグできれば、2 つの構成の間の違いを特定することに役立ちます。 URL の書き換えルールなど、web.config ファイルで設定の違いを探してください。

## <a name="see-also"></a>関連項目
- [Web アプリケーションのデバッグ: エラーとトラブルシューティング](../debugger/debugging-web-applications-errors-and-troubleshooting.md)

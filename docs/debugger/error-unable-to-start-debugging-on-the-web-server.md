---
title: 'エラー: Web サーバーでデバッグを開始できません |Microsoft Docs'
ms.date: 05/23/2018
ms.topic: troubleshooting
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2f0e3666c313c55df605cd7b79199827765f40f3
ms.sourcegitcommit: 8e123bcb21279f2770b28696995450270b4ec0e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75404354"
---
# <a name="error-unable-to-start-debugging-on-the-web-server"></a>エラー ： Web サーバーでデバッグを開始できません

Web サーバーで実行されている ASP.NET アプリケーションをデバッグしようとすると、次のエラーメッセージが表示される場合があります: `Unable to start debugging on the Web server`。

多くの場合、このエラーは、アプリケーションプール、IIS のリセット、またはその両方を更新する必要があるエラーまたは構成の変更が発生したことが原因で発生します。 管理者特権でのコマンドプロンプトを開いて `iisreset`を入力すると、IIS をリセットできます。

## <a name="specificerrors"></a>詳細なエラーメッセージは何ですか?

`Unable to start debugging on the Web server` メッセージは汎用です。 通常、より具体的なメッセージがエラー文字列に含まれ、問題の原因を特定したり、より正確な修正プログラムを検索したりするのに役立ちます。 メインエラーメッセージに追加される一般的なエラーメッセージのいくつかを次に示します。

- [IIS では、起動 url に一致する web サイトが一覧表示されない](#IISlist)
- [Web サーバーは正しく構成されていません](#web_server_config)
- [Web サーバーに接続できません](#unabletoconnect)
- [Web サーバーが時間内に応答しませんでした](#webservertimeout)
- [Microsoft Visual Studio リモート デバッグ モニター (msvsmon.exe) は、リモート コンピューター上では実行されていません。](#msvsmon)
- [リモートサーバーからエラーが返されました](#server_error)
- [ASP.NET デバッグを開始できませんでした](#aspnet)
- [デバッガーがリモートコンピューターに接続できません](#cannot_connect)
- [一般的な構成エラーについては、ヘルプを参照してください。デバッガーの外部で web ページを実行すると、詳細情報が提供される場合があります。](#see_help)
- [サポートされていない操作です。不明なエラー:*エラー番号*](#operation_not_supported)

## <a name="IISlist"></a>IIS では、起動 url に一致する web サイトが一覧表示されない

- 管理者として Visual Studio を再起動して、デバッグを再試行してください。 (一部の ASP.NET のデバッグシナリオでは、昇格された特権が必要です)。

    Visual Studio のショートカットアイコンを右クリックし、 **[プロパティ > 詳細設定]** をクリックして、常に管理者として実行するように選択すると、visual Studio を管理者として常に実行するように構成できます。

## <a name="web_server_config"></a> Web サーバーは正しく構成されていません

- 「[エラー: web サーバーが正しく構成されていません」を](../debugger/error-the-web-server-is-not-configured-correctly.md)参照してください。

## <a name="unabletoconnect"></a>Web サーバーに接続できません

- Visual Studio と Web サーバーを同じコンピューターで実行し、 **F5 キー**を使用してデバッグしますか (**プロセスにアタッチ**するのではなく)。 プロジェクトのプロパティを開き、適切な Web サーバーと起動 URL に接続するようにプロジェクトが構成されていることを確認します。 ([**プロパティ] > [Web > サーバー**またはプロパティ] を開いて、プロジェクトの種類に応じて**デバッグ >** ます。 Web フォームプロジェクトの場合は、[プロパティページ] を開き **> [オプション > サーバーの開始] を選択**します)。

- それ以外の場合は、アプリケーションプールを再起動し、IIS をリセットします。 詳細については、「 [IIS 構成を確認する](#vxtbshttpservererrorsthingstocheck)」を参照してください。

## <a name="webservertimeout"></a>Web サーバーが時間内に応答しませんでした

- IIS をリセットし、デバッグを再試行します。 複数のデバッガーインスタンスを IIS プロセスにアタッチすることができます。リセットによって終了します。 詳細については、「 [IIS 構成を確認する](#vxtbshttpservererrorsthingstocheck)」を参照してください。

## <a name="msvsmon"></a> Microsoft Visual Studio リモート デバッグ モニター (msvsmon.exe) は、リモート コンピューター上では実行されていません。

- リモートコンピューターでデバッグしている場合は、[リモートデバッガーをインストールして実行](../debugger/remote-debugging.md)していることを確認します。 メッセージにファイアウォールがある場合は、[ファイアウォールの正しいポート](../debugger/remote-debugger-port-assignments.md)が開いていることを確認します (特にサードパーティのファイアウォールを使用している場合)。
- HOSTS ファイルを使用している場合は、正しく構成されていることを確認します。 たとえば、 **F5 キー** (**プロセスにアタッチする**のではなく) を使用してデバッグする場合、ホストファイルにはプロジェクトのプロパティと同じプロジェクト URL を含める必要があります。また、プロジェクトの種類に応じて、[**プロパティ] > [Web > サーバー** ] または [プロパティ] に**デバッグ >** ます。

## <a name="server_error"></a>リモートサーバーからエラーが返されました

[Iis ログファイル](https://support.microsoft.com/help/943891/the-http-status-code-in-iis-7-0--iis-7-5--and-iis-8-0)で、エラーのサブコードと追加情報、およびこの iis 7 の[ブログ記事](https://blogs.iis.net/tomkmvp/troubleshoot-a-403)を確認してください。

また、一般的なエラーコードといくつかの推奨事項についても説明します。
- (403) 禁止。 このエラーには多くの原因が考えられます。そのため、web サイトのログファイルと IIS のセキュリティ設定を確認してください。 サーバーの web.config に、コンパイル要素に `debug=true` が含まれていることを確認します。 Web アプリケーションフォルダーに適切なアクセス許可があり、アプリケーションプールの構成が正しいことを確認します (パスワードが変更された可能性があります)。 「 [IIS 構成を確認する](#vxtbshttpservererrorsthingstocheck)」を参照してください。 これらの設定が既に正しく、ローカルでデバッグしている場合は、適切なサーバーの種類と URL に接続していることも確認します (プロジェクトの種類に応じて、**プロパティ > Web > サーバー**  または **プロパティ > デバッグ** をオンにします)。
- (503) サーバーは使用できません。 エラーまたは構成の変更により、アプリケーションプールが停止した可能性があります。 アプリケーションプールを再起動します。
- (404) 見つかりません。 アプリケーションプールが正しいバージョンの ASP.NET に構成されていることを確認してください。

## <a name="aspnet"></a>ASP.NET デバッグを開始できませんでした

- アプリケーションプールを再起動し、IIS をリセットします。 詳細については、「 [IIS 構成を確認する](#vxtbshttpservererrorsthingstocheck)」を参照してください。
- URL の書き換えを行う場合は、URL 書き換えを行わずに基本的な web.config をテストします。 「 [IIS 構成を確認](#vxtbshttpservererrorsthingstocheck)する」の URL 書き換えモジュールに関する**注意事項**を参照してください。

## <a name="cannot_connect"></a>デバッガーがリモートコンピューターに接続できません

ローカルでデバッグしている場合は、Visual Studio でプロジェクトのプロパティを開き、適切な Web サーバーと URL に接続するようにプロジェクトが構成されていることを確認します。 (プロジェクトの種類によっては、 **Web > サーバー**またはプロパティ > 開いて**デバッグ >** ます)。

このエラーは、Visual Studio が32ビットアプリケーションであるためにローカルでデバッグするときに発生する可能性があります。そのため、64ビット版のリモートデバッガーを使用して64ビットアプリケーションをデバッグします。 IIS のアプリプールを調べて、[ **32 ビットアプリケーションを有効に**する] が `true`に設定されていることを確認し、iis を再起動して、もう一度やり直してください。

また、ホストファイルを使用している場合は、正しく構成されていることを確認してください。 たとえば、ホストファイルには、プロジェクトのプロパティ、**プロパティ > Web > サーバー**またはプロパティのように、プロジェクトの種類に応じて **[デバッグ >]** と同じプロジェクト URL を含める必要があります。

## <a name="see_help"></a> 一般的な構成エラーについてはヘルプを参照してください。 デバッガーの外部で web ページを実行すると、詳細情報が提供される場合があります。

- 同じコンピューターで Visual Studio と Web サーバーを実行していますか? プロジェクトのプロパティを開き、適切な Web サーバーと起動 URL に接続するようにプロジェクトが構成されていることを確認します。 (プロジェクトの種類によっては、 **Web > サーバー**またはプロパティ > 開いて**デバッグ >** ます)。

- これが機能しない場合、またはリモートでデバッグしている場合は、「 [IIS 構成を確認](#vxtbshttpservererrorsthingstocheck)する」の手順に従います。

## <a name="operation_not_supported"></a>サポートされていない操作です。 不明なエラー:*エラー番号*

URL の書き換えを行う場合は、URL 書き換えを行わずに基本的な web.config をテストします。 「 [IIS 構成を確認](#vxtbshttpservererrorsthingstocheck)する」の URL 書き換えモジュールに関する**注意事項**を参照してください。

## <a name="vxtbshttpservererrorsthingstocheck"></a>IIS の構成を確認する

ここで説明する手順を実行して問題を解決した後、デバッグを再試行する前に、IIS のリセットが必要になる場合もあります。 これを行うには、管理者特権でのコマンドプロンプトを開き、`iisreset`入力します。

* IIS アプリケーションプールを停止して再起動してから、もう一度やり直してください。

    エラーのため、アプリケーションプールが停止している可能性があります。 また、別の構成を変更した場合は、アプリケーションプールを停止して再起動することが必要になることがあります。

    > [!NOTE]
    > アプリケーションプールが停止し続ける場合は、コントロールパネルから URL リライトモジュールをアンインストールする必要がある場合があります。 Web Platform Installer (WebPI) を使用して再インストールできます。 この問題は、システムの大規模なアップグレード後に発生する可能性があります。

* アプリケーションプールの構成を確認し、必要に応じて修正してから、再試行してください。

    アプリケーションプールが、Visual Studio プロジェクトに一致しないバージョンの ASP.NET 用に構成されている可能性があります。 アプリケーションプールの ASP.NET バージョンを更新し、再起動します。 詳細については、「 [ASP.NET 3.5 と ASP.NET 4.5 を使用した IIS 8.0](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45)」を参照してください。

    また、パスワードの資格情報が変更されている場合は、アプリケーションプールまたは Web サイトでそれらを更新する必要があります。  アプリケーションプールで、 **[詳細設定] > [プロセスモデル > id**] の資格情報を更新します。 Web サイトの場合は、[基本設定] で資格情報を更新し **> 接続**します。アプリケーションプールを再起動します。

* Web アプリケーションフォルダーに適切なアクセス許可があることを確認します。

    [アプリケーションプール](/iis/manage/configuring-security/application-pool-identities)に関連付けられている IIS_IUSRS、IUSR、または特定のユーザーに、Web アプリケーションフォルダーの読み取りと実行の権限を付与してください。 問題を解決し、アプリケーションプールを再起動してください。

* IIS に正しいバージョンの ASP.NET がインストールされていることを確認してください。

    IIS と Visual Studio プロジェクトで ASP.NET のバージョンが一致しないと、この問題が発生する可能性があります。 場合によっては、web.config でフレームワークのバージョンを設定する必要があります。IIS に ASP.NET をインストールするには、 [Web Platform Installer (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx)を使用します。 また、 [ASP.NET 3.5 と ASP.NET 4.5 を使用した iis 8.0](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45) 、ASP.NET Core の場合は[iis を使用した Windows でのホスト](https://docs.asp.net/en/latest/publishing/iis.html)を参照してください。

* IP アドレスのみを使用している場合は、認証エラーを解決します

     既定では、IP アドレスはインターネットの一部と見なされ、インターネット上では NTLM 認証が行われません。 Web サイトが IIS で認証を要求するように構成されている場合、この認証は失敗します。 この問題を解決するには、IP アドレスではなく、リモートコンピューターの名前を指定します。

## <a name="other-causes"></a>その他の原因

IIS 構成が問題の原因になっていない場合は、次の手順を試してください。

- 管理者特権で Visual Studio を再起動してから、操作をやり直してください。

    Web 配置の使用など、一部の ASP.NET デバッグシナリオでは、Visual Studio の高度な特権が必要です。

- Visual Studio の複数のインスタンスが実行されている場合は、(管理者特権を持つ) Visual Studio の1つのインスタンスでプロジェクトを再度開いて、もう一度やり直してください。

- ローカルアドレスを持つホストファイルを使用している場合は、コンピューターの IP アドレスではなく、ループバックアドレスを使用してみてください。

    ローカルアドレスを使用していない場合は、プロジェクトの種類に応じて、ホストファイルにプロジェクトのプロパティ、**プロパティ > Web > サーバー**または **> プロパティ**と同じプロジェクト URL が含まれていることを確認してください。

## <a name="more-troubleshooting-steps"></a>その他のトラブルシューティングの手順

* サーバーのブラウザーで localhost ページを表示します。

     IIS が正しくインストールされていない場合、ブラウザーに `http://localhost` を入力するとエラーが表示されます。

     IIS への展開の詳細については、 [ASP.NET 3.5 と ASP.NET 4.5 を使用した iis 8.0](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45) 、ASP.NET Core については、iis を使用し[た Windows でのホスト](https://docs.asp.net/en/latest/publishing/iis.html)」を参照してください。

* サーバー上に基本的な ASP.NET アプリケーションを作成します (または、基本的な web.config ファイルを使用します)。

    デバッガーで動作するアプリを取得できない場合は、基本的な ASP.NET アプリケーションをサーバー上でローカルに作成し、基本的なアプリのデバッグを試してみてください。 (既定の ASP.NET MVC テンプレートを使用することもできます)。基本的なアプリをデバッグできる場合は、2つの構成の違いを特定するのに役立ちます。 URL 書き換えルールなど、web.config ファイルの設定の相違点を探します。

## <a name="see-also"></a>関連項目
- [Web アプリケーションのデバッグ : エラーおよびトラブルシューティング](../debugger/debugging-web-applications-errors-and-troubleshooting.md)
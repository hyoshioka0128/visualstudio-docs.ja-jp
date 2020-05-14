---
title: ClickOnce 配置におけるサーバー/クライアント構成の問題
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications, ClickOnce
- troubleshooting ClickOnce deployments
- ClickOnce deployment, troubleshooting
- Windows applications, ClickOnce deployments
ms.assetid: 929e5fcc-dd56-409c-bb57-00bd9549b20b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b1d2512c14c0630d2268adfa465e092555150943
ms.sourcegitcommit: bf2e9d4ff38bf5b62b8af3da1e6a183beb899809
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2020
ms.locfileid: "77557868"
---
# <a name="server-and-client-configuration-issues-in-clickonce-deployments"></a>ClickOnce 配置でのサーバーおよびクライアント構成の問題
Windows Server でインターネットインフォメーションサービス (IIS) を使用していて、Windows で認識されないファイルの種類 (Microsoft Word ファイルなど) が配置に含まれている場合、IIS はそのファイルの送信を拒否し、配置は成功しません。

 また、一部の Web サーバーと Web アプリケーションソフトウェア ([!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]など) には、ダウンロードできないファイルとファイルの種類の一覧が含まれています。 たとえば、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] によって *、すべての web.config ファイル*がダウンロードされるのを防ぐことができます。 これらのファイルには、ユーザー名やパスワードなどの機密情報が含まれている場合があります。

 この制限によって、マニフェストやアセンブリなどのコア [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ファイルをダウンロードするときに問題が発生することはありませんが、この制限によって、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの一部として含まれるデータファイルをダウンロードできない場合があります。 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]では、このエラーを解決するには、IIS 構成マネージャーからのそのようなファイルのダウンロードを禁止するハンドラーを削除します。 詳細については、IIS サーバーのドキュメントを参照してください。

 一部の Web サーバーでは、 *.dll*、 *.config*、 *.mdf*などの拡張子を持つファイルがブロックされる場合があります。 Windows ベースのアプリケーションには、通常、これらの拡張機能を含むファイルが含まれます。 ユーザーが Web サーバー上のブロックされたファイルにアクセスする [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを実行しようとすると、エラーが発生します。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] は、すべてのファイル拡張子を解除するのではなく、既定で *.deploy*ファイル拡張子を持つすべてのアプリケーションファイルを発行します。 そのため、管理者は Web サーバーを構成して、次の3つのファイル拡張子をブロック解除する必要があります。

- *.application*

- *.manifest*

- *.deploy*

  ただし、このオプションを無効にするには、[[発行オプション] ダイアログボックス](/previous-versions/visualstudio/visual-studio-2010/7z83t16a(v=vs.100))で [ **. .deploy ファイル拡張子を使用**する] オプションをオフにします。この場合、アプリケーションで使用されているすべてのファイル拡張子のブロックを解除するように Web サーバーを構成する必要があります。

  たとえば、.NET Framework をインストールしていない IIS を使用している場合や、別の Web サーバー (Apache など) を使用している場合は、 *.manifest*、*アプリケーション*、および *. deploy*を構成する必要があります。

## <a name="clickonce-and-secure-sockets-layer-ssl"></a>ClickOnce と Secure Sockets Layer (SSL)
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは、Internet Explorer が SSL 証明書についてのプロンプトを表示する場合を除き、SSL を使用して正常に動作します。 このプロンプトは、サイト名が一致しない場合や証明書の有効期限が切れている場合など、証明書に何らかの問題がある場合に発生する可能性があります。 SSL 接続を使用して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 機能させるには、証明書が最新であること、および証明書のデータがサイトデータと一致していることを確認します。

## <a name="clickonce-and-proxy-authentication"></a>ClickOnce とプロキシ認証
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] は .NET Framework 3.5 以降の Windows 統合プロキシ認証のサポートを提供します。 特定の machine.config ディレクティブは必要ありません。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] は、基本やダイジェストなどの他の認証プロトコルをサポートしていません。

 また、.NET Framework 2.0 に修正プログラムを適用して、この機能を有効にすることもできます。 詳細については、「 [FIX: .NET Framework 2.0 で作成した ClickOnce アプリケーションをプロキシサーバーを使用するように構成されたクライアントコンピューターにインストールしようとした場合のエラーメッセージ: プロキシ認証が必要です」](https://support.microsoft.com/help/917952/fix-error-message-when-you-try-to-install-a-clickonce-application-that)を参照してください。

 詳細については、「 [\<defaultProxy > 要素 (ネットワーク設定)](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings)」を参照してください。

## <a name="clickonce-and-web-browser-compatibility"></a>ClickOnce と Web ブラウザーの互換性
 現時点では、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] インストールは、Internet Explorer を使用して配置マニフェストの URL が開かれている場合にのみ起動されます。 Internet Explorer が既定の Web ブラウザーとして設定されている場合にのみ、URL を別のアプリケーションから起動した配置 (Outlook Microsoft Office など) が正常に起動します。

> [!NOTE]
> 展開プロバイダーが空白でない場合、または Microsoft .NET Framework Assistant 拡張機能がインストールされている場合は、Mozilla Firefox がサポートされます。 この拡張機能は .NET Framework 3.5 SP1 でパッケージ化されています。 XBAP のサポートの場合、NPWPF プラグインは必要に応じてアクティブ化されます。

## <a name="activate-clickonce-applications-through-browser-scripting"></a>ブラウザースクリプトを使用した ClickOnce アプリケーションのアクティブ化
 アクティブスクリプティングを使用して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを起動するカスタム Web ページを開発した場合は、一部のコンピューターでアプリケーションが起動しないことがあります。 Internet Explorer には、この動作に影響する [**ファイルのダウンロードを自動的に**確認する] という設定が含まれています。 この設定は、[**オプション**] メニューの [**セキュリティ**] タブにあり、この動作に影響します。 **ファイルのダウンロードを自動的に確認する**ように求められ、[**ダウンロード**] カテゴリの下に一覧表示されます。 既定では、プロパティはイントラネット Web ページに対して [**有効**] に設定されており、インターネット web ページでは既定で**無効**になっています。 この設定が [**無効**] に設定されている場合、プログラムによって [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションをアクティブ化しようとすると (たとえば、URL を `document.location` プロパティに割り当てることにより)、ブロックされます。 この場合、ユーザーは、アプリケーションの URL に設定されているハイパーリンクをクリックするなどして、ユーザーが開始したダウンロードを使用してのみアプリケーションを起動できます。

## <a name="additional-server-configuration-issues"></a>サーバー構成に関するその他の問題

##### <a name="administrator-permissions-required"></a>管理者のアクセス許可が必要です
 HTTP を使用して発行する場合は、対象サーバーに対する管理者権限が必要です。 IIS にはこのアクセス許可レベルが必要です。 HTTP を使用して発行しない場合は、ターゲットパスに対する書き込みアクセス許可のみが必要です。

##### <a name="server-authentication-issues"></a>サーバー認証の問題
 "匿名アクセス" がオフになっているリモートサーバーに発行すると、次の警告が表示されます。

```
"The files could not be downloaded from http://<remoteserver>/<myapplication>/.  The remote server returned an error: (401) Unauthorized."
```

> [!NOTE]
> 既定の資格情報以外の資格情報を要求するメッセージが表示された場合は、NTLM (NT チャレンジ応答) 認証を行うことができます。また、[セキュリティ] ダイアログボックスで、今後のセッション用に指定された資格情報を保存するかどうかを確認するメッセージが表示されたら、[ **OK** ] をクリックします。 ただし、この回避策は基本認証では機能しません。

## <a name="use-third-party-web-servers"></a>サードパーティの Web サーバーを使用する
 IIS 以外の Web サーバーから [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを配置する場合、配置マニフェストやアプリケーションマニフェストなど、キー [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ファイルの不適切なコンテンツの種類がサーバーから返されると、問題が発生する可能性があります。 この問題を解決するには、新しいコンテンツタイプをサーバーに追加する方法に関する Web サーバーのヘルプドキュメントを参照し、次の表に記載されているすべてのファイル名拡張子のマッピングを確認してください。

|ファイル名拡張子|Content type|
|-------------------------|------------------|
|`.application`|`application/x-ms-application`|
|`.manifest`|`application/x-ms-manifest`|
|`.deploy`|`application/octet-stream`|
|`.msu`|`application/octet-stream`|
|`.msp`|`application/octet-stream`|

## <a name="clickonce-and-mapped-drives"></a>ClickOnce とマップされたドライブ
 Visual Studio を使用して ClickOnce アプリケーションを発行する場合は、マップされたドライブをインストール場所として指定することはできません。 ただし、マニフェストジェネレーターとエディター (Mage.exe および Mageui.exe) を使用して、マップされたドライブからインストールするように ClickOnce アプリケーションを変更することができます。 詳細については、次を参照してください。 [Mage.exe (マニフェスト生成および編集ツール)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)と[MageUI.exe (マニフェスト生成および編集ツールのグラフィカル クライアント)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)します。

## <a name="ftp-protocol-not-supported-for-installing-applications"></a>アプリケーションのインストールで FTP プロトコルがサポートされていない
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] は、HTTP 1.1 Web サーバーまたはファイルサーバーからのアプリケーションのインストールをサポートしています。 ファイル転送プロトコルの FTP は、アプリケーションのインストールではサポートされていません。 FTP を使用してアプリケーションのみを発行できます。 次の表は、これらの違いをまとめたものです。

| URL の種類 | Description |
|----------| - |
| ftp:// | このプロトコルを使用して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを発行できます。 |
| http:// | このプロトコルを使用して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションをインストールすることができます。 |
| https:// | このプロトコルを使用して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションをインストールすることができます。 |
| file:// | このプロトコルを使用して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションをインストールすることができます。 |

## <a name="windows-xp-sp2-windows-firewall"></a>Windows XP SP2: Windows ファイアウォール
 Windows XP SP2 では、windows ファイアウォールが既定で有効になっています。 Windows XP がインストールされているコンピューターでアプリケーションを開発している場合でも、IIS を実行しているローカルサーバーから [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを発行して実行することはできます。 ただし、Windows ファイアウォールを開いた場合を除き、IIS を実行しているサーバーに別のコンピューターからアクセスすることはできません。 Windows ファイアウォールを管理する手順については、Windows ヘルプを参照してください。

## <a name="windows-server-enable-frontpage-server-extensions"></a>Windows Server: FrontPage サーバー拡張機能を有効にする
 HTTP を使用する Windows Web サーバーにアプリケーションを発行するには、Microsoft からの FrontPage Server Extensions が必要です。

 既定では、Windows Server には FrontPage Server Extensions がインストールされていません。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を使用して、FrontPage Server Extensions で HTTP を使用する Windows Server Web サーバーに発行する場合は、まず FrontPage Server Extensions をインストールする必要があります。 インストールを実行するには、Windows Server のサーバー管理ツールの管理ツールを使用します。

## <a name="windows-server-locked-down-content-types"></a>Windows Server: ロックダウンされたコンテンツの種類
 [!INCLUDE[WinXPSvr](../debugger/includes/winxpsvr_md.md)] の IIS は、特定の既知のコンテンツの種類 ( *.htm*、 *.html*、 *.txt*など) を除くすべてのファイルの種類をロックダウンします。 このサーバーを使用して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの展開を有効にするには、アプリケーションで使用されるアプリケーション *、**マニフェスト*、およびその他のカスタムファイルの種類のファイルをダウンロードできるように IIS の設定を変更する必要があります。

 IIS サーバーを使用してを展開する場合は、 *inetmgr.exe*を実行し、既定の Web ページに新しいファイルの種類を追加します。

- *アプリケーション*と*マニフェスト*の拡張子の場合、MIME の種類は "application/x-ms-application" にする必要があります。 その他のファイルの種類については、MIME の種類は "application/オクテット-stream" にする必要があります。

- 拡張子が "" で mime タイプが "application/オクテット-stream" の MIME タイプを作成する場合、<em>ブロックされていないファイルの種類のファイルをダウンロードできるようになります。(ただし、* .aspx</em>や *.asmx*などのブロックされたファイルの種類はダウンロードできません)。

  Windows Server で MIME の種類を構成する具体的な手順については、「 [Web サイトまたはアプリケーションに mime の種類を追加する方法](/iis/configuration/system.webserver/staticcontent/mimemap#how-to-add-a-mime-type-to-a-web-site-or-application)」を参照してください。

## <a name="content-type-mappings"></a>コンテンツの種類のマッピング
 HTTP 経由で公開する場合、*アプリケーション*ファイルのコンテンツの種類 (MIME の種類とも呼ばれます) は、"application/x-ms-application" にする必要があります。 サーバーに .NET Framework 2.0 がインストールされている場合は、自動的に設定されます。 これがインストールされていない場合は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーション vroot (またはサーバー全体) に対して MIME の種類の関連付けを作成する必要があります。

 IIS サーバーを使用してを展開する場合は、inetmgr.exe を実行<em>します。</em>exe を実行し、*アプリケーション*の拡張子に "application/x-ms アプリケーション" という新しいコンテンツタイプを追加します。

## <a name="http-compression-issues"></a>HTTP 圧縮に関する問題
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]では、クライアントにストリームを送信する前に、GZIP アルゴリズムを使用してデータストリームを圧縮する Web サーバーテクノロジである HTTP 圧縮を使用するダウンロードを実行できます。 クライアント (この場合は [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]) では、ファイルを読み取る前にストリームが圧縮解除されます。

 IIS を使用している場合は、HTTP 圧縮を簡単に有効にすることができます。 ただし、HTTP 圧縮を有効にすると、特定のファイルの種類 (つまり、HTML ファイルとテキストファイル) に対してのみ有効になります。 アセンブリ (*.dll*)、xml (*.xml*)、配置マニフェスト (*. application*)、およびアプリケーションマニフェスト (*.manifest*) の圧縮を有効にするには、これらのファイルの種類を、IIS で圧縮する型のリストに追加する必要があります。 ファイルの種類を配置に追加するまでは、テキストファイルと HTML ファイルのみが圧縮されます。

 IIS の詳細な手順については、「 [HTTP 圧縮用に追加のドキュメントの種類を指定する方法](https://support.microsoft.com/help/234497)」を参照してください。

## <a name="see-also"></a>参照
- [ClickOnce 配置のトラブルシューティング](../deployment/troubleshooting-clickonce-deployments.md)
- [ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)
- [アプリケーション配置の必要条件](../deployment/application-deployment-prerequisites.md)
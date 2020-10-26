---
title: ClickOnce 配置でのサーバーとクライアントの構成に関する問題 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
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
caps.latest.revision: 35
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f8e5054b4da0122c40c3ad62cfebcace973f7b20
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "77558012"
---
# <a name="server-and-client-configuration-issues-in-clickonce-deployments"></a>ClickOnce 配置でのサーバーおよびクライアント構成の問題
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows Server でインターネットインフォメーションサービス (IIS) を使用していて、Windows で認識されないファイルの種類 (Microsoft Word ファイルなど) が配置に含まれている場合、IIS はそのファイルの送信を拒否し、配置は成功しません。  
  
 また、一部の Web サーバーと Web アプリケーションソフトウェア (など) には、 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ダウンロードできないファイルとファイルの種類の一覧が含まれています。 たとえば、は、 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] すべての Web.config ファイルをダウンロードできないようにします。 これらのファイルには、ユーザー名やパスワードなどの機密情報が含まれている場合があります。  
  
 この制限によってマニフェストやアセンブリなどのコアファイルのダウンロードに問題が発生することはありませんが [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 、この制限によって、アプリケーションの一部として含まれているデータファイルをダウンロードできない場合があり [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。 では、このエラーを解決するには、 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] IIS 構成マネージャーからのそのようなファイルのダウンロードを禁止するハンドラーを削除します。 詳細については、IIS サーバーのドキュメントを参照してください。  
  
 一部の Web サーバーでは、.dll、.config、.mdf などの拡張子を持つファイルがブロックされる場合があります。 Windows ベースのアプリケーションには、通常、これらの拡張機能を含むファイルが含まれます。 Web サーバー上のブロックされたファイルにアクセスするアプリケーションをユーザーが実行しようとすると [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 、エラーが発生します。 では、すべてのファイル拡張子のブロックを解除するのではなく、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 既定ですべてのアプリケーションファイルに ".deploy" ファイル拡張子を付けて発行します。 そのため、管理者は Web サーバーを構成して、次の3つのファイル拡張子をブロック解除する必要があります。  
  
- .application  
  
- .manifest  
  
- .deploy  
  
  ただし、このオプションを無効にするには、[[発行オプション] ダイアログボックス](https://msdn.microsoft.com/fd9baa1b-7311-4f9e-8ffb-ae50cf110592)で [ **. .deploy ファイル拡張子を使用**する] オプションをオフにします。この場合、アプリケーションで使用されているすべてのファイル拡張子のブロックを解除するように Web サーバーを構成する必要があります。  
  
  をインストールしていない IIS を使用している場合 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] や、別の Web サーバー (Apache など) を使用している場合は、.manifest、アプリケーション、および. deploy を構成する必要があります。  
  
## <a name="clickonce-and-secure-sockets-layer-ssl"></a>ClickOnce と Secure Sockets Layer (SSL)  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]アプリケーションは ssl 経由で動作しますが、Internet Explorer で ssl 証明書に関するプロンプトが表示される場合を除きます。 このプロンプトは、サイト名が一致しない場合や証明書の有効期限が切れている場合など、証明書に何らかの問題がある場合に発生する可能性があります。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]SSL 接続を使用して作業を行うには、証明書が最新であること、および証明書のデータがサイトデータと一致していることを確認してください。  
  
## <a name="clickonce-and-proxy-authentication"></a>ClickOnce とプロキシ認証  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] では、.NET Framework 3.5 以降の Windows 統合プロキシ認証がサポートされています。 特定の machine.config ディレクティブは必要ありません。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] は、基本やダイジェストなどの他の認証プロトコルをサポートしていません。  
  
 また、.NET Framework 2.0 に修正プログラムを適用して、この機能を有効にすることもできます。 詳細については、「 [FIX: .NET Framework 2.0 で作成した ClickOnce アプリケーションをプロキシサーバーを使用するように構成されたクライアントコンピューターにインストールしようとした場合のエラーメッセージ: プロキシ認証が必要です」](https://support.microsoft.com/en-in/help/917952/fix-error-message-when-you-try-to-install-a-clickonce-application-that)を参照してください。 
  
 詳細については、「[\<defaultProxy> 要素 (ネットワーク設定)](https://msdn.microsoft.com/library/9d663c4b-07b4-4f6f-9b12-efbd3630354f)」を参照してください。  
  
## <a name="clickonce-and-web-browser-compatibility"></a>ClickOnce と Web ブラウザーの互換性  
 現在、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] インストールは、Internet Explorer を使用して配置マニフェストの URL が開かれている場合にのみ起動されます。 Internet Explorer が既定の Web ブラウザーとして設定されている場合にのみ、URL を別のアプリケーションから起動した配置 (Outlook Microsoft Office など) が正常に起動します。  
  
> [!NOTE]
> 展開プロバイダーが空白でない場合、または Microsoft .NET Framework Assistant 拡張機能がインストールされている場合は、Mozilla Firefox がサポートされます。 この拡張機能は .NET Framework 3.5 SP1 でパッケージ化されています。 XBAP のサポートの場合、NPWPF プラグインは必要に応じてアクティブ化されます。  
  
## <a name="activating-clickonce-applications-through-browser-scripting"></a>ブラウザースクリプトを使用した ClickOnce アプリケーションのアクティブ化  
 アクティブスクリプティングを使用してアプリケーションを起動するカスタム Web ページを開発した場合は、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 一部のコンピューターでアプリケーションが起動しないことがあります。 Internet Explorer には、この動作に影響する [ **ファイルのダウンロードを自動的に**確認する] という設定が含まれています。 この設定は、[**オプション**] メニューの [**セキュリティ**] タブにあり、この動作に影響します。 **ファイルのダウンロードを自動的に確認する**ように求められ、[**ダウンロード**] カテゴリの下に一覧表示されます。 既定では、プロパティはイントラネット Web ページに対して [ **有効** ] に設定されており、インターネット web ページでは既定で **無効** になっています。 この設定が [ **無効**] に設定されている場合、プログラムによってアプリケーションをアクティブ化しようとすると [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] (たとえば、その URL をプロパティに割り当てることによって `document.location` )、ブロックされます。 この場合、ユーザーは、アプリケーションの URL に設定されているハイパーリンクをクリックするなどして、ユーザーが開始したダウンロードを使用してのみアプリケーションを起動できます。  
  
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
  
## <a name="using-third-party-web-servers"></a>サードパーティの Web サーバーの使用  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]IIS 以外の Web サーバーからアプリケーションを配置する場合、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 配置マニフェストやアプリケーションマニフェストなど、キーファイルの不適切なコンテンツの種類をサーバーが返すと、問題が発生することがあります。 この問題を解決するには、新しいコンテンツタイプをサーバーに追加する方法に関する Web サーバーのヘルプドキュメントを参照し、次の表に記載されているすべてのファイル名拡張子のマッピングを確認してください。  
  
|ファイル名の拡張子|Content type|  
|-------------------------|------------------|  
|`.application`|`application/x-ms-application`|  
|`.manifest`|`application/x-ms-manifest`|  
|`.deploy`|`application/octet-stream`|  
|`.msu`|`application/octet-stream`|  
|`.msp`|`application/octet-stream`|  
  
## <a name="clickonce-and-mapped-drives"></a>ClickOnce とマップされたドライブ  
 Visual Studio を使用して ClickOnce アプリケーションを発行する場合は、マップされたドライブをインストール場所として指定することはできません。 ただし、マニフェストジェネレーターとエディター (Mage.exe および MageUI.exe) を使用して、マップされたドライブからインストールするように ClickOnce アプリケーションを変更することができます。 詳細については、次を参照してください。 [Mage.exe (マニフェスト生成および編集ツール)](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)と[MageUI.exe (マニフェスト生成および編集ツールのグラフィカル クライアント)](https://msdn.microsoft.com/library/f9e130a6-8117-49c4-839c-c988f641dc14)します。  
  
## <a name="ftp-protocol-not-supported-for-installing-applications"></a>アプリケーションのインストールで FTP プロトコルがサポートされていない  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] は、任意の HTTP 1.1 Web サーバーまたはファイルサーバーからのアプリケーションのインストールをサポートしています。 ファイル転送プロトコルの FTP は、アプリケーションのインストールではサポートされていません。 FTP を使用してアプリケーションのみを発行できます。 次の表は、これらの違いをまとめたものです。  
  
|URL の種類|説明|  
|--------------|-----------------|  
|ftp://|[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]このプロトコルを使用してアプリケーションを公開できます。|  
|http://|[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]このプロトコルを使用してアプリケーションをインストールできます。|  
|https://|[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]このプロトコルを使用してアプリケーションをインストールできます。|  
|file://|[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]このプロトコルを使用してアプリケーションをインストールできます。|  
  
## <a name="windows-xp-sp2-windows-firewall"></a>Windows XP SP2: Windows ファイアウォール  
 Windows XP SP2 では、windows ファイアウォールが既定で有効になっています。 Windows XP がインストールされているコンピューターでアプリケーションを開発している場合でも、IIS を実行しているローカルサーバーからアプリケーションを発行して実行することはでき [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。 ただし、Windows ファイアウォールを開いた場合を除き、IIS を実行しているサーバーに別のコンピューターからアクセスすることはできません。 Windows ファイアウォールを管理する手順については、Windows ヘルプを参照してください。  
  
## <a name="windows-server-enable-frontpage-server-extensions"></a>Windows Server: FrontPage サーバー拡張機能を有効にする  
 HTTP を使用する Windows Web サーバーにアプリケーションを発行するには、Microsoft からの FrontPage Server Extensions が必要です。  
  
 既定では、Windows Server には FrontPage Server Extensions がインストールされていません。 を使用し [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] て FrontPage Server Extensions で HTTP を使用する Windows Server Web サーバーに発行する場合は、まず FrontPage Server Extensions をインストールする必要があります。 インストールを実行するには、Windows Server のサーバー管理ツールの管理ツールを使用します。  
  
## <a name="windows-server-locked-down-content-types"></a>Windows Server: ロックダウンされたコンテンツの種類  
 の IIS では、 [!INCLUDE[WinXPSvr](../includes/winxpsvr-md.md)] 特定の既知のコンテンツの種類 (.htm、.html、.txt など) を除くすべてのファイルの種類がロックダウンされます。 このサーバーを使用してアプリケーションの展開を有効にするには、アプリケーションで [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 使用されるアプリケーション、マニフェスト、およびその他のカスタムファイルの種類のファイルをダウンロードできるように、IIS の設定を変更する必要があります。  
  
 IIS サーバーを使用してを展開する場合は、inetmgr.exe を実行し、既定の Web ページの新しいファイルの種類を追加します。  
  
- アプリケーションとマニフェストの拡張子の場合、MIME の種類は "application/x-ms-application" にする必要があります。 その他のファイルの種類については、MIME の種類は "application/オクテット-stream" にする必要があります。  
  
- 拡張子が "*" で mime タイプが "application/オクテット-stream" の MIME タイプを作成した場合、ブロックされていないファイルの種類のファイルをダウンロードできます。 (ただし、.aspx や .asmx などのブロックされたファイルの種類はダウンロードできません)。  
  
  Windows Server で MIME の種類を構成する具体的な手順については、「 [Web サイトまたはアプリケーションに mime の種類を追加する方法](/iis/configuration/system.webserver/staticcontent/mimemap#how-to-add-a-mime-type-to-a-web-site-or-application)」を参照してください。  
  
## <a name="content-type-mappings"></a>コンテンツの種類のマッピング  
 HTTP 経由で公開する場合、アプリケーションファイルのコンテンツの種類 (MIME の種類とも呼ばれます) は、"application/x-ms-application" にする必要があります。 サーバーにがインストールされている場合は [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] 、自動的に設定されます。 これがインストールされていない場合は、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーション vroot (またはサーバー全体) に対して MIME の種類の関連付けを作成する必要があります。  
  
 IIS サーバーを使用してを展開する場合は、inetmgr.exe を実行し、アプリケーションの拡張子に "application/x-ms-application" という新しいコンテンツの種類を追加します。  
  
## <a name="http-compression-issues"></a>HTTP 圧縮に関する問題  
 では [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 、HTTP 圧縮を使用するダウンロードを実行できます。これは、クライアントにストリームを送信する前に、GZIP アルゴリズムを使用してデータストリームを圧縮する Web サーバーテクノロジです。 クライアント (この場合は) では、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ファイルを読み取る前にストリームが圧縮解除されます。  
  
 IIS を使用している場合は、HTTP 圧縮を簡単に有効にすることができます。 ただし、HTTP 圧縮を有効にすると、特定のファイルの種類 (つまり、HTML ファイルとテキストファイル) に対してのみ有効になります。 アセンブリ (.dll)、XML (.xml)、配置マニフェスト (. application)、およびアプリケーションマニフェスト (.manifest) の圧縮を有効にするには、これらのファイルの種類を、IIS で圧縮する型のリストに追加する必要があります。 ファイルの種類を配置に追加するまでは、テキストファイルと HTML ファイルのみが圧縮されます。  
  
## <a name="see-also"></a>参照  
 [ClickOnce 配置のトラブルシューティング](../deployment/troubleshooting-clickonce-deployments.md)   
 [ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)   
 [アプリケーションの展開の前提条件](../deployment/application-deployment-prerequisites.md)

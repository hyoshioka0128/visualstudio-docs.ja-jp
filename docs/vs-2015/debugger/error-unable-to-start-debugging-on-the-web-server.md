---
title: エラー :Web サーバー上でデバッグを開始できません | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.http
- vwd.nonadmin.error.
dev_langs:
- FSharp
- VB
- CSharp
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
ms.assetid: f62e378a-3a99-4f78-9d97-8bb63a4da181
caps.latest.revision: 40
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0b0cbd7afe90b1dbc091263e3a2594c9ca739e1c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68185481"
---
# <a name="error-unable-to-start-debugging-on-the-web-server"></a>エラー :Web サーバー上でデバッグを開始できません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Web サーバーで実行されている ASP.NET アプリケーションをデバッグしようとする場合、次のエラー メッセージが表示されることがあります。Web サーバーでデバッグを開始できません。
  
多くの場合、このエラーは IIS が正しく構成されていないことが原因で発生します。

## <a name="check-your-iis-configuration"></a><a name="vxtbshttpservererrorsthingstocheck"></a> IIS 構成を確認する

ここで説明した問題を解決する手順を実行してから、デバッグを再試行する前に、IIS のリセットが必要になる場合があります。 これを行うには、管理者のコマンドプロンプトを開き、「」と入力する `iisreset` か、IIS マネージャーでこの操作を実行します。 

* アプリケーションプールを停止して再起動してから、もう一度やり直してください。

    アプリケーションプールが停止したか、アプリケーションプールを停止して再起動する必要がある場合があります。
    
    > [!NOTE]
    > アプリケーションプールが停止し続ける場合は、コントロールパネルから URL リライトモジュールをアンインストールし、Web Platform Installer (WPI) を使用して再インストールする必要がある場合があります。 この問題は、システムの大規模なアップグレード後に発生する可能性があります。

* アプリケーション プールの構成を確認し、必要に応じて修正してから、やり直します。

    パスワードの資格情報が変更されている場合は、アプリケーションプールでそれらを更新する必要がある場合があります。 また、ASP.NET を最近インストールした場合は、アプリケーションプールが間違ったバージョンの ASP.NET 用に構成されている可能性があります。 問題を解決してから、アプリケーションプールを再起動してください。
    
* Web アプリケーション フォルダーに適切なアクセス許可があることを確認します。

    IIS_IUSRS または IUSR (または、アプリケーションプールに関連付けられている特定のユーザー) に Web アプリケーションフォルダーの読み取りおよび実行権限を付与してください。 問題を解決し、アプリケーション プールを再起動します。

* ローカル アドレスを含む HOSTS ファイルを使用している場合は、コンピューターの IP アドレスの代わりにループバック アドレスを使用してみてください。

* ブラウザーで localhost ページを表示します。

     IIS が正しくインストールされていない場合、ブラウザーに `http://localhost` を入力するとエラーが表示されます。
     
     IIS への展開の詳細については、リモート [Iis コンピューターのリモートデバッグ ASP.NET に](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md) 関する説明、ASP.NET Core の場合は [Iis への発行](https://docs.asp.net/en/latest/publishing/iis.html)に関する説明を参照してください。

* ASP.NET の正しいバージョンが IIS にインストールされていることを確認します。  「 [Deploy an ASP.NET Application](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md#BKMK_deploy_asp_net) 」を参照するか、ASP.NET CORE、 [IIS に発行](https://docs.asp.net/en/latest/publishing/iis.html)してください)。

* サーバー上に基本的な ASP.NET アプリケーションを作成します。

     アプリとデバッガーを連携できない場合は、基本の ASP.NET アプリケーションをサーバー上にローカルに作成してみて、基本のアプリのデバッグを試してください。 基本的なアプリをデバッグできる場合は、2つの構成の違いを特定するのに役立ちます。
  
* IP アドレスのみを使用している場合は、認証エラーを解決します

     既定では、IP アドレスはインターネットの一部と見なされ、インターネット上では NTLM 認証が行われません。 Web サイトが IIS で認証を要求するように構成されている場合、この認証は失敗します。 この問題を解決するには、IP アドレスではなくリモート コンピューターの名前を指定することができます。
     
## <a name="other-causes"></a>その他の原因

以前のバージョンの Visual Studio を使用している場合は、次のようになります。

- 昇格した特権で Visual Studio を再起動して、もう一度やり直してください。

    以前のバージョンのバグ (後で修正) では、一部の ASP.NET デバッグシナリオで昇格された特権が必要でした。
    
- Visual Studio の複数のインスタンスが実行されている場合は、Visual Studio の1つのインスタンスでプロジェクトを再度開き、もう一度やり直してください。

## <a name="see-also"></a>参照  
 [Web アプリケーションのデバッグ: エラーとトラブルシューティング](../debugger/debugging-web-applications-errors-and-troubleshooting.md)

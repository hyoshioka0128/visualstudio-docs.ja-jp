---
title: 'リモートデバッグ ASP.NET: リモートの IIS 7.5 コンピューター上のリモートデバッグMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 573a3fc5-6901-41f1-bc87-557aa45d8858
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c43f392cddfd5ea36180d9b2675db82469f86ce0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841797"
---
# <a name="remote-debugging-aspnet-on-a-remote-iis-computer"></a>リモートの IIS コンピューター上の ASP.NET のリモート デバッグ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

IIS を使用して ASP.NET Web アプリケーションを Windows Server コンピューターに配置し、リモートデバッグ用に設定することができます。 このガイドでは、Visual Studio 2015 MVC 4.5.2 アプリケーションをセットアップして構成し、IIS に配置して、リモートデバッガーを Visual Studio からアタッチする方法について説明します。

これらの手順は、次のサーバー構成でテストされています。
* Windows Server 2012 R2 および IIS 10
* Windows Server 2008 R2 および IIS 7.5

この記事の情報の大部分は、ASP.NET Core アプリケーションのリモートデバッグにも適用されます。ただし、ASP.NET Core アプリの展開は異なるため、追加の手順が必要です。 ASP.NET Core アプリを IIS にデプロイするには、 [この記事](https://docs.asp.net/en/latest/publishing/iis.html)のすべてのセクションを完了する必要があります。

## <a name="prerequisites-install-the-remote-debugger-on-the-windows-server-computer"></a>前提条件: Windows Server コンピューターにリモートデバッガーをインストールする

リモートデバッガーを Windows Server コンピューターにダウンロードする手順については、「 [リモートデバッグ](../debugger/remote-debugging.md)」を参照してください。

ASP.NET アプリケーションのリモートデバッグを実行するには、リモートデバッガーアプリケーションを管理者として実行するか、リモートデバッガーをサービスとして起動します。 リモート デバッガーをサービスとして実行する方法の詳細については、「 [Remote Debugging](../debugger/remote-debugging.md)」を参照してください。

インストールが完了したら、ターゲットコンピューターでリモートデバッガーが実行されていることを確認します。 (そうでない場合は、[**スタート**] メニューで**リモートデバッガー**を検索します。 ) リモートデバッガーウィンドウは次のようになります。 (4020 は既定のポート番号です)

![RemoteDebuggerWindow](../debugger/media/remotedebuggerwindow.png "RemoteDebuggerWindow")
  
## <a name="create-the-application-on-the-visual-studio-computer"></a>Visual Studio コンピューターでアプリケーションを作成する  
  
1. MVC の ASP.NET アプリケーションを新規作成します。 (**[ファイル] / [新規作成] / [プロジェクト]** の順に選択してから、 **[Visual C#] / [Web] / [ASP.NET Web アプリケーション]** の順に選択します。 **[ASP.NET 4.5.2** テンプレート] セクションで、 **[MVC]** を選択します。 [Azure] セクションで [ **クラウド内のホスト** ] が選択されていないことを確認します。 プロジェクトに **MyMVC**という名前を指定します。)
1. HomeController.cs ファイルを開き、 `About()` メソッドにブレークポイントを設定します。
1. **ソリューション エクスプローラー**で、プロジェクト ノードを右クリックして **[公開]** を選択します。
1. **[発行先を選択します]** で、 **[カスタム]** を選択し、プロファイルに「 **MyMVC**」と名前を付けます。 **[次へ]** をクリックします。
1. **[接続]** タブで、 **[発行方法]** フィールドを **[ファイル システム]** に、 **[ターゲットの場所]** フィールドをローカル ディレクトリに設定します。 **[次へ]** をクリックします。

    ![RemoteDBG_Publish_Local](../debugger/media/remotedbg-publish-local.png "RemoteDBG_Publish_Local")
1. 構成を **[デバッグ]** に設定します。 **[発行]** をクリックします。

    ![RemoteDBG_Publish_Debug_Config](../debugger/media/remotedbg-publish-debug-config.png "RemoteDBG_Publish_Debug_Config")
    
    アプリケーションがローカル ディレクトリに発行されるはずです。

## <a name="deploy-the-aspnet-application-on-the-windows-server-remote-computer"></a><a name="BKMK_deploy_asp_net"></a> Windows Server リモートコンピューターに ASP.NET アプリケーションを展開する

 このセクションでは、Windows Server コンピューターで既に IIS が有効になっていることを前提としています。 Windows Server 2012 R2 の場合、iis を有効にするための [Iis 構成](https://docs.asp.net/en/latest/publishing/iis.html#iis-configuration) を参照してください。 (ASP.NET Core アプリをデプロイしようとしている場合を除き、この記事の他のセクションはスキップできます。 ASP.NET Core については、ここで説明する手順ではなく、記事の手順に従ってアプリをデプロイしてください。)
1. ASP.NET をインストールする Web Platform コンポーネントを使用して ASP.NET 4.5 をインストールします (Windows Server 2012 R2 のサーバーノードから、[ **新しい Web プラットフォームコンポーネントの取得** ] を選択し、ASP.NET を検索します)。

    ![RemoteDBG_IIS_AspNet_45](../debugger/media/remotedbg-iis-aspnet-45.png "RemoteDBG_IIS_AspNet_45")

    Windows Server 2008 R2 では、代わりに次のコマンドを使用して ASP.NET 4 をインストールします:   **c:\windows\ microsoft.net \framework (64) \v4.0.30319\aspnet_regiis.exe-ir**
1. ASP.NET プロジェクト ディレクトリを Visual Studio コンピューターから Windows Server コンピューター上のローカル ディレクトリ (ここでは、 **C:\Publish**と呼びます) にコピーします。 プロジェクトは手動でコピーすることも、Xcopy、Web 配置、Robocopy、Powershell などのオプションを使用することもできます。

    > [!CAUTION]
    > コードの変更やリビルドが必要な場合は、再発行してこの手順を繰り返す必要があります。 リモート コンピューターにコピーした実行可能ファイルは、ローカルのソースとシンボルに正確に一致している必要があります。
1. web.config ファイルに .NET Framework の正しいバージョンが示されていることを確認します。  たとえば、Windows Server 2008 R2 に既定でインストールされている .NET Framework のバージョンは v4.0.30319 ですが、ASP.NET 4.5.2 バージョンを作成しました。 Windows Server コンピューターで ASP.NET 4.0 アプリが実行されている場合は、バージョンを変更する必要があります。
  
    ```xml
    <system.web>
        <authentication mode="None" />  
        <compilation debug="true" targetFramework="4.0.30319" />
        <httpRuntime targetFramework="4.0.30319" />
      </system.web>
  
    ```

1. **インターネット インフォメーション サービス (IIS) マネージャー** を開き、 **[サイト]** に移動します。
1. **[既定の Web サイト]** ノードを右クリックして、 **[アプリケーションの追加]** を選択します。
1. [ **エイリアス** ] フィールドを **MyMVC** に設定し、[アプリケーションプール] フィールドを **ASP.NET** v4.0 に設定します (ASP.NET 4.5 はアプリケーションプールのオプションではありません)。 **[物理パス]** を「 **C:\Publish** 」 (ASP.NET プロジェクト ディレクトリをコピーしたディレクトリ) に設定します。

    >[!NOTE] 
    > ASP.NET Core アプリの場合は、[アプリケーションプール] フィールドを [ **マネージコードなし**] に設定します。
1. [ **既定の Web サイト** ] を右クリックし、[ **参照**] を選択してデプロイをテストします。
    アプリを正常にデプロイした場合は、web ページが表示されます。

## <a name="attach-to-the-aspnet-application-from-the-visual-studio-computer"></a>Visual Studio コンピューターから ASP.NET アプリケーションにアタッチする

1. Visual Studio コンピューターで、 **MyMVC** ソリューションを開きます。
1. Visual Studio で、[ **デバッグ]/[プロセスにアタッチ** ] (**Ctrl + Alt + P**) をクリックします。
1. [修飾子] フィールドを** \<remote computer name> 「4020**」に設定します。
1. **[最新の情報に更新]** をクリックします。
    **[選択可能なプロセス]** ウィンドウにプロセスがいくつか表示されます。

    プロセスが表示されない場合は、リモート コンピューター名ではなく IP アドレスを使用してみてください (ポートは必須です)。 `ipconfig`IPv4 アドレスを取得するには、コマンドラインでを使用します。
1. **[すべてのユーザーからのプロセスを表示する]** をオンにします。
1. **w3wp.exe** を見つけて **[アタッチ]** をクリックします。

     プロセス名をすばやく検索するには、プロセスの最初の文字を入力します。
     
    >[!NOTE]
    > ASP.NET Core アプリの場合は、w3wp.exe ではなく dnx.exe プロセスを選択します。 (このプロセス名は、今後のリリースで変更される可能性があります。)

    ![RemoteDBG_AttachToProcess](../debugger/media/remotedbg-attachtoprocess.png "RemoteDBG_AttachToProcess")

1. リモート コンピューターの Web サイトを開きます。 ブラウザーで、**http://\<remote computer name>** に移動します。
    
    ASP.NET の Web ページが表示されるはずです。
1. ASP.NET web ページで、[ **バージョン情報** ] ページへのリンクをクリックします。

    Visual Studio で、ブレークポイントにヒットするはずです。

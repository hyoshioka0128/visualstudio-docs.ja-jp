---
title: リモートデバッグ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.remote.overview
dev_langs:
- C++
- CSharp
- FSharp
- JScript
- VB
helpviewer_keywords:
- remote debugging, setup
ms.assetid: 5a94ad64-100d-43ca-9779-16cb5af86f97
caps.latest.revision: 81
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 68ebd9ab8c4f9d3cda1371d90a8da459edb1592b
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300567"
---
# <a name="remote-debugging"></a>リモート デバッグ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

別のコンピューターに配置されている Visual Studio アプリケーションをデバッグすることができます。  このデバッグを行うには、Visual Studio リモート デバッガーを使用します。  
  
 ここに記載された情報は、Windows デスクトップ アプリケーションと ASP.NET アプリケーションに適用されます。  Windows ストアアプリと Azure アプリのリモートデバッグの詳細については、「 [Windows ストアアプリと azure アプリでのリモートデバッグ](#bkmk_winstoreAzure)」を参照してください。  
  
## <a name="get-the-remote-tools"></a>リモートツールを入手する  
リモートツールは、デバッグするデバイスまたはサーバーに直接ダウンロードすることも、Visual Studio がインストールされているホストコンピューターからリモートツールを取得することもできます。

### <a name="to-download-and-install-the-remote-tools"></a>リモートツールをダウンロードしてインストールするには
  
1. (Visual Studio を実行するコンピューターではなく) デバッグするデバイスまたはサーバーコンピューターで、適切なバージョンのリモートツールを取得します。

    |バージョン|リンク|説明|
    |-|-|-|
    |Visual Studio 2015 更新プログラム 3|[リモート ツール](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|プロンプトが表示されたら、無料の Visual Studio Dev Essentials グループに参加するか、有効な Visual Studio サブスクリプションを使用してサインインします。 必要に応じて、リンクを再度開きます。 デバイスのオペレーティングシステム (x86、x64、または ARM バージョン) に一致するバージョンを常にダウンロードする|
    |Visual Studio 2015 (古い)|[リモート ツール](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|プロンプトが表示されたら、無料の Visual Studio Dev Essentials グループに参加するか、有効な Visual Studio サブスクリプションを使用してサインインします。 必要に応じて、リンクを再度開きます。|
    |Visual Studio 2013|[リモート ツール](https://msdn.microsoft.com/library/bt727f1t(v=vs.120).aspx#BKMK_Installing_the_Remote_Tools)|Visual Studio 2013 ドキュメントのダウンロードページ|
    |Visual Studio 2012|[リモート ツール](https://msdn.microsoft.com/library/bt727f1t(v=vs.110).aspx#BKMK_Installing_the_Remote_Tools)|Visual Studio 2012 ドキュメントのダウンロードページ|
  
2. [ダウンロード] ページで、使用しているオペレーティングシステム (x86、x64、または ARM バージョン) に一致するツールのバージョンを選択し、リモートツールをダウンロードします。
  
    > [!IMPORTANT]
    > お使いの Visual Studio のバージョンに適した最新バージョンのリモートツールをインストールすることをお勧めします。 一致しないバージョンは推奨されません。  
    >   
    >  また、インストールするオペレーティングシステムと同じアーキテクチャを持つリモートツールをインストールする必要があります。 つまり、64ビットのオペレーティングシステムを実行しているリモートコンピューターで32ビットアプリケーションをデバッグする場合は、リモートコンピューターに64ビットバージョンのリモートツールをインストールする必要があります。  
  
3. 実行可能ファイルのダウンロードが完了したら、アプリケーションをリモート コンピューターにインストールするための指示に従います。 「[セットアップ手順](#bkmk_setup)」を参照してください。

リモートデバッガー (msvsmon) をリモートコンピューターにコピーして実行する場合は、ツールをダウンロードするときにのみ**リモートデバッガー構成ウィザード**(**rdbgwiz .exe**) がインストールされていることに注意してください。また、リモートデバッガーをサービスとして実行する場合は特に、後で構成するためにウィザードを使用する必要があります。 詳細については、次を参照してください。 [(省略可能) 以下のサービスとしてリモートデバッガーを構成](#bkmk_configureService)します。

### <a name="to-run-the-remote-debugger-from-a-file-share"></a>ファイル共有からリモートデバッガーを実行するには

リモートデバッガー (**msvsmon**) は、Visual Studio 2015 Community、Professional、または Enterprise が既にインストールされているコンピューターで見つけることができます。 多くのシナリオでは、リモートデバッグをセットアップする最も簡単な方法は、ファイル共有からリモートデバッガー (msvsmon) を実行することです。 使用に関する制限事項については、リモートデバッガーのヘルプページ (リモートデバッガーの**ヘルプ/使用状況**) を参照してください。

1. 使用している Visual Studio のバージョンと一致するディレクトリで、 **msvsmon**を見つけます。 Visual Studio 2015 の場合:

      **Program 14.0 Visual Studio Common7\ide\remote debugger Debugger\x86\msvsmon.exe**
      
      **Program 14.0 Visual Studio Common7\ide\remote debugger Debugger\x64\msvsmon.exe**

2. Visual Studio コンピューターで**リモートデバッガー**フォルダーを共有します。

3. リモートコンピューターで、 **msvsmon**を実行します。 セットアップの[指示](#bkmk_setup)に従います。

> [!TIP] 
> コマンドラインインストールおよびコマンドラインリファレンスについては、Visual Studio がインストールされているコンピューターのコマンドラインで ``msvsmon.exe /?`` を入力して、 **msvsmon**のヘルプページを参照してください (または、リモートデバッガーの [**ヘルプ]/[使用状況]** を参照してください)。

## <a name="supported-operating-systems"></a>Supported Operating Systems  
 リモート コンピューターで次のいずれかのオペレーティング システムが実行されている必要があります。  
  
- Windows 10  
  
- Windows 8 または 8.1  
  
- Windows 7 Service Pack 1  
  
- Windows Server 2012 または Windows Server 2012 R2  
  
- Windows Server 2008 Service Pack 2、Windows Server 2008 R2 Service Pack 1  
  
## <a name="supported-hardware-configurations"></a>サポートされているハードウェア構成  
  
- 1.6 GHz 以上の高速プロセッサ  
  
- 1 GB の RAM (仮想マシン上で実行されている場合は 1.5 GB)  
  
- 1 GB のハード ディスク空き容量  
  
- 5400 RPM のハード ドライブ  
  
- 1024 x 768 以上の表示解像度の DirectX 9 対応ビデオ カード  
  
## <a name="network-configuration"></a>ネットワーク構成  
 リモート コンピューターと Visual Studio コンピューターは、ネットワーク、ワークグループ、またはホームグループを介して接続されているか、あるいはイーサネット ケーブルによって直接接続されている必要があります。 インターネットを介したデバッグはサポートされません。  
  
## <a name="bkmk_setup"></a>リモートデバッガーを設定する  
 リモート コンピューターに対する管理アクセス許可が必要です。  
  
1. リモート デバッガー アプリケーションを探します。 ([スタート] メニューを開き、**リモートデバッガー**を検索します)。
  
    リモートサーバーでリモートデバッガーを実行している場合は、リモートデバッガーアプリを右クリックし、 **[管理者として実行]** を選択します (または、サービスとしてリモートデバッガーを実行できます)。リモートサーバーで実行していない場合は、通常どおりに起動します。
  
2. リモートツールを初めて起動すると (または、構成する前に)、[**リモートデバッグの構成**dalog] ボックスが表示されます。  
  
    ![Remoteデバッガ Confwizardpage](../debugger/media/remotedebuggerconfwizardpage.png "RemoteDebuggerConfWizardPage")  
  
3. Windows サービス API がインストールされていない (Windows Server 2008 R2 でのみ発生する) 場合は、 **[インストール]** ボタンをクリックします。  
  
4. リモート ツールで利用される、使用するネットワークの種類を選択します。 少なくとも 1 つのネットワークの種類を選択する必要があります。 コンピューターがドメインを介して接続されている場合は、最初の項目を選択する必要があります。 コンピューターがワークグループまたはホーム グループを介して接続されている場合は、必要に応じて、2 番目または 3 番目の項目を選択する必要があります。  
  
5. **[リモートデバッグの構成]** を選択して、ファイアウォールを構成し、ツールを起動します。  
  
6. 構成が完了すると、リモート デバッガーのウィンドウが表示されます。
  
    ![Remoteデバッガウィンドウ](../debugger/media/remotedebuggerwindow.png "リモート デバッガーのウィンドウ")
  
    リモートデバッガーは接続を待機しています。 表示されるサーバー名とポート番号をメモしておきます。これは、後で Visual Studio の構成に必要になります。  
  
   デバッグが完了し、リモートデバッガーを停止する必要がある場合は、ウィンドウの ファイル、**終了** をクリックします。 **[スタート]** メニューから、またはコマンドラインから再起動できます。  
  
   **\<Visual Studio のインストールディレクトリ > \Common7\IDE\Remote デバッガー\\< x86、x64、または Appx\msvsmon.exe**です。  
  
## <a name="configure-the-remote-debugger"></a>リモート デバッガーの構成  
 リモート デバッガーを初めて起動した後、リモート デバッガーの構成の一部を変更できます。
  
- 他のユーザーがリモートデバッガーに接続できるようにするには、ツール、**アクセス許可** の順に選択します。 アクセス許可を付与または拒否するには、管理者特権が必要です。

  > [!IMPORTANT]
  > リモートデバッガーは、Visual Studio コンピューターで使用しているユーザーアカウントとは異なるユーザーアカウントで実行できますが、リモートデバッガーのアクセス許可には、別のユーザーアカウントを追加する必要があります。 

   または、コマンドラインからリモートデバッガーを起動することもできます。これには、次のように指定します。 **\<ユーザー名 >** パラメーター: **msvsmon/allow \<username@computer>** 。
  
- 認証モードまたはポート番号を変更するか、リモートツールのタイムアウト値を指定するには、ツール、**オプション** の順に選択します。  
  
   既定で使用されるポート番号の一覧については、「[リモートデバッガーのポートの割り当て](../debugger/remote-debugger-port-assignments.md)」を参照してください。  
  
   > [!WARNING]
  > リモート ツールを認証なしモードで実行することも選択できますが、このモードの使用は避けることを強く推奨します。 このモードで実行した場合、ネットワーク セキュリティはまったく提供されません。 [認証なし] モードは、ネットワークに悪意のあるコードや悪意のあるトラフィックのリスクがないことが確実である場合にのみ選択してください。

## <a name="bkmk_configureService"></a>Optionalリモートデバッガーをサービスとして構成する
 ASP.NET およびその他のサーバー環境でのデバッグでは、リモートデバッガーを管理者として実行するか、常に実行する場合は、リモートデバッガーをサービスとして実行する必要があります。
  
 リモートデバッガーをサービスとして構成する場合は、次の手順を実行します。  
  
1. **リモート デバッガー構成ウィザード** (rdbgwiz.exe) を見つけます (これは、リモートデバッガーとは別のアプリケーションです)。リモートツールをインストールする場合にのみ使用できます。 Visual Studio と共にはインストールされません。  
  
2. 構成ウィザードの実行を開始します。 最初のページが表示されたら、 **[次へ]** をクリックします。  
  
3. **[Visual Studio 2015 リモート デバッガー サービスを実行する]** チェック ボックスをオンにします。  
  
4. ユーザー アカウントの名前とパスワードを追加します。  
  
    このアカウントに、 **[サービスとしてログオン]** のユーザー権限を追加することが必要になる場合があります。 ( **ローカル セキュリティ ポリシー** (secpol.msc) を **[スタート]** ページまたはウィンドウで、あるいはコマンド プロンプトに「 **secpol** 」と入力して見つけます。 ウィンドウが表示されたら、 **[ユーザー権利の割り当て]** をダブルクリックし、右ペインで **[サービスとしてログオン]** を見つけます。 これをダブルクリックします。 **[プロパティ]** ウィンドウにユーザーアカウントを追加し、[ **OK]** をクリックします)。 **[次へ]** をクリックします。  
  
5. リモート ツールが通信するネットワークの種類を選択します。 少なくとも 1 つのネットワークの種類を選択する必要があります。 コンピューターがドメインを介して接続されている場合は、最初の項目を選択する必要があります。 コンピューターがワークグループまたはホーム グループを介して接続されている場合は、2 番目または 3 番目の項目を選択する必要があります。 **[次へ]** をクリックします。  
  
6. サービスを開始できた場合は、「 **Visual Studio リモート デバッガー構成ウィザードは正常に完了しました**」と表示されます。 サービスを開始できなかった場合は、「 **Visual Studio リモート デバッガー構成ウィザードを完了できませんでした**」と表示されます。 このページには、サービスを開始するために従う必要があるヒントもいくつか提供されます。  
  
7. **[完了]** をクリックします。  
  
   この時点で、リモート デバッガーはサービスとして実行されています。 これを確認するには、 **[コントロール パネル] / [サービス]** に移動して **[Visual Studio 2015 リモート デバッガー]** を探します。  
  
   リモート デバッガー サービスは、 **[コントロール パネル] / [サービス]** で停止してから開始することができます。  

## <a name="remote-debug-an-aspnet-application"></a>ASP.NET アプリケーションのリモート デバッグ  
 IIS が実行されているリモート コンピューターに ASP.NET アプリケーションを配置する手順は、オペレーティング システムと IIS のバージョンによって異なります。 IIS 7.5 以降がインストールされている Windows Server 2008 または Windows Server 2012 を実行しているリモートコンピューターについては、リモート[IIS コンピューターのリモートデバッグ ASP.NET に](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)関する説明を参照してください。
 
 ASP.NET Core アプリをデバッグする場合は、「 [IIS への発行](https://docs.asp.net/en/latest/publishing/iis.html)」を参照してください。 IIS で ASP.NET Core を公開するには、さまざまな手順が必要です。 ASP.NET Core アプリを正常に発行したら、[他の ASP.NET アプリと同様](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)にリモートデバッグできます。ただし、にアタッチする必要があるプロセスは、w3wp.exe ではなく dnx です。

## <a name="remote-debug-a-visual-c-project"></a>Visual C++ プロジェクトのリモート デバッグ  
 次の手順では、プロジェクトの名前とパスを C:\remotetemp\MyMfc にし、リモートコンピューターの名前を「 **Mjo-DL**」にします。  
  
1. **mymfc** という名前の MFC アプリケーションを作成します。  
  
2. ブレークポイントを、アプリケーション内の達しやすい任意の箇所 (たとえば、**の開始時の**MainFrm.cpp`CMainFrame::OnCreate`) に設定します。  
  
3. ソリューションエクスプローラーで、プロジェクトを右クリックし、 **[プロパティ]** を選択します。 **[デバッグ]** タブを開きます。  
  
4. **[起動するデバッガー]** を **[リモート Windows デバッガー]** に設定します。  
  
    ![Remoteデバッグ Cplus](../debugger/media/remotedebuggingcplus.png "RemoteDebuggingCPlus")  
  
5. プロパティに次の変更を適用します。  
  
   |設定|値|
   |-|-|  
   |リモート コマンド|C:\remotetemp\mymfc.exe|  
   |作業ディレクトリ|C:\remotetemp|  
   |リモート サーバー名|MJO-DL:*ポート*番号|  
   |接続|Windows 認証を使用したリモート接続|  
   |[デバッガーのタイプ]|ネイティブのみ|  
   |配置ディレクトリ|C:\remotetemp|  
   |追加の配置ファイル|C:\data\mymfcdata.txt|  
  
    追加のファイルを展開する (オプション) 場合は、フォルダーが両方のコンピューターに存在している必要があります。  
  
6. ソリューションエクスプローラーで、ソリューションを右クリックし、 **[Configuration Manager]** を選択します。  
  
7. **[デバッグ]** 構成の **[配置]** チェック ボックスをオンにします。  
  
    ![RemoteDebugCplusDeploy](../debugger/media/remotedebugcplusdeploy.png "RemoteDebugCplusDeploy")  
  
8. デバッグを開始します ([**デバッグ]/[デバッグの開始**]、または**F5 キーを押し**ます)。  
  
9. 実行可能ファイルが、リモート コンピューターに自動的に配置されます。  
  
10. メッセージが表示されたら、リモートコンピューターに接続するためのネットワーク資格情報を入力します。  
  
     必要な資格情報は、ネットワークのセキュリティ構成に固有のものです。 たとえば、ドメインコンピューターで、セキュリティ証明書を選択するか、ドメイン名とパスワードを入力することができます。 ドメイン以外のコンピューターでは、コンピューター名と有効なユーザーアカウント名 ( <strong>MJO-DL\name@something.com</strong>など) と、正しいパスワードを入力することができます。  
  
11. Visual Studio コンピューターで、実行がブレークポイントで停止したことを確認できるはずです。  
  
    > [!TIP]
    > また、これらのファイルは別の手順でも配置できます。 **ソリューション エクスプローラー**で、 **[mymfc]** ノードを右クリックして **[配置]** を選択します。  
  
    アプリケーションで使用する必要がある、コード以外のファイルがある場合は、Visual Studio プロジェクトに含める必要があります。 追加のファイルのプロジェクトフォルダーを作成します (**ソリューションエクスプローラー**で、追加、**新しいフォルダー** の順にクリックします)。次に、ファイルをフォルダーに追加します (**ソリューションエクスプローラー**で、追加、**既存の項目** の順にクリックし、ファイルを選択します)。 ファイルごとの **[プロパティ]** ページで、 **[出力ディレクトリにコピー]** を **[常にコピーする]** に設定します。  
  
## <a name="remote-debug-a-visual-c-or-visual-basic-project"></a>Visual C# プロジェクトまたは Visual Basic プロジェクトのリモート デバッグ  
 デバッガーでは、Visual C# または Visual Basic のデスクトップ アプリケーションをリモート コンピューターに配置できませんが、次のようにリモートからそれらのデスクトップ アプリケーションをデバッグすることはできます。 次の手順では、前の図に示したように、 **Mjo-DL**という名前のコンピューターでデバッグすることを前提としています。
  
1. **MyWpf** という名前の WPF プロジェクトを作成します。  
  
2. ブレークポイントをコード内の達しやすい任意の箇所に設定します。  
  
    たとえば、ブレークポイントをボタン ハンドラーに設定できます。 これを行うには、Mainwindow.xaml を開き、[ツールボックス] から Button コントロールを追加します。次に、ボタンをダブルクリックして、そのハンドラーを開きます。
  
3. ソリューション エクスプローラーでプロジェクトを右クリックし、 **[プロパティ]** を選択します。  
  
4. **[プロパティ]** ページで、 **[デバッグ]** タブをクリックします。  
  
    ![Remoteデバッガ Csharp](../debugger/media/remotedebuggercsharp.png "RemoteDebuggerCSharp")  
  
5. **[作業ディレクトリ]** テキスト ボックスが空であることを確認してください。  
  
6. **[リモートコンピューターを使用する]** を選択し、テキストボックスに「 **MJO-DL: 4020** 」と入力します。 (4020 は、リモートデバッガーウィンドウに表示されるポート番号です)。  
  
7. **[ネイティブ コードのデバッグを有効にする]** がオフであることを確認します。  
  
8. プロジェクトをビルドする。  
  
9. Visual Studio コンピューター上の **Debug** フォルダー ( **\<ソース パス>\MyWPF\MyWPF\bin\Debug**) と同じパスのフォルダーをリモート コンピューター上に作成します。  
  
10. 上で作成した実行可能ファイルを、Visual Studio コンピューターから、リモート コンピューター上の新しく作成したフォルダーにコピーします。
  
    > [!CAUTION]
    > コードに変更を加えたりリビルドしたりしないでください (または、この手順を繰り返す必要があります)。 リモート コンピューターにコピーした実行可能ファイルは、ローカルのソースとシンボルに正確に一致している必要があります。

    プロジェクトは手動でコピーすることも、Xcopy、Robocopy、Powershell などのオプションを使用することもできます。
  
11. ターゲットコンピューターでリモートデバッガーが実行されていることを確認します。 (そうでない場合は、 **[スタート]** メニューで**リモートデバッガー**を検索します。 ) リモートデバッガーウィンドウは次のようになります。  
  
     ![Remoteデバッガウィンドウ](../debugger/media/remotedebuggerwindow.png "リモート デバッガーのウィンドウ")  
  
12. Visual Studio で、デバッグを開始します ([**デバッグ]/[デバッグの開始**]、または**F5 キーを押し**ます)。  
  
13. メッセージが表示されたら、リモートコンピューターに接続するためのネットワーク資格情報を入力します。  
  
     必要な資格情報は、ネットワークのセキュリティ構成によって異なります。 たとえば、ドメインコンピューターでは、ドメイン名とパスワードを入力できます。 ドメイン以外のコンピューターでは、コンピューター名と有効なユーザーアカウント名 ( <strong>MJO-DL\name@something.com</strong>など) と、正しいパスワードを入力することができます。

     WPF アプリケーションのメイン ウィンドウがリモート コンピューター上で開いていることを確認できるはずです。
  
14. 必要に応じて、ブレークポイントにヒットするアクションを実行します。 ブレークポイントがアクティブになっていることを確認できるはずです。 ブレークポイントがアクティブでない場合、アプリケーションのシンボルが読み込まれていません。 もう一度お試しください。それでもうまくいかない場合は、シンボルの読み込みと、シンボル[ファイルと Visual Studio のシンボル設定](https://devblogs.microsoft.com/devops/understanding-symbol-files-and-visual-studios-symbol-settings/)についてのトラブルシューティングに関する情報を参照してください。
  
15. Visual Studio コンピューターで、実行がブレークポイントで停止したことを確認できるはずです。
  
    アプリケーションで使用する必要がある、コード以外のファイルがある場合は、Visual Studio プロジェクトに含める必要があります。 追加のファイルのプロジェクトフォルダーを作成します (**ソリューションエクスプローラー**で、追加、**新しいフォルダー** の順にクリックします)。次に、ファイルをフォルダーに追加します (**ソリューションエクスプローラー**で、追加、**既存の項目** の順にクリックし、ファイルを選択します)。 ファイルごとの **[プロパティ]** ページで、 **[出力ディレクトリにコピー]** を **[常にコピーする]** に設定します。
  
## <a name="set-up-debugging-with-remote-symbols"></a>リモート シンボルを使用したデバッグのセットアップ  
 Visual Studio コンピューターで生成したシンボルを使用して、コードをデバッグすることができます。 リモート デバッガーのパフォーマンスは、ローカル シンボルを使用すると大幅に向上します。  リモート シンボルを使用する必要がある場合、リモート コンピューター上のシンボルを検索するように、リモート デバッグ モニターに指示する必要があります。  
  
 Visual Studio 2013 Update 2 以降では、msvsmon コマンド ライン スイッチの `Msvsmon / /FallbackLoadRemoteManagedPdbs` を使用して、マネージド コードにリモート シンボルを使用できます。  
  
 詳細については、リモートデバッグのヘルプを参照してください (リモートデバッガーウィンドウで**F1**キーを押すか、 **[ヘルプ/使用状況]** をクリックしてください)。 詳細については、「[.NET Remote Symbol Loading Changes in Visual Studio 2012 and 2013 (Visual Studio 2012 および 2013 における .NET のリモート シンボルの読み込みの変更)](https://devblogs.microsoft.com/devops/net-remote-symbol-loading-changes-in-visual-studio-2012-and-2013/)」を参照してください。  
  
## <a name="bkmk_winstoreAzure"></a>Windows ストアアプリと Azure アプリでのリモートデバッグ  
 Windows ストアアプリを使用したリモートデバッグの詳細については、「 [Visual Studio からのリモートデバイスでの Windows ストアアプリのデバッグとテスト](https://msdn.microsoft.com/library/windows/apps/hh441469.aspx)」を参照してください。  
  
 Azure でのデバッグ方法の詳細については、これらのトピックのいずれかを参照してください。  
  
- [Visual Studio でのクラウドサービスまたは仮想マシンのデバッグ](../azure/vs-azure-tools-debug-cloud-services-virtual-machines.md)  
  
- [Visual Studio での .NET バックエンドのデバッグ](https://blogs.msdn.microsoft.com/azuremobile/2014/03/14/debugging-net-backend-in-visual-studio/)  
  
- Azure Websites でのリモートデバッグの概要 (パート[1](https://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/)、パート[2](https://azure.microsoft.com/blog/2014/05/07/introduction-to-remote-debugging-azure-web-sites-part-2-inside-remote-debugging/)、[パート 3](https://azure.microsoft.com/blog/2014/05/08/introduction-to-remote-debugging-on-azure-web-sites-part-3-multi-instance-environment-and-git/))。  
  
## <a name="see-also"></a>関連項目  
 [Visual Studio でのデバッグ](../debugger/debugging-in-visual-studio.md)   
 [Windows ファイアウォールをリモート デバッグ用に構成する](../debugger/configure-the-windows-firewall-for-remote-debugging.md)   
 [Remote Debugger Port Assignments](../debugger/remote-debugger-port-assignments.md)   
 [リモートの IIS コンピューター上の ASP.NET のリモート デバッグ](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)  
 [リモート デバッグ エラーとトラブルシューティング](../debugger/remote-debugging-errors-and-troubleshooting.md)

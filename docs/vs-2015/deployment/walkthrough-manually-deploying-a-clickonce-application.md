---
title: 'チュートリアル: ClickOnce アプリケーションを手動で配置する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Mage.exe, manual ClickOnce deployments
- MageUI.exe, manual ClickOnce deployments
- deploying applications [ClickOnce], manual ClickOnce deployments
- ClickOnce deployment, manually
- ClickOnce deployment, SDK tools
- manual ClickOnce deployments
- manifests [ClickOnce]
ms.assetid: ccee6551-a1b9-4ca2-8845-9c1cf4ac2560
caps.latest.revision: 51
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: cba55c9f4a8f7436b97099b6b548b916ea6e5ecb
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75844935"
---
# <a name="walkthrough-manually-deploying-a-clickonce-application"></a>チュートリアル : ClickOnce アプリケーションを手動で配置する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio を使用して [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションを配置できない場合、または、信頼されたアプリケーションの配置などの高度な配置機能を使用する必要がある場合は、Mage.exe コマンドラインツールを使用して、[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] マニフェストを作成する必要があります。 このチュートリアルでは、コマンドラインバージョン (Mage.exe) またはマニフェスト生成および編集ツールのグラフィカルバージョン (Mageui.exe) を使用して [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 展開を作成する方法について説明します。  
  
## <a name="prerequisites"></a>[前提条件]  
 このチュートリアルでは、デプロイを構築する前に選択する必要があるいくつかの前提条件とオプションについて説明します。  
  
- Mage.exe と Mageui.exe をインストールします。  
  
     Mage.exe と Mageui.exe は、[!INCLUDE[winsdklong](../includes/winsdklong-md.md)]の一部です。 [!INCLUDE[winsdkshort](../includes/winsdkshort-md.md)] がインストールされているか、Visual Studio に含まれているバージョンの [!INCLUDE[winsdkshort](../includes/winsdkshort-md.md)] である必要があります。 詳細については、MSDN の「 [Windows SDK](https://msdn.microsoft.com/windowsserver/bb980924.aspx) 」を参照してください。  
  
- デプロイするアプリケーションを指定します。  
  
     このチュートリアルでは、展開する準備ができている Windows アプリケーションがあることを前提としています。 このアプリケーションは、AppToDeploy と呼ばれます。  
  
- デプロイの配布方法を決定します。  
  
     配布オプションには、Web、ファイル共有、CD などがあります。 詳細については、「 [ClickOnce Security and Deployment](../deployment/clickonce-security-and-deployment.md)」を参照してください。  
  
- アプリケーションが高いレベルの信頼を必要とするかどうかを判断します。  
  
     アプリケーションが完全な信頼を必要とする場合 (ユーザーのシステムへのフルアクセスなど)、Mage.exe の `-TrustLevel` オプションを使用してこれを設定できます。 アプリケーションのカスタムアクセス許可セットを定義する場合は、別のマニフェストからインターネットまたはイントラネットのアクセス許可セクションをコピーし、ニーズに合わせて変更し、テキストエディターまたは Mageui.exe を使用してアプリケーションマニフェストに追加することができます。 詳細については、「 [Trusted Application Deployment Overview](../deployment/trusted-application-deployment-overview.md)」を参照してください。  
  
- Authenticode 証明書を取得します。  
  
     デプロイには Authenticode 証明書を使用して署名する必要があります。 テスト証明書を生成するには、Visual Studio、Mageui.exe、または MakeCert と Pvk2Pfx ツールを使用するか、証明機関 (CA) から証明書を取得します。 信頼されたアプリケーションの展開を使用することを選択した場合は、証明書をすべてのクライアントコンピューターに1回だけインストールする必要があります。 詳細については、「 [Trusted Application Deployment Overview](../deployment/trusted-application-deployment-overview.md)」を参照してください。  
  
    > [!NOTE]
    > また、証明機関から取得できる CNG 証明書を使用して、デプロイに署名することもできます。  
  
- アプリケーションに UAC 情報を含むマニフェストがないことを確認します。  
  
     アプリケーションに、`<dependentAssembly>` 要素などのユーザーアカウント制御 (UAC) 情報を含むマニフェストが含まれているかどうかを確認する必要があります。 アプリケーションマニフェストを確認するには、Windows Sysinternals [Sigcheck](https://technet.microsoft.com/sysinternals/bb897441.aspx)ユーティリティを使用します。  
  
     アプリケーションに UAC の詳細を含むマニフェストが含まれている場合は、UAC 情報を使用せずにアプリケーションを再構築する必要があります。 Visual Studio C#のプロジェクトの場合は、プロジェクトのプロパティを開き、アプリケーション タブを選択します。**マニフェスト** ドロップダウンリストで、**マニフェストなしでアプリケーションを作成**する を選択します。 Visual Studio の Visual Basic プロジェクトの場合は、プロジェクトのプロパティを開いて アプリケーション タブを選択し、 **UAC 設定の表示** をクリックします。 開いているマニフェストファイルで、1つの `<asmv1:assembly>` 要素内のすべての要素を削除します。  
  
- アプリケーションでクライアントコンピュータの前提条件が満たされているかどうかを判断します。  
  
     Visual Studio から配置された [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションには、配置に必要なインストールブートストラップ (setup.exe) を含めることができます。 このチュートリアルでは、[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] のデプロイに必要な2つのマニフェストを作成します。 [Generatebootstrapper タスク](../msbuild/generatebootstrapper-task.md)を使用して、前提条件のブートストラップを作成できます。  
  
### <a name="to-deploy-an-application-with-the-mageexe-command-line-tool"></a>Mage.exe コマンドラインツールを使用してアプリケーションを展開するには  
  
1. [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] の配置ファイルを格納するディレクトリを作成します。  
  
2. 先ほど作成した配置ディレクトリで、バージョンのサブディレクトリを作成します。 アプリケーションを初めてデプロイする場合は、バージョンのサブディレクトリに**1.0.0.0**という名前を指定します。  
  
    > [!NOTE]
    > 配置のバージョンは、アプリケーションのバージョンとは異なる場合があります。  
  
3. すべてのアプリケーションファイルを、実行可能ファイル、アセンブリ、リソース、およびデータファイルを含むバージョンのサブディレクトリにコピーします。 必要に応じて、追加のファイルを含む追加のサブディレクトリを作成できます。  
  
4. [!INCLUDE[winsdkshort](../includes/winsdkshort-md.md)] または Visual Studio コマンドプロンプトを開き、バージョンのサブディレクトリに移動します。  
  
5. Mage.exe の呼び出しを使用して、アプリケーションマニフェストを作成します。 次のステートメントは、Intel x86 プロセッサで実行するようにコンパイルされたコードのアプリケーションマニフェストを作成します。  
  
    ```  
    mage -New Application -Processor x86 -ToFile AppToDeploy.exe.manifest -name "My App" -Version 1.0.0.0 -FromDirectory .   
    ```  
  
    > [!NOTE]
    > `-FromDirectory` オプションの後に、現在のディレクトリを示すドット (.) を含めるようにしてください。 ドットを含めない場合は、アプリケーションファイルへのパスを指定する必要があります。  
  
6. Authenticode 証明書を使用して、アプリケーションマニフェストに署名します。 *Mycert .pfx*を証明書ファイルのパスに置き換えます。 *Passwd*を、証明書ファイルのパスワードに置き換えます。  
  
    ```  
    mage -Sign AppToDeploy.exe.manifest -CertFile mycert.pfx -Password passwd  
    ```  
  
     CNG 証明書を使用してアプリケーションマニフェストに署名するには、次のようにします。 *Cngcert .pfx*を実際の証明書ファイルへのパスに置き換えます。  
  
    ```  
    mage -Sign AppToDeploy.exe.manifest -CertFile cngCert.pfx  
    ```  
  
7. デプロイディレクトリのルートに変更します。  
  
8. Mage.exe の呼び出しを使用して、配置マニフェストを生成します。 既定では、Mage.exe は、[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] の展開を、インストールされているアプリケーションとしてマークし、オンラインとオフラインの両方で実行できるようにします。 ユーザーがオンラインのときにのみアプリケーションを使用できるようにするには、`-Install` オプションを `false`の値と共に使用します。 既定のを使用し、ユーザーが Web サイトまたはファイル共有からアプリケーションをインストールする場合は、[`-ProviderUrl`] オプションの値が、Web サーバーまたは共有のアプリケーションマニフェストの場所を指していることを確認します。  
  
    ```  
    mage -New Deployment -Processor x86 -Install true -Publisher "My Co." -ProviderUrl "\\myServer\myShare\AppToDeploy.application" -AppManifest 1.0.0.0\AppToDeploy.exe.manifest -ToFile AppToDeploy.application  
    ```  
  
9. Authenticode または CNG 証明書を使用して、デプロイマニフェストに署名します。  
  
    ```  
    mage -Sign AppToDeploy.application -CertFile mycert.pfx -Password passwd  
    ```  
  
     または  
  
    ```  
    mage -Sign AppToDeploy.exe.manifest -CertFile cngCert.pfx  
    ```  
  
10. Deployment ディレクトリ内のすべてのファイルを、展開先またはメディアにコピーします。 Web サイトまたは FTP サイトのフォルダー、ファイル共有、または CD-ROM を指定できます。  
  
11. アプリケーションをインストールするために必要な URL、UNC、または物理メディアをユーザーに提供します。 URL または UNC を指定する場合は、配置マニフェストへの完全パスをユーザーに付与する必要があります。 AppToDeploy を配置する場合の例の http://webserver01/ AppToDeploy ディレクトリに完全な URL パスになります。 http://webserver01/AppToDeploy/AppToDeploy.application します。  
  
### <a name="to-deploy-an-application-with-the-mageuiexe-graphical-tool"></a>Mageui.exe グラフィックツールを使用してアプリケーションを配置するには  
  
1. [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] の配置ファイルを格納するディレクトリを作成します。  
  
2. 先ほど作成した配置ディレクトリで、バージョンのサブディレクトリを作成します。 アプリケーションを初めてデプロイする場合は、バージョンのサブディレクトリに**1.0.0.0**という名前を指定します。  
  
    > [!NOTE]
    > 配置のバージョンは、アプリケーションのバージョンとは異なる場合があります。  
  
3. すべてのアプリケーションファイルを、実行可能ファイル、アセンブリ、リソース、およびデータファイルを含むバージョンのサブディレクトリにコピーします。 必要に応じて、追加のファイルを含む追加のサブディレクトリを作成できます。  
  
4. Mageui.exe グラフィックツールを起動します。  
  
    ```  
    MageUI.exe  
    ```  
  
5. メニューから **[ファイル]** 、 **[新規]** 作成、 **[アプリケーションマニフェスト]** の順に選択して、新しいアプリケーションマニフェストを作成します。  
  
6. [既定の**名前**] タブで、この展開の名前とバージョン番号を入力します。 また、アプリケーションのビルドに使用する**プロセッサ**(x86 など) も指定します。  
  
7. **[ファイル]** タブを選択し、 **[アプリケーションディレクトリ]** テキストボックスの横にある省略記号ボタン ( **[...]** ) をクリックします。 [フォルダーの参照] ダイアログボックスが表示されます。  
  
8. アプリケーションファイルが含まれているバージョンのサブディレクトリを選択し、[ **OK]** をクリックします。  
  
9. インターネットインフォメーションサービス (IIS) から展開する場合は、**配置するときに拡張子を付ける** チェックボックスがオンになっていないファイルに 追加 をクリックして展開します。  
  
10. **[設定]** ボタンをクリックして、すべてのアプリケーションファイルをファイルの一覧に追加します。 アプリケーションに複数の実行可能ファイルが含まれている場合は、 **[ファイルの種類]** ドロップダウンリストから **[エントリポイント]** を選択して、この展開のメインの実行可能ファイルをスタートアップアプリケーションとしてマークします。 (アプリケーションに1つの実行可能ファイルしか含まれていない場合は、Mageui.exe によってマークされます)。  
  
11. **[必要なアクセス許可]** タブを選択し、アプリケーションでアサートする必要がある信頼のレベルを選択します。 既定値は**FullTrust**です。これはほとんどのアプリケーションに適しています。  
  
12. メニューから **[ファイル]** 、 **[名前を付けて保存]** を選択します。 [署名オプション] ダイアログボックスが開き、アプリケーションマニフェストに署名するよう求められます。  
  
13. ファイルシステムにファイルとして保存されている証明書がある場合は、[**証明書ファイルで署名**する] オプションを使用して、省略記号 ( **..** .) ボタンを使用してファイルシステムから証明書を選択します。 次に、証明書のパスワードを入力します。  
  
     -または-  
  
     お使いのコンピューターからアクセスできる証明書ストアに証明書が保持されている場合は、[**保存された証明書で署名**する] オプションを選択し、提供された一覧から証明書を選択します。  
  
14. **[OK]** をクリックして、アプリケーションマニフェストに署名します。 [名前を付けて保存] ダイアログ ボックスが表示されます。  
  
15. 名前を付けて保存 ダイアログボックスで、バージョンディレクトリを指定し、**保存** をクリックします。  
  
16. メニューから **[ファイル]** 、 **[新規作成]** 、 **[配置マニフェスト]** を選択して、配置マニフェストを作成します。  
  
17. **[名前]** タブで、この展開の名前とバージョン番号 (この例では**1.0.0.0** ) を指定します。 また、アプリケーションのビルドに使用する**プロセッサ**(x86 など) も指定します。  
  
18. **[説明]** タブを選択し、[**発行元**と**製品**] の値を指定します。 (**Product**は、アプリケーションをオフラインで使用するためにクライアントコンピューターにインストールするときに、Windows の [スタート] メニューでアプリケーションに指定された名前です)。  
  
19. **[配置オプション]** タブを選択し、 **[開始場所]** テキストボックスで、Web サーバーまたは共有のアプリケーションマニフェストの場所を指定します。 たとえば、\\\myServer\myShare\AppToDeploy.application.  
  
20. 前の手順で .deploy 拡張子を追加した場合は、[**ファイル名拡張子**を指定してください] も選択します。  
  
21. **[更新オプション]** タブを選択し、このアプリケーションを更新する頻度を指定します。 アプリケーションで <xref:System.Deployment.Application.UpdateCheckInfo> を使用して更新プログラムを確認する場合は、[**このアプリケーションで更新プログラムを確認**する] チェックボックスをオフにします。  
  
22. **[アプリケーション参照]** タブを選択し、 **[マニフェストの選択]** ボタンをクリックします。 [開く] ダイアログボックスが表示されます。  
  
23. 前の手順で作成したアプリケーションマニフェストを選択し、 **[開く]** をクリックします。  
  
24. メニューから **[ファイル]** 、 **[名前を付けて保存]** を選択します。 [署名オプション] ダイアログボックスが表示され、配置マニフェストに署名するよう求められます。  
  
25. ファイルシステムにファイルとして保存されている証明書がある場合は、[**証明書ファイルで署名**する] オプションを使用して、省略記号 ( **..** .) ボタンを使用してファイルシステムから証明書を選択します。 次に、証明書のパスワードを入力します。  
  
     -または-  
  
     お使いのコンピューターからアクセスできる証明書ストアに証明書が保持されている場合は、[**保存された証明書で署名**する] オプションを選択し、提供された一覧から証明書を選択します。  
  
26. **[OK]** をクリックして、配置マニフェストに署名します。 [名前を付けて保存] ダイアログ ボックスが表示されます。  
  
27. **[名前を付けて保存]** ダイアログボックスで、1つ上のディレクトリをデプロイのルートに移動し、 **[保存]** をクリックします。  
  
28. Deployment ディレクトリ内のすべてのファイルを、展開先またはメディアにコピーします。 Web サイトまたは FTP サイトのフォルダー、ファイル共有、または CD-ROM を指定できます。  
  
29. アプリケーションをインストールするために必要な URL、UNC、または物理メディアをユーザーに提供します。 URL または UNC を指定する場合は、配置マニフェストの完全パスをユーザーに付与する必要があります。 AppToDeploy を配置する場合の例の http://webserver01/ AppToDeploy ディレクトリに完全な URL パスになります。 http://webserver01/AppToDeploy/AppToDeploy.application します。  
  
## <a name="next-steps"></a>次のステップ  
 新しいバージョンのアプリケーションを展開する必要がある場合は、新しいバージョン (たとえば、1.0.0.1) の後にという名前の新しいディレクトリを作成し、新しいディレクトリに新しいアプリケーションファイルをコピーします。 次に、前の手順に従って、新しいアプリケーションマニフェストを作成して署名し、配置マニフェストを更新して署名する必要があります。 Mage.exe `-New` と `–Update` 呼び出しの両方で同じ上位バージョンを指定するように注意してください。これは、[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] のバージョンが上位の整数で最も重要なものであるためです。 Mageui.exe を使用した場合、配置マニフェストを更新するには、 **[アプリケーション参照]** タブをクリックし、 **[マニフェストの選択]** ボタンをクリックして、更新されたアプリケーションマニフェストを選択します。  
  
## <a name="see-also"></a>参照  
 [Mage.exe (マニフェストの生成および編集ツール)](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)   
 [MageUI.exe (マニフェスト生成および編集ツールのグラフィカル クライアント)](https://msdn.microsoft.com/library/f9e130a6-8117-49c4-839c-c988f641dc14)   
 [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)   
 [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)   
 [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)

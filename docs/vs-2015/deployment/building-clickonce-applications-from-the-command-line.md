---
title: コマンドラインから ClickOnce アプリケーションをビルドする |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, from command line
- publishing
- publishing, ClickOnce
ms.assetid: d9bc6212-c584-4f72-88c9-9a4b998c555e
caps.latest.revision: 25
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2625a8d4caa7dd53e9ce86395a98622f91d686b3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68155707"
---
# <a name="building-clickonce-applications-from-the-command-line"></a>ClickOnce アプリケーションのコマンド ラインからのビルド
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

では、 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 統合開発環境 (IDE: integrated development environment) で作成されたプロジェクトであっても、コマンドラインからプロジェクトをビルドできます。 実際には、がインストールされている別のコンピューターで、を使用して作成したプロジェクトをリビルドでき [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] ます。 これにより、たとえば、中央のビルドラボや、プロジェクト自体を構築する範囲を超えた高度なスクリプト手法を使用して、自動化されたプロセスを使用してビルドを再現できます。  
  
## <a name="using-msbuild-to-reproduce-clickonce-application-deployments"></a>MSBuild を使用して ClickOnce アプリケーションの配置を再現する  
 Msbuild/target: publish をコマンドラインで起動すると、MSBuild システムに対してプロジェクトをビルドし、publish フォルダーにアプリケーションを作成するように指示され [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。 これは、IDE で [ **発行** ] コマンドを選択することと同じです。  
  
 このコマンドは msbuild.exe を実行します。これは Visual Studio のコマンドプロンプト環境のパスにあります。  
  
 "ターゲット" は、コマンドの処理方法に関する MSBuild のインジケーターです。 キーターゲットは、"ビルド" ターゲットと "発行" ターゲットです。 ビルドターゲットは、IDE でビルドコマンドを選択する (または F5 キーを押す) ことに相当します。 プロジェクトをビルドするだけの場合は、「」と入力することでこれを実現でき `msbuild` ます。 このコマンドは、ビルドターゲットがによって生成されるすべてのプロジェクトの既定のターゲットであるため、機能 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] します。 これは、ビルドターゲットを明示的に指定する必要がないことを意味します。 したがって、「」と入力し `msbuild` た場合と同じ操作が実行され `msbuild /target:build` ます。  
  
 この `/target:publish` コマンドは、発行ターゲットを呼び出すように MSBuild に指示します。 発行ターゲットは、ビルドターゲットに依存します。 これは、発行操作がビルド操作のスーパーセットであることを意味します。 たとえば、Visual Basic または C# のソースファイルのいずれかを変更した場合、対応するアセンブリは発行操作によって自動的に再構築されます。  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]Mage.exe コマンドラインツールを使用してマニフェストを作成する完全な展開を生成する方法については [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 、「[チュートリアル: ClickOnce アプリケーションを手動で配置](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)する」を参照してください。  
  
## <a name="creating-and-building-a-basic-clickonce-application-using-msbuild"></a>MSBuild を使用した基本的な ClickOnce アプリケーションの作成とビルド  
  
#### <a name="to-create-and-publish-a-clickonce-project"></a>ClickOnce プロジェクトを作成および発行するには  
  
1. [**ファイル**] メニューの [**新しいプロジェクト**] をクリックします。 **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
2. [ **Windows アプリケーション** ] を選択し、という名前を指定 `CmdLineDemo` します。  
  
3. [ **ビルド** ] メニューの [ **発行** ] をクリックします。  
  
    この手順により、アプリケーションの配置を生成するようにプロジェクトが適切に構成され [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。  
  
    発行ウィザードが表示されます。  
  
4. 発行ウィザードで、[ **完了**] をクリックします。  
  
    Visual Studio によって、Publish.htm と呼ばれる既定の Web ページが生成されて表示されます。  
  
5. プロジェクトを保存し、格納されているフォルダーの場所をメモします。  
  
   上記の手順では、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 初めて発行されたプロジェクトを作成します。 これで、IDE の外部でビルドを再現できます。  
  
#### <a name="to-reproduce-the-build-from-the-command-line"></a>コマンドラインからビルドを再現するには  
  
1. [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] を終了します。  
  
2. Windows の [ **スタート** ] メニューから、[ **すべてのプログラム**]、[ **Microsoft Visual Studio**]、[ **Visual Studio Tools**]、[ **Visual Studio コマンドプロンプト**] の順にクリックします。 これにより、現在のユーザーのルートフォルダーでコマンドプロンプトが開きます。  
  
3. **Visual Studio のコマンドプロンプト**で、現在のディレクトリを、先ほど作成したプロジェクトの場所に変更します。 たとえば、「 `chdir My Documents\Visual Studio\Projects\CmdLineDemo`」と入力します。  
  
4. 「プロジェクトを作成および発行するには」で作成した既存のファイルを削除するには [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 、「」と入力 `rmdir /s publish` します。  
  
    この手順は省略可能ですが、新しいファイルがすべてコマンドラインビルドによって生成されるようになります。  
  
5. 「`msbuild /target:publish`.  
  
   上記の手順を実行すると、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] **Publish**という名前のプロジェクトのサブフォルダーにアプリケーションの完全配置が生成されます。 CmdLineDemo. アプリケーションは [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 配置マニフェストです。 0.0.0 CmdLineDemo_1 フォルダーには、CmdLineDemo.exe ファイルと CmdLineDemo.exe アプリケーションマニフェストのファイルが含まれています。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] Setup.exe はブートストラップで、既定では、をインストールするように構成されてい [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] ます。 Dotnetfx.exe フォルダーには、の再頒布可能パッケージが含まれてい [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] ます。 これは、Web 経由で、または UNC または CD/DVD 経由でアプリケーションをデプロイするために必要なファイルのセット全体です。  
  
## <a name="publishing-properties"></a>発行のプロパティ  
 上記の手順でアプリケーションを発行すると、発行ウィザードによって次のプロパティがプロジェクトファイルに挿入されます。 これらのプロパティは、アプリケーションの生成方法に直接影響 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] します。  
  
 CmdLineDemo. .vbproj/CmdLineDemo. .csproj:  
  
```  
<AssemblyOriginatorKeyFile>WindowsApplication3.snk</AssemblyOriginatorKeyFile>  
<GenerateManifests>true</GenerateManifests>  
<TargetZone>LocalIntranet</TargetZone>  
<PublisherName>Microsoft</PublisherName>  
<ProductName>CmdLineDemo</ProductName>  
<PublishUrl>http://localhost/CmdLineDemo</PublishUrl>  
<Install>true</Install>  
<ApplicationVersion>1.0.0.*</ApplicationVersion>  
<ApplicationRevision>1</ApplicationRevision>  
<UpdateEnabled>true</UpdateEnabled>  
<UpdateRequired>false</UpdateRequired>  
<UpdateMode>Foreground</UpdateMode>  
<UpdateInterval>7</UpdateInterval>  
<UpdateIntervalUnits>Days</UpdateIntervalUnits>  
<UpdateUrlEnabled>false</UpdateUrlEnabled>  
<IsWebBootstrapper>true</IsWebBootstrapper>  
<BootstrapperEnabled>true</BootstrapperEnabled>  
```  
  
 これらのプロパティは、プロジェクトファイル自体を変更せずに、コマンドラインでオーバーライドできます。 たとえば、次のようにすると、ブートストラップを使用せずにアプリケーションの展開がビルドされ [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。  
  
```  
msbuild /target:publish /property:BootstrapperEnabled=false  
```  
  
 発行プロパティは [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 、**プロジェクトデザイナー**の [**発行**]、[**セキュリティ**]、[**署名**] の各プロパティページからで制御されます。 次に示すのは、発行プロパティの説明と、アプリケーションデザイナーのさまざまなプロパティページでそれぞれがどのように設定されているかを示しています。  
  
- `AssemblyOriginatorKeyFile` アプリケーションマニフェストに署名するために使用するキーファイルを指定し [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。 この同じキーを使用して、アセンブリに厳密な名前を割り当てることもできます。 このプロパティは、**プロジェクトデザイナー**の [**署名**] ページで設定します。  
  
  [ **セキュリティ** ] ページでは、次のプロパティが設定されます。  
  
- **ClickOnce セキュリティ設定を有効に** すると、マニフェストを生成するかどうか [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] が決まります。 プロジェクトが最初に作成されたとき、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] マニフェストの生成は既定で無効になっています。 初回の発行時に、ウィザードによって自動的にこのフラグがオンになります。  
  
- **Targetzone** は、アプリケーションマニフェストに出力する信頼のレベルを決定し [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。 指定できる値は、"Internet"、"LocalIntranet"、および "Custom" です。 インターネットとイントラネットでは、既定のアクセス許可セットがアプリケーションマニフェストに出力され [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。 既定値は LocalIntranet で、基本的には完全信頼であることを意味します。 Custom は、基本アプリケーションのマニフェストファイルで明示的に指定されたアクセス許可のみがアプリケーションマニフェストに出力されることを指定し [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。 アプリケーションのマニフェストファイルは、信頼情報の定義のみを含む部分的なマニフェストファイルです。 これは、[ **セキュリティ** ] ページでアクセス許可を構成するときにプロジェクトに自動的に追加される、非表示のファイルです。  
  
  [ **発行** ] ページでは、次のプロパティが設定されます。  
  
- `PublishUrl` は、アプリケーションが IDE で公開される場所です。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] `InstallUrl` またはプロパティが指定されていない場合は、アプリケーションマニフェストに挿入され `UpdateUrl` ます。  
  
- `ApplicationVersion` アプリケーションのバージョンを指定し [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。 これは4桁のバージョン番号です。 最後の数字が "*" の場合、 `ApplicationRevision` ビルド時にマニフェストに挿入される値の代わりにが使用されます。  
  
- `ApplicationRevision` リビジョンを指定します。 これは、IDE で公開するたびにインクリメントされる整数です。 これは、コマンドラインで実行されるビルドに対して自動的にはインクリメントされないことに注意してください。  
  
- `Install` アプリケーションがインストールされているアプリケーションであるか、Web アプリケーションから実行されているかを判断します。  
  
- `InstallUrl` (表示されません) は、ユーザーがアプリケーションをインストールする場所です。 この値が指定されている場合は、 `IsWebBootstrapper` プロパティが有効になっている場合に setup.exe ブートストラップに書き込まれます。 が指定されていない場合は、アプリケーションマニフェストにも挿入され `UpdateUrl` ます。  
  
- `SupportUrl` (表示されません) は、インストールされているアプリケーションの [ **プログラムの追加と削除** ] ダイアログボックスにリンクされている場所です。  
  
  [ **アプリケーションの更新** ] ダイアログボックスでは、次のプロパティが設定されます。このダイアログボックスは、[ **発行** ] ページからアクセスします。  
  
- `UpdateEnabled` アプリケーションが更新プログラムを確認する必要があるかどうかを示します。  
  
- `UpdateMode` フォアグラウンド更新またはバックグラウンド更新のいずれかを指定します。  
  
- `UpdateInterval` アプリケーションが更新プログラムを確認する頻度を指定します。  
  
- `UpdateIntervalUnits``UpdateInterval`値が時間単位、日単位、または週単位のどちらであるかを指定します。  
  
- `UpdateUrl` (表示されません) は、アプリケーションが更新プログラムを受信する場所です。 この値が指定されている場合は、アプリケーションマニフェストに挿入されます。  
  
- [発行 **オプション** ] ダイアログボックスでは、次のプロパティが設定されます。このダイアログボックスは、[ **発行** ] ページからアクセスします。  
  
- `PublisherName` アプリケーションのインストール時または実行時に表示されるプロンプトに表示される発行元の名前を指定します。 インストールされているアプリケーションの場合は、[ **スタート** ] メニューのフォルダー名を指定するためにも使用されます。  
  
- `ProductName` アプリケーションのインストール時または実行時に表示されるプロンプトに表示される製品の名前を指定します。 アプリケーションがインストールされている場合は、[ **スタート** ] メニューのショートカット名を指定するためにも使用されます。  
  
- [ **必須コンポーネント** ] ダイアログボックスでは、次のプロパティが設定されます。このダイアログボックスは、[ **発行** ] ページからアクセスします。  
  
- `BootstrapperEnabled` setup.exe ブートストラップを生成するかどうかを決定します。  
  
- `IsWebBootstrapper` setup.exe ブートストラップが Web またはディスクベースモードのどちらで動作するかを決定します。  
  
## <a name="installurl-supporturl-publishurl-and-updateurl"></a>InstallURL、SupportUrl、PublishURL、UpdateURL  
 次の表は、ClickOnce 配置の4つの URL オプションを示しています。  
  
|URL オプション|説明|  
|----------------|-----------------|  
|`PublishURL`|ClickOnce アプリケーションを Web サイトに発行する場合に必要です。|  
|`InstallURL`|省略可能。 インストールサイトがと異なる場合は、この URL オプションを設定し `PublishURL` ます。 たとえば、を `PublishURL` FTP パスに設定し、を `InstallURL` Web URL に設定できます。|  
|`SupportURL`|省略可能。 サポートサイトがと異なる場合は、この URL オプションを設定し `PublishURL` ます。 たとえば、を `SupportURL` 会社のカスタマーサポート Web サイトに設定できます。|  
|`UpdateURL`|省略可能。 更新プログラムの場所がと異なる場合は、この URL オプションを設定し `InstallURL` ます。 たとえば、を `PublishURL` FTP パスに設定し、を `UpdateURL` Web URL に設定できます。|  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.Build.Tasks.GenerateBootstrapper>   
 <xref:Microsoft.Build.Tasks.GenerateApplicationManifest>   
 <xref:Microsoft.Build.Tasks.GenerateDeploymentManifest>   
 [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)   
 [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)

---
title: コマンドラインから ClickOnce アプリケーションをビルドする |Microsoft Docs
description: コマンドラインから Visual Studio プロジェクトをビルドする方法について説明します。これにより、自動化されたプロセスを使用してビルドを再現できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4b719f9609dfb2feb432f4692b31e820d806ff92
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94437724"
---
# <a name="build-clickonce-applications-from-the-command-line"></a>ClickOnce アプリケーションのコマンド ラインからのビルド

では、 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] 統合開発環境 (IDE: integrated development environment) で作成されたプロジェクトであっても、コマンドラインからプロジェクトをビルドできます。 実際には、.NET Framework がインストールされている別のコンピューターで、を使用して作成されたプロジェクトをリビルドすることができ [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] ます。 これにより、たとえば、中央のビルドラボや、プロジェクト自体を構築する範囲を超えた高度なスクリプト手法を使用して、自動化されたプロセスを使用してビルドを再現できます。

## <a name="use-msbuild-to-reproduce-net-framework-clickonce-application-deployments"></a>MSBuild を使用して .NET Framework ClickOnce アプリケーションの配置を再現する

 Msbuild/target: publish をコマンドラインで起動すると、MSBuild システムに対してプロジェクトをビルドし、publish フォルダーにアプリケーションを作成するように指示され [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 これは、IDE で [ **発行** ] コマンドを選択することと同じです。

 このコマンドは *msbuild.exe* を実行します。これは Visual Studio のコマンドプロンプト環境のパスにあります。

 "ターゲット" は、コマンドの処理方法に関する MSBuild のインジケーターです。 キーターゲットは、"ビルド" ターゲットと "発行" ターゲットです。 ビルドターゲットは、IDE でビルドコマンドを選択する (または F5 キーを押す) ことに相当します。 プロジェクトをビルドするだけの場合は、「」と入力することでこれを実現でき `msbuild` ます。 このコマンドは、ビルドターゲットがによって生成されるすべてのプロジェクトの既定のターゲットであるため、機能 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] します。 これは、ビルドターゲットを明示的に指定する必要がないことを意味します。 したがって、「」と入力し `msbuild` た場合と同じ操作が実行され `msbuild /target:build` ます。

 この `/target:publish` コマンドは、発行ターゲットを呼び出すように MSBuild に指示します。 発行ターゲットは、ビルドターゲットに依存します。 これは、発行操作がビルド操作のスーパーセットであることを意味します。 たとえば、Visual Basic または C# のソースファイルのいずれかを変更した場合、対応するアセンブリは発行操作によって自動的に再構築されます。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]Mage.exe コマンドラインツールを使用してマニフェストを作成する完全な展開を生成する方法については [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 、「[チュートリアル: ClickOnce アプリケーションを手動で配置](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)する」を参照してください。

## <a name="create-and-build-a-basic-clickonce-application-with-msbuild"></a>MSBuild を使用した基本的な ClickOnce アプリケーションの作成とビルド

### <a name="to-create-and-publish-a-clickonce-project"></a>ClickOnce プロジェクトを作成および発行するには

1. Visual Studio を起動し、新しいプロジェクトを作成します。

    [ **Windows デスクトップアプリケーション** ] プロジェクトテンプレートを選択し、プロジェクトに名前を指定し `CmdLineDemo` ます。

1. [ **ビルド** ] メニューの [ **発行** ] をクリックします。

    この手順により、アプリケーションの配置を生成するようにプロジェクトが適切に構成され [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。

    発行ウィザードが表示されます。

1. 発行ウィザードで、[ **完了** ] をクリックします。

    Visual Studio によって、 *Publish.htm* と呼ばれる既定の Web ページが生成されて表示されます。

1. プロジェクトを保存し、格納されているフォルダーの場所をメモします。

   上記の手順では、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 初めて発行されたプロジェクトを作成します。 これで、IDE の外部でビルドを再現できます。

#### <a name="to-reproduce-the-build-from-the-command-line"></a>コマンドラインからビルドを再現するには

1. [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] を終了します。

2. Windows の [ **スタート** ] メニューから、[ **すべてのプログラム** ]、[ **Microsoft Visual Studio** ]、[ **Visual Studio Tools** ]、[ **Visual Studio コマンドプロンプト** ] の順にクリックします。 これにより、現在のユーザーのルートフォルダーでコマンドプロンプトが開きます。

3. **Visual Studio のコマンドプロンプト** で、現在のディレクトリを、先ほど作成したプロジェクトの場所に変更します。 たとえば、「 `chdir My Documents\Visual Studio\Projects\CmdLineDemo`」と入力します。

4. 「プロジェクトを作成および発行するには」で作成した既存のファイルを削除するには [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 、「」と入力 `rmdir /s publish` します。

    この手順は省略可能ですが、新しいファイルがすべてコマンドラインビルドによって生成されるようになります。

5. 「`msbuild /target:publish`」と入力します。

   上記の手順を実行すると、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] **Publish** という名前のプロジェクトのサブフォルダーにアプリケーションの完全配置が生成されます。 *Cmdlinedemo. アプリケーション* は [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置マニフェストです。 *0.0.0 CmdLineDemo_1* フォルダーには、 *CmdLineDemo.exe* ファイルと *CmdLineDemo.exe* アプリケーションマニフェストのファイルが含まれています。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] *Setup.exe* はブートストラップで、既定で .NET Framework をインストールするように構成されています。 Dotnetfx.exe フォルダーには、.NET Framework の再頒布可能ファイルが含まれています。 これは、Web 経由で、または UNC または CD/DVD 経由でアプリケーションをデプロイするために必要なファイルのセット全体です。

> [!NOTE]
> MSBuild システムでは、 **Publishdir** オプションを使用して、出力の場所を指定します。たとえば、のようにし `msbuild /t:publish /p:PublishDir="<specific location>"` ます。

::: moniker range=">=vs-2019"

## <a name="build-net-clickonce-applications-from-the-command-line"></a>コマンドラインからの .NET ClickOnce アプリケーションのビルド

コマンドラインからの .NET ClickOnce アプリケーションのビルドは同様の操作ですが、MSBuild コマンドラインで発行プロファイルに追加のプロパティを指定する必要があります。 発行プロファイルを作成する最も簡単な方法は、Visual Studio を使用することです。  詳細について [は、「ClickOnce を使用した .Net Windows アプリケーションの配置](quickstart-deploy-using-clickonce-folder.md) 」を参照してください。

発行プロファイルを作成した後は、msbuild コマンドラインで pubxml ファイルをプロパティとして指定できます。 次に例を示します。

```cmd
    msbuild /t:publish /p:PublishProfile=<pubxml file> /p:PublishDir="<specific location>"
```
::: moniker-end

## <a name="publish-properties"></a>[発行] プロパティ

 上記の手順でアプリケーションを発行すると、発行ウィザード、または .NET Core 3.1 またはそれ以降のプロジェクトの発行プロファイルファイルによって、プロジェクトファイルに次のプロパティが挿入されます。 これらのプロパティは、アプリケーションの生成方法に直接影響 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] します。

 *Cmdlinedemo. .vbproj* で、次のようにします。  /  *CmdLineDemo.csproj*

```xml
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

 .NET Framework プロジェクトでは、プロジェクトファイル自体を変更せずに、コマンドラインでこれらのプロパティをオーバーライドできます。 たとえば、次のようにすると、ブートストラップを使用せずにアプリケーションの展開がビルドされ [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。

```cmd
msbuild /target:publish /property:BootstrapperEnabled=false
 ```

::: moniker range=">=vs-2019"
.NET Core 3.1 以降では、これらの設定は pubxml ファイルに含まれています。

 発行プロパティは [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 、 **プロジェクトデザイナー** の [ **発行** ]、[ **セキュリティ** ]、[ **署名** ] の各プロパティページからで制御されます。 次に示すのは、発行プロパティの説明と、アプリケーションデザイナーのさまざまなプロパティページでそれぞれがどのように設定されているかを示しています。

> [!NOTE]
> .NET Windows デスクトッププロジェクトの場合、これらの設定は発行ウィザードに含まれるようになりました
::: moniker-end

- `AssemblyOriginatorKeyFile` アプリケーションマニフェストに署名するために使用するキーファイルを指定し [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 この同じキーを使用して、アセンブリに厳密な名前を割り当てることもできます。 このプロパティは、 **プロジェクトデザイナー** の [ **署名** ] ページで設定します。
::: moniker range=">=vs-2019"
.NET windows アプリケーションの場合、この設定はプロジェクトファイルに残ります
::: moniker-end

  [ **セキュリティ** ] ページでは、次のプロパティが設定されます。

- **ClickOnce セキュリティ設定を有効に** すると、マニフェストを生成するかどうか [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] が決まります。 プロジェクトが最初に作成されたとき、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] マニフェストの生成は既定で無効になっています。 初回の発行時に、ウィザードによって自動的にこのフラグがオンになります。

- **Targetzone** は、アプリケーションマニフェストに出力する信頼のレベルを決定し [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 指定できる値は、"Internet"、"LocalIntranet"、および "Custom" です。 インターネットとイントラネットでは、既定のアクセス許可セットがアプリケーションマニフェストに出力され [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 既定値は LocalIntranet で、基本的には完全信頼であることを意味します。 Custom は、基本アプリケーションの *マニフェスト* ファイルで明示的に指定されたアクセス許可のみがアプリケーションマニフェストに出力されることを指定し [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 *アプリケーションのマニフェスト* ファイルは、信頼情報の定義のみを含む部分的なマニフェストファイルです。 これは、[ **セキュリティ** ] ページでアクセス許可を構成するときにプロジェクトに自動的に追加される、非表示のファイルです。
-
::: moniker range=">=vs-2019"
> [!NOTE]
> .NET Core 3.1 以降、Windows デスクトッププロジェクトでは、これらのセキュリティ設定はサポートされていません。
::: moniker-end

  [ **発行** ] ページでは、次のプロパティが設定されます。

- `PublishUrl` は、アプリケーションが IDE で公開される場所です。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] `InstallUrl` またはプロパティが指定されていない場合は、アプリケーションマニフェストに挿入され `UpdateUrl` ます。

- `ApplicationVersion` アプリケーションのバージョンを指定し [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 これは4桁のバージョン番号です。 最後の数字が "*" の場合、 `ApplicationRevision` ビルド時にマニフェストに挿入される値の代わりにが使用されます。

- `ApplicationRevision` リビジョンを指定します。 これは、IDE で公開するたびにインクリメントされる整数です。 これは、コマンドラインで実行されるビルドに対して自動的にはインクリメントされないことに注意してください。

- `Install` アプリケーションがインストールされているアプリケーションであるか、Web アプリケーションから実行されているかを判断します。

- `InstallUrl` (表示されません) は、ユーザーがアプリケーションをインストールする場所です。 この値が指定されている場合 *setup.exe* は、 `IsWebBootstrapper` プロパティが有効になっている場合にsetup.exeブートストラップに書き込まれます。 が指定されていない場合は、アプリケーションマニフェストにも挿入され `UpdateUrl` ます。

- `SupportUrl` (表示されません) は、インストールされているアプリケーションの [ **プログラムの追加と削除** ] ダイアログボックスにリンクされている場所です。

  [ **アプリケーションの更新** ] ダイアログボックスでは、次のプロパティが設定されます。このダイアログボックスは、[ **発行** ] ページからアクセスします。

- `UpdateEnabled` アプリケーションが更新プログラムを確認する必要があるかどうかを示します。

- `UpdateMode` フォアグラウンド更新またはバックグラウンド更新のいずれかを指定します。
::: moniker range=">=vs-2019"
   .NET Core 3.1 以降では、プロジェクト、背景はサポートされていません。  
::: moniker-end
- `UpdateInterval` アプリケーションが更新プログラムを確認する頻度を指定します。
::: moniker range=">=vs-2019"
   .NET Core 3.1 以降では、この設定はサポートされていません。
::: moniker-end

- `UpdateIntervalUnits``UpdateInterval`値が時間単位、日単位、または週単位のどちらであるかを指定します。
::: moniker range=">=vs-2019"
   .NET Core 3.1 以降では、この設定はサポートされていません。
::: moniker-end

- `UpdateUrl` (表示されません) は、アプリケーションが更新プログラムを受信する場所です。 この値が指定されている場合は、アプリケーションマニフェストに挿入されます。

  [発行 **オプション** ] ダイアログボックスでは、次のプロパティが設定されます。このダイアログボックスは、[ **発行** ] ページからアクセスします。

- `PublisherName` アプリケーションのインストール時または実行時に表示されるプロンプトに表示される発行元の名前を指定します。 インストールされているアプリケーションの場合は、[ **スタート** ] メニューのフォルダー名を指定するためにも使用されます。

- `ProductName` アプリケーションのインストール時または実行時に表示されるプロンプトに表示される製品の名前を指定します。 アプリケーションがインストールされている場合は、[ **スタート** ] メニューのショートカット名を指定するためにも使用されます。

  [ **必須コンポーネント** ] ダイアログボックスでは、次のプロパティが設定されます。このダイアログボックスは、[ **発行** ] ページからアクセスします。

- `BootstrapperEnabled`*setup.exe* ブートストラップを生成するかどうかを決定します。

- `IsWebBootstrapper`*setup.exe* ブートストラップが Web またはディスクベースモードのどちらで動作するかを決定します。

## <a name="installurl-supporturl-publishurl-and-updateurl"></a>InstallURL、SupportUrl、PublishURL、UpdateURL

 次の表は、ClickOnce 配置の4つの URL オプションを示しています。

|URL オプション|説明|
|----------------|-----------------|
|`PublishURL`|ClickOnce アプリケーションを Web サイトに発行する場合に必要です。|
|`InstallURL`|任意。 インストールサイトがと異なる場合は、この URL オプションを設定し `PublishURL` ます。 たとえば、を `PublishURL` FTP パスに設定し、を `InstallURL` Web URL に設定できます。|
|`SupportURL`|任意。 サポートサイトがと異なる場合は、この URL オプションを設定し `PublishURL` ます。 たとえば、を `SupportURL` 会社のカスタマーサポート Web サイトに設定できます。|
|`UpdateURL`|任意。 更新プログラムの場所がと異なる場合は、この URL オプションを設定し `InstallURL` ます。 たとえば、を `PublishURL` FTP パスに設定し、を `UpdateURL` Web URL に設定できます。|

## <a name="see-also"></a>関連項目

- <xref:Microsoft.Build.Tasks.GenerateBootstrapper>
- <xref:Microsoft.Build.Tasks.GenerateApplicationManifest>
- <xref:Microsoft.Build.Tasks.GenerateDeploymentManifest>
- [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)
- [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)

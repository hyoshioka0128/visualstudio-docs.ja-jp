---
title: コマンドラインから ClickOnce アプリケーションをビルドする |Microsoft Docs
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
ms.openlocfilehash: 065eea058ffa78c84428e031832e24837eb81d08
ms.sourcegitcommit: af9bbf9116a63c0631ff2f4f3a878564aa63cd8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74797202"
---
# <a name="build-clickonce-applications-from-the-command-line"></a>ClickOnce アプリケーションのコマンド ラインからのビルド
[!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)]では、統合開発環境 (IDE: integrated development environment) で作成されている場合でも、コマンドラインからプロジェクトをビルドできます。 実際には、.NET Framework がインストールされている別のコンピューターで、[!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] で作成したプロジェクトをリビルドできます。 これにより、たとえば、中央のビルドラボや、プロジェクト自体を構築する範囲を超えた高度なスクリプト手法を使用して、自動化されたプロセスを使用してビルドを再現できます。

## <a name="use-msbuild-to-reproduce-clickonce-application-deployments"></a>MSBuild を使用して ClickOnce アプリケーションの配置を再現する
 Msbuild/target: publish をコマンドラインで起動すると、MSBuild システムに対してプロジェクトをビルドし、publish フォルダーに [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを作成するように指示します。 これは、IDE で **[発行]** コマンドを選択することと同じです。

 このコマンドは、Visual Studio のコマンドプロンプト環境のパスにある*msbuild.exe*を実行します。

 "ターゲット" は、コマンドの処理方法に関する MSBuild のインジケーターです。 キーターゲットは、"ビルド" ターゲットと "発行" ターゲットです。 ビルドターゲットは、IDE でビルドコマンドを選択する (または F5 キーを押す) ことに相当します。 プロジェクトをビルドするだけの場合は、「`msbuild`」と入力することでこれを実現できます。 このコマンドは、ビルドターゲットが [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)]によって生成されるすべてのプロジェクトの既定のターゲットであるため、機能します。 これは、ビルドターゲットを明示的に指定する必要がないことを意味します。 したがって、`msbuild` を入力する操作は `msbuild /target:build`の入力と同じです。

 `/target:publish` コマンドは、発行ターゲットを呼び出すように MSBuild に指示します。 発行ターゲットは、ビルドターゲットに依存します。 これは、発行操作がビルド操作のスーパーセットであることを意味します。 たとえば、Visual Basic またはC#ソースファイルのいずれかを変更した場合、対応するアセンブリは発行操作によって自動的に再構築されます。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] マニフェストを作成するために Mage.exe コマンドラインツールを使用して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] の完全な展開を生成する方法については、「[チュートリアル: ClickOnce アプリケーションを手動で配置](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)する」を参照してください。

## <a name="create-and-build-a-basic-clickonce-application-with-msbuild"></a>MSBuild を使用した基本的な ClickOnce アプリケーションの作成とビルド

#### <a name="to-create-and-publish-a-clickonce-project"></a>ClickOnce プロジェクトを作成および発行するには

1. Visual Studio を起動し、新しいプロジェクトを作成します。

    **[Windows デスクトップアプリケーション]** プロジェクトテンプレートを選択し、プロジェクトに `CmdLineDemo`という名前を指定します。

1. **[ビルド]** メニューの **[発行]** をクリックします。

    この手順により、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの配置を生成するようにプロジェクトが適切に構成されます。

    公開ウィザードが表示されます。

1. 発行ウィザードで、 **[完了]** をクリックします。

    Visual Studio によって、 *Publish*という既定の Web ページが生成されて表示されます。

1. プロジェクトを保存し、格納されているフォルダーの場所をメモします。

   上記の手順では、初めて発行された [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] プロジェクトを作成します。 これで、IDE の外部でビルドを再現できます。

#### <a name="to-reproduce-the-build-from-the-command-line"></a>コマンドラインからビルドを再現するには

1. [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] を終了します。

2. Windows の **[スタート]** メニューから、 **[すべてのプログラム]** 、 **[Microsoft Visual Studio]** 、 **[Visual Studio Tools]** 、 **[Visual Studio コマンドプロンプト]** の順にクリックします。 これにより、現在のユーザーのルートフォルダーでコマンドプロンプトが開きます。

3. **Visual Studio のコマンドプロンプト**で、現在のディレクトリを、先ほど作成したプロジェクトの場所に変更します。 たとえば、「`chdir My Documents\Visual Studio\Projects\CmdLineDemo`」を入力します。

4. 「[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] プロジェクトを作成して発行するには」で作成した既存のファイルを削除するには、「`rmdir /s publish`」と入力します。

    この手順は省略可能ですが、新しいファイルがすべてコマンドラインビルドによって生成されるようになります。

5. 「`msbuild /target:publish`」と入力します。

   上記の手順を実行すると、 **Publish**という名前のプロジェクトのサブフォルダーに、完全な [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーション配置が生成されます。 *Cmdlinedemo. アプリケーション*は [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置マニフェストです。 *0.0.0 CmdLineDemo_1*フォルダーには、 *cmdlinedemo .Exe*および*cmdlinedemo .exe*([!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションマニフェスト) のファイルが含まれています。 *Setup.exe* はブートストラップで、既定では .NET Framework をインストールするように構成されています。 Dotnetfx.exe フォルダーには、.NET Framework の再頒布可能ファイルが含まれています。 これは、Web 経由で、または UNC または CD/DVD 経由でアプリケーションをデプロイするために必要なファイルのセット全体です。
   
> [!NOTE]
> MSBuild システムでは、 **Publishdir**オプションを使用して、出力の場所を指定します (`msbuild /t:publish /p:PublishDir="<specific location>"`など)。

## <a name="publish-properties"></a>[発行] プロパティ
 上記の手順でアプリケーションを発行すると、発行ウィザードによって次のプロパティがプロジェクトファイルに挿入されます。 これらのプロパティは、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの生成方法に直接影響します。

 *CmdLineDemo.vbproj* / *CmdLineDemo.csproj*で：

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

 これらのプロパティは、プロジェクトファイル自体を変更せずに、コマンドラインでオーバーライドできます。 たとえば、次の例では、ブートストラップを使用せずに [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの展開をビルドします。

```cmd
msbuild /target:publish /property:BootstrapperEnabled=false
```

 発行プロパティは、**プロジェクトデザイナー**の **[発行]** 、 **[セキュリティ]** 、 **[署名]** の各プロパティページから [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] で制御されます。 次に示すのは、発行プロパティの説明と、アプリケーションデザイナーのさまざまなプロパティページでそれぞれがどのように設定されているかを示しています。

- `AssemblyOriginatorKeyFile` は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションマニフェストに署名するために使用されるキーファイルを決定します。 この同じキーを使用して、アセンブリに厳密な名前を割り当てることもできます。 このプロパティは、**プロジェクトデザイナー**の **[署名]** ページで設定します。

  **[セキュリティ]** ページでは、次のプロパティが設定されます。

- **ClickOnce セキュリティ設定を有効に**する [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] マニフェストを生成するかどうかを決定します。 プロジェクトが最初に作成されたときに、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] マニフェスト生成が既定でオフになっています。 初回の発行時に、ウィザードによって自動的にこのフラグがオンになります。

- **Targetzone**は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションマニフェストに出力する信頼のレベルを決定します。 指定できる値は、"Internet"、"LocalIntranet"、および "Custom" です。 インターネットとイントラネットでは、既定のアクセス許可セットが [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションマニフェストに出力されます。 既定値は LocalIntranet で、基本的には完全信頼であることを意味します。 Custom は、基本アプリケーションの*マニフェスト*ファイルで明示的に指定されたアクセス許可のみを [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションマニフェストに出力することを指定します。 *アプリケーションのマニフェスト*ファイルは、信頼情報の定義のみを含む部分的なマニフェストファイルです。 これは、 **[セキュリティ]** ページでアクセス許可を構成するときにプロジェクトに自動的に追加される、非表示のファイルです。

  **[発行]** ページでは、次のプロパティが設定されます。

- `PublishUrl` は、IDE でアプリケーションが発行される場所です。 `InstallUrl` または `UpdateUrl` プロパティが指定されていない場合は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションマニフェストに挿入されます。

- `ApplicationVersion` [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションのバージョンを指定します。 これは4桁のバージョン番号です。 最後の桁が "*" の場合、ビルド時にマニフェストに挿入される値の代わりに `ApplicationRevision` が使用されます。

- `ApplicationRevision` リビジョンを指定します。 これは、IDE で公開するたびにインクリメントされる整数です。 これは、コマンドラインで実行されるビルドに対して自動的にはインクリメントされないことに注意してください。

- `Install` は、アプリケーションがインストールされているアプリケーションであるか、Web から実行するアプリケーションであるかを判断します。

- `InstallUrl` (表示されません) は、ユーザーがアプリケーションをインストールする場所です。 この値が指定されている場合 、 `IsWebBootstrapper`プロパティが有効になっている場合は、*setup.exe* ブートストラップに書き込まれます。 `UpdateUrl` が指定されていない場合は、アプリケーションマニフェストにも挿入されます。

- `SupportUrl` (表示されません) は、インストールされているアプリケーションの **[プログラムの追加と削除]** ダイアログボックスにリンクされている場所です。

  **[アプリケーションの更新]** ダイアログボックスでは、次のプロパティが設定されます。このダイアログボックスは、 **[発行]** ページからアクセスします。

- `UpdateEnabled` アプリケーションで更新プログラムをチェックするかどうかを示します。

- `UpdateMode` は、フォアグラウンド更新またはバックグラウンド更新のいずれかを指定します。

- `UpdateInterval` は、アプリケーションが更新プログラムを確認する頻度を指定します。

- `UpdateIntervalUnits` `UpdateInterval` の値が時間単位、日単位、または週単位のどちらであるかを指定します。

- `UpdateUrl` (表示されません) は、アプリケーションが更新プログラムを受信する場所です。 この値が指定されている場合は、アプリケーションマニフェストに挿入されます。

  発行 **[オプション]** ダイアログボックスでは、次のプロパティが設定されます。このダイアログボックスは、 **[発行]** ページからアクセスします。

- `PublisherName` アプリケーションのインストール時または実行時に表示されるプロンプトに表示される発行元の名前を指定します。 インストールされているアプリケーションの場合は、 **[スタート]** メニューのフォルダー名を指定するためにも使用されます。

- `ProductName` アプリケーションのインストール時または実行時に表示されるプロンプトに表示される製品の名前を指定します。 アプリケーションがインストールされている場合は、 **[スタート]** メニューのショートカット名を指定するためにも使用されます。

  **[必須コンポーネント]** ダイアログボックスでは、次のプロパティが設定されます。このダイアログボックスは、 **[発行]** ページからアクセスします。

- `BootstrapperEnabled`*setup.exe* ブートストラップを生成するかどうかを決定します。

- `IsWebBootstrapper`*setup.exe* ブートストラップが Web またはディスクベースモードのどちらで動作するかを決定します。

## <a name="installurl-supporturl-publishurl-and-updateurl"></a>InstallURL、SupportUrl、PublishURL、UpdateURL
 次の表は、ClickOnce 配置の4つの URL オプションを示しています。

|URL オプション|説明|
|----------------|-----------------|
|`PublishURL`|ClickOnce アプリケーションを Web サイトに発行する場合に必要です。|
|`InstallURL`|省略可。 インストールサイトが `PublishURL`と異なる場合は、この URL オプションを設定します。 たとえば、`PublishURL` を FTP パスに設定し、`InstallURL` を Web URL に設定することができます。|
|`SupportURL`|省略可。 サポートサイトが `PublishURL`と異なる場合は、この URL オプションを設定します。 たとえば、会社のカスタマーサポート Web サイトに `SupportURL` を設定することができます。|
|`UpdateURL`|省略可。 更新プログラムの場所が `InstallURL`と異なる場合は、この URL オプションを設定します。 たとえば、`PublishURL` を FTP パスに設定し、`UpdateURL` を Web URL に設定することができます。|

## <a name="see-also"></a>参照
- <xref:Microsoft.Build.Tasks.GenerateBootstrapper>
- <xref:Microsoft.Build.Tasks.GenerateApplicationManifest>
- <xref:Microsoft.Build.Tasks.GenerateDeploymentManifest>
- [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)
- [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)

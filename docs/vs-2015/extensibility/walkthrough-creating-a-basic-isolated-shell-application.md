---
title: 'チュートリアル: 基本的な分離シェルアプリケーションの作成 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio shell, walkthroughs
- Shell [Visual Studio], walkthroughs
- walkthroughs [Visual Studio], isolated shell-based application
ms.assetid: 8b12e223-aae3-4c23-813d-ede1125f5f69
caps.latest.revision: 55
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6192eb5583e7d0bc37518e995aacccad643cc9ec
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75850349"
---
# <a name="walkthrough-creating-a-basic-isolated-shell-application"></a>チュートリアル: 基本的な分離シェル アプリケーションを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、分離シェルソリューションを作成する方法、ツールウィンドウに関するヘルプをカスタマイズする方法、および分離シェルをインストールするセットアッププログラムを作成する方法について説明します。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)」を参照してください。 分離シェルをデプロイするには、Visual Studio Shell (分離) 再頒布可能パッケージも使用する必要があります。  
  
## <a name="creating-an-isolated-shell-solution"></a>分離シェルソリューションの作成  
 このセクションでは、Visual Studio Shell 分離プロジェクトテンプレートを使用して、分離シェルソリューションを作成する方法について説明します。 このソリューションには、次のプロジェクトが含まれています。  
  
- *SolutionName*。Boxpackage プロジェクトでは、[ヘルプ/バージョン情報] ボックスの外観をカスタマイズできます。  
  
- ShellExtensionsVSIX プロジェクト。分離シェルアプリケーションのさまざまなコンポーネントを定義する source.extension.vsixmanifest ファイルが含まれています。  
  
- *SolutionName*プロジェクト。分離シェルアプリケーションを呼び出す実行可能ファイルを生成します。 このプロジェクトには、分離シェルアプリケーションの外観と動作を customiz できるシェルカスタマイズフォルダーが含まれています。  
  
- *SolutionName* UI プロジェクト。アクティブなメニューコマンドとローカライズ可能な文字列を定義するサテライトアセンブリを生成します。  
  
#### <a name="to-create-a-basic-isolated-shell-solution"></a>基本的な分離シェルソリューションを作成するには  
  
1. Visual Studio を起動し、新しいプロジェクトを作成します。  
  
2. [ **新しいプロジェクト** ] ウィンドウで、[ **その他のプロジェクトの種類** ]、[ **機能拡張**] の順に展開します。 [ **Visual Studio Shell 分離** プロジェクト] テンプレートを選択します。  
  
3. プロジェクトに名前 `MyVSShellStub` を指定し、場所を指定します。 [ **ソリューションのディレクトリを作成** ] チェックボックスがオンになっていることを確認し、[ **OK]** をクリックします。  
  
     新しいソリューションが **ソリューションエクスプローラー**に表示されます。  
  
4. ソリューションをビルドし、分離シェルアプリケーションのデバッグを開始します。  
  
     Visual Studio の分離シェルが表示されます。 タイトルバーは **Myvsshellstub**を読み取ります。 タイトルバーアイコンは \MyVSShellStub\Resource Files\ApplicationIcon.ico. から生成されます。  
  
## <a name="customizing-the-application-name-and-icon"></a>アプリケーション名とアイコンのカスタマイズ  
 会社の名前とそのロゴをタイトルバーに使用して、アプリケーションをブランド化することができます。 次の手順では、カスタムアプリケーションのタイトルバーに表示される名前とアイコンを変更する方法を示します。パッケージ定義ファイル (MyVSShellStub. Application. pkgdef) を変更します。  
  
#### <a name="to-customize-the-application-name-and-icon"></a>アプリケーション名とアイコンをカスタマイズするには  
  
1. MyVSShellStub プロジェクトで、Customization\MyVSShellStub.Application.pkgdef. を開きます。  
  
2. 要素の `AppName` 値を **"AppName" = "Fabrikam Music Editor"** に変更します。  
  
3. アプリケーションアイコンを変更するには、別のアイコンを \MyVSShellStub\MyVSShellStub\MyVSShellStub\ ディレクトリにコピーします。 既存の ApplicationIcon .ico ファイルの名前を ApplicationIcon1 に変更します。 新しいファイルの名前を ApplicationIcon .ico に変更します。  
  
4. ソリューションをビルドし、デバッグを開始します。 分離シェル IDE が表示されます。 タイトルバーには、 **Fabrikam Music Editor**という単語の横に新しいアイコンが表示されます。  
  
## <a name="customizing-the-default-web-browser-home-page"></a>既定の Web ブラウザーのホームページのカスタマイズ  
 このセクションでは、パッケージ定義ファイルを変更して、 **Web ブラウザー** ウィンドウの既定のホームページを変更する方法について説明します。  
  
#### <a name="to-customize-the-default-web-browser-home-page"></a>既定の Web ブラウザーのホームページをカスタマイズするには  
  
1. MyVSShellStub. Application. pkgdef ファイルで、 `DefaultHomePage` 要素の値を "" に変更します <https://www.microsoft.com> 。  
  
2. MyVSShellStub プロジェクトをリビルドします。  
  
3. ソリューションをビルドし、デバッグを開始します。  
  
4. **表示/その他のウィンドウ**で、[ **Web ブラウザー**] をクリックします。 [ **Web ブラウザー** ] ウィンドウに、Microsoft Corporation のホームページが表示されます。  
  
## <a name="removing-the-print-command"></a>印刷コマンドを削除しています  
 分離シェル UI プロジェクトの vsct ファイルは、form 要素の一連の宣言で構成されています。 `<Define name=No_` *Element* `>` *Element*は、標準の Visual Studio のメニューおよびコマンドの1つです。  
  
 宣言をコメント解除すると、そのメニューまたはコマンドが分離シェルから除外されます。 逆に、宣言にコメントが付いている場合は、メニューまたはコマンドが分離シェルに含まれます。  
  
 次の手順では、vsct ファイルの print コマンドのコメントを解除します。  
  
#### <a name="to-remove-the-print-command"></a>印刷コマンドを削除するには  
  
1. 分離シェルアプリケーションの [**ファイル**] メニューに [**印刷**] コマンドが表示されていることを確認します。  
  
2. MyVSShellStubUI プロジェクトで、\ Resource Files\MyVSShellStubUI.vsct を開いて編集します。  
  
3. 次の行のコメントを解除:  
  
    ```  
    <!-- <Define name="No_PrintChildrenCommand"/> -->  
    ```  
  
4. これにより、印刷コマンドが削除されます。  
  
5. 分離シェルアプリケーションのデバッグを開始します。 **ファイル/印刷**コマンドが実行されていないことを確認します。  
  
## <a name="removing-features-from-the-isolated-shell"></a>分離シェルからの機能の削除  
 カスタム分離シェルアプリケーションでこれらの機能を使用しない場合は、Visual Studio で読み込まれたパッケージの一部を削除できます。 パッケージは、$RootKey $ \ Packages レジストリキーのいずれかのサブキーで指定します。  
  
> [!NOTE]
> Visual Studio の機能の Guid については、「 [Visual studio の機能のパッケージ guid](../extensibility/package-guids-of-visual-studio-features.md)」を参照してください。  
  
 次の手順は、分離シェルから XML エディターを削除する方法を示しています。  
  
#### <a name="to-remove-the-xml-editor"></a>XML エディターを削除するには  
  
1. MyVSShellStub プロジェクトの Shell カスタマイズフォルダーで、MyVSShellStub を開きます。  
  
2. 次の行のコメントを解除します。  
  
     [$RootKey $ \ パッケージ \\{87 569308481340 a0-9cd0-d7a30838ca3f}]  
  
3. ソリューションをリビルドし、分離シェルのデバッグを開始します。 XML ファイルを開きます (たとえば、\MyVSShellStub\MyVSShellStub\MyVSShellStubUI\MyVSShellStubUI.vsct.)。 ファイル内の XML キーワードが色分けされていないこと、および行に "<" と入力しても XML ツールヒントが表示されないことを確認します。  
  
## <a name="customizing-the-helpabout-box"></a>[ヘルプ]/[バージョン情報] ボックスのカスタマイズ  
 分離シェルプロジェクトテンプレートの一部として作成される [ヘルプ/バージョン情報] ボックスをカスタマイズできます。  
  
#### <a name="to-customize-the-company-name"></a>会社名をカスタマイズするには  
  
1. 会社名、著作権情報、製品バージョン、および製品の説明は、\Properties\AssemblyInfo.cs ファイルの MyVSShellStub.. Boxpackage プロジェクトにあります。 このファイルを開きます。  
  
2. 値を `AssemblyCompany` **fabrikam**、値、 `AssemblyProduct` および `AssemblyTitle` **fabrikam ミュージックエディター**に変更し、 `AssemblyCopyright` 値を **Copyright © fabrikam 2015**に変更します。  
  
    ```  
    [assembly: AssemblyTitle("Fabrikam Music Editor")]  
    [assembly: AssemblyDescription("")]  
    [assembly: AssemblyConfiguration("")]  
    [assembly: AssemblyCompany("Fabrikam")]  
    [assembly: AssemblyProduct("Fabrikam Music Editor")]  
    [assembly: AssemblyCopyright("Copyright © Fabrikam 2015")] [assembly: AssemblyCompany("Fabrikam")]  
    [assembly: AssemblyProduct("Fabrikam Music Editor ")]  
    [assembly: AssemblyCopyright("Copyright © Fabrikam 2015”)]  
    ```  
  
3. 製品の説明を追加するには、 `AssemblyDescription` 値を**Fabrikam Music editor の説明に変更します。**  
  
    ```  
    [assembly: AssemblyDescription("The description of Fabrikam Music editor.”)]  
    ```  
  
4. デバッグを開始し、分離シェルアプリケーションで [ **ヘルプ/バージョン情報** ] ボックスを開きます。 変更した文字列が表示されます。 [ヘルプ/バージョン情報] ボックスのタイトルは、 `AssemblyTitle` AssemblyInfo.cs の値と同じです。  
  
5. [ **ヘルプ]/[バージョン情報** ] ボックス自体のプロパティは、MyVSShellStub に含まれています。 [ヘルプ/バージョン情報] ボックスの幅を変更するには、ブロックに移動 `AboutDialogStyle` し、 `Width` プロパティを200に設定します。  
  
    ```  
    <Style x:Key="AboutDialogStyle" TargetType="Window">  
        <Setter Property="Height" Value="Auto" />  
        <Setter Property="Width" Value="200" />  
        <Setter Property="ShowInTaskbar" Value="False" />  
        <Setter Property="ResizeMode" Value="NoResize" />  
        <Setter Property="WindowStyle" Value="SingleBorderWindow" />  
        <Setter Property="SizeToContent" Value="Height" />  
    </Style>  
    ```  
  
6. ソリューションをリビルドし、分離シェルのデバッグを開始します。 [ヘルプ/バージョン情報] ボックスは、ほぼ正方形である必要があります。  
  
## <a name="before-you-deploy-the-isolated-shell-application"></a>分離シェルアプリケーションを展開する前に  
 分離シェルアプリケーションは、Visual Studio Shell (分離) 再頒布可能パッケージがインストールされている任意のコンピューターにインストールできます。 再頒布可能パッケージの詳細については、 [Visual Studio 機能拡張ダウンロード](https://msdn.microsoft.com/vstudio/bb984878.aspx) の web サイトを参照してください。  
  
## <a name="deploying-the-isolated-shell-application"></a>分離シェルアプリケーションの展開  
 セットアッププロジェクトを作成して、対象のコンピューターに分離シェルアプリケーションを配置します。 次の項目を指定する必要があります。  
  
- ターゲットコンピューター上のフォルダーとファイルのレイアウト。  
  
- .NET Framework と Visual Studio shell ランタイムがターゲットコンピューターにインストールされることを保証する起動条件。  
  
  次の手順では、InstallShield 限定版 Edition をコンピューターにインストールする必要があります。  
  
#### <a name="to-create-the-setup-project"></a>セットアッププロジェクトを作成するには  
  
1. **ソリューションエクスプローラー**で、ソリューションノードを右クリックし、[**新しいプロジェクトの追加**] をクリックします。  
  
2. [ **新しいプロジェクト** ] ダイアログボックスで、[ **その他のプロジェクトの種類** ] を展開し、[ **セットアップと配置**] を選択します。 InstallShield テンプレートを選択します。 新しいプロジェクトに名前を指定し、 `MySetup` [ **OK]** をクリックします。  
  
3. InstallShield の制限付きエディションが既にインストールされている場合は、次の手順に進みます。  
  
    InstallShield の制限付きエディションがまだインストールされていない場合は、InstallShield のダウンロードページが表示されます。 指示に従って製品をダウンロードしてインストールし、使用している Visual Studio のバージョンと互換性のある InstallShield のバージョンを選択します。 InstallShield のインストールを登録するか、評価として使用するかを決定する必要があります。 インストールが完了したら、Visual Studio を再起動する必要があります。  
  
   > [!IMPORTANT]
   > InstallShield プロジェクトを作成する前に、管理者として Visual Studio を起動する必要があります。 そうしないと、プロジェクトのビルド時にエラーが発生します。  
  
   次の手順では、セットアッププロジェクトの構成方法について説明します。  
  
> [!IMPORTANT]
> セットアッププロジェクトを構成する前に、分離シェルプロジェクトのリリース構成が少なくとも1回ビルドされていることを確認してください。  
  
#### <a name="to-configure-the-setup-project"></a>セットアッププロジェクトを構成するには  
  
1. **ソリューションエクスプローラー**の**mysetup**プロジェクトで、[ **project Assistant**] を選択します。 **プロジェクトアシスタント**ウィンドウの下部の行で、[**アプリケーション情報**] を選択します。 アプリケーション名として「 **fabrikam** 」と入力し、会社名と **fabrikam ミュージックエディター** を入力します。 **プロジェクトアシスタント**の右下にある [進む] 矢印をクリックします。  
  
2. [アプリケーションで**コンピューターにソフトウェアをインストールする必要がありますか?** ] で [**はい**] を選択し、[ **Microsoft .NET Framework 4.5 Full Package**] を選択します。  
  
3. ウィンドウの下部にある [ **アプリケーションファイル** ] ボタンをクリックし、[ **Fabrikam Music Editor** ] フォルダーが選択されていることを確認します。  
  
4. [ **ファイルの追加** ] ボタンをクリックします。 [ **ファイルの追加** ] ダイアログボックスで、 **MyVSShellStub\Release** フォルダーから次のファイルを追加します。  
  
    1. MyVSShellStub.exe.config  
  
    2. DebuggerProxy.dll  
  
    3. DebuggerProxy.dll .manifest  
  
    4. MyVSShellStub。 pkgdef  
  
    5. MyVSShellStub。 pkgundef  
  
    6. MyVSShellStub. winprf  
  
    7. Splash.bmp  
  
5. [ **プロジェクト出力の追加** ] ボタンをクリックし、 **Myvsshellstub/プライマリ出力**を追加します。 **[OK]** をクリックします。  
  
6. 左側のウィンドウの [**対象コンピューター**] で、 **Fabrikam MUSIC Editor [INSTALLDIR]** ノードを右クリックし、[ **Extensions**] という名前の**新しいフォルダー**を追加します。  
  
7. 左ペインで [ **拡張機能** ] ノードを右クリックし、[ **アプリケーション**] という名前の新しいフォルダーを追加します。  
  
8. **アプリケーション**フォルダーを選択し、[**プロジェクト出力の追加**] ボタンをクリックしてから、myvsshellstub... boxpackage プロジェクトのプライマリ出力を選択します。  
  
9. [ **Add files** ] \ (ファイルの追加 \) ボタンをクリックし、\MyVSShellStub\Release\Extensions\Application\ フォルダーから次のファイルを追加します。  
  
    - MyVSShellStub.... pkgdef  
  
    - MyVSShellStub. Application. pkgdef  
  
10. 左側のウィンドウで **Fabrikam Music Editor [INSTALLDIR]** ノードを右クリックし、 **1033**という名前の新しいフォルダーを追加します。  
  
11. 1033フォルダーを選択し、[ **プロジェクト出力の追加** ] ボタンをクリックして、MyVSShellStubUI プロジェクトのプライマリ出力を選択します。  
  
12. **アプリケーションショートカット**ウィンドウに移動します。  
  
13. ショートカットを作成するには [ **新規** ] をクリックし、 **[programfilesfolder] \Fabrikam\Fabrikam Music Output**を選択します。  
  
14. [インストールの **インタビュー** ] ウィンドウに移動します。  
  
15. すべての項目を **No**に設定します。  
  
16. **ソリューションエクスプローラー**の mysetup プロジェクトで、[**セットアップ要件とアクション \ 要件を定義**する] を開きます。 [ **要件** ] ウィンドウが開きます。  
  
17. [ **システムソフトウェアの要件** ] を右クリックし、[ **新しい起動条件の作成**] を選択します。 **システム検索ウィザード**が表示されます。  
  
18. [ **検索する項目** ] ウィンドウで、ドロップダウンリストの [ **レジストリエントリ** ] を選択し、[ **次へ**] をクリックします。  
  
19. [ **検索方法** を選択してください] ウィンドウで、レジストリルートとして [ **HKEY_LOCAL_MACHINE** ] を選択します。 64ビットシステムの場合は「 **SOFTWARE\Wow6432Node\Microsoft\DevDiv\vs\Servicing\14.0\isoshell** 」、32ビットシステムの場合は「 **SOFTWARE\Microsoft\DevDiv\vs\Servicing\14.0\isoshell** 」と入力し、レジストリ値として「 **Install** 」と入力します。 **[次へ]** をクリックします。  
  
20. [値を入力し**てください]** ウィンドウで、「**この製品をインストールするには、Visual Studio 2015 の分離シェル再頒布可能パッケージが必要です**」と入力します。 表示テキストとして、[ **完了**] をクリックします。  
  
21. セットアッププロジェクトを作成するために、分離シェルソリューションをリビルドします。  
  
     setup.exe ファイルは次のフォルダーにあります。  
  
     \MyVSShellStub\MySetup\MySetup\Express\SingleImage\DiskImages\DISK1  
  
## <a name="testing-the-installation-program"></a>インストールプログラムのテスト  
 セットアップをテストするには、setup.exe ファイルを別のコンピューターにコピーし、セットアップ実行可能ファイルを実行します。 分離シェルアプリケーションを実行できるようになります。

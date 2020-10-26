---
title: 分離シェルアプリケーションのインストール |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Shell [Visual Studio], deploying shell-based applications
- Visual Studio shell, deploying shell-based applications
ms.assetid: 33416226-9083-41b5-b153-10d2bf35c012
caps.latest.revision: 41
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0adc81cfe9ea4462940c31a02c6429be89709565
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75944260"
---
# <a name="installing-an-isolated-shell-application"></a>分離シェル アプリケーションのインストール
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

シェルアプリをインストールするには、次の手順を実行する必要があります。  
  
- ソリューションを準備します。  
  
- アプリケーションの Windows インストーラー (MSI) パッケージを作成します。  
  
- セットアップブートストラップを作成します。  
  
  このドキュメントのコード例はすべて、「 [シェルデプロイのサンプル](https://code.msdn.microsoft.com/Sample-setup-program-for-81ca73f7)」から入手できます。このサンプルは、MSDN web サイトのコードギャラリーからダウンロードできます。 このサンプルは、これらの各手順を実行した結果を示しています。  
  
## <a name="prerequisites"></a>前提条件  
 このトピックで説明する手順を実行するには、次のツールをコンピューターにインストールする必要があります。  
  
- Visual Studio SDK  
  
- [WINDOWS インストーラー XML ツールセット](https://documentation.help/WiX-Toolset/index.html/)バージョン3.6  
  
  このサンプルでは、すべてのシェルが必要としない Microsoft の視覚化およびモデリング SDK も必要です。  
  
## <a name="preparing-your-solution"></a>ソリューションの準備  
 既定では、シェルテンプレートは VSIX パッケージに対してビルドされますが、この動作は主にデバッグ目的で使用されます。 シェルアプリケーションを展開するときに、MSI パッケージを使用して、レジストリへのアクセスを許可し、インストール中に再起動する必要があります。 MSI の展開のためにアプリケーションを準備するには、次の手順を実行します。  
  
#### <a name="to-prepare-a-shell-application-for-msi-deployment"></a>MSI 展開用のシェルアプリケーションを準備するには  
  
1. ソリューション内の各 source.extension.vsixmanifest ファイルを編集します。  
  
     要素に要素 `Identifier` `InstalledByMSI` と要素を追加し、 `SystemComponent` その値をに設定し `true` ます。  
  
     これらの要素を使用すると、VSIX インストーラーによってコンポーネントがインストールされないようにすることができ、ユーザーは [ **拡張機能と更新プログラム** ] ダイアログボックスを使用してコンポーネントをアンインストールできなくなります。  
  
2. VSIX マニフェストを含むプロジェクトごとに、ビルドタスクを編集して、MSI がインストールされる場所にコンテンツを出力します。 VSIX マニフェストをビルド出力に含めますが、.vsix ファイルはビルドしません。  
  
## <a name="creating-an-msi-for-your-shell"></a>シェルの MSI の作成  
 MSI パッケージをビルドするには、標準のセットアッププロジェクトよりも柔軟性が高いため、 [WINDOWS インストーラー XML ツールセット](https://documentation.help/WiX-Toolset/index.html) を使用することをお勧めします。  
  
 製品の wxs ファイルで、検出ブロックとシェルコンポーネントのレイアウトを設定します。  
  
 次に、ソリューションの .reg ファイルと ApplicationRegistry の両方にレジストリエントリを作成します。  
  
### <a name="detection-blocks"></a>検出ブロック  
 検出ブロックは、 `Property` 検出する前提条件を指定する要素と、 `Condition` 前提条件がコンピューターに存在しない場合に返されるメッセージを指定する要素で構成されます。 たとえば、シェルアプリケーションには Microsoft Visual Studio シェル再頒布可能パッケージが必要であり、検出ブロックは次のマークアップに似ています。  
  
```xml  
<Property Id="ISOSHELLSFX">  
  <RegistrySearch Id="IsoShellSfx" Root="HKLM" Key="Software\Microsoft\DevDiv\vs\Servicing\\$(var.ShellVersion)\IsoShell\$(var.ProductLanguage)" Name="Install" Type="raw" />  
</Property>  
<Property Id="INTSHELLSFX">  
  <RegistrySearch Id="IntShellSfx" Root="HKLM" Key="SOFTWARE\Microsoft\DevDiv\vs\Servicing\$(var.ShellVersion)\devenv\$(var.ProductLanguage)" Name="Install" Type="raw" />  
</Property>  
  
<Condition Message="This application requires $(var.IsoShellName).  Please install $(var.IsoShellName) then run this installer again.">  
  <![CDATA[Installed OR ISOSHELLSFX]]>  
</Condition>  
<Condition Message="This application requires $(var.IntShellName).  Please install $(var.IntShellName) then run this installer again.">  
  <![CDATA[Installed OR INTSHELLSFX]]>  
</Condition>  
  
```  
  
### <a name="layout-of-shell-components"></a>シェルコンポーネントのレイアウト  
 ターゲットディレクトリの構造とインストールするコンポーネントを識別するために、要素を追加する必要があります。  
  
##### <a name="to-set-the-layout-of-shell-components"></a>シェルコンポーネントのレイアウトを設定するには  
  
1. `Directory`次の例に示すように、ターゲットコンピューター上のファイルシステムに作成するすべてのディレクトリを表す要素の階層を作成します。  
  
    ```xml  
    <Directory Id="TARGETDIR" Name="SourceDir">  
      <Directory Id="ProgramFilesFolder">  
        <Directory Id="CompanyDirectory" Name="$(var.CompanyName)">  
          <Directory Id="INSTALLDIR" Name="$(var.FullProductName)">  
            <Directory Id="ExtensionsFolder" Name="Extensions" />  
            <Directory Id="Folder1033" Name="1033" />  
          </Directory>  
        </Directory>  
      </Directory>  
      <Directory Id="ProgramMenuFolder">  
        <Directory Id="ApplicationProgramsFolder" Name="$(var.FullProductName)"/>  
      </Directory>  
    </Directory>  
    ```  
  
     これらのディレクトリは、インストールする必要があるファイルが指定されているときに、によって参照され `Id` ます。  
  
2. 次の例に示すように、シェルとシェルアプリケーションが必要とするコンポーネントを特定します。  
  
    > [!NOTE]
    > 一部の要素は、他の wxs ファイル内の定義を参照する場合があります。  
  
    ```xml  
    <Feature Id="ProductFeature" Title="$(var.ShortProductName)Shell" Level="1">  
      <ComponentGroupRef Id="ApplicationGroup" />  
      <ComponentGroupRef Id="HelpAboutPackage" />  
      <ComponentRef Id="GeneralProfile" />  
      <ComponentGroupRef Id="EditorAdornment"/>        
      <ComponentGroupRef Id="SlideShowDesignerGroup"/>  
  
      <!-- Note: The following ComponentGroupRef is required to pull in generated authoring from project references. -->  
      <ComponentGroupRef Id="Product.Generated" />  
    </Feature>  
    ```  
  
    1. 要素は、 `ComponentRef` 現在のコンポーネントが必要とするファイルを識別する別の wxs ファイルを参照しています。 たとえば、[全般] プロファイルには、HelpAbout. wxs の次の定義があります。  
  
        ```xml  
        <Fragment Id="FragmentProfiles">  
          <DirectoryRef Id="INSTALLDIR">  
            <Directory Id="ProfilesFolder" Name="Profiles">  
              <Component Id='GeneralProfile' Guid='*'>  
                <File Id='GeneralProfile' Name='General.vssettings' DiskId='1' Source='$(var.BuildOutputDir)Profiles\General.vssettings' KeyPath='yes' />  
              </Component>  
            </Directory>  
          </DirectoryRef>  
        </Fragment>  
        ```  
  
         要素は、 `DirectoryRef` ユーザーのコンピューター上でのファイルの移動先を指定します。 要素は、 `Directory` サブディレクトリにインストールされることを指定します。各要素は、ビルドされた `File` ファイル、またはソリューションの一部として存在するファイルを表し、MSI ファイルの作成時にそのファイルがどこで検出されるかを識別します。  
  
    2. 要素は、 `ComponentGroupRef` 他のコンポーネント (またはコンポーネントおよびコンポーネントグループ) のグループを参照します。 たとえば、 `ComponentGroupRef` ApplicationGroup の下には、次のようにアプリケーションが定義されています。  
  
        ```xml  
        <ComponentGroup Id="ApplicationGroup">  
          <ComponentGroupRef Id="DebuggerProxy" />  
          <ComponentRef Id="MasterPkgDef" />  
          <ComponentRef Id="SplashResource" />  
          <ComponentRef Id="IconResource" />  
          <ComponentRef Id="WinPrfResource" />  
          <ComponentRef Id="AppExe" />  
          <ComponentRef Id="AppConfig" />  
          <ComponentRef Id="AppPkgDef" />  
          <ComponentRef Id="AppPkgDefUndef" />  
          <ComponentRef Id="$(var.ShortProductName)UI1033" />  
          <ComponentRef Id="ApplicationShortcut"/>  
          <ComponentRef Id="ApplicationRegistry"/>  
        </ComponentGroup>  
        ```  
  
    > [!NOTE]
    > シェル (分離) アプリケーションに必要な依存関係は、デバッガプロキシ、MasterPkgDef、Resources (特に winprf ファイル)、Application、および PkgDefs です。  
  
### <a name="registry-entries"></a>レジストリ エントリ  
 Shell (分離) プロジェクトテンプレートには、インストール時にマージするレジストリキーの *ProjectName*ファイルが含まれています。 これらのレジストリエントリは、インストールとクリーンアップの両方の目的で MSI の一部である必要があります。 また、ApplicationRegistry で一致するレジストリブロックを作成する必要があります。  
  
##### <a name="to-integrate-registry-entries-into-the-msi"></a>レジストリエントリを MSI に統合するには  
  
1. [ **シェルのカスタマイズ** ] フォルダーで、 *ProjectName*. reg を開きます。  
  
2. $RootFolder $ token のすべてのインスタンスを、ターゲットのインストールディレクトリのパスに置き換えます。  
  
3. アプリケーションで必要なその他のレジストリエントリを追加します。  
  
4. ApplicationRegistry を開きます。  
  
5. 次の例に示すように、 *ProjectName*の各レジストリエントリに、対応するレジストリブロックを追加します。  
  
    |*ProjectName*. reg|ApplicationRegisty。 wxs|  
    |-----------------------|----------------------------|  
    |[HKEY_CLASSES_ROOT/CLSID \\{bb431796-a179-4df7-b65d-c0df6bda7cc6}]<br /><br /> @ = "PhotoStudio DTE オブジェクト"|\<RegistryKey Id='DteClsidRegKey' Root='HKCR' Key='$(var.DteClsidRegKey)' Action='createAndRemoveOnUninstall'><br /><br /> \<RegistryValue Type='string' Name='@' Value='$(var.ShortProductName) DTE Object' /><br /><br /> \</RegistryKey>|  
    |[HKEY_CLASSES_ROOT/CLSID \\{bb431796-a179-4df7-b65d-c0df6bda7cc6} \ localserver32]<br /><br /> @ = "$RootFolder $\PhotoStudio.exe"|\<RegistryKey Id='DteLocSrv32RegKey' Root='HKCR' Key='$(var.DteClsidRegKey)\LocalServer32' Action='createAndRemoveOnUninstall'><br /><br /> \<RegistryValue Type='string' Name='@' Value='[INSTALLDIR]$(var.ShortProductName).exe' /><br /><br /> \</RegistryKey>|  
  
     この例では、Var. DteClsidRegKey は先頭行のレジストリキーに解決されます。 Var. 短縮 Productname は、に解決さ `PhotoStudio` れます。  
  
## <a name="creating-a-setup-bootstrapper"></a>セットアップブートストラップの作成  
 完成した MSI は、すべての前提条件が最初にインストールされた場合にのみインストールされます。 エンドユーザーエクスペリエンスを簡単にするために、アプリケーションをインストールする前にすべての前提条件を収集してインストールするセットアッププログラムを作成します。 正常にインストールされるようにするには、次の操作を実行します。  
  
- 管理者によるインストールを強制します。  
  
- Visual Studio Shell (分離) がインストールされているかどうかを検出します。  
  
- 1つまたは両方のシェルインストーラーを順番に実行します。  
  
- 再起動要求を処理します。  
  
- MSI を実行します。  
  
### <a name="enforcing-installation-by-administrator"></a>管理者によるインストールの実施  
 この手順は、セットアッププログラムが、ファイルなどの必要なディレクトリにアクセスできるようにするために必要です \\ 。  
  
##### <a name="to-enforce-installation-by-administrator"></a>管理者によるインストールを強制するには  
  
1. セットアッププロジェクトのショートカットメニューを開き、[ **プロパティ**] を選択します。  
  
2. [ **構成プロパティ**]、[リンカー]、[マニフェストファイル] の下で、 **UAC 実行レベル** を **requireAdministrator**に設定します。  
  
     このプロパティは、プログラムを管理者として実行する必要がある属性を埋め込みマニフェストファイルに配置します。  
  
### <a name="detecting-shell-installations"></a>シェルインストールの検出  
 Visual Studio Shell (分離) をインストールする必要があるかどうかを判断するには、まず、HKLM\Software\Microsoft\DevDiv\vs\Servicing\ShellVersion\isoshell\LCID\Install. のレジストリ値を確認して、インストールされているかどうかを確認します。  
  
> [!NOTE]
> これらの値も、シェル検出ブロックによって読み取られます。  
  
 HKLM\Software\Microsoft\AppEnv\14.0\ShellFolder Visual Studio シェルがインストールされている場所を指定します。ファイルを確認することもできます。  
  
 シェルのインストールを検出する方法の例については、 `GetProductDirFromReg` シェル展開サンプルの「ユーティリティの機能」を参照してください。  
  
 パッケージに必要な Visual Studio シェルの1つまたは両方がコンピューターにインストールされていない場合は、インストールするコンポーネントの一覧に追加する必要があります。 例については、 `ComponentsPage::OnInitDialog` シェルデプロイサンプルの ComponentsPage の関数を参照してください。  
  
### <a name="running-the-shell-installers"></a>シェルインストーラーの実行  
 シェルインストーラーを実行するには、正しいコマンドライン引数を使用して Visual Studio シェル再頒布可能パッケージを呼び出します。 少なくとも、コマンドライン引数 **/norestart/q** を使用して、次に何を行う必要があるかを判断するためにリターンコードを監視する必要があります。 次の例では、シェル (分離) 再頒布可能パッケージを実行します。  
  
```  
dwResult = ExecCmd("Vs_IsoShell.exe /norestart /q", TRUE);  
```  
  
### <a name="running-the-shell-language-pack-installers"></a>シェル言語パックインストーラーの実行  
 シェルまたはシェルがインストールされていて、言語パックが必要な場合は、次の例に示すように言語パックをインストールできます。  
  
```  
dwResult = ExecCmd("Vs_IsoShellLP.exe /norestart /q", TRUE);  
  
```  
  
### <a name="deciphering-return-values"></a>戻り値の解読  
 一部のオペレーティングシステムでは、Visual Studio Shell (分離) インストールに再起動が必要です。 この条件は、の呼び出しのリターンコードによって決定でき `ExecCmd` ます。  
  
|戻り値|説明|  
|------------------|-----------------|  
|ERROR_SUCCESS|インストールが完了しました。 これで、アプリケーションをインストールできるようになりました。|  
|ERROR_SUCCESS_REBOOT_REQUIRED|インストールが完了しました。 コンピューターを再起動した後で、アプリケーションをインストールできます。|  
|3015|インストールが進行中です。 インストールを続行するには、コンピューターを再起動する必要があります。|  
  
### <a name="handling-restarts"></a>再起動の処理  
 **/Norestart**引数を使用してシェルインストーラーを実行したときに、コンピューターを再起動しないように指定した場合、またはコンピューターの再起動を要求した場合。 ただし、再起動が必要になる場合があります。コンピューターを再起動した後も、インストーラーが続行されるようにする必要があります。  
  
 再起動を正しく処理するには、1つのセットアッププログラムだけを再開するように設定し、再開プロセスは正しく処理されるようにします。  
  
 ERROR_SUCCESS_REBOOT_REQUIRED または3015が返された場合は、インストールが続行される前に、コードでコンピューターを再起動する必要があります。  
  
 再起動を処理するには、次の操作を実行します。  
  
- Windows の起動時にインストールを再開するようにレジストリを設定します。  
  
- ブートストラップのダブル再起動を実行します。  
  
- シェルインストーラー ResumeData キーを削除します。  
  
- Windows を再起動します。  
  
- MSI の開始パスをリセットします。  
  
### <a name="setting-the-registry-to-resume-setup-when-windows-starts"></a>Windows の起動時にセットアップを再開するようにレジストリを設定する  
 HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce\ レジストリキーは、システムの起動時に管理者権限で実行され、消去されます。 HKEY_CURRENT_USER には同様のキーが含まれていますが、通常のユーザーとして実行され、インストールには適していません。 インストーラーを呼び出す RunOnce キーに文字列値を指定することで、インストールを再開できます。 ただし、 **/restart」** または同様のパラメーターを使用してインストーラーを呼び出すことをお勧めします。これにより、開始時ではなく再開することがアプリケーションに通知されます。 また、インストールプロセス内の場所を示すパラメーターを含めることもできます。これは、複数の再起動が必要になる可能性があるインストールで特に便利です。  
  
 次の例は、インストールを再開するための RunOnce レジストリキー値を示しています。  
  
 `"c:\MyAppInstaller.exe /restart /SomeOtherDataFlag"`  
  
### <a name="installing-double-restart-of-bootstrapper"></a>ブートストラップのダブル再起動のインストール  
 セットアップを RunOnce から直接使用すると、デスクトップを完全に読み込むことができなくなります。 完全なユーザーインターフェイスを使用できるようにするには、セットアップの別の実行を作成して、RunOnce インスタンスを終了する必要があります。  
  
 次の例に示すように、適切なアクセス許可を取得するようにセットアッププログラムを再実行する必要があります。また、再起動の前に停止した場所を知るために十分な情報を指定する必要があります。  
  
```  
if (_cmdLineInfo.IsRestart())  
{  
    TCHAR path[MAX_PATH]={0};  
    GetModuleFileName(NULL, path, MAX_PATH * sizeof(TCHAR));      
    ShellExecute( NULL, _T( "open" ), path, _T("/install"), 0, SW_SHOWNORMAL );  
}  
  
```  
  
### <a name="deleting-the-shell-installer-resumedata-key"></a>シェルインストーラー ResumeData キーを削除しています  
 シェルインストーラーは、再起動後にセットアップを再開するために、HKLM\Software\Microsoft\VisualStudio\14.0\Setup\ResumeData レジストリキーにデータを設定します。 シェルインストーラーではなくアプリケーションが再開されているため、次の例に示すように、そのレジストリキーを削除します。  
  
```  
CString resumeSetupPath(MAKEINTRESOURCE("SOFTWARE\\Microsoft\\VisualStudio\\14.0\\Setup\\ResumeData"));  
RegDeleteKey(HKEY_LOCAL_MACHINE, resumeSetupPath);  
```  
  
### <a name="restarting-windows"></a>Windows の再起動  
 必要なレジストリキーを設定したら、Windows を再起動することができます。 次の例では、さまざまな Windows オペレーティングシステムの再起動コマンドを呼び出します。  
  
```  
OSVERSIONINFO ov;  
HANDLE htoken ;  
//Ask for the SE_SHUTDOWN_NAME token as this is needed by the thread calling for a system shutdown.  
if (OpenProcessToken(GetCurrentProcess(), TOKEN_ADJUST_PRIVILEGES | TOKEN_QUERY, &htoken))  
{  
    LUID luid ;  
    LookupPrivilegeValue(NULL, SE_SHUTDOWN_NAME, &luid) ;  
    TOKEN_PRIVILEGES    privs ;  
    privs.Privileges[0].Luid = luid ;  
    privs.PrivilegeCount = 1 ;  
    privs.Privileges[0].Attributes = SE_PRIVILEGE_ENABLED ;  
    AdjustTokenPrivileges(htoken, FALSE, &privs, 0, (PTOKEN_PRIVILEGES) NULL, 0) ;  
}   
  
//Use InitiateSystemShutdownEx to avoid unexpected restart message box  
try  
{              
    if ( (ov.dwMajorVersion > 5) || ( (ov.dwMajorVersion == 5) && (ov.dwMinorVersion  > 0) ))  
    {  
        bExitWindows = InitiateSystemShutdownEx(0, _T(""), 0, TRUE, TRUE, REASON_PLANNED_FLAG);  
    }  
    else  
    {  
#pragma prefast(suppress:380,"ignore warning about legacy api")  
        bExitWindows = InitiateSystemShutdown(0, _T(""), 0, TRUE, TRUE);  
    }  
}  
catch(...)  
{  
    //advapi32.dll call not available! Will not restart!  
}  
  
```  
  
### <a name="resetting-the-start-path-of-msi"></a>MSI の開始パスをリセットしています  
 再起動する前に、現在のディレクトリはセットアッププログラムの場所ですが、再起動後に、その場所は system32 ディレクトリになります。 次の例に示すように、セットアッププログラムによって、各 MSI 呼び出しの前に現在のディレクトリがリセットされます。  
  
```  
CString GetSetupPath()  
{  
    TCHAR file[MAX_PATH];  
    GetModuleFileName(NULL, file, MAX_PATH * sizeof(TCHAR));  
    CString path(file);  
    int fpos = path.ReverseFind('\\');  
    if (fpos != -1)  
    {  
        path = path.Left(fpos + 1);  
    }  
  
    return path;  
}  
  
```  
  
### <a name="running-the-application-msi"></a>アプリケーション MSI の実行  
 Visual Studio シェルインストーラーによって ERROR_SUCCESS が返されたら、アプリケーションの MSI を実行できます。 セットアッププログラムはユーザーインターフェイスを提供しているため、次の例に示すように、quiet モード (**/q**) とログ記録 (**/L**) で MSI を起動します。  
  
```cpp#  
TCHAR temp[MAX_PATH];  
GetTempPath(MAX_PATH, temp);  
  
CString boutiqueInstallCmd, msi, log;  
CString cmdLine(MAKEINTRESOURCE("msiexec /q /I %s /L*vx %s REBOOT=ReallySuppress"));  
CString name(MAKEINTRESOURCE("PhotoStudioIntShell.msi"));  
log.Format(_T("\"%s%s.log\""), temp, name);  
msi.Format(_T("\"%s%s\""), GetSetupPath(), name);  
boutiqueInstallCmd.Format(cmdLine, msi, log);  
  
//TODO: You can use MSI API to gather and present install progress feedback from your MSI.  
dwResult = ExecCmd(boutiqueInstallCmd, FALSE);  
```  
  
## <a name="see-also"></a>参照  
 [チュートリアル: 基本的な分離シェル アプリケーションを作成する](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)

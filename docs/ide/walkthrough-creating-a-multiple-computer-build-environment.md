---
title: 'チュートリアル: 複数のコンピューターを使用するビルド環境の作成'
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, building on multiple computers
- build environment, MSBuild
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 11b158854a0026de28cb2fb0a582bbaf764eeaa4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68461534"
---
# <a name="walkthrough-create-a-multiple-computer-build-environment"></a>チュートリアル: 複数のコンピューターを使用するビルド環境の作成

組織内でビルド環境を作成するには、ホスト コンピューターに Visual Studio をインストールし、ビルドに参加できるように各種のファイルおよび設定を別のコンピューターにコピーします。 別コンピューターの方に Visual Studio をインストールする必要はありません。

このドキュメントは、ソフトウェアを外部に再配布する権利または第三者にビルド環境を提供する権利を付与するものではありません。

> 免責情報<br /><br /> このドキュメントは "現状有姿" で提供されます。 ここに記載されている手順はテスト済みですが、あらゆる構成を網羅してテストすることはできません。 Microsoft では、追加情報があればこのドキュメントを更新するように努めます。 URL および他の参照されているインターネットの Web サイトをはじめ、このドキュメントに記載されている情報および見解は、通知なく変更されることがあります。 Microsoft はここに示されている情報について、明示か黙示かを問わず、一切保証しません。 お客様は、その使用に関するリスクを負うものとします。<br /><br /> このドキュメントは、Microsoft 製品の知的財産権に関する法的な権利をお客様に許諾するものではありません。 内部的な参照目的に限り、このドキュメントを複製して使用することができます。<br /><br /> お客様がこのドキュメントに関する提案、コメント、またはその他のフィードバック (以下 "フィードバック") を Microsoft に提供する義務はありません。 ただし、お客様から自発的に提供されたフィードバックは、Microsoft 製品および関連する仕様書またはその他のドキュメント (以下総称して "Microsoft 提供物") に使用されることがあります。さらに、これらのドキュメントは第三者によって独自製品の開発時に使用されることがあります。 これに基づき、お客様がこのドキュメントまたは Microsoft 提供物のいずれかのバージョンに関するフィードバックを Microsoft に提供する場合、お客様は次の点に同意するものとします。(a) Microsoft は、Microsoft 提供物の中で、お客様のフィードバックを自由に複製、使用許諾、配布、およびその他の方法で商品化できる。(b) 第三者の製品において、お客様のフィードバックを反映した Microsoft 製品の特定部分を使用または Microsoft 製品の特定部分と連携するために必要な特許権のみをお客様が無償で第三者に付与する。(c) 次のような場合、お客様はフィードバックを Microsoft に提供しない。(i) 第三者の特許、著作権、またはその他の知的財産権の主張または権限がそのフィードバックに適用されるとお客様が確信する根拠がある場合、または (ii) そのフィードバックが反映されているかそのフィードバックから派生する Microsoft 提供物またはその他の Microsoft 知的財産を第三者に使用許諾またはその他の方法で共有することを求めるライセンス条件がそのフィードバックに適用される場合。

このチュートリアルは、次のオペレーティング システムに対して検証済みです。

- Windows 8 (x86 および x64)
- Windows 7 Ultimate
- Windows Server 2008 R2 Standard

このチュートリアルの手順を完了すると、複数コンピューター環境を使用して、次の種類のアプリをビルドできます。

- Windows 8 SDK を使用する C++ デスクトップ アプリ
- .NET Framework 4.5 を対象とする Visual Basic または C# のデスクトップ アプリ

次の種類のアプリのビルドには、複数コンピューター環境を使用できません。

- UWP アプリ。 UWP アプリをビルドするには、ビルド コンピューターに Visual Studio をインストールする必要があります。
- .NET Framework 4 以前を対象とするデスクトップ アプリ。 これらの種類のアプリをビルドするには、ビルド コンピューターに Visual Studio または .NET 参照アセンブリおよびツール (Windows 7.1 SDK に含まれます) をインストールする必要があります。

## <a name="prerequisites"></a>必須コンポーネント

**.NET デスクトップ開発**ワークロードがインストールされた Visual Studio。

## <a name="install-software-on-the-computers"></a>コンピューターにソフトウェアをインストールする

最初にホスト コンピューターを設定し、次にビルド コンピューターを設定します。

ホスト コンピューターに Visual Studio をインストールすると、ファイルや設定が作成されます。後でこれらをビルド コンピューターにコピーします。 Visual Studio は x86 または x64 コンピューターにインストールできますが、ビルド コンピューターのアーキテクチャは、ホスト コンピューターのアーキテクチャと一致する必要があります。

1. ホスト コンピューターに、Visual Studio をインストールします。

2. ビルド コンピューターに、.NET Framework 4.5 以降をインストールします。 インストールされていることを確認するには、レジストリ サブキー **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full** の **[バージョン]** エントリが **4.5** 以上の値であることを確認します。

## <a name="copy-files-from-the-host-computer-to-the-build-computer"></a>ホスト コンピューターからビルド コンピューターにファイルをコピーする

このセクションでは、特定のファイル、コンパイラ、ビルド ツール、MSBuild の資産、およびレジストリ設定をホスト コンピューターからビルド コンピューターにコピーする操作ついて説明します。 ここに示す手順では、Visual Studio がホスト コンピューターの既定の場所にインストールされていることを想定しています。別の場所にインストールした場合は、手順を適宜調整してください。

- x86 コンピューターの既定の場所は *C:\Program Files\Microsoft Visual Studio* です
- x64 コンピューターの既定の場所は *C:\Program Files (x86)\Microsoft Visual Studio* です

*Program Files* フォルダーの名前が、インストールされているオペレーティング システムによって異なる点に注意してください。 x86 コンピューターでは *Program Files*、x64 コンピューターでは *Program Files (x86)* です。 システムのアーキテクチャに関係なく、このチュートリアルでは、*Program Files* フォルダーを *%ProgramFiles%* と示します。

> [!NOTE]
> ビルド コンピューターでは、関連するファイルをすべて同じドライブに配置する必要があります。 ただし、そのドライブのドライブ文字は、Visual Studio がホスト コンピューターにインストールされているドライブのドライブ文字と異なってもかまいません。 いずれにしても、後でこのドキュメント内で説明するように、レジストリ エントリの作成時にファイルの場所の情報が必要になります。

### <a name="copy-the-windows-sdk-files-to-the-build-computer"></a>Windows SDK ファイルをビルド コンピューターにコピーする

1. Windows SDK for Windows 8 のみがインストールされている場合は、次に示すフォルダーを再帰的にホスト コンピューターからビルド コンピューターにコピーします。

   - %ProgramFiles%\Windows Kits\8.0\bin\

   - %ProgramFiles%\Windows Kits\8.0\Catalogs\

   - %ProgramFiles%\Windows Kits\8.0\DesignTime\

   - %ProgramFiles%\Windows Kits\8.0\include\

   - %ProgramFiles%\Windows Kits\8.0\Lib\

   - %ProgramFiles%\Windows Kits\8.0\Redist\

   - %ProgramFiles%\Windows Kits\8.0\References\

   次に示す他の Windows 8 キットもインストールされている場合:

   - Microsoft Windows アセスメント & デプロイメント キット

   - Microsoft Windows Driver Kit

   - Microsoft Windows ハードウェア認定キット

   これらもインストールされている場合、前の手順で示した *%ProgramFiles%\Windows Kits\8.0* フォルダーにファイルがインストールされている可能性があります。また、ライセンス条項によっては、ビルド サーバーでこれらのファイルへのアクセスが許可されない可能性があります。 インストールされているすべての Windows キットについてライセンス条項を調べて、ファイルをビルド コンピューターにコピーできるかどうかを確認します。 ライセンス条項によってビルド サーバーでのアクセスが許可されていない場合は、該当するファイルをビルド コンピューターから削除します。

2. ホスト コンピューターからビルド コンピューターに、次のフォルダーを再帰的にコピーします。

    - %ProgramFiles%\Microsoft SDKs\Windows\v8.0A\bin\NETFX 4.0 Tools\

    - %ProgramFiles%\Common Files\Merge Modules\

    - %ProgramFiles%\Microsoft Visual Studio\\\<version>\\\<edition>\VC\

    - %ProgramFiles%\Microsoft Visual Studio\\\<version>\\\<edition>\Common7\Tools\ProjectComponents\

    - %ProgramFiles%\MSBuild\Microsoft.Cpp\v4.0\v110\

    - %ProgramFiles%\Reference Assemblies\Microsoft\Framework\\.NETCore\v4.5\

    - %ProgramFiles%\Reference Assemblies\Microsoft\Framework\\.NETFramework\v4.5\

3. ホスト コンピューターからビルド コンピューターに、次のファイルをコピーします。

    - %ProgramFiles%\Microsoft Visual Studio\\\<version>\\\<edition>\Common7\IDE\msobj110.dll

    - %ProgramFiles%\Microsoft Visual Studio\\\<version>\\\<edition>\Common7\IDE\mspdb110.dll

    - %ProgramFiles%\Microsoft Visual Studio\\\<version>\\\<edition>\Common7\IDE\mspdbcore.dll

    - %ProgramFiles%\Microsoft Visual Studio\\\<version>\\\<edition>\Common7\IDE\mspdbsrv.exe

    - %ProgramFiles%\Microsoft Visual Studio\\\<version>\\\<edition>\Common7\IDE\msvcdis110.dll

    - %ProgramFiles%\Microsoft Visual Studio\\\<version>\\\<edition>\Common7\Tools\makehm.exe

    - %ProgramFiles%\Microsoft Visual Studio\\\<version>\\\<edition>\Common7\Tools\VCVarsQueryRegistry.bat

    - %ProgramFiles%\Microsoft Visual Studio\\\<version>\\\<edition>\Common7\Tools\vsvars32.bat

4. 次に示す Visual C++ ランタイム ライブラリは、ビルド コンピューターで (たとえば自動テストの一部として) ビルド出力を実行する場合にのみ必要です。 これらのファイルは通常、システムのアーキテクチャに応じて *%ProgramFiles%\Microsoft Visual Studio\\\<version>\\\<edition>\VC\redist\x86* または *%ProgramFiles%\Microsoft Visual Studio\\\<version>\\\<edition>\VC\redist\x64* フォルダー内のサブフォルダーに配置されます。 x86 システムの場合は、x86 バイナリを *Windows\System32* フォルダーにコピーします。 x64 システムでは、x86 バイナリを *Windows\SysWOW64* フォルダーに、x64 バイナリを *Windows\System32* フォルダーにコピーします。

    - \Microsoft.VC110.ATL\atl110.dll

    - \Microsoft.VC110.CRT\msvcp110.dll

    - \Microsoft.VC110.CRT\msvcr110.dll

    - \Microsoft.VC110.CXXAMP\vcamp110.dll

    - \Microsoft.VC110.MFC\mfc110.dll

    - \Microsoft.VC110.MFC\mfc110u.dll

    - \Microsoft.VC110.MFC\mfcm110.dll

    - \Microsoft.VC110.MFC\mfcm110u.dll

    - \Microsoft.VC110.MFCLOC\mfc110chs.dll

    - \Microsoft.VC110.MFCLOC\mfc110cht.dll

    - \Microsoft.VC110.MFCLOC\mfc110deu.dll

    - \Microsoft.VC110.MFCLOC\mfc110enu.dll

    - \Microsoft.VC110.MFCLOC\mfc110esn.dll

    - \Microsoft.VC110.MFCLOC\mfc110fra.dll

    - \Microsoft.VC110.MFCLOC\mfc110ita.dll

    - \Microsoft.VC110.MFCLOC\mfc110jpn.dll

    - \Microsoft.VC110.MFCLOC\mfc110kor.dll

    - \Microsoft.VC110.MFCLOC\mfc110rus.dll

    - \Microsoft.VC110.OPENMP\vcomp110.dll

5. 「[デバッグの実行可能ファイルを実行するテスト用コンピューターの準備](/cpp/windows/preparing-a-test-machine-to-run-a-debug-executable)」の説明に従って、*Debug_NonRedist\x86* フォルダーまたは *Debug_NonRedist\x64* フォルダーから次のファイルのみをビルド コンピューターにコピーします。 他のファイルはコピーしないでください。

    - \Microsoft.VC110.DebugCRT\msvcp110d.dll

    - \Microsoft.VC110.DebugCRT\msvcr110d.dll

    - \Microsoft.VC110.DebugCXXAMP\vcamp110d.dll

    - \Microsoft.VC110.DebugMFC\mfc110d.dll

    - \Microsoft.VC110.DebugMFC\mfc110ud.dll

    - \Microsoft.VC110.DebugMFC\mfcm110d.dll

    - \Microsoft.VC110.DebugMFC\mfcm110ud.dll

    - \Microsoft.VC110.DebugOpenMP\vcomp110d.dll

## <a name="create-registry-settings"></a>レジストリ設定を作成する

MSBuild 用の設定を構成するには、レジストリ エントリを作成する必要があります。

1. レジストリ エントリの親フォルダーを特定します。 レジストリ エントリはすべて、同じ親キーの下に作成します。 x86 コンピューターの場合、親キーは **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft** です。 x64 コンピューターの場合、親キーは **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft** です。 システムのアーキテクチャに関係なく、このチュートリアルでは、親キーを %RegistryRoot% と示します。

    > [!NOTE]
    > ホスト コンピューターのアーキテクチャがビルド コンピューターと異なる場合は、各コンピューターで適切な親キーを使用してください。 このことは、エクスポート プロセスを自動化する場合に特に重要です。
    >
    > また、ホスト コンピューターで使用しているものと異なるドライブ文字をビルド コンピューターで使用する場合は、レジストリ エントリの値が一致するように必ず変更してください。

2. 次のレジストリ エントリをビルド コンピューターに作成します。 これらのエントリはすべて、文字列 (レジストリでの種類は "REG_SZ") です。 これらのエントリの値が、ホスト コンピューターの該当するエントリの値と同じになるように設定します。

   - **%RegistryRoot%\\.NETFramework\v4.0.30319\AssemblyFoldersEx\VCMSBuild Public Assemblies@(Default)**

   - <strong>%RegistryRoot%\Microsoft SDKs\Windows\v8.0@InstallationFolder</strong>

   - <strong>%RegistryRoot%\Microsoft SDKs\Windows\v8.0A@InstallationFolder</strong>

   - <strong>%RegistryRoot%\Microsoft SDKs\Windows\v8.0A\WinSDK-NetFx40Tools@InstallationFolder</strong>

   - <strong>%RegistryRoot%\Microsoft SDKs\Windows\v8.0A\WinSDK-NetFx40Tools-x86@InstallationFolder</strong>

   - **%RegistryRoot%\VisualStudio\11.0@Source ディレクトリ**

   - <strong>%RegistryRoot%\VisualStudio\11.0\Setup\VC@ProductDir</strong>

   - <strong>%RegistryRoot%\VisualStudio\SxS\VC7@FrameworkDir32</strong>

   - <strong>%RegistryRoot%\VisualStudio\SxS\VC7@FrameworkDir64</strong>

   - <strong>%RegistryRoot%\VisualStudio\SxS\VC7@FrameworkVer32</strong>

   - <strong>%RegistryRoot%\VisualStudio\SxS\VC7@FrameworkVer64</strong>

   - **%RegistryRoot%\VisualStudio\SxS\VC7@11.0**

   - **%RegistryRoot%\VisualStudio\SxS\VS7@11.0**

   - <strong>%RegistryRoot%\Windows Kits\Installed Roots@KitsRoot</strong>

   - <strong>%RegistryRoot%\MSBuild\ToolsVersions\4.0\11.0@VCTargetsPath</strong>

   - <strong>%RegistryRoot%\MSBuild\ToolsVersions\4.0\11.0@VCTargetsPath10</strong>

   - <strong>%RegistryRoot%\MSBuild\ToolsVersions\4.0\11.0@VCTargetsPath11</strong>

   x64 ビルド コンピューターでは、次のレジストリ エントリも作成し、ホスト コンピューターを参照して設定方法を決定します。

   - <strong>%RegistryRoot%\Microsoft SDKs\Windows\v8.0A\WinSDK-NetFx40Tools-x64@InstallationFolder</strong>

   ビルド コンピューターが x64 であり MSBuild の 64 ビット バージョンを使用する場合または x64 コンピューターで Team Foundation Server ビルド サービスを使用している場合は、ネイティブの 64 ビット レジストリに次のレジストリ エントリを作成します。 これらのエントリの設定方法を決定するには、ホスト コンピューターを参照してください。

   - <strong>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\11.0\Setup\VS@ProductDir</strong>

   - <strong>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSBuild\ToolsVersions\4.0\11.0@VCTargetsPath</strong>

   - <strong>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSBuild\ToolsVersions\4.0\11.0@VCTargetsPath10</strong>

   - <strong>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSBuild\ToolsVersions\4.0\11.0@VCTargetsPath11</strong>

## <a name="set-environment-variables-on-the-build-computer"></a>ビルド コンピューターで環境変数を設定する

ビルド コンピューターで MSBuild を使用するには、PATH 環境変数を設定する必要があります。 *vcvarsall.bat* を使用して変数を設定することも、手動で構成することもできます。

### <a name="use-vcvarsallbat-to-set-environment-variables"></a>vcvarsall.bat を使用して環境変数を設定する

ビルド コンピューターで**コマンド プロンプト** ウィンドウを開き、 *%Program Files%\Microsoft Visual Studio\\\<version>\\\<edition>\VC\vcvarsall.bat* を実行します。 使用するツールセット (x86、ネイティブ x64、x64 クロス コンパイラ) を指定するには、コマンド ライン引数を使用します。 コマンド ライン引数を指定しなかった場合は、x86 のツールセットが使用されます。

次の表では、*vcvarsall.bat* でサポートされている引数を説明しています。

|vcvarsall.bat 引数|コンパイラ|ビルド コンピューターのアーキテクチャ|ビルド出力のアーキテクチャ|
| - |--------------| - | - |
|x86 (既定)|32 ビット ネイティブ|x86、x64|x86|
|x86_amd64|x64 クロス|x86、x64|X64|
|amd64|x64 ネイティブ|X64|X64|

*vcvarsall.bat* が正常に実行された (エラー メッセージが表示されない) 場合は、次の手順をスキップして、このドキュメントの「[ビルド コンピューターのグローバル アセンブリ キャッシュ (GAC) に MSBuild アセンブリをインストールする](#install-msbuild-to-gac)」に進むことができます。

### <a name="manually-set-environment-variables"></a>手動で環境変数を設定する

1. 手動でコマンド ライン環境を構成するには、次のパスを PATH 環境変数に追加します。

    - %Program Files%\Microsoft Visual Studio\\\<version>\\\<edition>\Common7\IDE

2. 必要に応じて、ソリューションのビルド時に MSBuild を使用しやすくなるように、次のパスも PATH 環境変数に追加することができます。

   ネイティブ 32 ビットの MSBuild を使用する場合は、次のパスを PATH 変数に追加します。

   - %Program Files%\Microsoft SDKs\Windows\v8.0A\bin\NETFX 4.0 Tools

   - %windir%\Microsoft.NET\Framework\v4.0.30319

   ネイティブ 64 ビットの MSBuild を使用する場合は、次のパスを PATH 変数に追加します。

   - %Program Files%\Microsoft SDKs\Windows\v8.0A\bin\NETFX 4.0 Tools\x64

   - %windir%\Microsoft.NET\Framework64\v4.0.30319

## <a name="install-msbuild-assemblies-to-the-global-assembly-cache-gac-on-the-build-computer"></a><a name="install-msbuild-to-gac" /> ビルド コンピューターのグローバル アセンブリ キャッシュ (GAC) に MSBuild アセンブリをインストールする

MSBuild を使用するには、ビルド コンピューターの GAC にいくつかの追加のアセンブリをインストールする必要があります。

1. ホスト コンピューターからビルド コンピューターに次のアセンブリをコピーします。 これらは GAC にインストールされるため、ビルド コンピューター上のコピー先の場所は重要ではありません。

    - %ProgramFiles%\MSBuild\Microsoft.Cpp\v4.0\v110\Microsoft.Build.CPPTasks.Common.v110.dll

    - %ProgramFiles%\Microsoft Visual Studio\\\<version>\\\<edition>\Common7\IDE\CommonExtensions\Microsoft\VC\Project\Microsoft.VisualStudio.Project.VisualC.VCProjectEngine.dll

    - %ProgramFiles%\Microsoft Visual Studio\\\<version>\\\<edition>\Common7\IDE\PublicAssemblies\Microsoft.VisualStudio.VCProjectEngine.dll

2. アセンブリを GAC にインストールするには、ビルド コンピューター上で *gacutil.exe* を探します。一般的には %ProgramFiles%\Microsoft SDKs\Windows\v8.0A\bin\NETFX 4.0 Tools\\ にあります。 このフォルダーが見つからない場合は、このチュートリアルの「[ホスト コンピューターからビルド コンピューターにファイルをコピーする](../ide/walkthrough-creating-a-multiple-computer-build-environment.md#copy-files-from-the-host-computer-to-the-build-computer)」に記載されている手順を繰り返します。

     管理者権限で**コマンド プロンプト** ウィンドウを開き、ファイルごとに次のコマンドを実行します。

     **gacutil -i \<file>**

    > [!NOTE]
    > GAC へのアセンブリのインストールを完了するために、再起動が必要になる場合があります。

## <a name="build-projects"></a>プロジェクトをビルドする

Azure Pipelines を使用して Visual Studio プロジェクトとソリューションをビルドできます。または、コマンド ライン上でビルドすることもできます。 Azure Pipelines を使用してプロジェクトをビルドすると、システムのアーキテクチャに対応する MSBuild 実行可能ファイルが起動されます。 コマンド ラインでは、32 ビット MSBuild または 64 ビット MSBuild を使用できます。MSBuild のアーキテクチャは、PATH 環境変数を設定するか、アーキテクチャ固有の MSBuild 実行可能ファイルを直接呼び出すことによって選択できます。

コマンド プロンプトで *msbuild.exe* を使用するには、次のコマンドを実行します (*solution.sln* は、ソリューションの名前のプレースホルダーです)。

**msbuild** *solution.sln*

コマンド ラインで MSBuild を使用する方法については、[コマンド ライン リファレンス](../msbuild/msbuild-command-line-reference.md)に関するページをご覧ください。

## <a name="create-the-build-environment-so-that-it-can-be-checked-into-source-control"></a>ソース管理にチェックインできるようにビルド環境を作成する

さまざまなコンピューターに配置できる、GAC へのファイルのインストールやレジストリ設定の変更を必要としないビルド環境を作成できます。 次の手順は、これを実現する方法の 1 つです。 ビルド環境ごとの特性に合わせて、手順を調整してください。

> [!NOTE]
> ビルド時に *tracker.exe* によるエラーが発生しないように、インクリメンタル ビルドを無効にする必要があります。 インクリメンタル ビルドを無効にするには、次のビルド パラメーターを設定します。
>
> **msbuild** *solution.sln* **/p:TrackFileAccess=false**

1. ホスト コンピューターに *Depot* ディレクトリを作成します。

     ここに示す手順では、このディレクトリを %Depot% と示します。

2. このチュートリアルの「[ホスト コンピューターからビルド コンピューターにファイルをコピーする](../ide/walkthrough-creating-a-multiple-computer-build-environment.md#copy-files-from-the-host-computer-to-the-build-computer)」の説明に従って、ディレクトリとファイルをコピーします。ただし、コピー先は、先ほど作成した *%Depot%* ディレクトリ内とします。 たとえば、 *%ProgramFiles%\Windows Kits\8.0\bin* からのコピー先は *%Depot%\Windows Kits\8.0\bin* になります。

3. *%Depot%* にファイルを貼り付けたら、次の変更を行います。

    - %Depot%\MSBuild\Microsoft.Cpp\v4.0\v110\Microsoft.CPP.Targets、\Microsoft.Cpp.InvalidPlatforms.targets\\、\Microsoft.cppbuild.targets\\、および \Microsoft.CppCommon.targets\\ で、次のように変更します (すべてのインスタンスを変更します)。

         AssemblyName="Microsoft.Build.CppTasks.Common.v110, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"

         から

         AssemblyFile="$(VCTargetsPath11)Microsoft.Build.CppTasks.Common.v110.dll".

         変更前の名前は、GAC にインストールするアセンブリに依存しています。

    - %Depot% \MSBuild\Microsoft.Cpp\v4.0\v110\Microsoft.CPPClean.Targets で、

         AssemblyName="Microsoft.Build.CppTasks.Common.v110, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"

         から

         AssemblyFile="$(VCTargetsPath11)Microsoft.Build.CppTasks.Common.v110.dll".

4. *.props* ファイル (例: *Partner.AutoImports.props*) を作成し、プロジェクトが含まれるフォルダーのルートに配置します。 このファイルは、さまざまなリソースを検索するために MSBuild によって使用される変数の設定用に使用されます。 このファイルで設定されていない変数は、レジストリ値に依存する他の *.props* ファイルおよび *.targets* ファイルによって設定されます。 ここではレジストリ値を設定しないため、これらの変数が空になり、ビルドは失敗します。 代わりに、*Partner.AutoImports.props* に次のコードを追加します。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <!-- This file must be imported by all project files at the top of the project file. -->
    <Project ToolsVersion="4.0"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
    <VCTargetsPath>$(DepotRoot)MSBuild\Microsoft.Cpp\v4.0\v110\</VCTargetsPath>
    <VCTargetsPath11>$(DepotRoot)MSBuild\Microsoft.Cpp\v4.0\v110\</VCTargetsPath11>
    <MSBuildExtensionsPath>$(DepotRoot)MSBuild</MSBuildExtensionsPath>
    <MSBuildExtensionsPath32>$(DepotRoot)MSBuild</MSBuildExtensionsPath32>
    <VCInstallDir_110>$(DepotRoot)Microsoft Visual Studio\2017\Enterprise\VC\</VCInstallDir_110>
    <VCInstallDir>$(VCInstallDir_110)</VCInstallDir>
    <WindowsKitRoot>$(DepotRoot)Windows Kits\</WindowsKitRoot>
    <WindowsSDK80Path>$(WindowsKitRoot)</WindowsSDK80Path>
    <WindowsSdkDir_80>$(WindowsKitRoot)8.0\</WindowsSdkDir_80>
    <WindowsSdkDir>$(WindowsSDKDir_80)</WindowsSdkDir>
    <WindowsSdkDir_80A>$(DepotRoot)Microsoft SDKs\Windows\v8.0A\</WindowsSdkDir_80A>
    </PropertyGroup>
    </Project>
    ```

5. 各プロジェクト ファイル内の先頭で、`<Project Default Targets...>` 行の後に、次の行を追加します。

    ```xml
    <Import Project="$([MSBuild]::GetDirectoryNameOfFileAbove($(MSBuildThisFileDirectory), Partner.AutoImports.props))\Partner.AutoImports.props"/>
    ```

::: moniker range="vs-2017"

6. コマンド ライン環境を次のように変更します。

    - Set Depot=*location of the Depot directory that you created in step 1*

    - Set path=%path%;*location of MSBuild on the computer*;%Depot%\Windows\System32;%Depot%\Windows\SysWOW64;%Depot%\Microsoft Visual Studio 15.0\Common7\IDE\

       ネイティブ 64 ビットのビルドの場合は、64 ビット版の MSBuild が指定されるように調整します。

::: moniker-end

::: moniker range=">=vs-2019"

6. コマンド ライン環境を次のように変更します。

    - Set Depot=*location of the Depot directory that you created in step 1*

    - Set path=%path%;*location of MSBuild on the computer*;%Depot%\Windows\System32;%Depot%\Windows\SysWOW64;%Depot%\Microsoft Visual Studio 16.0\Common7\IDE\

       ネイティブ 64 ビットのビルドの場合は、64 ビット版の MSBuild が指定されるように調整します。

::: moniker-end

## <a name="see-also"></a>関連項目

- [デバッグの実行可能ファイルを実行するテスト用コンピューターの準備](/cpp/windows/preparing-a-test-machine-to-run-a-debug-executable)
- [コマンド ライン リファレンス](../msbuild/msbuild-command-line-reference.md)
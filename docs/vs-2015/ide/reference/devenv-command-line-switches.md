---
title: Devenv コマンド ライン スイッチ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- switches, Devenv
- builds [Team System], command-line
- applications [Visual Studio], executing
- compiling source code, Devenv
- command-line switches, Devenv
- command line [Visual Studio], switches
- Devenv
- environment, Devenv commands
- compilers, Devenv commands
- switches
- Devenv, syntax and list of switches
ms.assetid: e12bc6ed-74fd-4bea-8d7c-89b99c20bad8
caps.latest.revision: 36
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b8b0683024e2881f76bb6c54d9420d351fced08a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668722"
---
# <a name="devenv-command-line-switches"></a>Devenv コマンド ライン スイッチ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Devenv を使用すると、コマンド ラインから統合開発環境 (IDE: Integrated Development Environment) のさまざまなオプションを設定したり、プロジェクトをビルド、デバッグ、および配置できます。 これらのスイッチを使用して、スクリプトや .bat ファイル (夜間用のビルド スクリプトなど) から IDE を実行したり、特定の構成で IDE を起動したりします。

> [!NOTE]
> ビルド関連のタスクでは、devenv の代わりに MSBuild を使用することをお勧めします。 詳細については、「[コマンド ライン リファレンス](../../msbuild/msbuild-command-line-reference.md)」を参照してください。

> [!NOTE]
> [/Setup (devenv.exe)](../../ide/reference/setup-devenv-exe.md) スイッチおよび [/InstallVSTemplates (devenv.exe)](../../ide/reference/installvstemplates-devenv-exe.md) スイッチを使用するには、管理者として devenv を実行する必要があります。

## <a name="devenv-switch-syntax"></a>Devenv のスイッチの構文
 既定では、devenv コマンドは、devenv.com ユーティリティにスイッチを渡します。

 devenv.com ユーティリティは標準のシステム ストリーム、たとえば `stdout` および `stderr` などを介して結果を出力します。このユーティリティは出力をキャプチャする際に、txt ファイルなどの適切な入出力先を判断します。 `devenv.exe` で始まるコマンドも同じスイッチを使うことができますが、コマンドは devenv.com ユーティリティを介さずに devenv.exe プログラムに送られます。

 `devenv` スイッチの構文規則は、他の DOS コマンド ライン ユーティリティのものとよく似ています。 すべての `devenv` スイッチと引数に適用される構文規則は以下のとおりです。

- `devenv` で始まるコマンド。

- スイッチは大文字と小文字を区別しません。

- ソリューションまたはプロジェクトを指定するとき、最初の引数はソリューション ファイルまたはプロジェクト ファイルの名前 (ファイル パスを含む) です。

- 最初の引数がソリューションでもプロジェクトでもないファイルの場合、そのファイルが IDE の新しいインスタンスで適切なエディターを使用して開かれます。

- ソリューション ファイル名の代わりにプロジェクト ファイル名を入力すると、`devenv` コマンドは、プロジェクト フォルダーの親フォルダーで同じ名前が付いているソリューション ファイルを検索します。 たとえば、`devenv /build myproject1.vbproj` というコマンドは、親フォルダーで "myproject1.sln" という名前のついたソリューション ファイルを検索します。

    > [!NOTE]
    > このプロジェクトを参照するソリューション ファイルは、親フォルダーの中に 1 つだけ置かれている必要があります。 親フォルダーにこのプロジェクトを参照するソリューション ファイルがない場合、また親フォルダーにこのソリューション ファイルが 2 つ以上ある場合は、一時ソリューション ファイルが作成されます。一時ソリューション ファイルは、プロジェクトにちなんだ名前となり、プロジェクトを参照します。

- ファイル パスやファイル名にスペースが含まれる場合は、二重引用符 ("") で囲む必要があります。 たとえば、"c:\project a\\" と指定します。

- 1 行に複数のスイッチや引数を入力する場合は、空白文字 1 つで区切ります。 たとえば、**devenv /log output.txt** というコマンドは、IDE を開き、そのセッションのすべてのログ情報を output.txt に出力します。

- `devenv` コマンドではパターン一致構文を使用できません。

## <a name="devenv-switches"></a>Devenv のスイッチ
 次の表のコマンド ライン スイッチを使用して、IDE を表示し、説明されているタスクを実行します。

|コマンド ライン スイッチ|説明|
|-------------------------|-----------------|
|[/Command (devenv.exe)](../../ide/reference/command-devenv-exe.md)|IDE を起動し、指定したコマンドを実行します。|
|[/DebugExe (devenv.exe)](../../ide/reference/debugexe-devenv-exe.md)|[!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] の実行可能ファイルをデバッガーの制御下に読み込みます。 このスイッチは、[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] または [!INCLUDE[csprcs](../../includes/csprcs-md.md)] の実行可能ファイルには使用できません。 詳細については、「[デバッガーでプロセスを自動的に開始する](../../debugger/debug-multiple-processes.md#BKMK_Automatically_start_an_process_in_the_debugger)」を参照してください。|
|[/LCID (devenv.exe)](../../ide/reference/lcid-devenv-exe.md) または `/l`|IDE の既定の言語を設定します。 指定した言語が Visual Studio インストールに含まれていない場合、この設定は無視されます。|
|[/Log (devenv.exe)](../../ide/reference/log-devenv-exe.md)|[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] を起動し、ログ ファイルにすべてのアクティビティを記録します。|
|[/Run (devenv.exe)](../../ide/reference/run-devenv-exe.md) または `/r`|指定したソリューションをコンパイルして実行します。|
|[/Runexit (devenv.exe)](../../ide/reference/runexit-devenv-exe.md)|指定したソリューションをコンパイルして実行します。ソリューションの実行時には IDE を最小化し、ソリューションの実行終了後に IDE を終了します。|
|[/UseEnv (devenv.exe)](../../ide/reference/useenv-devenv-exe.md)|IDE で [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] のコンパイルをする場合に、 **[オプション]** ダイアログ ボックスの **[プロジェクト]** オプションの [VC++ ディレクトリ] セクションで指定した設定ではなく、PATH、INCLUDE、および LIB の各環境変数を使用します。 詳細については、「[コマンド ライン ビルドのパスと環境変数を設定する](https://msdn.microsoft.com/library/99389528-deb5-43b9-b99a-03c8773ebaf4)」を参照してください。|
|[/Edit (devenv.exe)](../../ide/reference/edit-devenv-exe.md)|指定したファイルを、このアプリケーションの実行中のインスタンスで開きます。 実行中のインスタンスがない場合は、簡略化されたウィンドウ レイアウトで新しいインスタンスを起動します。|
|[/ResetAddin (devenv.exe)](../../ide/reference/resetaddin-devenv-exe.md)|指定されたアドインを読み込まずに Visual Studio IDE のインスタンスを起動します。|
|[/SafeMode (devenv.exe)](../../ide/reference/safemode-devenv-exe.md)|[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] をセーフ モードで起動し、既定の環境とサービス、および出荷バージョンのサードパーティ パッケージだけを読み込みます。|
|[/ResetSkipPkgs (devenv.exe)](../../ide/reference/resetskippkgs-devenv-exe.md)|問題のある VSPackage が読み込まれないようにユーザーが VSPackages に追加した SkipLoading タグをすべて消去します。|
|[/Setup (devenv.exe)](../../ide/reference/setup-devenv-exe.md)|使用できるすべての VSPackages にある、メニュー、ツール バー、およびコマンド グループを記述したリソース メタデータが Visual Studio により強制的にマージされます。|

 次の表のコマンド ライン スイッチを使用して、タスクを実行します。 これらのコマンド ライン スイッチでは、IDE が表示されません。

|コマンド ライン スイッチ|説明|
|-------------------------|-----------------|
|[/? (devenv.exe)](../../ide/reference/q-devenv-exe.md)|Devenv のスイッチのヘルプを **[コマンド プロンプト]** ウィンドウ内に表示します。<br /><br /> **Devenv /?**|
|[/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)|指定のソリューションの構成に従って、指定のソリューションまたはプロジェクトをビルドします。<br /><br /> **Devenv myproj.csproj /build**|
|[/Clean (devenv.exe)](../../ide/reference/clean-devenv-exe.md)|ビルド コマンドによって作成されたすべてのファイルを、ソース ファイルに影響を与えずに削除します。<br /><br /> **Devenv myproj.csproj /clean**|
|[/Deploy (devenv.exe)](../../ide/reference/deploy-devenv-exe.md)|ソリューションの構成に従って、ソリューションを配置に必要なファイルと共にビルドします。<br /><br /> **Devenv myproj.csproj /deploy**|
|[/Diff](../../ide/reference/diff.md)|2 つのファイルを比較します。  4 つのパラメーター、SourceFile、TargetFile、SourceDisplayName (省略可能)、および TargetDisplayName (省略可能) を受け取ります。|
|[/InstallVSTemplates (devenv.exe)](../../ide/reference/installvstemplates-devenv-exe.md)|*\<VisualStudioInstallDir>* \Common7\IDE\ProjectTemplates または *\<VisualStudioInstallDir>* \Common7\IDE\ItemTemplates にあるプロジェクトや項目テンプレートを登録して、 **[新しいプロジェクト]** ダイアログ ボックスおよび **[新しい項目の追加]** ダイアログ ボックスからアクセスできるようにします。<br /><br /> **Devenv /InstallVSTemplates**|
|[/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)|ビルド時のエラーを受け取るファイルを指定できます。<br /><br /> **Devenv myproj.csproj /build /out log.txt**|
|[/Project (devenv.exe)](../../ide/reference/project-devenv-exe.md)|ビルド、消去、または配置するプロジェクトを指定します。 このスイッチは、/build、/rebuild、/clean、または /deploy スイッチを指定した場合にだけ使用できます。|
|[/ProjectConfig (devenv.exe)](../../ide/reference/projectconfig-devenv-exe.md)|ビルドまたは配置するプロジェクト構成を指定します。 このスイッチは、/project スイッチを指定した場合だけに使用できます。|
|[/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)|指定のソリューションの構成に従って、指定のソリューションまたはプロジェクトを消去してからビルドします。|
|[/ResetSettings (devenv.exe)](../../ide/reference/resetsettings-devenv-exe.md)|Visual Studio の既定の設定を復元します。 指定の .vssettings ファイルに準じた設定にリセットすることもできます。|
|[/Updateconfiguration (devenv.exe)](../../ide/reference/updateconfiguration-devenv-exe.md)|[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] にシステム上の [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] パッケージをマージさせ、MEF キャッシュに変更がないかを確認することを通知します。|
|[/Upgrade (devenv.exe)](../../ide/reference/upgrade-devenv-exe.md)|指定されたソリューション ファイルとそのすべてのプロジェクト ファイル、または指定されたプロジェクト ファイルを、そのファイルに対応する現在の [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] の形式にアップグレードします。|

## <a name="see-also"></a>関連項目
 [[全般]、[環境]、[オプション] ダイアログ ボックス](../../ide/reference/general-environment-options-dialog-box.md)

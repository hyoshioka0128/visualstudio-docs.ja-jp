---
title: Devenv コマンド ライン スイッチ
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- switches, Devenv
- command-line switches, Devenv
- command line [Visual Studio], switches
- Devenv
ms.assetid: e12bc6ed-74fd-4bea-8d7c-89b99c20bad8
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b3ed82bd8ba3845541d7dce628f99fb78b62ab9f
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75595710"
---
# <a name="devenv-command-line-switches"></a>Devenv コマンドライン スイッチ

Devenv を使用すると、コマンド ラインから IDE のさまざまなオプションの設定、プロジェクトのビルド、プロジェクトのデバッグ、およびプロジェクトの配置を行うことができます。 これらのスイッチを使用して、スクリプトや .bat ファイル (夜間用のビルド スクリプトなど) から IDE を実行したり、特定の構成で IDE を起動したりします。

> [!NOTE]
> ビルド関連のタスクでは、devenv の代わりに MSBuild を使用することをお勧めします。 詳細については、「[MSBuild コマンド ライン リファレンス](../../msbuild/msbuild-command-line-reference.md)」を参照してください。

VSPackage 開発に関連するスイッチの詳細については、「[VSPackage 開発の Devenv コマンド ライン スイッチ](../../extensibility/devenv-command-line-switches-for-vspackage-development.md)」も参照してください。

## <a name="devenv-switch-syntax"></a>Devenv のスイッチの構文

`devenv` で始まるコマンドは `devenv.com` ユーティリティによって処理されます。このユーティリティは、`stdout` や `stderr` のような標準のシステム ストリーム経由で出力を配信します。 このユーティリティは出力をキャプチャする際に、txt ファイルなどの適切な入出力先を判断します。

また、`devenv.exe` で始まるコマンドも同じスイッチを使うことができますが、`devenv.com` ユーティリティはバイパスされます。 `devenv.exe` を使用すると、コンソールの出力表示が直接的に禁止されます。

`devenv` スイッチの構文規則は、他の DOS コマンド ライン ユーティリティの規則とよく似ています。 すべての `devenv` スイッチと引数に適用される構文規則は以下のとおりです。

- `devenv` で始まるコマンド。

- スイッチは大文字と小文字が区別されません。

- ハイフン ("-") またはスラッシュ ("/") を使用してスイッチを指定できます。

- ソリューションまたはプロジェクトを指定するとき、最初の引数はソリューション ファイルまたはプロジェクト ファイルの名前 (ファイル パスを含む) です。

- 最初の引数がソリューションでもプロジェクトでもないファイルの場合、そのファイルが IDE の新しいインスタンスで適切なエディターを使用して開かれます。

- ソリューション ファイル名の代わりにプロジェクト ファイル名を入力すると、`devenv` コマンドは、プロジェクト フォルダーの親フォルダーで同じ名前が付いているソリューション ファイルを検索します。 たとえば、`devenv myproject1.vbproj /build` というコマンドは、親フォルダーで `myproject1.sln` という名前のソリューション ファイルを検索します。

  > [!NOTE]
  > このプロジェクトを参照するソリューション ファイルは、親フォルダーの中に 1 つだけ置かれている必要があります。 親フォルダーにこのプロジェクトを参照するソリューション ファイルがない場合、また親フォルダーにこのソリューション ファイルが 2 つ以上ある場合は、一時ソリューション ファイルが作成されます。

- ファイル パスやファイル名にスペースが含まれる場合は、二重引用符 ("") で囲む必要があります。 たとえば、`"c:\project a\"` のようにします。

- 1 行に複数のスイッチや引数を入力する場合は、空白文字 1 つで区切ります。 たとえば、`devenv /log output.txt` というコマンドは、IDE を開き、そのセッションのすべてのログ情報を output.txt に出力します。

- `devenv` コマンドではパターン一致構文を使用できません。

## <a name="devenv-switches"></a>Devenv のスイッチ

次の表のコマンド ライン スイッチを使用すると、IDE が表示され、説明されているタスクが実行されます。

|コマンド ライン スイッチ|説明|
| - |-----------------|
|[/Command](command-devenv-exe.md)|IDE を起動し、指定したコマンドを実行します。<br /><br /> `devenv /command "nav https://docs.microsoft.com/"`|
|[/DebugExe](debugexe-devenv-exe.md)|C++ の実行可能ファイルをデバッガーの制御下に読み込みます。 このスイッチは、Visual Basic または C# の実行可能ファイルには使用できません。 詳細については、「[デバッガーでプロセスを自動的に開始する](../../debugger/debug-multiple-processes.md#BKMK_Automatically_start_an_process_in_the_debugger)」を参照してください。<br /><br /> `devenv /debugexe mysln.exe`|
|[/Diff](diff.md)|2 つのファイルを比較します。 4 つのパラメーター、*SourceFile*、*TargetFile*、*SourceDisplayName* (省略可能)、*TargetDisplayName* (省略可能) を受け取ります。<br /><br /> `devenv /diff File1 File2 Alias1 Alias2`|
|[/DoNotLoadProjects](donotloadprojects-devenv-exe.md)|プロジェクトを読み込むことなく、指定したソリューションを開きます。<br /><br /> `devenv /donotloadprojects mysln.sln`|
|[/Edit](edit-devenv-exe.md)|指定したファイルを、このアプリケーションの実行中のインスタンスで開きます。 実行中のインスタンスがない場合は、簡略化されたウィンドウ レイアウトで新しいインスタンスを起動します。<br /><br /> `devenv /edit File1 File2`|
|[/LCID または /L](lcid-devenv-exe.md)|IDE の既定の言語を設定します。 指定した言語が Visual Studio インストールに含まれていない場合、この設定は無視されます。<br /><br /> `devenv /l 1033`|
|[/Log](log-devenv-exe.md)|Visual Studio を起動し、ログ ファイルにすべてのアクティビティを記録します。<br /><br /> `devenv /log mylogfile.xml`|
|[/NoSplash](nosplash-devenv-exe.md)|スプラッシュ スクリーンを表示せずに IDE を開きます。<br /><br /> `devenv /nosplash File1 File2`|
|[/Run または /R](run-devenv-exe.md)|指定したソリューションをコンパイルして実行します。<br /><br /> `devenv /run mysln.sln`|
|[/RunExit](runexit-devenv-exe.md)|指定したソリューションをコンパイルして実行します。ソリューションの実行時には IDE を最小化し、ソリューションの実行終了後に IDE を終了します。<br /><br /> `devenv /runexit mysln.sln`|
|[/SafeMode](safemode-devenv-exe.md)|Visual Studio をセーフ モードで起動します。 このスイッチを指定すると、既定の環境、既定のサービス、および出荷バージョンのサードパーティ パッケージのみが読み込まれます。<br /><br /> このスイッチは引数を取りません。|
|[/UseEnv](useenv-devenv-exe.md)|IDE で C++ のコンパイルに PATH、INCLUDE、LIBPATH、および LIB 環境変数が使用されます。 このスイッチは、**C++ によるデスクトップ開発**ワークロードと共にインストールされます。 詳細については、[コマンド ライン ビルドのパスと環境変数の設定](/cpp/build/setting-the-path-and-environment-variables-for-command-line-builds)に関するページを参照してください。|

次のコマンドライン スイッチでは、IDE が表示されません。

|コマンド ライン スイッチ|説明|
| - |-----------------|
|[/?](q-devenv-exe.md)|`devenv` のスイッチのヘルプを **[コマンド プロンプト]** ウィンドウ内に表示します。<br /><br /> このスイッチは引数を取りません。|
|[/Build](build-devenv-exe.md)|指定のソリューションの構成に従って、指定のソリューションまたはプロジェクトをビルドします。<br /><br /> `devenv mysln.sln /build`|
|[/Clean](clean-devenv-exe.md)|ビルド コマンドによって作成されたすべてのファイルを、ソース ファイルに影響を与えずに削除します。<br /><br /> `devenv mysln.sln /clean`|
|[/Deploy](deploy-devenv-exe.md)|ソリューションの構成に従って、ソリューションを配置に必要なファイルと共にビルドします。<br /><br /> `devenv mysln.sln /deploy`|
|[/Out](out-devenv-exe.md)|ビルド時のエラーを受け取るファイルを指定できます。<br /><br /> `devenv mysln.sln /build Debug /out log.txt`|
|[/Project](project-devenv-exe.md)|ビルド、消去、または配置するプロジェクトを指定します。 このスイッチは、`/Build`、`/Rebuild`、`/Clean`、または `/Deploy` スイッチも指定した場合にのみ使用できます。<br /><br /> `devenv mysln.sln /build Debug /project proj1`|
|[/ProjectConfig](projectconfig-devenv-exe.md)|ビルドまたは配置するプロジェクト構成を指定します。 このスイッチは、`/Project` スイッチも指定した場合にのみ使用できます。<br /><br /> `devenv mysln.sln /build Release /project proj1 /projectconfig Release`|
|[/Rebuild](rebuild-devenv-exe.md)|指定のソリューションの構成に従って、指定のソリューションまたはプロジェクトを消去してからビルドします。<br /><br /> `devenv mysln.sln /rebuild`|
|[/ResetSettings](resetsettings-devenv-exe.md)|Visual Studio の既定の設定を復元します。 指定の `.vssettings` ファイルに準じた設定にリセットすることもできます。<br /><br /> `devenv /resetsettings mysettings.vssettings`|
|[/Upgrade](upgrade-devenv-exe.md)|指定されたソリューション ファイルとそのすべてのプロジェクト ファイル、または指定されたプロジェクト ファイルを、そのファイルに対応する現在の Visual Studio の形式にアップグレードします。<br /><br /> `devenv mysln.sln /upgrade`|

## <a name="see-also"></a>関連項目

- [[全般]、[環境]、[オプション] ダイアログ ボックス](general-environment-options-dialog-box.md)
- [VSPackage 開発の Devenv コマンド ライン スイッチ](../../extensibility/devenv-command-line-switches-for-vspackage-development.md)

---
title: Python プロジェクトのカスタム メニュー コマンドを定義する
description: プロジェクトやターゲット ファイルを編集することで、Visual Studio で Python プロジェクト コンテキスト メニューにカスタム コマンドを追加し、実行可能プログラム、スクリプト、モジュール、インライン コード スニペット、pip を呼び出すことができます。
ms.date: 11/12/2018
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 6e9e7fe418528bb888672b1b73d421d811b9e69e
ms.sourcegitcommit: a77158415da04e9bb8b33c332f6cca8f14c08f8c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2020
ms.locfileid: "86386986"
---
# <a name="define-custom-commands-for-python-projects"></a>Python プロジェクトのカスタム コマンドを定義する

Python プロジェクトで作業していると、特定のスクリプトやモジュール、pip コマンド、または他の任意のツールを実行するために、コマンド ウィンドウに切り替えると便利なことに気付く場合があります。 ワークフローを改良するため、Python プロジェクトのコンテキスト メニューの **[Python]** サブメニューに、カスタム コマンドを追加することができます。 これらのコマンドは、コンソール ウィンドウまたは Visual Studio の**出力**ウィンドウで実行できます。 また、正規表現を使って、コマンドの出力からエラーと警告を解析する方法を Visual Studio に指示することもできます。

既定では、そのメニューに含まれる **[PyLint を実行]** コマンドは 1 つのみです。

![プロジェクトのコンテキスト メニューの [Python] サブメニューの既定の外観](media/custom-commands-default-menu.png)

この同じコンテキスト メニューにカスタム コマンドが表示されます。 カスタム コマンドはプロジェクト ファイルに直接追加され、その特定のプロジェクトに適用されます。 *.targets* ファイルでカスタム コマンドを定義して、複数のプロジェクト ファイルに簡単にインポートすることもできます。

Visual Studio の特定の Python プロジェクト テンプレートでは、 *.targets* ファイルを使って独自のカスタム コマンドが既に追加されています。 たとえば、Bottle Web プロジェクトと Flask Web プロジェクトのテンプレートでは、2 つのコマンド **[サーバーの起動]** と **[デバッグ サーバーの開始]** が追加されています。 Django Web プロジェクト テンプレートでは、これら 2 つのコマンドに加えてさらにかなりの数のコマンドが追加されています。

![Django プロジェクトのコンテキスト メニューの [Python] サブメニューの外観](media/custom-commands-django-menu.png)

各カスタム コマンドでは、Python ファイル、Python モジュール、インライン Python コード、任意の実行可能ファイル、または pip コマンドを参照できます。 また、コマンドを実行する方法と場所も指定できます。

> [!Tip]
> テキスト エディターでプロジェクト ファイルを変更するたびに、Visual Studio でプロジェクトを再度読み込んで変更を適用する必要があります。 たとえば、カスタム コマンドの定義を追加した後でプロジェクトのコンテキスト メニューにそのコマンドを表示するには、プロジェクトを読み込み直す必要があります。
>
> ご存知のように、Visual Studio にはプロジェクト ファイルを直接編集する手段があります。 最初にプロジェクト ファイルを右クリックして **[プロジェクトのアンロード]** を選んでから、再び右クリックして **[\<project-name> の編集]** を選び、Visual Studio エディターでプロジェクトを開きます。 その後、編集を行って保存し、プロジェクトをもう一度右クリックして、 **[プロジェクトの再読み込み]** を選びます。エディターのプロジェクト ファイルを閉じる確認も求められます。
>
> ただし、カスタム コマンドを開発するときにこのようなクリックをすべて行うのは煩わしいことがあります。 ワークフローの効率をよくするには、Visual Studio でプロジェクトを読み込み、それと一緒に別のエディター (Visual Studio の別のインスタンス、Visual Studio Code、メモ帳など) で *.pyproj* ファイルを開きます。 エディターで変更を保存して Visual Studio に切り替えると、Visual Studio は変更を検出し、プロジェクトの再読み込みを行うかどうかの確認を求めます (**プロジェクト \<name> は環境外で変更されています**)。 **[再読み込み]** を選ぶと、1 ステップですぐに変更内容が適用されます。

## <a name="walkthrough-add-a-command-to-a-project-file"></a>チュートリアル: プロジェクト ファイルにコマンドを追加する

カスタム コマンドに慣れてもらうため、このセクションでは、直接 *python.exe* を使ってプロジェクトのスタートアップ ファイルを実行する簡単な例の手順を説明します (このようなコマンドは、実質的に **[デバッグ]**  >  **[デバッグなしで開始]** を使うのと同じです)。

1. **Python アプリケーション** テンプレートを使って、"Python-CustomCommands" という名前の新しいプロジェクトを作成します (プロセスにまだ慣れていない場合は、「[クイック スタート:Visual Studio のテンプレートから Python プロジェクトを作成する](quickstart-02-python-in-visual-studio-project-from-template.md)」の説明を参照してください。)

1. *Python_CustomCommands.py*、コードを追加`print("Hello custom commands")`します。

1. **ソリューション エクスプローラー**でプロジェクトを右クリックして **[Python]** を選び、サブメニューに表示されるコマンドが **[PyLint を実行]** だけであることを確認します。 カスタム コマンドはこの同じサブメニューに表示されます。

1. 概要で指摘したように、*Python-CustomCommands.pyproj* を別のテキスト エディターで開きます。 次の行を、ファイル末尾の終わりの `</Project>` のすぐ内側に追加して、ファイルを保存します。

    ```xml
    <PropertyGroup>
      <PythonCommands>
        $(PythonCommands);
      </PythonCommands>
    </PropertyGroup>
    ```

1. Visual Studio に戻り、ファイルの変更に関するプロンプトが表示されたら **[再読み込み]** を選びます。 次に、 **[Python]** を再び表示して、 **[PyLint を実行]** がまだ唯一の項目であることを確認します。これは、追加した行は、PyLint コマンドを含む既定の `<PythonCommands>` プロパティ グループを複製しているだけであるためです。

1. プロジェクト ファイルのエディターに切り替え、次の `<Target>` 定義を `<PropertyGroup>` の後に追加します。 後で説明するように、この `Target` 要素では、コンソール ウィンドウで *python.exe* を使って ("StartupFile" プロパティによって示される) スタートアップ ファイルを実行するためのカスタム コマンドを定義します。 属性 `ExecuteIn="consolepause"` は、閉じる前にユーザーのキー押下を待っているコンソールを使います。

    ```xml
    <Target Name="Example_RunStartupFile" Label="Run startup file" Returns="@(Commands)">
      <CreatePythonCommandItem
        TargetType="script"
        Target="$(StartupFile)"
        Arguments=""
        WorkingDirectory="$(MSBuildProjectDirectory)"
        ExecuteIn="consolepause">
        <Output TaskParameter="Command" ItemName="Commands" />
      </CreatePythonCommandItem>
    </Target>
    ```

1. Target の `Name` 属性の値を前に追加した `<PythonCommands>` プロパティ グループに追加し、要素が次のコードのようになるようにします。 ターゲットの名前をこの一覧に追加するのは、 **[Python]** メニューに追加することと同じです。

    ```xml
      <PythonCommands>
        $(PythonCommands);
        Example_RunStartupFile
      </PythonCommands>
    ```

    `$(PythonCommands)` で定義されているものより前にカスタム コマンドを表示したい場合は、そのトークンの前に配置します。

1. プロジェクト ファイルを保存し、Visual Studio に切り替えて、メッセージが表示されたらプロジェクトを再度読み込みます。 Then right-click the **Python-CustomCommands** プロジェクトを右クリックし、 **[Python]** を選択します。 **[Run startup file]** 項目がメニューに表示されるはずです。 メニュー項目が表示されない場合は、名前を `<PythonCommands>` 要素に追加したことを確認します。 また、後の「[トラブルシューティング](#troubleshooting)」も参照してください。

    ![Python コンテキスト サブメニューに表示されたカスタム コマンド](media/custom-commands-walkthrough-menu-item.png)

1. **[Run startup file]** コマンドを選ぶと、"**Hello custom commands**" の後に、"**Press any key to continue**" と続く、コマンド ウィンドウが開きます。  任意のキーを押して、ウィンドウを閉じます。

    ![コンソール ウィンドウのカスタム コマンドの出力](media/custom-commands-walkthrough-console.png)

1. プロジェクト ファイルのエディターに戻り、`ExecuteIn` 属性の値を `output` に変更します。 ファイルを保存し、Visual Studio に切り替え、プロジェクトを再度読み込み、コマンドをもう一度呼び出します。 今度は、プログラムの出力が Visual Studio の **[出力]** ウィンドウに表示されます。

    ![出力ウィンドウのカスタム コマンドの出力](media/custom-commands-walkthrough-output-window.png)

1. さらにコマンドを追加するには、各コマンドの適切な `<Target>` 要素を定義し、ターゲットの名前を `<PythonCommands>` プロパティ グループに追加して、Visual Studio でプロジェクトを再び読み込みます。

>[!Tip]
> プロジェクトのプロパティ (`($StartupFile)` など) を使うコマンドを呼び出すと、トークンが定義されていないためにコマンドが失敗する場合は、Visual Studio はプロジェクトが再び読み込まれるまでコマンドを無効にします。 ただし、プロパティが定義されているプロジェクトを変更しても、コマンドの状態は更新されないので、このような場合でもプロジェクトの再読み込みが必要です。

## <a name="command-target-structure"></a>コマンド ターゲットの構造

次の擬似コードは、`<Target>` 要素の一般的な形式を示したものです。

```xml
<Target Name="Name1" Label="Display Name" Returns="@(Commands)">
    <CreatePythonCommandItem Target="filename, module name, or code"
        TargetType="executable/script/module/code/pip"
        Arguments="..."
        ExecuteIn="console/consolepause/output/repl[:Display name]/none"
        WorkingDirectory="..."
        ErrorRegex="..."
        WarningRegex="..."
        RequiredPackages="...;..."
        Environment="...">

      <!-- Output always appears in this form, with these exact attributes -->
      <Output TaskParameter="Command" ItemName="Commands" />
    </CreatePythonCommandItem>
  </Target>
```

属性値でプロジェクトのプロパティまたは環境変数を参照するには、`$()` トークン内で名前を使います (例: `$(StartupFile)`、`$(MSBuildProjectDirectory)`)。 詳細については、「[MSBuild プロパティ](../msbuild/msbuild-properties.md)」を参照してください。

### <a name="target-attributes"></a>Target の属性

| 属性 | Required | Description |
| --- | --- | --- |
| 名前 | はい | Visual Studio プロジェクト内でのコマンドの識別子です。 [Python] のサブメニューにコマンドを表示するには、この名前を `<PythonCommands>` プロパティ グループに追加する必要があります。 |
| ラベル | はい | [Python] のサブメニューに表示される UI の表示名です。 |
| 戻り値 | はい | ターゲットをコマンドとして識別する `@(Commands)` を含む必要があります。 |

### <a name="createpythoncommanditem-attributes"></a>CreatePythonCommandItem の属性

すべての属性値は、大文字と小文字を区別されません。

| 属性 | Required | 説明 |
| --- | --- | --- |
| TargetType | はい | 含まれる Target 属性と、Arguments 属性でのその使い方を指定します。<ul><li>**executable**:Target で指定されている実行可能ファイルを実行します。コマンド ラインで直接入力された場合と同じように、Arguments の値を追加します。 値には、引数なしのプログラム名のみが含まれる必要があります。</li><li>**script**:Target のファイル名とそれに続く Arguments の値で、*python.exe* を実行します。</li><li>**module**:`python -m` の後に Target のモジュール名と Arguments の値を指定して実行します。</li><li>**code**:Target に含まれるインライン コードを実行します。 Arguments の値は無視されます。</li><li>**pip**:Target のコマンドと Arguments の値で `pip` を実行します。ただし、ExecuteIn は "output" に設定され、pip は `install` コマンドを想定し、Target をパッケージ名として使います。</li></ul> |
| Target | はい | TargetType に応じて、使うファイル名、モジュール名、コード、または pip コマンドです。 |
| 引数 | Optional | ターゲットに渡す引数の文字列を指定します (存在する場合)。 TargetType が `script` の場合は、引数は *python.exe* ではなく Python プログラムに渡されることに注意してください。 TargetType が `code` のときは無視されます。 |
| ExecuteIn | はい | コマンドを実行する環境を指定します。<ul><li>**console**:(既定値) Target と引数を、コマンド ラインで直接入力された場合と同じように実行します。 Target の実行中はコマンド ウィンドウが表示された後、自動的に閉じられます。</li><li>**consolepause**:console と同じですが、キー押下を待ってからウィンドウを閉じます。</li><li>**output**:Target を実行し、Visual Studio の**出力**ウィンドウに結果を表示します。 TargetType が "pip" の場合、Visual Studio は Target をパッケージ名として使い、Arguments を付加します。</li><li>**repl**:Target を [Python Interactive ウィンドウ](python-interactive-repl-in-visual-studio.md)で実行します。ウィンドウのタイトルには、省略可能な表示名が使われます。</li><li>**none**: 動作は console と同じです。</li></ul>|
| WorkingDirectory | Optional | コマンドを実行するフォルダーです。 |
| ErrorRegex<br>WarningRegEx | Optional | ExecuteIn が `output` の場合にのみ使われます。 どちらの値も、Visual Studio が **[エラー一覧]** ウィンドウにエラーと警告を表示するためにコマンド出力を解析するときに使う正規表現を指定します。 指定しないと、コマンドは **[エラー一覧]** ウィンドウに反映されません。 Visual Studio が想定する値の詳細については、「[正規表現の名前付きキャプチャ グループ](#named-capture-groups-for-regular-expressions)」を参照してください。 |
| RequiredPackages | Optional | コマンドのパッケージ要件の一覧です。[*requirements.txt*](https://pip.pypa.io/en/stable/user_guide/#requirements-files) (pip.readthedocs.io) と同じ形式を使います。 たとえば、 **[PyLint の実行]** コマンドでは、`pylint>=1.0.0` と指定されています。 コマンドを実行する前に、Visual Studio は一覧内のすべてのパッケージがインストールされていることを確認します。 Visual Studio は、pip を使ってすべての足りないパッケージをインストールします。 |
| 環境 | Optional | コマンドを実行する前に定義する環境変数の文字列です。 各変数では \<NAME>=\<VALUE> の形式を使い、複数の変数はセミコロンで区切ります。 複数の値を持つ変数は、一重引用符または二重引用符で囲む必要があります (例: 'NAME=VALUE1;VALUE2')。 |

#### <a name="named-capture-groups-for-regular-expressions"></a>正規表現の名前付きキャプチャ グループ

コマンドの出力からエラーと警告を解析するとき、Visual Studio は、`ErrorRegex` および `WarningRegex` の値の正規表現が次の名前付きグループを使っているものと想定します。

- `(?<message>...)`:エラーのテキスト
- `(?<code>...)`:エラー コード
- `(?<filename>...)`:エラーが報告されるファイルの名前
- `(?<line>...)`:エラーが報告されたファイル内の場所の行番号。
- `(?<column>...)`:エラーが報告されたファイル内の場所の列番号。

たとえば、PyLint は次の形式の警告を生成します。

```output
************* Module hello
C:  1, 0: Missing module docstring (missing-docstring)
```

Visual Studio がこのような警告から適切な情報を抽出し、 **[エラー一覧]** ウィンドウに表示できるようにするため、 **[Pylint の実行]** コマンドの `WarningRegex` の値は、次のように指定されています。

```regex
^(?<filename>.+?)\((?<line>\d+),(?<column>\d+)\): warning (?<msg_id>.+?): (?<message>.+?)$]]
```

値の `msg_id` は、実際には `code` でなければならないことに注意してください。[問題 3680](https://github.com/Microsoft/PTVS/issues/3680) に関する説明を参照してください。

## <a name="create-a-targets-file-with-custom-commands"></a>カスタム コマンドの .targets ファイルの作成

プロジェクト ファイルでカスタム コマンドを定義すると、そのコマンドはそのプロジェクト ファイルだけで使えるようになります。 複数のプロジェクト ファイルでコマンドを使うには、代わりに、`<PythonCommands>` プロパティ グループとすべての `<Target>` 要素を *.targets* ファイルで定義します。 そして、個々のプロジェクト ファイルにそのファイルをインポートします。

*.targets* ファイルの形式は次のとおりです。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <PythonCommands>
      $(PythonCommands);
      <!-- Additional command names -->
    </PythonCommands>
  </PropertyGroup>

  <Target Name="..." Label="..." Returns="@(Commands)">
    <!-- CreatePythonCommandItem and Output elements... -->
  </Target>

  <!-- Any number of additional Target elements-->
</Project>
```

*.targets* ファイルをプロジェクトに読み込むには、`<Import Project="(path)">` 要素を `<Project>` 要素内の任意の場所に配置します。 たとえば、プロジェクトの *targets* サブフォルダーに *CustomCommands.targets* という名前のファイルがある場合は、次のコードを使います。

```xml
<Import Project="targets/CustomCommands.targets"/>
```

> [!Note]
> *.targets* ファイルを変更するたびに、プロジェクト自体だけでなく、プロジェクトを含む "*ソリューション*" を再度読み込む必要があります。

## <a name="example-commands"></a>コマンドの例

### <a name="run-pylint-module-target"></a>PyLint の実行 (モジュール ターゲット)

次のコードが *Microsoft.PythonTools.targets* ファイルに表示されます。

```xml
<PropertyGroup>
  <PythonCommands>$(PythonCommands);PythonRunPyLintCommand</PythonCommands>
  <PyLintWarningRegex>
    <![CDATA[^(?<filename>.+?)\((?<line>\d+),(?<column>\d+)\): warning (?<msg_id>.+?): (?<message>.+?)$]]>
  </PyLintWarningRegex>
</PropertyGroup>

<Target Name="PythonRunPyLintCommand"
        Label="resource:Microsoft.PythonTools.Common;Microsoft.PythonTools.Common.Strings;RunPyLintLabel"
        Returns="@(Commands)">
  <CreatePythonCommandItem Target="pylint.lint"
                           TargetType="module"
                           Arguments="&quot;--msg-template={abspath}({line},{column}): warning {msg_id}: {msg} [{C}:{symbol}]&quot; -r n @(Compile, ' ')"
                           WorkingDirectory="$(MSBuildProjectDirectory)"
                           ExecuteIn="output"
                           RequiredPackages="pylint&gt;=1.0.0"
                           WarningRegex="$(PyLintWarningRegex)">
    <Output TaskParameter="Command" ItemName="Commands" />
  </CreatePythonCommandItem>
</Target>
```

### <a name="run-pip-install-with-a-specific-package-pip-target"></a>特定のパッケージで pip のインストールを実行する (pip ターゲット)

次のコマンドは、`pip install my-package` を **[出力]** ウィンドウで実行します。 このようなコマンドは、パッケージを開発してそのインストールをテストするときに使う場合があります。 Target には、`install` コマンドではなくパッケージ名が含まれることに注意してください。`ExecuteIn="output"` を使うときはそのように想定されます。

```xml
<PropertyGroup>
  <PythonCommands>$(PythonCommands);InstallMyPackage</PythonCommands>
</PropertyGroup>

<Target Name="InstallMyPackage" Label="pip install my-package" Returns="@(Commands)">
  <CreatePythonCommandItem Target="my-package" TargetType="pip" Arguments=""
    WorkingDirectory="$(MSBuildProjectDirectory)" ExecuteIn="output">
    <Output TaskParameter="Command" ItemName="Commands" />
  </CreatePythonCommandItem>
</Target>
```

### <a name="show-outdated-pip-packages-pip-target"></a>古くなったショー pip パッケージを表示する (pip ターゲット)

```xml
<PropertyGroup>
  <PythonCommands>$(PythonCommands);ShowOutdatedPackages</PythonCommands>
</PropertyGroup>

<Target Name="ShowOutdatedPackages" Label="Show outdated pip packages" Returns="@(Commands)">
  <CreatePythonCommandItem Target="list" TargetType="pip" Arguments="-o --format columns"
    WorkingDirectory="$(MSBuildProjectDirectory)" ExecuteIn="consolepause">
    <Output TaskParameter="Command" ItemName="Commands" />
  </CreatePythonCommandItem>
</Target>
```

### <a name="run-an-executable-with-consolepause"></a>consolepause で実行可能ファイルを実行する

次のコマンドは、`where` を単純に実行して、プロジェクト フォルダーから始まる Python ファイルを表示します。

```xml
<PropertyGroup>
  <PythonCommands>$(PythonCommands);ShowAllPythonFilesInProject</PythonCommands>
</PropertyGroup>

<Target Name="ShowAllPythonFilesInProject" Label="Show Python files in project" Returns="@(Commands)">
  <CreatePythonCommandItem Target="where" TargetType="executable" Arguments="/r . *.py"
    WorkingDirectory="$(MSBuildProjectDirectory)" ExecuteIn="output">
    <Output TaskParameter="Command" ItemName="Commands" />
  </CreatePythonCommandItem>
</Target>
```

### <a name="run-server-and-run-debug-server-commands"></a>サーバー起動コマンドとデバッグ サーバー起動コマンド

Web プロジェクトの **[サーバーの起動]** および **[デバッグ サーバーの開始]** コマンドがどのように定義されているのか調べるには、[Microsoft.PythonTools.Web.targets](https://github.com/Microsoft/PTVS/blob/master/Python/Product/BuildTasks/Microsoft.PythonTools.Web.targets) (GitHub) を参照してください。

### <a name="install-package-for-development"></a>開発用のパッケージをインストールする

```xml
<PropertyGroup>
  <PythonCommands>PipInstallDevCommand;$(PythonCommands);</PythonCommands>
</PropertyGroup>

<Target Name="PipInstallDevCommand" Label="Install package for development" Returns="@(Commands)">
    <CreatePythonCommandItem Target="pip" TargetType="module" Arguments="install --editable $(ProjectDir)"
        WorkingDirectory="$(WorkingDirectory)" ExecuteIn="Repl:Install package for development">
      <Output TaskParameter="Command" ItemName="Commands" />
    </CreatePythonCommandItem>
  </Target>
```

*[fxthomas/Example.pyproj.xml](https://gist.github.com/fxthomas/5c601e3e0c1a091bcf56aed0f2960cfa) (GitHub) から。アクセス許可を得て使用。*

### <a name="generate-windows-installer"></a>Windows インストーラーを生成する

```xml
<PropertyGroup>
  <PythonCommands>$(PythonCommands);BdistWinInstCommand;</PythonCommands>
</PropertyGroup>

<Target Name="BdistWinInstCommand" Label="Generate Windows Installer" Returns="@(Commands)">
    <CreatePythonCommandItem Target="$(ProjectDir)setup.py" TargetType="script"
        Arguments="bdist_wininst --user-access-control=force --title &quot;$(InstallerTitle)&quot; --dist-dir=&quot;$(DistributionOutputDir)&quot;"
        WorkingDirectory="$(WorkingDirectory)" RequiredPackages="setuptools"
        ExecuteIn="Repl:Generate Windows Installer">
      <Output TaskParameter="Command" ItemName="Commands" />
    </CreatePythonCommandItem>
  </Target>
```

*[fxthomas/Example.pyproj.xml](https://gist.github.com/fxthomas/5c601e3e0c1a091bcf56aed0f2960cfa) (GitHub) から。アクセス許可を得て使用。*

### <a name="generate-wheel-package"></a>ホイール パッケージを生成する

```xml
<PropertyGroup>
  <PythonCommands>$(PythonCommands);BdistWheelCommand;</PythonCommands>
</PropertyGroup>

<Target Name="BdistWheelCommand" Label="Generate Wheel Package" Returns="@(Commands)">

  <CreatePythonCommandItem Target="$(ProjectDir)setup.py" TargetType="script"
      Arguments="bdist_wheel --dist-dir=&quot;$(DistributionOutputDir)&quot;"
      WorkingDirectory="$(WorkingDirectory)" RequiredPackages="wheel;setuptools"
      ExecuteIn="Repl:Generate Wheel Package">
    <Output TaskParameter="Command" ItemName="Commands" />
  </CreatePythonCommandItem>
</Target>
```

*[fxthomas/Example.pyproj.xml](https://gist.github.com/fxthomas/5c601e3e0c1a091bcf56aed0f2960cfa) (GitHub) から。アクセス許可を得て使用。*

## <a name="troubleshooting"></a>トラブルシューティング

### <a name="message-the-project-file-could-not-be-loaded"></a>メッセージ:"プロジェクト ファイルを読み込めませんでした"

プロジェクト ファイルに構文エラーがあることを示します。 メッセージには、具体的なエラー、行番号、文字位置が含まれています。

### <a name="console-window-closes-immediately-after-command-is-run"></a>コマンド実行直後にコンソール ウィンドウが閉じる

`ExecuteIn="consolepause"` の代わりに `ExecuteIn="console"`を使用します。

### <a name="command-does-not-appear-on-the-menu"></a>コマンドがメニューに表示されない

コマンドが `<PythonCommands>` プロパティ グループに含まれること、およびコマンド一覧での名前が `<Target>` 要素で指定されている名前と一致することを、確認します。

たとえば、次の要素では、プロパティ グループでの名前 "Example" と、ターゲットでの名前 "ExampleCommand" が一致しません。 Visual Studio は "Example" という名前のコマンドを探さないので、コマンドは表示されません。 この問題を解決するには、コマンド一覧で "ExampleCommand" という名前を使うか、ターゲットの名前を "Example" だけに変更します。

```xml
  <PropertyGroup>
    <PythonCommands>$(PythonCommands);Example</PythonCommands>
  </PropertyGroup>
  <Target Name="ExampleCommand" Label="Example Command" Returns="@(Commands)">
    <!-- ... -->
  </Target>
```

### <a name="message-an-error-occurred-while-running-command-name-failed-to-get-command-target-name-from-project"></a>メッセージ:"\<command name> の実行中にエラーが発生しました。 プロジェクトからコマンド \<target-name> を取得できませんでした"

`<Target>` または `<CreatePythonCommandItem>` 要素の内容が正しくないことを示します。 次のような理由が考えられます。

- 必須の `Target` 属性が空です。
- 必須の `TargetType` 属性が空か、認識されない値を含みます。
- 必須の `ExecuteIn` 属性が空か、認識されない値を含みます。
- `ErrorRegex` または `WarningRegex` が、`ExecuteIn="output"` を設定しないで指定されています。
- 要素に認識されない属性が存在します。 たとえば、`Arguments` ではなく `Argumnets` (スペル ミス) を使っている可能性があります。

定義されていないプロパティを参照する場合は、属性値を空にすることができます。 たとえば、トークン `$(StartupFile)` を使っていて、スタートアップ ファイルがプロジェクトで定義されていない場合、そのトークンは空の文字列に解決されます。 このような場合は、既定値を定義できます。 たとえば、Bottle、Flask、Django Project テンプレートで定義されている **[サーバーの起動]** および **[デバッグ サーバーの開始]** コマンドは、プロジェクトのプロパティでサーバーのスタートアップ ファイルに別の値が定義されていない場合、既定で *manage.py* になります。

### <a name="visual-studio-stops-responding-and-crashes-when-running-the-command"></a>コマンドを実行すると Visual Studio が応答しなくなりクラッシュする

`ExecuteIn="output"` を指定してコンソール コマンドを実行しようとすると、Visual Studio が出力の解析を試みてクラッシュする場合があります。 代わりに、`ExecuteIn="console"` を使用してください。 ([問題 3682](https://github.com/Microsoft/PTVS/issues/3681) に関する説明を参照してください)

### <a name="executable-command-is-not-recognized-as-an-internal-or-external-command-operable-program-or-batch-file"></a>"<実行可能ファイル コマンド> は、内部コマンドまたは外部コマンド、操作可能なプログラムまたはバッチ ファイルとして認識されていません"

`TargetType="executable"` を使うとき、`Target` の値には、引数を含まないプログラム名 *のみ* を指定する必要があります (例: *python*や *python.exe* のみ)。 引数はすべて `Arguments` 属性に移動します。

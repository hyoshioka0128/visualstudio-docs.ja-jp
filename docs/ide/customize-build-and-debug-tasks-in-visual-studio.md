---
title: tasks.vs.json と launch.vs.json を使用してビルド タスクとデバッグ タスクをカスタマイズする
ms.date: 02/21/2018
ms.topic: conceptual
helpviewer_keywords:
- NMAKE [Visual Studio]
- makefiles [Visual Studio]
- customize codebases [Visual Studio]
- tasks.vs.json file [Visual Studio]
- launch.vs.json file [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ffd0f7378893b52e93480272c73acc2aa413320d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533720"
---
# <a name="customize-build-and-debug-tasks-for-open-folder-development"></a>"フォルダーを開く" の開発のためにビルド タスクとデバッグ タスクをカスタマイズする

Visual Studio は多くのさまざまな言語やコードベースを実行する方法を認識していますが、すべてを認識しているわけではありません。 Visual Studio が実行方法を認識しているコードの場合は、Visual Studio で[コード フォルダーを開いて](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)、追加の構成をせずにすぐに実行できます。

コードベースで Visual Studio が認識できないカスタムのビルド ツールを使用する場合は、Visual Studio でコードを実行およびデバッグするために構成の詳細情報を指定する必要があります。 *ビルド タスク*を定義してコードのビルド方法を Visual Studio に指示します。 1 つ以上のビルド タスクを作成して、そのコードをビルドおよび実行するために言語で必要なすべての項目を指定することができます。 必要な操作をほぼすべて実行できる任意のタスクを作成することもできます。 たとえば、フォルダーの内容を一覧表示したり、ファイルの名前を変更するタスクを作成することができます。

プロジェクトなしのコードベースをカスタマイズするには、以下の *.json* ファイルを使用します。

|ファイル名|目的|
|-|-|
|*tasks.vs.json*|カスタム ビルド コマンドとコンパイラ スイッチ、および任意の (ビルドに関連しない) タスクを指定します。<br>指定するには、**ソリューション エクスプローラー**の右クリック メニュー項目 **[タスクの構成]** を使用します。|
|*launch.vs.json*|デバッグ用のコマンドライン引数を指定します。<br>指定するには、**ソリューション エクスプローラー**の右クリック メニュー項目 **[デバッグ設定と起動設定]** を使用します。|

これらの *.json* ファイルは、コードベースのルート フォルダーの *.vs* という非表示のフォルダーにあります。 **ソリューション エクスプローラー**でファイルまたはフォルダーに対して **[タスクの構成]** または **[デバッグ設定と起動設定]** を選択すると、必要に応じて *tasks.vs.json* および *launch.vs.json* ファイルが作成されます。 これらの *.json* ファイルは、一般的にソース管理にチェックインする必要がないため、非表示になっています。 ただし、ソース管理にチェックインできるようにするには、ファイルをコードベースのルートにドラッグして表示します。

> [!TIP]
> Visual Studio で非表示ファイルを表示するには、**ソリューション エクスプローラー**のツール バーで **[すべてのファイルを表示]** ボタンを選択します。

## <a name="define-tasks-with-tasksvsjson"></a>tasks.vs.json でタスクを定義する

IDE でタスクとして直接実行することで、現在のワークスペースにあるファイルに対してビルド スクリプトやその他の外部操作を自動化できます。 ファイルまたはフォルダーを右クリックし、 **[タスクの構成]** を選択すると、新しいタスクを構成できます。

![[タスクの構成] メニュー](../ide/media/customize-configure-tasks-menu.png)

*.vs* フォルダーに *tasks.vs.json* ファイルを作成します (または開きます)。 このファイルでビルド タスクまたは任意のタスクを定義し、**ソリューション エクスプローラー**の右クリック メニューから指定した名前を使用して呼び出すことができます。

カスタム タスクは、個々のファイル、または特定の種類のすべてのファイルに追加できます。 たとえば、NuGet パッケージ ファイルを "パッケージの復元" タスクを含むように構成するか、すべてのソース ファイルをスタティック分析タスク (すべての *.js* ファイルのリンターなど) を含むように構成することができます。

### <a name="define-custom-build-tasks"></a>カスタム ビルド タスクの定義

Visual Studio で認識できないカスタム ビルド ツールをコードベースで使用している場合、Visual Studio でコードを実行してデバッグするには、いくつかの構成手順を完了する必要があります。 Visual Studio には*ビルド タスク*が用意されています。ビルド タスクを使用して、コードのビルド、リビルド、およびクリーンの方法を Visual Studio に指示できます。 *tasks.vs.json* ビルド タスク ファイルは、Visual Studio の内部開発ループを、コードベースによって使用されるカスタム ビルド ツールに組み込みます。

*hello.cs* という単一の C# ファイルで構成されるコードベースについて考えてみましょう。 このようなコードベースの *makefile* の例を次に示します。

<!-- markdownlint-disable MD010 -->
```makefile
build: directory hello.exe

hello.exe: hello.cs
    csc -debug hello.cs /out:bin\hello.exe

clean:
    del bin\hello.exe bin\hello.pdb

rebuild: clean build

directory: bin

bin:
    md bin
```
<!-- markdownlint-enable MD010 -->

ビルド、クリーン、リビルドのターゲットを含む *makefile* の場合、次の *tasks.vs.json* ファイルを定義できます。 このファイルには、NMAKE をビルド ツールとして使用してコードベースのビルド、リビルド、およびクリーンを行うための 3 つのビルド タスクが含まれています。

```json
{
  "version": "0.2.1",
  "outDir": "\"${workspaceRoot}\\bin\"",
  "tasks": [
    {
      "taskName": "makefile-build",
      "appliesTo": "makefile",
      "type": "launch",
      "contextType": "build",
      "command": "nmake",
      "args": [ "build" ],
      "envVars": {
        "VSCMD_START_DIR": "\"${workspaceRoot}\""
      }
    },
    {
      "taskName": "makefile-clean",
      "appliesTo": "makefile",
      "type": "launch",
      "contextType": "clean",
      "command": "nmake",
      "args": [ "clean" ],
      "envVars": {
        "VSCMD_START_DIR": "\"${workspaceRoot}\""
      }
    },
    {
      "taskName": "makefile-rebuild",
      "appliesTo": "makefile",
      "type": "launch",
      "contextType": "rebuild",
      "command": "nmake",
      "args": [ "rebuild" ],
      "envVars": {
        "VSCMD_START_DIR": "\"${workspaceRoot}\""
      }
    }
  ]
}
```

*tasks.vs.json* でビルド タスクを定義すると、**ソリューション エクスプローラー**の対応するファイルに追加の右クリック メニュー (コンテキスト メニュー) 項目が追加されます。 この例では、*makefile* ファイルのコンテキスト メニューに、"ビルド"、"リビルド"、"クリーン" オプションが追加されます。

![[ビルド]、[リビルド]、[クリーン] がある makefile のコンテキスト メニュー](media/customize-build-rebuild-clean.png)

> [!NOTE]
> `contextType` 設定に応じて、コンテキスト メニューの **[タスクの構成]** コマンドの下にこれらのコマンドが表示されます。 [ビルド]、[リビルド]、[クリーン] はビルド コマンドなので、コンテキスト メニューの途中のビルド セクションに表示されます。

これらのオプションのいずれかを選択すると、タスクが実行されます。 出力は **[出力]** ウィンドウに表示され、ビルド エラーは **[エラー一覧]** に表示されます。

### <a name="define-arbitrary-tasks"></a>任意のタスクを定義する

任意のタスクを *tasks.vs.json* ファイルで定義して、必要なタスクだけを実行できます。 たとえば、 **[出力]** ウィンドウに現在選択されているファイルの名前を表示したり、指定したディレクトリ内のファイルを一覧表示したりするタスクを定義できます。

単一のタスクを定義する *tasks.vs.json* ファイルの例を次に示します。 このファイルが呼び出されると、タスクによって現在選択されている *.js* ファイルのファイル名が表示されます。

```json
{
  "version": "0.2.1",
  "tasks": [
    {
      "taskName": "Echo filename",
      "appliesTo": "*.js",
      "type": "default",
      "command": "${env.COMSPEC}",
      "args": [ "echo ${file}" ]
    }
  ]
}
```

- 右クリック メニューに表示される名前を `taskName` に指定します。
- コマンドを実行できるファイルを `appliesTo` に指定します。
- 呼び出すコマンドを `command` プロパティに指定します。 この例では、環境変数 `COMSPEC` を使用して、コマンド ライン インタープリター (通常は *cmd.exe*) を指定します。
- 呼び出されたコマンドに渡される引数を `args` プロパティに指定します。
- `${file}` マクロは、**ソリューション エクスプローラー**で選択したファイルを取得します。

*tasks.vs.json* を保存した後に、フォルダー内の *.js* ファイルを右クリックし、 **[Echo filename]** を選択します。 **[出力]** ウィンドウにファイル名が表示されます。

> [!NOTE]
> コードベースに *tasks.vs.json* ファイルが含まれていない場合は、**ソリューション エクスプローラー**でファイルの右クリック メニューまたはコンテキスト メニューから **[タスクの構成]** を選択して作成できます。

次の例では、*bin* ディレクトリのファイルとサブフォルダーを一覧表示するタスクを定義しています。

```json
{
  "version": "0.2.1",
  "outDir": "\"${workspaceRoot}\\bin\"",
  "tasks": [
    {
      "taskName": "List Outputs",
      "appliesTo": "*",
      "type": "default",
      "command": "${env.COMSPEC}",
      "args": [ "dir ${outDir}" ]
    }
  ]
}
```

- `${outDir}` は、`tasks` ブロックの前に最初に定義されているカスタム マクロです。 このマクロは `args` プロパティで呼び出されます。

このタスクはすべてのファイルに適用されます。 **ソリューション エクスプローラー** で任意のファイルのコンテキスト メニューを開くと、タスク名の **[List Outputs]** がメニューの下部に表示されます。 **[List Outputs]** を選択すると、*bin* ディレクトリの内容が Visual Studio の **[出力]** ウィンドウに表示されます。

![コンテキスト メニューの任意のタスク](../ide/media/customize-arbitrary-task-menu.png)

### <a name="settings-scope"></a>設定スコープ

コードベースのルートとサブディレクトリに複数の *tasks.vs.json* ファイルが存在する可能性があります。 この設計により、異なるサブディレクトリにあるコードベースで異なる動作を実行する柔軟な処理が可能になります。 Visual Studio は、次のようにファイルに優先順位を付け、コードベース全体の設定の集計またはオーバーライドを行います。

- ルート フォルダーの *.vs* ディレクトリにある設定ファイル。
- 設定が計算されているディレクトリ。
- 現在のディレクトリの親ディレクトリ (ルート ディレクトリまでのすべてのディレクトリ) です。
- ルート ディレクトリの設定ファイル。

これらの集計ルールは、*tasks.vs.json* に適用されます。 他のファイルの設定を集計する方法については、この記事の該当するファイルのセクションを参照してください。

### <a name="properties-for-tasksvsjson"></a>tasks.vs.json のプロパティ

このセクションでは、*tasks.vs.json* で指定できる主なプロパティについて説明します。

#### <a name="appliesto"></a>AppliesTo

任意のファイルまたはフォルダーのタスクを作成するには、`appliesTo` フィールドに名前を指定します (例:`"appliesTo": "hello.js"`)。 次のファイル マスクを値として使用できます。

|ファイル マスク|説明|
|-|-|
|`"*"`| タスクは、ワークスペース内のすべてのファイルとフォルダーで使用できます|
|`"*/"`| タスクは、ワークスペース内のすべてのフォルダーで使用できます|
|`"*.js"`| タスクは、ワークスペース内の拡張子が *.js* のすべてのファイルで使用できます|
|`"/*.js"`| タスクは、ワークスペースのルートにある拡張子が *.js* のすべてのファイルで使用できます|
|`"src/*/"`| タスクは、*src* フォルダーのすべてのサブフォルダーで使用できます|
|`"makefile"`| タスクは、ワークスペース内のすべての *makefile* ファイルで使用できます|
|`"/makefile"`| タスクは、ワークスペースのルートにある *makefile* にのみ使用できます|

#### <a name="macros-for-tasksvsjson"></a>tasks.vs.json のマクロ

|マクロ|説明|
|-|-|
|`${env.<VARIABLE>}`| 開発者コマンド プロンプトに設定されている環境変数 (たとえば、${env.PATH}、${env.COMSPEC} など) を指定します。 詳細については、「[Visual Studio 用開発者コマンド プロンプト](/dotnet/framework/tools/developer-command-prompt-for-vs)」を参照してください。|
|`${workspaceRoot}`| ワークスペース フォルダーの完全なパス (例: *C:\sources\hello*)|
|`${file}`| このタスクの実行対象として選択されたファイルまたはフォルダーの完全なパス (例: *C:\sources\hello\src\hello.js*)|
|`${relativeFile}`| ファイルまたはフォルダーの相対パス (例: *src\hello.js*)|
|`${fileBasename}`| パスまたは拡張子のないファイル名 (例: *hello*)|
|`${fileDirname}`| ファイル名を除いたファイルの完全なパス (例: *C:\sources\hello\src*)|
|`${fileExtname}`| 選択したファイルの拡張子 (例: *.js*)|

## <a name="configure-debugging-with-launchvsjson"></a>launch.vs.json によるデバッグの構成

デバッグ用に CMake プロジェクトを構成するには、「[CMake デバッグ セッションを構成する](/cpp/build/configure-cmake-debugging-sessions)」を参照してください。

1. デバッグ用にコードベースを構成するには、**ソリューション エクスプローラー**で、実行可能ファイルの右クリック メニューまたはコンテキスト メニューから **[デバッグ設定と起動設定]** メニュー項目を選択します。

   ![[デバッグ設定と起動設定] コンテキスト メニュー](media/customize-debug-launch-menu.png)

1. **[デバッガーの選択]** ダイアログ ボックスでオプションを選択し、 **[選択]** ボタンを選択します。

   ![[デバッガーの選択] ダイアログ ボックス](media/customize-select-a-debugger.png)

   *launch.vs.json* ファイルがまだ存在しない場合は作成されます。

   ```json
   {
     "version": "0.2.1",
     "defaults": {},
     "configurations": [
       {
         "type": "default",
         "project": "bin\\hello.exe",
         "name": "hello.exe"
       }
     ]
   }
   ```

1. 次に、**ソリューション エクスプローラー**で実行可能ファイルを右クリックし、 **[スタートアップ アイテムとして設定]** とを選択します。

   実行可能ファイルはコードベースのスタート アップ アイテムとして指定され、デバッグの **[開始]** ボタンのタイトルには実行ファイルの名前が反映されます。

   ![カスタマイズされた [開始] ボタン](media/customize-start-button.png)

   **F5** キーを押すとデバッガーが起動し、ブレークポイントが既に設定されている場合は、そこで停止します。 使い慣れたデバッガー ウィンドウのすべての機能を利用できます。

   > [!IMPORTANT]
   > C++ の "フォルダーを開く" プロジェクトのカスタム ビルドおよびデバッグ タスクの詳細については、「[Visual Studio での C++ ビルド システムの [フォルダーを開く] のサポート](/cpp/build/open-folder-projects-cpp)」を参照してください。

### <a name="specify-arguments-for-debugging"></a>デバッグの引数を指定する

デバッグのために渡すコマンドライン引数は、*launch.vs.json* ファイルで指定できます。 次の例に示すように、引数を `args` 配列に追加します。

```json
{
  "version": "0.2.1",
  "defaults": {},
  "configurations": [
    {
      "type": "default",
      "project": "bin\\hello.exe",
      "name": "hello.exe"
    },
    {
      "type": "default",
      "project": "bin\\hello.exe",
      "name": "hello.exe a1",
      "args": [ "a1" ]
    }
  ]
}
```

このファイルを保存すると、[デバッグ ターゲット] ドロップダウン リストに新しい構成の名前が表示され、名前を選択してデバッガーを起動できるようになります。 必要に応じて、任意の数のデバッグ構成を作成できます。

![デバッグ構成のドロップダウン リスト](media/customize-debug-configurations.png)

> [!NOTE]
> *launch.vs.json* の `configurations` 配列プロパティは、コードベースのルート ディレクトリと *.vs* ディレクトリという 2 つのディレクトリから読み取られます。 競合がある場合は、 *.vs\launch.vs.json* の値が優先されます。

## <a name="additional-settings-files"></a>その他の設定ファイル

このトピックで説明されている 3 つの *.json* ファイルに加えて、Visual Studio では、コードベースに存在するその他のファイルから設定が読み取られます。

### <a name="vscodesettingsjson"></a>.vscode\settings.json

*.vscode* というディレクトリにファイルがある場合、*settings.json* というファイルから制限付きの設定が読み取られます。 この機能は、Visual Studio Code で以前に開発されたコードベース用に用意されています。 現在、 *.vscode\settings.json* から読み取られる唯一の設定は `files.exclude` です。ソリューション エクスプローラーおよび一部の検索ツールで視覚的にファイルがフィルター処理されます。

コードベースには、任意の数の *.vscode\settings.json* ファイルを配置できます。 このファイルから読み取られた設定は、 *.vscode* の親ディレクトリとそのすべてのサブディレクトリに適用されます。

### <a name="gitignore"></a>.gitignore

*.gitignore* ファイルは、無視するファイル (チェックインしたくないファイルとディレクトリ) を Git に伝えるために使用されます。 通常、 *.gitignore* ファイルはコードベースの一部として組み込まれているため、設定をコードベースのすべての開発者と共有することができます。 Visual Studio は *.gitignore* ファイルのパターンを読み取り、視覚的に、また一部の検索ツールから項目をフィルター処理します。

*.gitignore* ファイルから読み取られた設定は、親ディレクトリとすべてのサブディレクトリに適用されます。

## <a name="see-also"></a>関連項目

- [プロジェクトまたはソリューションを使用せずにコードを開発する](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)
- [C++ でフォルダーのプロジェクトを開く](/cpp/build/open-folder-projects-cpp)
- [C++ の CMake プロジェクト](/cpp/build/cmake-projects-in-visual-studio)
- [NMAKE リファレンス](/cpp/build/reference/nmake-reference)
- [コード エディターの機能](../ide/writing-code-in-the-code-and-text-editor.md)

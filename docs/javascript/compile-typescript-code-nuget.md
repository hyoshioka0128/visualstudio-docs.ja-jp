---
title: NuGet を使用した TypeScript コードのコンパイルとビルド
description: NuGet パッケージを使用し、Visual Studio プロジェクトに Typescript サポートを追加する方法について説明します。
ms.date: 7/23/2020
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 929c17c9cbd2a0987bebca02c70b3b751c19fc9a
ms.sourcegitcommit: d577818d3d8e365baa55c6108fa8159c46ed8b43
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2021
ms.locfileid: "97846821"
---
# <a name="compile-typescript-code-aspnet-core"></a>TypeScript コードのコンパイル (ASP.NET Core)

TypeScript SDK を使用して、プロジェクトに TypeScript サポートを追加することができます。これは Visual Studio インストーラーで既定で使用できます。または NuGet パッケージを使用します。 プロジェクトが Visual Studio 2019 で開発されている場合は、TypeScript NuGet を使用することをお勧めします。これにより、さまざまなプラットフォームや環境の間で移植性が向上します。

ASP.NET Core プロジェクトの場合、NuGet パッケージの一般的な使用方法の 1 つは、.NET Core CLI を使用して TypeScript をコンパイルすることです。 TypeScript SDK インストールからビルド ターゲットをインポートするように、プロジェクト ファイルを手動で編集しない限り、NuGet パッケージが `dotnet build` や `dotnet publish` などの .NET Core CLI コマンドを使用して TypeScript コンパイルを有効にする唯一の方法です。 また、ASP.NET Core および TypeScript との [MSBuild 統合](https://www.staging-typescript.org/docs/handbook/compiler-options-in-msbuild.html)のために、npm パッケージよりも NuGet パッケージを選択します。

## <a name="add-typescript-support-with-nuget"></a>NuGet で TypeScript サポートを追加する

[TypeScript NuGet パッケージ](https://www.nuget.org/packages/Microsoft.TypeScript.MSBuild)によって、TypeScript サポートを追加できます。 TypeScript 3.2 以降の NuGet パッケージがプロジェクトにインストールされているときは、対応するバージョンの TypeScript 言語サービスがエディターに読み込まれます。

Visual Studio がインストールされている場合は、バンドルされている node.exe が Visual Studio によって自動的に選択されます。 Node.js をインストールしていない場合は、[Node.js](https://nodejs.org/en/download/) Web サイトから LTS バージョンをインストールすることをお勧めします。

1. Visual Studio で ASP.NET Core プロジェクトを開きます。

1. ソリューション エクスプローラー (右ウィンドウ) で、 プロジェクト ノードを右クリックして **[NuGet パッケージの管理]** を選択します。 **[参照]** タブで **[Microsoft.TypeScript.MSBuild]** を検索し、右側にある **[インストール]** をクリックしてパッケージをインストールします。

   ![NuGet パッケージを追加する](../javascript/media/aspnet-core-ts-nuget.png)

   Visual Studio によってソリューション エクスプローラーの **[依存関係]** ノードの下に NuGet パッケージが追加されます。 次のパッケージ参照が *.csproj ファイルに追加されます。

   ```xml
   <PackageReference Include="Microsoft.TypeScript.MSBuild" Version="3.9.7">
      <PrivateAssets>all</PrivateAssets>
      <IncludeAssets>runtime; build; native; contentfiles; analyzers; buildtransitive</IncludeAssets>
   </PackageReference>
   ```

1. プロジェクト ノードを右クリックし、 **[追加] > [新しいアイテム]** の順に選択します。 **[TypeScript JSON 構成ファイル]** を選択し、 **[追加]** をクリックします。

   Visual Studio によって *tsconfig.json* ファイルがプロジェクト ルートに追加されます。 このファイルを使用して、TypeScript コンパイラの[オプションを構成](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)することができます。

1. *tsconfig.json* を開き、更新して必要なコンパイラ オプションを設定します。

   シンプルな *tsconfig.json* ファイルの例を次に示します。

   ```json
   {
     "compilerOptions": {
       "noImplicitAny": false,
       "noEmitOnError": true,
       "removeComments": false,
       "sourceMap": true,
       "target": "es5",
       "outDir": "wwwroot/js"
     },
     "include": [
       "scripts/**/*"
     ]
   }
   ```

   この例では、次のように記述されています。
   - *include* によって、TypeScript (*.ts) ファイルを検索する場所をコンパイラに指示します。
   - *outDir* オプションを使用して、TypeScript コンパイラによってトランスパイルされるプレーンな JavaScript ファイルの出力フォルダーを指定します。
   - *sourceMap* オプションによって、コンパイラが *sourceMap* ファイルを生成するかどうかを指定します。

   前述の構成では、TypeScript の構成に関する基本事項のみが説明されています。 他のオプションについては、「[tsconfig.json](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)」を参照してください。

### <a name="build-the-application"></a>アプリケーションのビルド

1. TypeScript ( *.ts*) ファイルまたは TypeScript JSX ( *.tsx*) ファイルをプロジェクトに追加してから、TypeScript コードを追加します。 TypeScript のシンプルな例として、次をお使いください。

   ```typescript
   let message: string = 'Hello World';
   console.log(message);
   ```

1. 非 SDK スタイルの古いプロジェクトを使用している場合は、「[既定のインポートを削除する](#remove-default-imports)」の手順に従ってください。

1. **[ビルド] > [ソリューションのビルド]** の順に選択します。

   アプリは実行時に自動的にビルドされますが、ここではビルド処理中に何が起きるのかを確認します。

   ソース マップを生成した場合は、*outDir* オプションで指定したフォルダーを開くと、生成された *.js ファイルと生成された *js.map ファイルが見つかります。

   ソース マップ ファイルはデバッグで必要となります。

1. プロジェクトを保存するたびにコンパイルする場合は、*.tsconfig で *compileOnSave* オプションを使用します。

   ```json
   ```{
      "compileOnSave":  true,
      "compilerOptions": {
      }
   }
   ```

タスク ランナーで gulp を使用してアプリをビルドする例については、[ASP.NET Core と TypeScript](https://www.typescriptlang.org/docs/handbook/asp-net-core.html) に関するページをご覧ください。

Visual Studio で、想定したバージョンとは異なるバージョンの Node.js またはサード パーティ製ツールが使用される問題が発生した場合は、Visual Studio で使用するパスの設定が必要になることがあります。 **[ツール]**  >  **[オプション]** を選択します。 **[プロジェクトとソリューション]** で、 **[Web パッケージ管理]**  >  **[外部 Web ツール]** を選択します。

### <a name="run-the-application"></a>アプリケーションの実行

アプリをコンパイルした後に実行する手順については、[初めての Node.js アプリの作成](/visualstudio/ide/quickstart-nodejs?toc=%2Fvisualstudio%2Fjavascript%2Ftoc.json#run-the-application)に関するページを参照してください。

### <a name="nuget-package-structure-details"></a>NuGet パッケージ構造の詳細

`Microsoft.TypeScript.MSBuild.nupkg` には 2 つの主要なフォルダーがあります。

- *build* フォルダー

    このフォルダーには 2 つのファイルが配置されます。
    両方ともエントリ ポイントであり、1 つはメインの TypeScript ターゲット ファイル用、もう 1 つは props ファイル用です。

    1. *Microsoft.TypeScript.MSBuild.targets*

        このファイルによって、*tools* フォルダーから *Microsoft.TypeScript.targets* をインポートする前に、実行時プラットフォームを指定する変数 (*TypeScript.Tasks.dll* へのパスなど) を設定できます。

    2. *Microsoft.TypeScript.MSBuild.props*

        このファイルによって、*tools* フォルダーから *Microsoft.TypeScript.Default.props* をインポートし、NuGet を通じてビルドが開始されたことを示すプロパティを設定できます。

- *tools* フォルダー

    2\.3 より前のパッケージ バージョンには、tsc フォルダーだけが含まれています。 *Microsoft.TypeScript.targets* と *TypeScript.Tasks.dll* は、ルート レベルに配置されます。

    2\.3 以降のパッケージ バージョンでは、ルート レベルに `Microsoft.TypeScript.targets` と `Microsoft.TypeScript.Default.props` が含まれています。 これらのファイルの詳細については、[MSBuild の構成](https://www.typescriptlang.org/docs/handbook/compiler-options-in-msbuild.html)に関するページをご覧ください。

    さらに、このフォルダーには次の 3 つのサブフォルダーがあります。

    1. *net45*

        このフォルダーには、`TypeScript.Tasks.dll` と、それが依存するその他の DLL が含まれています。
        Windows プラットフォームでプロジェクトをビルドする場合、MSBuild によってこのフォルダーの DLL が使用されます。

    2. *netstandard1.3*

        このフォルダーには、Windows 以外のコンピューターでプロジェクトをビルドするときに使用される、別のバージョンの `TypeScript.Tasks.dll` が含まれています。

    3. *tsc*

        このフォルダーには、`tsc.js`、`tsserver.js`、およびこれらをノード スクリプトとして実行するために必要なすべての依存関係ファイルが含まれています。

        > [!NOTE]
        > Visual Studio がインストールされている場合は、バンドルされている *node.exe* が自動的に選択されます。 それ以外の場合は、コンピューターに Node.js をインストールする必要があります。

        3\.1 より前のバージョンには、コンパイルを実行するための `tsc.exe` 実行可能ファイルが含まれていました。 `node.exe` の使用を優先するため、これはバージョン 3.1 で削除されました。

### <a name="remove-default-imports"></a>既定のインポートを削除する

[非 SDK スタイルの形式](https://docs.microsoft.com/nuget/resources/check-project-format)を使用する以前の ASP.NET Core プロジェクトでは、一部のプロジェクト ファイルの要素を削除する必要がある場合があります。

プロジェクトの MSBuild サポートに NuGet パッケージを使用している場合、プロジェクト ファイルで `Microsoft.TypeScript.Default.props` または `Microsoft.TypeScript.targets` をインポートしないでください。 ファイルは NuGet パッケージによってインポートされるため、個別に含めると、意図しない動作が発生する可能性があります。

1. プロジェクトを右クリックして **[プロジェクトのアンロード]** を選択します。

1. プロジェクトを右クリックし、 **[\<*project file name*\> の編集]** を選択します。

   プロジェクト ファイルが開きます。

1. `Microsoft.TypeScript.Default.props` および `Microsoft.TypeScript.targets` への参照を削除します。

   削除するインポートは、次のようになります。

   ```xml
   <Import
      Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\TypeScript\Microsoft.TypeScript.Default.props"
      Condition="Exists('$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\TypeScript\Microsoft.TypeScript.Default.props')" />

   <Import
      Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\TypeScript\Microsoft.TypeScript.targets"
      Condition="Exists('$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\TypeScript\Microsoft.TypeScript.targets')" />
   ```

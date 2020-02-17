---
title: JavaScript または TypeScript のアプリをデバッグする
description: Visual Studio では、Visual Studio での JavaScript アプリと TypeScript アプリのデバッグをサポートします
ms.date: 11/01/2019
ms.topic: conceptual
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 3f8fa8fcd859a7464d471972689728dc556a79bd
ms.sourcegitcommit: 0d8488329263cc0743a89d43f6de863028e982ff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/06/2020
ms.locfileid: "75678975"
---
# <a name="debug-a-javascript-or-typescript-app-in-visual-studio"></a>Visual Studio で JavaScript アプリまたは TypeScript アプリをデバッグする

Visual Studio を使用して、JavaScript および TypeScript のコードをデバッグすることができます。 ブレークポイントを設定してそこにヒットし、変数を検査し、呼び出し履歴を表示し、その他のデバッグ機能を使用することができます。

> [!TIP]
> Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads/) ページに移動し、無料試用版をインストールしてください。 実行するアプリ開発の種類によっては、Visual Studio と共に **Node.js ワークロード**をインストールする必要がある場合があります。

## <a name="debug-server-side-script"></a>サーバー側のスクリプトをデバッグする

1. Visual Studio でプロジェクトを開いた状態で、サーバー側の JavaScript ファイル (*server.js* など) を開き、左の余白をクリックしてブレークポイントを設定します。

    ![ブレークポイントの設定](../javascript/media/tutorial-nodejs-react-set-breakpoint.png)

    ブレークポイントは、信頼できるデバッグの最も基本的で重要な機能です。 ブレークポイントは、Visual Studio が実行コードを中断する場所を示します。これにより、変数の値またはメモリの動作を確認したり、コードの分岐が実行されるかどうかを確認したりすることができます。

1. アプリを実行するには、**F5** キーを押します ( **[デバッグ]**  >  **[デバッグの開始]** )。

    設定したブレークポイントでデバッガーが一時停止します (現在のステートメントは黄色でマークされます)。 ここで、 **[ローカル]** ウィンドウや **[ウォッチ]** ウィンドウなどのデバッガー ウィンドウを使って、現在スコープ内にある変数をマウスでポイントすることにより、アプリの状態を調べることができます。

1. アプリを続行するには **F5** キーを押します。

1. Chrome の開発者ツールまたは F12 ツールを使う場合は、**F12** キーを押します。 これらのツールでは、DOM を調べたり、JavaScript コンソールを使ってアプリを操作したりできます。

## <a name="debug-client-side-script"></a>クライアント側のスクリプトをデバッグする

::: moniker range=">=vs-2019"
Visual Studio では、Chrome および Microsoft Edge (Chromium) のみのクライアント側デバッグ サポートが提供されます。 一部のシナリオでは、デバッガーで自動的に、HTML ファイルの埋め込みスクリプトおよび JavaScript や TypeScript コードのブレークポイントにヒットします。 ASP.NET アプリでのクライアント側スクリプトのデバッグについては、ブログ記事「[Microsoft Edge での JavaScript のデバッグ](https://devblogs.microsoft.com/visualstudio/debug-javascript-in-microsoft-edge-from-visual-studio/)」と、[Google Chrome に関するこちらの記事](https://devblogs.microsoft.com/aspnet/client-side-debugging-of-asp-net-projects-in-google-chrome)を参照してください。 ASP.NET Core での TypeScript のデバッグについては、[TypeScript を使用した ASP.NET Core アプリの作成](tutorial-aspnet-with-typescript.md)に関する記事も参照してください。
::: moniker-end
::: moniker range="vs-2017"
Visual Studio では、Chrome および Internet Explorer のみのクライアント側デバッグ サポートが提供されます。 一部のシナリオでは、デバッガーで自動的に、HTML ファイルの埋め込みスクリプトおよび JavaScript や TypeScript コードのブレークポイントにヒットします。 ASP.NET アプリでのクライアント側スクリプトのデバッグについては、ブログ投稿「[Google Chrome での ASP.NET プロジェクトのクライアント側デバッグ](https://devblogs.microsoft.com/aspnet/client-side-debugging-of-asp-net-projects-in-google-chrome/)」を参照してください。
::: moniker-end

ASP.NET 以外のアプリケーションについては、ここで説明する手順に従ってください。

### <a name="prepare-your-app-for-debugging"></a>デバッグ用にアプリを準備する

TypeScript や Babel などのトランスパイラによってソースが縮小または作成されている場合、最適なデバッグ エクスペリエンスを得るために、[ソース マップ](#generate_source_maps)を使用する必要があります。 ソース マップを使用しなくても、実行中のクライアント側スクリプトにデバッガーをアタッチすることはできます。 しかし、ブレークポイントの設定やヒットが可能なのは、元のソース ファイルではなく、縮小またはトランスパイルされたファイルでのみとなります。 たとえば、Vue.js アプリでは、縮小されたスクリプトは文字列として `eval` ステートメントに渡されます。ソース マップを使用しない限り、Visual Studio デバッガーを効果的に使って、このコードをステップ実行する方法はありません。 複雑なデバッグ シナリオでは、代わりに Chrome の開発者ツールまたは Microsoft Edge の F12 ツールを使用する場合もあります。

ソース マップを生成する方法については、「[デバッグ用のソース マップを生成する](#generate_source_maps)」を参照してください。

### <a name="prepare_the_browser_for_debugging"></a>デバッグのためにブラウザーを準備する

::: moniker range=">=vs-2019"
このシナリオでは、現在 IDE 上で **Microsoft Edge Beta** という名前になっている Microsoft Edge (Chromium)、または Chrome のいずれかを使用します。
::: moniker-end
::: moniker range="vs-2017"
このシナリオでは、Chrome を使用します。
::: moniker-end

1. ターゲット ブラウザーのすべてのウィンドウを閉じます。

   そのブラウザーをデバッグを有効にした状態で開くことが、その他のブラウザー インスタンスによって妨げられる可能性があります (ブラウザーの拡張機能が実行され、フル デバッグ モードが阻止されている場合があります。そのため、タスク マネージャーを開き、Chrome の予期しないインスタンスを見つけることが必要な場合があります)。

   ::: moniker range=">=vs-2019"
   Microsoft Edge (Chromium) の場合は、Chrome のすべてのインスタンスもシャットダウンします。 どちらのブラウザーでも Chromium コードベースが使用されているため、これによって最適な結果が得られます。
   ::: moniker-end

2. デバッグが有効な状態でブラウザーを起動します。

    ::: moniker range=">=vs-2019"
    Visual Studio 2019 以降では、ブラウザーの起動時に `--remote-debugging-port=9222` フラグを設定することもできます。 **[デバッグ]** ツール バーから **[ブラウザーの選択]** を選択し、 **[追加]** を選択した後、 **[引数]** フィールドにフラグを設定します。 ブラウザーに **Microsoft Edge でのデバッグ**や **Chrome でのデバッグ**などの別のフレンドリ名を使用します。 詳細については、[リリース ノート](/visualstudio/releases/2019/release-notes-v16.2)を参照してください。

    ![ブラウザーをデバッグが有効な状態で開くように設定する](../javascript/media/tutorial-nodejs-react-edge-with-debugging.png)

    別の方法として、Windows の **[スタート]** ボタンから **[ファイル名を指定して実行]** コマンドを開き (右クリックして **[ファイル名を指定して実行]** を選択)、次のコマンドを入力します。

    `msedge --remote-debugging-port=9222`

    または、

    `chrome.exe --remote-debugging-port=9222`
    ::: moniker-end

    ::: moniker range="vs-2017"
    Windows の **[スタート]** ボタンから **[ファイル名を指定して実行]** コマンドを開き (右クリックして **[ファイル名を指定して実行]** を選択)、次のコマンドを入力します。

    `chrome.exe --remote-debugging-port=9222`
    ::: moniker-end

    これにより、デバッグが有効な状態でブラウザーが起動します。

    アプリはまだ実行されていないため、空のブラウザー ページが表示されます。

### <a name="attach-the-debugger-to-client-side-script"></a>クライアント側スクリプトにデバッガーをアタッチする

クライアント側のコードに Visual Studio からデバッガーをアタッチしてブレークポイントをヒットさせるには、デバッガーが正しいプロセスを識別できるように手助けする必要があります。 ここではその方法の 1 つを示します。

1. Visual Studio に切り替えて、JavaScript ファイル、TypeScript ファイル、JSX ファイルなどのソース コードにブレークポイントを設定します。 (return ステートメントや var 宣言など、ブレークポイントが許可されるコード行にブレークポイントを設定します)。

    ![ブレークポイントの設定](../javascript/media/tutorial-nodejs-react-set-breakpoint-client-code.png)

    トランスパイルされたファイル内の特定のコードを検索するには、**Ctrl**+**F** キー ( **[編集]**  >  **[検索と置換]**  >  **[クイック検索]** ) を使用します。

    クライアント側コードの場合、TypeScript ファイル、 *.vue*、または JSX ファイル内のブレークポイントをヒットさせるには、通常、[ソース マップ](#generate_source_maps)を使用する必要があります。 ソース マップは、Visual Studio でのデバッグをサポートするように正しく構成されている必要があります。

2. Visual Studio でデバッグ ターゲットとして目的のブラウザーを選択し、次に **Ctrl**+**F5** キーを押して ( **[デバッグ]**  >  **[デバッグなしで開始]** )、ブラウザーでアプリを実行します。

    ::: moniker range=">=vs-2019"
    フレンドリ名を使用してブラウザー構成を作成した場合は、それをデバッグ ターゲットとして選択します。
    ::: moniker-end

    アプリがブラウザーの新しいタブで開きます。

3. **[デバッグ]**  >  **[プロセスにアタッチ]** の順に選びます。

    > [!TIP]
    > Visual Studio 2017 以降では、以上の手順に従って初めてプロセスにアタッチした後は、 **[デバッグ]**  >  **[プロセスに再アタッチする]** を選ぶことで、同じプロセスにすぐに再アタッチできます。

4. **[プロセスにアタッチ]** ダイアログ ボックスで、アタッチできるブラウザー インスタンスのフィルター処理された一覧を取得します。
    ::: moniker range=">=vs-2019"
    Visual Studio 2019 では、 **[アタッチ先]** フィールドでターゲット ブラウザー用の適切なデバッガーとして **JavaScript (Chrome)** または **JavaScript (Microsoft Edge - Chromium)** を選び、フィルター ボックスに「**chrome**」または「**edge**」と入力して検索結果をフィルター処理します。
    ::: moniker-end
    ::: moniker range="vs-2017"
    Visual Studio 2017 では、 **[アタッチ先]** フィールドで **[WebKit code]\(WebKit コード\)** を選び、フィルター ボックスに「**chrome**」と入力して検索結果をフィルター処理します。
    ::: moniker-end

5. 正しいホスト ポート (この例では localhost) のブラウザー プロセスを選び、 **[アタッチ]** を選択します。

    ポート (1337 など) も **[タイトル]** フィールドに表示され、適切なブラウザー インスタンスを選択するのに役立ちます。

    ::: moniker range=">=vs-2019"
    Microsoft Edge (Chromium) ブラウザーの場合の例を次に示します。

    ![プロセスにアタッチする](../javascript/media/tutorial-nodejs-react-attach-to-process-edge.png)
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![プロセスにアタッチする](../javascript/media/tutorial-nodejs-react-attach-to-process.png)

    Visual Studio で DOM Explorer と JavaScript コンソールが開けば、デバッガーが正しくアタッチしたことがわかります。 これらのデバッグ ツールは、Chrome の開発者ツールや Microsoft Edge の F12 ツールに似ています。
    ::: moniker-end

    > [!TIP]
    > デバッガーがアタッチされず、"デバッグ アダプターを起動できませんでした" または "プロセスにアタッチできません。 現在の状態での操作は無効です" というメッセージが表示される場合、ターゲット ブラウザーをデバッグ モードで開始する前に、Windows タスク マネージャーを使用してそのブラウザーのすべてのインスタンスを閉じます。 ブラウザーの拡張機能が実行され、フル デバッグ モードが阻止されている場合があります。

6. ブレークポイントを設定したコードは既に実行しているので、ブラウザーのページを更新します。 必要に応じて、ブレークポイントを設定したコードを実行するためのアクションを実行します。

    デバッガーで一時停止している間に、変数をマウスでポイントし、デバッガー ウィンドウを使って、アプリの状態を確認できます。 コードをステップ実行することにより (**F5**、**F10**、**F11**)、デバッガーを進めることができます。 基本的なデバッグ機能の詳細については、[デバッガーでのはじめに](../debugger/debugger-feature-tour.md)に関するページを参照してください。

    アプリの種類、前に実行した手順、ブラウザーの状態などのその他の要素に応じて、トランスパイルされた *.js* ファイル内またはソース ファイル内で、ブレークポイントにヒットする可能性があります。 どちらの場合も、コードをステップ実行して、変数を確認できます

   * TypeScript、JSX、または *.vue* ソース ファイル内のコードを中断する必要があるときに、それができない場合は、「[トラブルシューティング](#troubleshooting_source_maps)」のセクションにある説明に従って、環境が正しく設定されていることを確認します。

   * トランスパイルされた JavaScript ファイル (*app-bundle.js* など) 内のコードを中断する必要があるときに、それができない場合は、ソース マップ ファイルである *filename.js.map* を削除します。

### <a name="troubleshooting_source_maps"></a>ブレークポイントとソース マップのトラブルシューティング

TypeScript または JSX ソース ファイル内のコードを中断する必要があるときに、それができない場合は、前の手順で説明したデバッガーをアタッチするための **[プロセスにアタッチ]** を使用します。 環境が正しく設定されていることを確認してください。

* ブラウザーをデバッグ モードで実行できるように、Chrome 拡張機能を含むすべてのブラウザー インスタンスを (タスク マネージャーを使用して) 閉じます。
      
* 必ず[ブラウザーをデバッグ モードで起動](#prepare_the_browser_for_debugging)します。

* ソース マップ ファイルにソース ファイルへの正しい相対パスが含まれていること、*webpack:///* などのサポートされていないプレフィックスが含まれていないことを確認します。そうでないと Visual Studio デバッガーでソース ファイルを検索できません。 たとえば、*webpack:///.app.tsx* のような参照は、 *./app.tsx* に修正される可能性があります。 これは、ソース マップ ファイル (テストで役立ちます) 内で手動で行うことも、カスタム ビルド構成を使用して行うこともできます。 詳細については、「[デバッグ用のソース マップを生成する](#generate_source_maps)」を参照してください。

または、ソース ファイル (*app.tsx* など) 内のコードを中断する必要があるときに、それができない場合は、ソース ファイル内で `debugger;` ステートメントを使うか、代わりに Chrome の開発者ツール (または Microsoft Edge の F12 ツール) でブレークポイントを設定してみてください。

## <a name="generate_source_maps"></a> デバッグ用のソース マップを生成する

Visual Studio には、JavaScript ソース ファイルでソース マップを使用して生成する機能があります。 これは多くの場合、ソースが TypeScript や Babel のようなトランスパイラによって縮小または作成されている場合に必要です。 使用できるオプションはプロジェクトの種類によって異なります。

* Visual Studio の TypeScript プロジェクトでは、既定でソース マップが生成されます。 詳細については、「[tsconfig.json ファイルを使用してソース マップを構成する](#configure_source_maps)」を参照してください。

* JavaScript プロジェクトでは、webpack などのバンドラーと、プロジェクトに追加できる TypeScript コンパイラ (または Babel) などのコンパイラを使用して、ソース マップを生成することができます。 TypeScript コンパイラの場合は、*tsconfig.json* ファイルを追加して `sourceMap` コンパイラ オプションを設定する必要もあります。 基本的な webpack 構成を使用してこれを行う方法を示す例については、[React を使用した Node.js アプリの作成](../javascript/tutorial-nodejs-with-react-and-jsx.md)に関するページを参照してください。

> [!NOTE]
> ソース マップを初めて使用する場合は、続行する前に「[Introduction to JavaScript Source Maps](https://www.html5rocks.com/en/tutorials/developertools/sourcemaps/)」 (JavaScript ソース マップの概要) をお読みください。 

ソース マップの詳細設定を構成するには、*tsconfig.json* と、TypeScript プロジェクトのプロジェクト設定の両方ではなく、いずれかを使用します。

Visual Studio を使用したデバッグを有効にするには、生成されたソース マップ内のソース ファイルへの参照が正しいことを確認する必要があります (テストが必要な場合があります)。 たとえば、webpack を使用している場合、ソース マップ ファイル内の参照には *webpack:///* プレフィックスが含まれています。これにより、Visual Studio で TypeScript または JSX ソース ファイルを検索できなくなります。 具体的には、デバッグの目的でこの問題を修正する場合、ソース ファイル (*app.tsx* など) への参照を、*webpack:///./app.tsx* などから *./app.tsx* などのように変更する必要があります。そうすることでデバッグが有効になります (パスはソース ファイルの相対パスです)。 次の例は、Visual Studio で使用できるように、最も一般的なバンドラーの 1 つである webpack でソース マップを構成する方法を示しています。

(webpack のみ) JSX ファイルの TypeScript で (トランスパイルされた JavaScript ファイルではなく) ブレークポイントを設定する場合は、webpack の構成を更新する必要があります。 たとえば、*webpack-config.js* では、次のコードを置き換えることが必要な場合があります。

```javascript
  output: {
    filename: "./app-bundle.js", // This is an example of the filename in your project
  },
```

を、次のコードで置換します。

```javascript
  output: {
    filename: "./app-bundle.js", // Replace with the filename in your project
    devtoolModuleFilenameTemplate: '[resource-path]'  // Removes the webpack:/// prefix
  },
```

これは、Visual Studio でクライアント側コードのデバッグを有効にするための開発専用の設定です。

複雑なシナリオの場合は、ブラウザー ツール (**F12**) がデバッグに最適な場合があります (カスタム プレフィックスを変更する必要がないため)。

### <a name="configure_source_maps"></a>tsconfig.json ファイルを使用してソース マップを構成する

*tsconfig.json* ファイルをプロジェクトに追加する場合、Visual Studio ではディレクトリ ルートが TypeScript プロジェクトとして扱われます。 ファイルを追加するには、ソリューション エクスプローラーでプロジェクトを右クリックし、 **[追加] > [新しい項目] > [TypeScript JSON 構成ファイル]** を選択します。 *tsconfig.json* ファイルは、次のようにプロジェクトに追加されます。

```json
{
  "compilerOptions": {
    "noImplicitAny": false,
    "noEmitOnError": true,
    "removeComments": false,
    "sourceMap": true,
    "target": "es5"
  },
  "exclude": [
    "node_modules",
    "wwwroot"
  ]
}
```

#### <a name="compiler-options-for-tsconfigjson"></a>tsconfig.json のコンパイラ オプション

* **inlineSourceMap**:ソース ファイルごとに別のソース マップを作成するのではなく、ソース マップを含む 1 つのファイルを出力します。
* **inlineSources**:1 つのファイル内のソース マップと共にソースを出力します。*inlineSourceMap* または *sourceMap* を設定する必要があります。
* **mapRoot**:既定の場所ではなく、デバッガーでソース マップ ( *.map*) ファイルを検索する必要がある場所を指定します。 実行時の *.map* ファイルを、 *.js* ファイルとは異なる場所に配置する必要がある場合は、このフラグを使用します。 指定された場所は、 *.map* ファイルの場所にデバッガーを移動するために、ソース マップに埋め込まれます。
* **sourceMap**:対応する *.map* ファイルを生成します。
* **sourceRoot**:ソースの場所ではなく、デバッガーで TypeScript ファイルを検索する必要がある場所を指定します。 実行時のソースを、設計時の場所とは異なる場所に配置する必要がある場合は、このフラグを使用します。 指定された場所は、ソース ファイルが配置されている場所にデバッガーを移動するために、ソース マップに埋め込まれます。

コンパイラ オプションの詳細については、TypeScript ハンドブックの「[Compiler Options](https://www.typescriptlang.org/docs/handbook/compiler-options.html)」 (コンパイラ オプション) ページを確認してください。

### <a name="configure-source-maps-using-project-settings-typescript-project"></a>プロジェクト設定を使用してソース マップを構成する (TypeScript プロジェクト)

プロジェクトを右クリックし、 **[プロジェクト]、[プロパティ]、[TypeScript ビルド]、[デバッグ]** の順に選択することで、プロジェクト プロパティを使用してソース マップ設定を構成することもできます。

以下のプロジェクト設定を使用できます。

* **ソース マップを生成する** (*tsconfig.json* の **sourceMap** と同等):対応する *.map* ファイルを生成します。
* **ソース マップのルート ディレクトリを指定する** (*tsconfig.json* の **mapRoot** と同等):生成された場所ではなく、デバッガーでマップ ファイルを検索する必要がある場所を指定します。 実行時の *.map* ファイルを、.js ファイルとは異なる場所に配置する必要がある場合は、このフラグを使用します。 指定された場所は、マップ ファイルが配置されている場所にデバッガーを移動するために、ソース マップに埋め込まれます。
* **TypeScript ファイルのルート ディレクトリを指定する** (*tsconfig.json* の **sourceRoot** と同等):ソースの場所ではなく、デバッガーで TypeScript ファイルを検索する必要がある場所を指定します。 実行時のソース ファイルを、設計時の場所とは異なる場所に配置する必要がある場合は、このフラグを使用します。 指定された場所は、ソース ファイルが配置されている場所にデバッガーを移動するために、ソース マップに埋め込まれます。

## <a name="debug-javascript-in-dynamic-files-using-razor-aspnet"></a>Razor (ASP.NET) を使用して動的ファイルで JavaScript をデバッグする

::: moniker range=">=vs-2019"
Visual Studio 2019 以降、Visual Studio では Chrome および Microsoft Edge (Chromium) のみのデバッグ サポートが提供されます。
::: moniker-end
::: moniker range="vs-2017"
Visual Studio では、Chrome および Internet Explorer のみのデバッグ サポートが提供されます。
::: moniker-end

ただし、Razor 構文 (cshtml、vbhtml) で生成されたファイルのブレークポイントに自動的にヒットすることはできません。 この種のファイルのデバッグに使用できる方法は、次の 2 つです。

* **中断する場所に `debugger;` ステートメントを配置する**:これにより、動的スクリプトで実行が停止され、作成中にすぐにデバッグが開始されます。
* **Visual Studio でページを読み込み、動的なドキュメントを開く**:デバッグ中に動的ファイルを開き、ブレークポイントを設定し、この方法が機能するようにページを更新する必要があります。 Chrome と Internet Explorer のどちらを使用するかに応じて、次の方法のいずれかを使ってファイルを見つけます。

   Chrome の場合は、 **[ソリューション エクスプローラー]、[スクリプト ドキュメント]、[YourPageName]** の順に移動します。

    > [!NOTE]
    > Chrome を使用する場合、 **\<script> タグ間に使用できるソースがない**という内容のメッセージが表示される場合があります。 これは問題ありませんので、デバッグを続けることができます。

   ::: moniker range=">=vs-2019"
   Microsoft Edge (Chromium) の場合は、Chrome と同じ手順を使用します。
   ::: moniker-end

   ::: moniker range="vs-2017"
   Internet Explorer の場合は、 **[ソリューション エクスプローラー]、[スクリプト ドキュメント]、[Windows Internet Explorer]、[YourPageName]** の順に移動します。
   ::: moniker-end

詳細については、「[Client-side debugging of ASP.NET projects in Google Chrome](https://devblogs.microsoft.com/aspnet/client-side-debugging-of-asp-net-projects-in-google-chrome/)」 (Google Chrome での ASP.NET プロジェクトのクライアント側デバッグ) をご覧ください。

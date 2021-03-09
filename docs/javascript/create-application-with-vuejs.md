---
title: Node.js を使用して Vue.js アプリを作成する
description: Visual Studio で Vue.js フレームワークを使用して Node.js アプリケーションを作成することができます
ms.custom: seodec18
ms.date: 07/06/2018
ms.topic: how-to
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jmartens
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 338e53d576e9f4d73b32c3f432223480d9e708c3
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/03/2021
ms.locfileid: "101683931"
---
# <a name="create-a-vuejs-application-using-nodejs-tools-for-visual-studio"></a>Node.js Tools for Visual Studio を使用して Vue.js アプリケーションを作成する

Visual Studio では、JavaScript、TypeScript のいずれかで [Vue.js](https://vuejs.org/) フレームワークを使ったアプリの開発をサポートしています。

次の新機能は、Visual Studio での Vue.js アプリケーションの開発をサポートします。

* *.vue* ファイルの Script、Style、Template ブロックのサポート
* *.vue* ファイルでの `lang` 属性の認識
* Vue.js プロジェクトとファイル テンプレート

## <a name="prerequisites"></a>前提条件

* Visual Studio 2017 バージョン 15.8 以降のバージョンと **Node.js 開発** ワークロードがインストールされている必要があります。

    > [!IMPORTANT]
    > この記事では、Visual Studio 2017 バージョン 15.8 以降でのみ使用できる機能が必要です。

    ::: moniker range=">=vs-2019"
    必要なバージョンがまだインストールされていない場合は、[Visual Studio 2019](https://visualstudio.microsoft.com/downloads) をインストールしてください。
    ::: moniker-end
    ::: moniker range="vs-2017"
    Visual Studio をまだインストールしていない場合は、[Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) ページに移動し、無料試用版をインストールしてください。
    ::: moniker-end

    Visual Studio は既にあり、ワークロードだけをインストールする必要がある場合は、 **[ツール]**  >  **[ツールと機能を取得]** に移動すると、Visual Studio インストーラーが開きます。 **[Node.js 開発]** ワークロードを選択し、 **[変更]** を選択します。

* ASP.NET Core プロジェクトを作成するには、ASP.NET と、Web 開発ワークロードおよび .NET Core クロスプラットフォーム開発ワークロードがインストールされている必要があります。

* Node.js ランタイムをインストールしている必要があります。

    インストールされていない場合は、LTS バージョンを [Node.js](https://nodejs.org/en/download/) Web サイトからインストールしてください。 一般に、Visual Studio はインストール済みの Node.js ランタイムを自動的に検出します。 インストール済みのランタイムが検出されない場合は、プロパティ ページでインストール済みのランタイムを参照するようにプロジェクトを構成できます。 (プロジェクトを作成した後、プロジェクト ノードを右クリックして **[プロパティ]** を選択します)。

## <a name="create-a-vuejs-project-using-nodejs"></a>Node.js を使用して Vue.js プロジェクトを作成する

新しい Vue.js テンプレートを使用して新しいプロジェクトを作成できます。 テンプレートを使うのが開始する最も簡単な方法です。 詳細については、「[Use Visual Studio to create your first Vue.js app](../javascript/quickstart-vuejs-with-nodejs.md)」(Visual Studio を使用して初めての Vue.js アプリを作成する) をご覧ください。

## <a name="create-a-vuejs-project-with-aspnet-core-and-the-vue-cli"></a>ASP.NET Core と Vue CLI を使用して Vue.js プロジェクトを作成する

Vue.js では、迅速にスキャフォールディングするプロジェクトの正式な CLI が提供されています。 CLI を使用してアプリケーションを作成する場合は、この記事の手順に従って開発環境を設定します。

> [!IMPORTANT]
> 以下の手順では、Vue.js フレームワークについてある程度の経験があるものとします。 ない場合は、[Vue.js](https://vuejs.org/) にアクセスしてフレームワークの詳細を学習してください。

### <a name="create-a-new-aspnet-core-project"></a>新しい ASP.NET Core プロジェクトを作成する

この例では、空の ASP.NET Core アプリケーション (C#) を使用します。 ただし、さまざまなプロジェクトやプログラミング言語から選択することができます。

#### <a name="create-an-empty-project"></a>空のプロジェクトを作成する

* Visual Studio を起動し、新しいプロジェクトを作成します。

    ::: moniker range=">=vs-2019"
    Visual Studio 2019 で、スタート ウィンドウの **[新しいプロジェクトの作成]** を選択します。 スタート ウィンドウが開いていない場合は、 **[ファイル]**  >  **[スタート ウィンドウ]** を選択します。 「**Web アプリ**」と入力し、言語として **C#** を選択した後、 **[ASP.NET Core Empty]\(ASP.NET Core (空)\)** を選択し、 **[次へ]** を選択します。 次の画面で、プロジェクトに「**client-app**」という名前を指定し、 **[次へ]** を選択します。

    推奨されるターゲット フレームワーク (.NET Core 3.1) または .NET 5 を選択し、 **[作成]** を選択します。
    ::: moniker-end
    ::: moniker range="vs-2017"
    上部のメニュー バーから、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで **[Visual C#]** を展開した後、 **[Web]** を選択します。 中央のウィンドウで、 **[ASP.NET Core Web アプリケーション]** を選択し、**client-app** という名前を入力してから **[OK]** を選択します。

    **[空]** を選択して、 **[OK]** をクリックします。

    Visual Studio によってプロジェクトが作成され、ソリューション エクスプローラー (右側のウィンドウ) で開かれます。
    ::: moniker-end

    **ASP.NET Core Web アプリケーション** プロジェクト テンプレートが表示されない場合は、**ASP.NET と Web 開発** ワークロードと **.NET Core 開発** ワークロードを最初にインストールする必要があります。 ワークロードをインストールするには、 **[新しいプロジェクト]** ダイアログ ボックス ( **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択) の左側のウィンドウで **[Visual Studio インストーラーを開く]** リンクをクリックします。 Visual Studio インストーラーが起動します。 必要なワークロードを選択します。

#### <a name="configure-the-project-startup-file"></a>プロジェクトのスタートアップ ファイルを構成する

* *./Startup.cs* ファイルを開き、Configure メソッドに次の行を追加します。

    ```csharp
    app.UseDefaultFiles(); // Enables default file mapping on the web root.
    app.UseStaticFiles(); // Marks files on the web root as servable.
    ```

### <a name="install-the-vue-cli"></a>Vue CLI をインストールする

vue-cli npm モジュールをインストールするには、コマンド プロンプトを開き、「`npm install --g vue-cli`」または「`npm install -g @vue/cli`」 (現在ベータ版のバージョン 3.0 の場合) と入力します。

### <a name="scaffold-a-new-client-application-using-the-vue-cli"></a>Vue CLI を使用して新しいクライアント アプリケーションをスキャフォールディングする

1. コマンド プロンプトに移動し、現在のディレクトリをお使いのプロジェクト ルート フォルダーに変更します。

1. 「`vue init webpack client-app`」と入力し、追加の質問に回答するように求められたら手順に従います。

    > [!NOTE]
    > *.vue* ファイルについては、WebPac または類似のフレームワークをローダーと共に使って変換を行う必要があります。 TypeScript および Visual Studio では、 *.vue* ファイルをコンパイルできません。 バンドルについても同様です。TypeScript では、ES2015 モジュール (つまり、`import` と `export` ステートメント) を、ブラウザーで読み込む最終的な 1 つの *.js* ファイルに変換できません。 ここでも WebPack が最善の選択肢となります。 MSBuild を使って Visual Studio 内からこのプロセスを進めるには、Visual Studio テンプレートから開始する必要があります。 現在のところ、すぐに使える Vue.js 開発用の ASP.NET テンプレートはありません。

#### <a name="modify-the-webpack-configuration-to-output-the-built-files-to-wwwroot"></a>ビルドされたファイルを wwwroot に出力するように webpack の構成を変更する

* *./client-app/config/index.js* ファイルを開き、`build.index` および `build.assetsRoot` を wwwroot のパスに変更します。

    ```js
    // Template for index.html
    index: path.resolve(__dirname, '../../wwwroot/index.html'),

    // Paths
    assetsRoot: path.resolve(__dirname, '../../wwwroot'),
    ```

#### <a name="indicate-the-project-to-build-the-client-app-each-time-that-a-build-is-triggered"></a>ビルドがトリガーされるたびにクライアント アプリをビルドするようにプロジェクトを設定する

1. Visual Studio で **[プロジェクト]**  >  **[プロパティ]**  >  **[ビルド イベント]** に移動します。

1. **[ビルド前に実行するコマンド ライン]** に「`npm --prefix ./client-app run build`」と入力します。

#### <a name="configure-webpacks-output-module-names"></a>webpack の出力モジュール名を構成する

* *./client-app/build/webpack.base.conf.js* ファイルを開き、出力のプロパティに次のプロパティを追加します。

    ```js
    devtoolModuleFilenameTemplate: '[absolute-resource-path]',
    devtoolFallbackModuleFilenameTemplate: '[absolute-resource-path]?[hash]'
    ```

### <a name="add-typescript-support-with-the-vue-cli"></a>Vue CLI で TypeScript のサポートを追加する

次の手順では、現在ベータ版である vue-cli 3.0 が必要です。

1. コマンド プロンプトに移動し、現在のディレクトリをプロジェクト ルート フォルダーに変更します。

1. 「`vue create client-app`」と入力し、 **[Manually select features]\(手動で機能を選択する\)** を選択します。

1. **[TypeScript]** を選択し、他の必要なオプションを選択します。

1. 残りの手順に従って、質問に応答します。

#### <a name="configure-a-vuejs-project-for-typescript"></a>TypeScript の Vue.js プロジェクトを構成する

1. *./client-app/tsconfig.json* ファイルを開き、コンパイラ オプションに `noEmit:true` を追加します。

    このオプションを設定すると、Visual Studio でプロジェクトをビルドするたびにプロジェクトが繁雑にならなくなります。

1. 次に、 *./client-app/* に *vue.config.js* ファイルを作成し、次のコードを追加します。

    ```js
    module.exports = {
        outputDir: '../wwwroot',

        configureWebpack: {
            output: {
                devtoolModuleFilenameTemplate: '[absolute-resource-path]',
                devtoolFallbackModuleFilenameTemplate: '[absolute-resource-path]?[hash]'
            }
        }
    };
    ```

    上記のコードは、webpack を構成して、wwwroot フォルダーを設定します。

#### <a name="build-with-vue-cli-30"></a>vue-cli 3.0 でビルドする

vue-cli 3.0 の原因がわからない問題によって、ビルド プロセスを自動化できない可能性があります。 wwwroot フォルダーを更新するたびに、client-app フォルダーで `npm run build` コマンドを実行する必要があります。

または、ASP.NET プロジェクトのプロパティを使用して、vue-cli 3.0 プロジェクトをビルド前イベントとしてビルドできます。 プロジェクトを右クリックし、 **[プロパティ]** を選択し、 **[ビルド]** タブの **[ビルド前に実行するコマンド ライン]** テキスト ボックスに次のコマンドを含めます。

``` cmd
cd ./client-app
npm run build
cd ../
```

## <a name="limitations"></a>制限事項

* `lang` 属性は、JavaScript および TypeScript 言語のみをサポートします。 受け付けられる値は、js、jsx、ts、tsx です。
* `lang` 属性は、template または style タグでは動作しません。
* *.vue* ファイル内の script ブロックのデバッグは、その前処理される性質によりサポートされていません。
* TypeScript は *.vue* ファイルをモジュールとして認識しません。 *.vue* ファイルがどのようなものかを TypeScript に伝えるには、次のようなコードを含むファイルが必要です (vue-cli 3.0 のテンプレートにはこのファイルが既に含まれます)。

    ```js
    // ./client-app/vue-shims.d.ts
    declare module "*.vue" {
        import Vue from "vue";
        export default Vue;
    }
    ```

* vue-cli 3.0 を使用しているときは、プロジェクト プロパティでのビルド前イベントとしての `npm run build` コマンドの実行は動作しません。

## <a name="see-also"></a>関連項目

- [Vue の概要ガイド](https://vuejs.org/v2/guide)
- [Vue CLI プロジェクト](https://github.com/vuejs/vue-cli)
- [webpack 構成ドキュメント](https://webpack.js.org/configuration/)

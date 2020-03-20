---
title: 'クイック スタート: Visual Studio を使用して初めての Node.js Web アプリを作成する'
description: このクイック スタートでは、Visual Studio で Node.js アプリを作成します
ms.date: 06/27/2018
ms.technology: vs-javascript
ms.topic: quickstart
ms.devlang: javascript
ms.assetid: b0e4ebed-1a01-41ef-aad1-4d8465ce5322
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: f716421da3b9f888dbb7656c55db6814de88332b
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "78235055"
---
# <a name="quickstart-use-visual-studio-to-create-your-first-nodejs-app"></a>クイック スタート: Visual Studio を使用して初めての Node.js Web アプリを作成する

ここでは 5 分から 10 分で Visual Studio 統合開発環境 (IDE) の概要を示し、単純な Node.js Web アプリケーションを作成します。

## <a name="prerequisites"></a>必須コンポーネント

* Visual Studio および Node.js 開発ワークロードをインストールしている必要があります。

    ::: moniker range=">=vs-2019"
    Visual Studio 2019 をまだインストールしていない場合は、 [Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads)  ページに移動し、無料試用版をインストールしてください。
    ::: moniker-end
    ::: moniker range="vs-2017"
    Visual Studio 2017 をまだインストールしていない場合は、 [Visual Studio のダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)  ページに移動し、無料試用版をインストールしてください。
    ::: moniker-end

    Visual Studio は既にあり、ワークロードだけをインストールする必要がある場合は、 **[ツール]**  >  **[ツールと機能を取得]** に移動すると、Visual Studio インストーラーが開きます。 **[Node.js 開発]** ワークロードを選択し、 **[変更]** を選択します。

    ![VS インストーラーの Node.js ワークロード](../ide/media/quickstart-nodejs-workload.png)

* Node.js ランタイムをインストールしている必要があります。

    インストールされていない場合は、[Node.js](https://nodejs.org/en/download/) Web サイトから LTS バージョンをインストールして、外部のフレームワークおよびライブラリとの最善の互換性を確保することをお勧めします。 Node.js は、32 ビットおよび 64 ビット アーキテクチャ用にビルドされています。 Visual Studio の Node.js ツールは Node.js ワークロードに含まれており、両方のバージョンをサポートしています。 必要なのは 1 つだけであり、Node.js インストーラーでは、一度に 1 つのインストールのみをサポートしています。
    
    一般に、Visual Studio はインストール済みの Node.js ランタイムを自動的に検出します。 インストール済みのランタイムが検出されない場合は、プロパティ ページ上のインストール済みのランタイムを参照するようにプロジェクトを構成することができます (プロジェクトを作成した後、プロジェクト ノードを右クリックして、 **[プロパティ]** を選択し、 **[Node.exe のパス]** を設定します)。 Node.js のグローバル インストールを使用するか、または Node.js プロジェクトごとにローカル インタープリターへのパスを指定することが可能です。 

## <a name="create-a-project"></a>プロジェクトを作成する

まず、Node.js Web アプリケーション プロジェクトを作成します。

1. Node.js ランタイムがまだインストールされていない場合は、LTS バージョンを [Node.js](https://nodejs.org/en/download/) Web サイトからインストールしてください。

    詳細については、前提条件を参照してください。

1. Visual Studio を開きます。

1. 新しいプロジェクトを作成します。

    ::: moniker range=">=vs-2019"
    **Esc** キーを押してスタート ウィンドウを閉じます。 **Ctrl + Q** キーを押して検索ボックスを開き、「**Node.js**」と入力してから、 **[Create new Blank Node.js Web application project]\(新しい空の Node.js Web アプリケーション プロジェクトの作成\)** (JavaScript) を選択します。 表示されたダイアログ ボックスで、 **[作成]** を選択します。
    ::: moniker-end
    ::: moniker range="vs-2017"
    上部のメニュー バーから、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで、 **[JavaScript]** を展開して、 **[Node.js]** を選択します。 中央のウィンドウで、 **[空白の Node.js Web アプリケーション]** を選択してから **[OK]** を選択します。
    ::: moniker-end
    **[空白の Node.js Web アプリケーション]** プロジェクト テンプレートが表示されない場合は、**Node.js 開発**ワークロードを追加する必要があります。 手順について詳しくは、「[必須コンポーネント](#prerequisites)」をご覧ください。

    Visual Studio は新しいソリューションを作成し、プロジェクトを開きます。 *server.js* が左側のウィンドウのエディターで開きます。

## <a name="explore-the-ide"></a>IDE を探索する

1. 右ウィンドウの**ソリューション エクスプローラー**を見てください。

   ![ソリューション エクスプローラー](../ide/media/quickstart-nodejs-solution-explorer.png)

   - **[新しいプロジェクト]** ダイアログ ボックスに指定した名前が使用され、太字で強調表示されているのがあなたのプロジェクトです。 ディスク上では、このプロジェクトは、プロジェクト フォルダーの *.njsproj* ファイルに該当します。

   - 最上位レベルにあるのは、ソリューションです。既定では、名前はプロジェクトと同じです。 ディスク上の *.sln* ファイルで表されるソリューションは、1 つ以上の関連プロジェクトのコンテナーです。

   - npm ノードには、インストールされているすべての npm パッケージが表示されます。 npm ノードを右クリックし、ダイアログ ボックスを使用して npm パッケージを検索し、インストールすることができます。

1. コマンド プロンプトから npm パッケージまたは Node.js コマンドをインストールする場合は、プロジェクト ノードを右クリックし、 **[ここでコマンド プロンプトを開く]** を選択します。

   ![Node.js コマンド プロンプト](../ide/media/quickstart-nodejs-command-prompt.png)

1. エディター (左ウィンドウ) の *server.js* で、`http.createServer` を選択してから **F12 キー**を押すか、コンテキスト (右クリック) メニューから **[定義に移動]** を選択します。 このコマンドで *index.d.ts* の `createServer` 関数の定義が示されます。

   ![[定義に移動] コンテキスト メニュー](../ide/media/quickstart-nodejs-gotodefinition.png)

1. *server.js* に戻り、このコード行の文字列の末尾 `res.end('Hello World\n');` にカーソルを置き、次のように変更します。

    `res.end('Hello World\n' + res.connection.`

    `connection.` と入力すると、IntelliSense によってコード入力をオートコンプリートするオプションが表示されます。

   ![IntelliSense のオートコンプリート](../ide/media/quickstart-nodejs-intellisense.png)

1. **[localPort]** を選択し、`);` と入力して、次のようにステートメントを完成させます。

    `res.end('Hello World\n' + res.connection.localPort);`

## <a name="run-the-application"></a>アプリケーションの実行

1. **Ctrl** キーを押しながら **F5** キーを押すか、 **[デバッグ]、[デバッグなしで開始]** の順に選択してアプリケーションを実行します。 アプリがブラウザーで開きます。

1. ブラウザー ウィンドウに "Hello World" とローカルのポート番号が表示されます。

1. Web ブラウザーを閉じます。

Visual Studio IDE と Node.js の入門となるこのクイック スタートは以上で完了です。 機能についてさらに深く理解したい場合は、目次の**チュートリアル** セクションに示されているチュートリアルを続行してください。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [アプリを Linux App Service にデプロイする](../javascript/publish-nodejs-app-azure.md)

- [Node.js と Express のチュートリアル](../javascript/tutorial-nodejs.md)
- [Node.js と React のチュートリアル](../javascript/tutorial-nodejs-with-react-and-jsx.md)
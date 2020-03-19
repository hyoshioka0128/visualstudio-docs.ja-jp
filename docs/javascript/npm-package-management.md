---
title: npm パッケージを管理する
description: Visual Studio では、Node.js パッケージ マネージャー (npm) を利用してパッケージを管理できます。
ms.custom: seodec18
ms.date: 06/06/2018
ms.topic: conceptual
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: de92c3f1f0d0e29d1ba2dfaf5d536a42e636be2c
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79307221"
---
# <a name="manage-npm-packages-in-visual-studio"></a>Visual Studio で npm パッケージを管理する

npm を利用すると、Node.js アプリケーションで使用するパッケージをインストールしたり、管理したりできます。 npm に不慣れで詳細が必要な場合、[npm ドキュメント](https://docs.npmjs.com/) ページにお進みください。

Visual Studio では、npm を操作したり、UI から、または直接 npm コマンドを実行したりすることが簡単にできます。 次の方法を使用できます。
* [ソリューション エクスプローラーからパッケージをインストールする](#npmInstallWindow)
* [ソリューション エクスプローラーからインストール済みのパッケージを管理する](#solutionExplorer)
* [Node.js 対話型ウィンドウで `.npm` コマンドを使用する](#interactive)

これらの機能は連動し、プロジェクト システムやプロジェクトの *package.json* ファイルによって同期します。

> [!Important]
> NPM では、プロジェクト ルートに *node_modules* フォルダーと *package.json* が必要です。 お使いのアプリのフォルダー構造が異なる場合、Visual Studio を使用して npm パッケージを管理するには、フォルダー構造を更新する必要があります。

> [!NOTE]
> 既存の NPM プロジェクトの場合は、**既存の Node.js コードから**というソリューション テンプレートを使用します。

## <a name="npmInstallWindow"></a> ソリューション エクスプローラーからパッケージをインストールする

npm パッケージをインストールする最も簡単な方法は、npm パッケージ インストール ウィンドウを使用することです。 このウィンドウにアクセスするには、プロジェクトの **npm** ノードを右クリックし、 **[新しい npm パッケージのインストール]** を選択します。

![ソリューション エクスプローラーから新しい npm パッケージをインストールする](../javascript/media/solution-explorer-install-package.png)

このウィンドウでは、パッケージを検索し、オプションを指定し、インストールできます。

![npm パッケージを検索する](../javascript/media/search-package.png)

* **[依存関係の種類]** - **[Standard]** 、 **[Development]** 、 **[Optional]** からパッケージを選択します。 [Standard] の場合、パッケージはランタイム依存となります。[Development] の場合、パッケージは開発中にのみ必須となります。
* **[package.json に追加]** - このオプションは非推奨です。
* **[選択したバージョン]** - インストールするパッケージのバージョンを選択します。
* **[他の npm 引数]** - 他の標準 npm 引数を指定します。 たとえば、`@~0.8` のようなバージョン値を入力し、バージョン リストでは利用できない特定のバージョンをインストールできます。

インストールの進捗状況を [出力] ウィンドウの npm タブで確認できます。 これには時間がかかる場合があります。

> [!TIP]
> 関心があるスコープを検索クエリの前に付加するとスコープ パッケージを検索できます。たとえば、mocha の TypeScript 定義ファイルを探すには「`@types/mocha`」と入力します。 また、TypeScript の型定義をインストールするとき、npm 引数フィールドに `@ts2.6` を追加すると、ターゲットの TypeScript バージョンを指定できます。

## <a name="solutionExplorer"></a>ソリューション エクスプローラーでインストール済みのパッケージを管理する

npm パッケージはソリューション エクスプローラーに表示されます。 **npm** ノードの下にあるエントリは、*package.json* ファイルの依存関係を模倣します。

![npm パッケージを検索する](../javascript/media/solution-explorer-status.png)

### <a name="package-status"></a>パッケージ ステータス
* ![インストール済みのパッケージ](../javascript/media/installed-npm.png) - インストールされ、package.json のリストに入っている
* ![無関係なパッケージ](../javascript/media/extraneous-npm.png) - インストールされているが、package.json のリストで明示されていない
* ![足りないパッケージ](../javascript/media/missing-npm.png) - インストールされていないが、package.json のリストに入っている

パッケージ ノードまたは **npm** ノードを右クリックし、次のいずれかのアクションを行います。
* **package.json** のリストに入っている*足りないパッケージをインストールする*
* 最新バージョンに**パッケージを更新する**
* **パッケージをアンインストールし**、*package.json* から削除する

## <a name="interactive"></a>Node.js 対話型ウィンドウで .npm コマンドを使用する

Node.js 対話型ウィンドウで `.npm` コマンドを使用して npm コマンドを実行することもできます。 Node.js 対話型ウィンドウを開くには、ソリューション エクスプローラーでプロジェクトを右クリックし、 **[Node.js 対話型ウィンドウを開く]** を選択します。

このウィンドウで次のようなコマンドを使用してパッケージをインストールできます。

`.npm install azure@4.2.3`

 > [!Tip]
 > 既定では、npm はプロジェクトのホーム ディレクトリで実行されます。 ソリューションにプロジェクトが複数ある場合、プロジェクトの名前かパスを括弧で指定します。
 > `.npm [MyProjectNameOrPath] install azure@4.2.3`

 > [!Tip]
 > プロジェクトに package.json ファイルが含まれない場合、`.npm init -y` を使用し、新しい package.json ファイルを既定のエントリで作成します。

---
title: Dotfuscator Community をインストールする
ms.date: 03/28/2019
ms.devlang: dotnet
ms.topic: conceptual
keywords: Dotfuscator, Dotfuscator Community, Dotfuscator CE, PreEmptive, PreEmptive Solutions, PreEmptive Protection, protection, Community Edition, 難読化, .NET, 無料, Visual Studio 2017, Visual Studio 2019, Visual Studio, インストール
helpviewer_keywords:
- PreEmptive Protection Dotfuscator
- Dotfuscator Community Edition
- Dotfuscator CE
- Dotfuscator Community
- Dotfuscator
- obfuscation
- protection
- Dotfuscator installer
- Dotfuscator setup
- install Dotfuscator
- installing Dotfuscator
- set up Dotfuscator
description: Visual Studio に含まれている Dotfuscator Community の無料コピーをインストールする方法について説明します。
ms.assetid: f2146651-e24a-4e24-ade8-8ddee8ff4e43
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: bb659976126713a11594ad1b4aeb536510744c38
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75596815"
---
# <a name="install-dotfuscator-community"></a>Dotfuscator Community をインストールする

Dotfuscator Community は、Visual Studio のオプション コンポーネントです。
これらの手順では、そのインストール方法について説明します。

> [!NOTE]
> 各リリースの Visual Studio に付属の Dotfuscator Community のバージョンだけでなく、PreEmptive Solutions もその Web サイトで定期的に更新バージョンが提供されます。
> Visual Studio からインストールするのではなく、**最新バージョン**を直接ダウンロードする場合は、 **[ここをクリックして Dotfuscator のダウンロード ページに移動してください][download]** 。

## <a name="within-visual-studio"></a>Visual Studio 内

::: moniker range="vs-2019"

Visual Studio IDE から Dotfuscator Community をインストールできます。

1. **検索ボックス** (Ctrl+Q) に `dotfuscator` と入力します。 <br/> <br/> ![検索ボックス](media/install_in_vs19_12.png) <br/> <br/>

2. 表示された検索結果で、 *[コンポーネント]* 見出しの下の **[Install PreEmptive Protection - Dotfuscator]\(PreEmptive Protection - Dotfuscator のインストール\)** を選択します。
   * *[メニュー]* 見出しの下に **[PreEmptive Protection - Dotfuscator Community]** と表示されている場合、Dotfuscator Community は既にインストールされています。 [開始する][get-started]には、そのオプションを選択します。

3. Dotfuscator Community のインストール用に事前構成された Visual Studio のインストーラー ウィンドウが起動します。
   > [!NOTE]
   > 続行するには管理者の資格情報を提供する必要がある場合があります。

4. Visual Studio インストーラー ウィンドウで、 *[インストール]* をクリックします。 <br/> <br/> ![[インストール] をクリックします](media/install_in_vs19_34.png) <br/> <br/>

::: moniker-end

::: moniker range="vs-2017"

Visual Studio IDE から Dotfuscator Community をインストールできます。

1. **クイック起動** (Ctrl キーを押しながら Q キーを押す) 検索バーで、「`dotfuscator`」と入力します。 <br/> <br/> ![クイック起動](media/install_from_vs_12.png) <br/> <br/>

2. 表示されたクイック起動の結果の *[インストール]* 見出しで、 **[PreEmptive Protection - Dotfuscator (個々のコンポーネント)]** を選択します。
   * または、 *[メニュー]* 見出しで、 **[ツール] > [PreEmptive Protection - Dotfuscator]** を選択します。この場合、Dotfuscator CE は既にインストールされています。 [開始する][get-started]には、そのオプションを選択します。

3. Dotfuscator CE のインストール用に事前構成された Visual Studio のインストーラー ウィンドウが起動します。
   > [!NOTE]
   > 続行するには管理者の資格情報を提供する必要がある場合があります。

4. Visual Studio インストーラー ウィンドウで、 *[インストール]* をクリックします。 <br/> <br/> ![[インストール] をクリックします](media/install_from_vs_345.png) <br/> <br/>

::: moniker-end

インストールが完了したら、[Dotfuscator Community の使用を開始][get-started]できます。

## <a name="during-visual-studio-installation"></a>Visual Studio のインストール中

Visual Studio をまだインストールしていない場合は、[Visual Studio の Web サイト][vs-install]からインストーラーを取得できます。
実行すると、選択した Visual Studio エディションのインストール オプションが表示されます。

::: moniker range="vs-2019"

![インストール オプション](media/install_ui.png)

::: moniker-end

::: moniker range="vs-2017"

![インストール オプション](media/install_ui_17.png)

::: moniker-end

その後、Visual Studio の個々のコンポーネントとして Dotfuscator Community をインストールできます。

1. **[個別のコンポーネント]** タブを選択します。
2. *[コード ツール]* で、 *[PreEmptive Protection - Dotfuscator]* 項目のチェック ボックスをオンにします。<br/> <br/> ![個々のコンポーネント](media/install_individually_12.png) <br/> <br/>
3. *[概要]* パネルの *[個々のコンポーネント]* セクションに *[PreEmptive Protection - Dotfuscator]* が表示されます。 <br/> <br/> ![概要ペイン](media/install_individually_3.png) <br/> <br/>
4. 使用環境に合わせて、インストール設定をさらに構成します。
5. Visual Studio をインストールする準備ができたら、 *[インストール]* ボタンをクリックします。

インストールが完了したら、Dotfuscator Community の使用を開始できます。 詳細については、[Dotfuscator Community の完全なユーザー ガイドの概要ページ][get-started]を参照してください。

## <a name="see-also"></a>参照

[Dotfuscator Community の完全なユーザー ガイドのこのトピック](https://www.preemptive.com/dotfuscator/ce/docs/help/)

<!-- Copyright © 2019 PreEmptive Solutions, LLC -->

[vs-install]:  https://visualstudio.microsoft.com/downloads/
[get-started]:  https://www.preemptive.com/dotfuscator/ce/docs/help/gui_getstarted.html

[download]:  https://www.preemptive.com/products/dotfuscator/downloads

[full]:  https://www.preemptive.com/dotfuscator/ce/docs/help/intro_install.html

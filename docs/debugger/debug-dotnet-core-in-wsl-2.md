---
title: WSL 2 で .NET Core アプリをデバッグする
description: Visual Studio を離れることなく、WSL 2 で .NET Core アプリを実行およびデバッグする方法について説明します。
ms.date: 01/25/2021
ms.topic: conceptual
helpviewer_keywords:
- debugging, linux
- debugging, wsl2
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: '>= vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: 736987a02ca7e2f59ce689b8402d9a6fcd7407e9
ms.sourcegitcommit: 586369f5aa61d4a0330802f718f0ceaa55d7e9c7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2021
ms.locfileid: "99227680"
---
# <a name="debug-net-core-apps-in-wsl-2-with-visual-studio"></a>Visual Studio を使用して WSL 2 で .NET Core アプリをデバッグする

WSL 2 を使用して、Visual Studio を離れることなく、Linux で .NET Core アプリを簡単に実行およびデバッグできます。 クロスプラットフォームの開発者は、より多くのターゲット環境をテストする簡単な方法として、この方法を使用できます。

Linux をターゲットとする Windows .NET ユーザーの場合、WSL 2 は、運用環境の現実主義と生産性の間のスイート スポットに存在します。 Visual Studio では、[リモート デバッガー](../debugger/remote-debugging-dotnet-core-linux-with-ssh.md)を使用するか、コンテナーで[コンテナー ツール](../containers/overview.md)を使用して、リモート Linux 環境で既にデバッグを行うことができます。 運用環境の現実主義が主な関心事である場合は、これらのオプションのいずれかを使用する必要があります。 簡単で高速な内部ループが重要な場合は、WSL 2 が最適なオプションです。

1 つの方法だけを選択する必要はありません。 同じプロジェクトで Docker と WSL 2 の起動プロファイルを使用し、どちらか特定の実行に適した方を選択できます。 アプリをデプロイした後は、問題が発生した場合はいつでも、リモート デバッガーを使用してアタッチできます。

## <a name="prerequisites"></a>前提条件

- .NET Core デバッグと WSL 2 オプション コンポーネントが含まれる Visual Studio 2019 v16.9 Preview 1 以降のバージョン。

  オプション コンポーネントは、.NET Core クロスプラットフォームに、または ASP.NET および Web 開発ワークロードに既定で含まれています。 これらのワークロードの一方または両方をインストールする必要があります。

- [WSL 2](/windows/wsl/about) をインストールします。

- 任意の[ディストリビューション](https://aka.ms/wslstore)をインストールします。

## <a name="start-debugging-with-wsl-2"></a>WSL 2 を使用してデバッグを開始する

1. 必須コンポーネントをインストールした後、Visual Studio で ASP.NET Core Web アプリまたは .NET Core コンソール アプリを開きます。WSL 2 という名前の新しい起動プロファイルが表示されます。

   ![起動プロファイル一覧の WSL 2 起動プロファイル](media/linux-wsl2-debugging-select-launch-profile.png)

1. このプロファイルを選択して、*launchSettings.json* に追加します。

   次の例には、ファイルのいくつかの重要な属性が示されています。

    ```json
    "WSL 2": {
        "commandName": "WSL2",
        "launchBrowser": true,
        "launchUrl": "https://localhost:5001",
        "environmentVariables": {
            "ASPNETCORE_URLS": "https://localhost:5001;http://localhost:5000",
            "ASPNETCORE_ENVIRONMENT": "Development"
        },
        "distributionName": ""
    }
    ```

   新しいプロファイルを選択すると、拡張機能により、WSL 2 のディストリビューションが .NET Core アプリを実行するように構成されていることが確認されるので、不足している依存関係をインストールするのに役立ちます。 これらの依存関係をインストールすると、WSL 2 でデバッグできるようになります。

1. 通常どおりデバッグを開始すると、アプリは既定の WSL 2 ディストリビューションで実行されます。

   Linux で実行されていることを確認する簡単な方法は、`Environment.OSVersion` の値を確認することです。

>[!NOTE]
> Ubuntu と Debian だけがテストされており、サポートされています。 .NET Core でサポートされている他のディストリビューションも機能するはずですが、[.NET Core ランタイム](https://aka.ms/wsldotnet)と [Curl](https://curl.haxx.se/) を手動でインストールする必要があります。

## <a name="choose-a-specific-distribution"></a>特定のディストリビューションを選択する

既定の WSL 2 起動プロファイルでは、*wsl.exe* で設定されている既定のディストリビューションが使用されます。 起動プロファイルのターゲットを特定のディストリビューションにする場合は、その既定値に関係なく、起動プロファイルを変更できます。 たとえば、Web アプリをデバッグしていて、それを Ubuntu 20.04 でテストしたい場合、起動プロファイルは次のようになります。

```json
"WSL 2": {
    "commandName": "WSL2",
    "launchBrowser": true,
    "launchUrl": "https://localhost:5001",
    "environmentVariables": {
        "ASPNETCORE_URLS": "https://localhost:5001;http://localhost:5000",
        "ASPNETCORE_ENVIRONMENT": "Development"
    },
    "distributionName": "Ubuntu-20.04"
}
```

## <a name="target-multiple-distributions"></a>複数のディストリビューションをターゲットにする

さらに一歩進んで、複数のディストリビューションで実行する必要があるアプリケーションの作業を行っていて、それぞれで簡単にテストする手段が必要な場合は、複数の起動プロファイルを使用できます。 たとえば、Debian、Ubuntu 18.04、Ubuntu 20.04 でコンソール アプリをテストする必要がある場合は、次の起動プロファイルを使用できます。

```json
"WSL 2 : Debian": {
    "commandName": "WSL2",
    "distributionName": "Debian"
},
"WSL 2 : Ubuntu 18.04": {
    "commandName": "WSL2",
    "distributionName": "Ubuntu-18.04"
},
"WSL 2 : Ubuntu 20.04": {
    "commandName": "WSL2",
    "distributionName": "Ubuntu-20.04"
}
```

これらの起動プロファイルを使用すると、快適な Visual Studio から離れなくても、ターゲット ディストリビューション間を簡単に切り替えることができます。

![起動プロファイル一覧の複数の WSL 2 起動プロファイル](media/linux-wsl2-debugging-switch-target-distribution.png)

## <a name="wsl-settings-in-the-launch-profile"></a>起動プロファイルでの WSL の設定

次の表は、起動プロファイルでサポートされている設定を示したものです。

|名前|Default|目的|トークンがサポートされているか?|
|-|-|-|-|
|executablePath|dotnet|実行する実行可能ファイル|Yes|
|commandLineArgs|WSL 環境にマップされている MSBuild のプロパティ TargetPath の値|executablePath に渡されるコマンド ライン引数|Yes|
|workingDirectory|コンソール アプリの場合: {*OutDir*}</br>Web アプリの場合: {*ProjectDir*}|デバッグを開始する作業ディレクトリ|Yes|
|environmentVariables||デバッグ対象のプロセスに設定する環境変数のキーと値のペア。|Yes|
|setupScriptPath||デバッグの前に実行するスクリプト。 ~/.bash_profile のようなスクリプトを実行する場合に便利です。|Yes|
|distributionName||使用する WSL ディストリビューションの名前。|いいえ|
|launchBrowser|false|ブラウザーを起動するかどうか|いいえ|
|launchUrl||launchBrowser が true の場合に起動する URL|いいえ|

サポートされているトークン:

{*ProjectDir*} - プロジェクト ディレクトリへのパス

{*OutDir*} - MSBuild のプロパティ `OutDir` の値

>[!NOTE]
> すべてのパスは Windows ではなく WSL 用です。

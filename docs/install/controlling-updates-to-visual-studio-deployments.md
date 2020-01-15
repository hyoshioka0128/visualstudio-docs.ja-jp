---
title: 配置の更新プログラムを制御する
description: ネットワークからインストールするときに、Visual Studio が更新プログラムを検索する場所を変更する方法を説明します。
ms.date: 03/30/2019
ms.custom: seodec18
ms.topic: conceptual
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 35C7AB05-07D5-4B38-BCAC-AB88444E7368
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 2cdf4d4e6fb90b18c8141d1d176629539a0a4f8b
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75570584"
---
# <a name="control-updates-to-network-based-visual-studio-deployments"></a>ネットワーク ベースの Visual Studio 配置の更新プログラムを制御する

企業の管理者は、多くの場合、レイアウトを作成してそれをネットワーク ファイル共有でホストし、エンド ユーザーに展開します。

## <a name="controlling-where-visual-studio-looks-for-updates"></a>Visual Studio が更新プログラムを探す場所を変更する

既定では、インストールがネットワーク共有から展開された場合でも、Visual Studio は引き続きオンラインで更新プログラムを探します。 更新プログラムがある場合、ユーザーがインストールできます。 更新された内容のうちオフライン レイアウトで見つからないものは、すべて Web からダウンロードされます。

Visual Studio が更新プログラムを検索する場所を変更することで直接制御することができます。 ユーザーが更新するバージョンも制御できます。 これを行うには、次の手順を実行します。

1. オフライン レイアウトを作成します。

   ```cmd
   vs_enterprise.exe --layout C:\vsoffline --lang en-US
   ```

2. それをホストするファイル共有にコピーします。

   ```cmd
   xcopy /e C:\vsoffline \\server\share\VS
   ```

3. レイアウトの response.json ファイルを変更し、管理者が制御する channelManifest.json のコピーを指すように `channelUri` 値を変更します。

   値のバックスラッシュは、次の例のように必ずエスケープしてください。

   ```json
   "channelUri":"\\\\server\\share\\VS\\ChannelManifest.json"
   ```

   これでエンド ユーザーはこの共有からセットアップを実行し、Visual Studio をインストールできます。

   ```cmd
   \\server\share\VS\vs_enterprise.exe
   ```

企業の管理者はユーザーが新しいバージョンの Visual Studio に更新する時期が来たと判断したとき、[レイアウトの場所を更新し](update-a-network-installation-of-visual-studio.md)、次のようにして更新されたファイルを組み込むことができます。

1. 次のようなコマンドを使用します。

   ```cmd
   vs_enterprise.exe --layout \\server\share\VS --lang en-US
   ```

2. 更新後のレイアウトの response.json ファイルにカスタマイズ内容が引き続き含まれているようにします。特に次のような channelUri の変更内容です。

   ```json
   "channelUri":"\\\\server\\share\\VS\\ChannelManifest.json"
   ```

   このレイアウトからの既存の Visual Studio インストールは `\\server\share\VS\ChannelManifest.json` で更新プログラムを探します。 この channelManifest.json がユーザーがインストールしているものより新しい場合、Visual Studio は更新プログラムが利用できることをユーザーに通知します。

   新しいインストールでは、更新されたバージョンの Visual Studio がレイアウトから直接インストールされます。

## <a name="controlling-notifications-in-the-visual-studio-ide"></a>Visual Studio IDE の通知を制御する

::: moniker range="vs-2017"

上述のとおり、Visual Studio はそのインストール元である場所 (ネットワーク共有やインターネットなど) で更新プログラムが利用できないか確認します。 更新プログラムが利用可能になると、Visual Studio は、ユーザーへの通知としてウィンドウの右上隅に通知フラグを表示します。

   ![更新プログラムの通知フラグ](media/notification-flag.png)

::: moniker-end

::: moniker range="vs-2019"

上述のとおり、Visual Studio はそのインストール元である場所 (ネットワーク共有やインターネットなど) で更新プログラムが利用できないか確認します。 更新プログラムが利用可能になると、Visual Studio では、ユーザーへの通知としてウィンドウの右下隅に通知アイコンが表示されます。

   ![Visual Studio IDE の通知アイコン](media/vs-2019/notification-bar.png "Visual Studio IDE の通知アイコン")

::: moniker-end

エンドユーザーに更新プログラムを通知したくない場合は、通知を無効にすることができます。 (たとえば、中央のソフトウェア配布メカニズムを使用して更新プログラムを提供する場合、通知を無効にしたい場合があります。)

::: moniker range="vs-2017"

Visual Studio 2017 は[プライベート レジストリにレジストリ エントリを保存する](tools-for-managing-visual-studio-instances.md#editing-the-registry-for-a-visual-studio-instance)ので、そのレジストリを通常の方法で直接編集することはできません。 ただし、Visual Studio には `vsregedit.exe` ユーティリティが含まれます。これを利用し、Visual Studio 設定を変更できます。 次のコマンドで通知をオフにできます。

```cmd
vsregedit.exe set "C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise" HKCU ExtensionManager AutomaticallyCheckForUpdates2Override dword 0
```

::: moniker-end

::: moniker range="vs-2019"

Visual Studio 2019 は[プライベート レジストリにレジストリ エントリを保存する](tools-for-managing-visual-studio-instances.md#editing-the-registry-for-a-visual-studio-instance)ので、そのレジストリを通常の方法で直接編集することはできません。 ただし、Visual Studio には `vsregedit.exe` ユーティリティが含まれます。これを利用し、Visual Studio 設定を変更できます。 次のコマンドで通知をオフにできます。

```cmd
vsregedit.exe set "C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise" HKCU ExtensionManager AutomaticallyCheckForUpdates2Override dword 0
```

::: moniker-end

(編集したいインストール済みのインスタンスと一致するようにディレクトリを置き換えてください。)

> [!TIP]
> [vswhere.exe](tools-for-managing-visual-studio-instances.md#detecting-existing-visual-studio-instances) を利用し、クライアント ワークステーションで特定のインスタンスの Visual Studio を見つけます。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio のインストール](install-visual-studio.md)
* [Visual Studio 管理者ガイド](visual-studio-administrator-guide.md)
* [コマンド ライン パラメーターを使用して Visual Studio をインストールする](use-command-line-parameters-to-install-visual-studio.md)
* [Visual Studio インスタンスの管理用のツール](tools-for-managing-visual-studio-instances.md)
* [Visual Studio の製品ライフサイクルとサービス](/visualstudio/releases/2019/servicing/)

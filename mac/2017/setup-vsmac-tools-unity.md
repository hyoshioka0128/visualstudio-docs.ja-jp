---
title: Visual Studio for Mac Tools for Unity をセットアップする
description: Visual Studio for Mac で使用するために Unity ツールを設定し、インストールする
author: therealjohn
ms.author: johmil
ms.date: 05/25/2018
ms.assetid: 83FDD7A3-5D16-4B4B-9080-078E3FB5C623
ms.topic: how-to
ms.openlocfilehash: 1ea23f701f251476693108b51da570fbcbaa7756
ms.sourcegitcommit: 5335a9864d5747bc917ed28d4ebeade3076b10e7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2020
ms.locfileid: "85950435"
---
# <a name="set-up-visual-studio-for-mac-tools-for-unity"></a>Visual Studio for Mac Tools for Unity を設定する

このセクションでは、Visual Studio for Mac Tools for Unity を使い始める方法について説明します。

## <a name="install-visual-studio-for-mac"></a>Visual Studio for Mac をインストールする

### <a name="unity-bundled-installation"></a>Unity バンドル済みインストール

Unity 2018.1 以降、Visual Studio for Mac は Unity の既定の C# 統合開発環境 (IDE) であり、Unity Download Assistant および Unity Hub インストール ツールに含まれます。 [store.unity.com](https://store.unity.com/) から Unity をダウンロードします。

インストールのとき、Unity でインストールするコンポーネントの一覧で Visual Studio for Mac がオンになっていることを確認します。

#### <a name="unity-hub"></a>Unity Hub

![Unity Hub のインストール](media/setup-vsmac-tools-unity-image7.png)

#### <a name="unity-download-assistant"></a>Unity Download Assistant

![Unity Download Assistant のインストール](media/setup-vsmac-tools-unity-image8.png)

#### <a name="check-for-updates-to-visual-studio-for-mac"></a>Visual Studio for Mac の更新プログラムを確認する

Unity のインストールに含まれる Visual Studio for Mac のバージョンが、最新できない可能性があります。 更新プログラムを調べて、最新のツールと機能にアクセスできることを確認することをお勧めします。

* [Visual Studio for Mac を更新する](update.md)

### <a name="manual-installation"></a>手動のインストール

Unity 5.6.1 以降は既にあるが、Visual Studio for Mac はない場合は、Visual Studio for Mac を手動でインストールすることができます。 無料の Community Edition を含む Visual Studio for Mac のすべてのエディションが、Visual Studio for Mac Tools for Unity にバンドルされています。

* Visual Studio for Mac を [visualstudio.microsoft.com](https://visualstudio.microsoft.com/) からダウンロードします。
* Visual Studio for Mac Tools for Unity は、インストール プロセスの間に自動的にインストールされます。
* インストールに関するその他のヘルプについては、[インストール ガイド](/visualstudio/mac/installation/?view=vsmac-2017)の手順に従ってください。

> [!NOTE]
> Visual Studio for Mac Tools for Unity では、Unity バージョン 5.6.1 以降が必要です。 お使いの Unity のバージョンで Visual Studio Tools for Unity が有効になっていることを確認するには、Unity のメニューから **[About Unity]\(Unity について\)** を選び、ダイアログの左下に [Microsoft Visual Studio Tools for Unity enabled]\(Microsoft Visual Studio Tools for Unity は有効です\) と表示されていることを確認します。
>
> ![Unity について](media/setup-vsmac-tools-unity-image3.png)

## <a name="confirm-that-the-visual-studio-for-mac-tools-for-unity-extension-is-enabled"></a>Visual Studio for Mac Tools for Unity 拡張機能が有効になっていることを確認する

Visual Studio for Mac Tools for Unity 拡張機能は既定で有効になりますが、それを確認し、インストールされているバージョン番号を調べることができます。

1. Visual Studio のメニューから **[拡張機能]** を選びます。

   ![[拡張機能] を選ぶ](media/setup-vsmac-tools-unity-image1.png)

2. [ゲーム開発] セクションを展開し、Visual Studio for Mac Tools for Unity エントリを確認します。

   ![Unity エントリの表示](media/setup-vsmac-tools-unity-image2.png)

## <a name="configure-unity-for-use-with-visual-studio-for-mac"></a>Visual Studio for Mac で使用するために Unity を構成する

Unity 2018.1 以降では、Visual Studio を Unity の既定の外部スクリプト エディターにする必要があります。 以下の手順で、これを確認したり、外部スクリプト エディターを Visual Studio に変更したりできます。

1. Unity メニューから **[Preferences]\(ユーザー設定\)** を選びます。

   ![[Preferences]\(ユーザー設定\) を選ぶ](media/setup-vsmac-tools-unity-image4.png)

2. [Preferences]\(ユーザー設定\) ダイアログで、 **[External Tools]\(外部ツール\)** タブを選びます。

3. [External Script Editor]\(外部スクリプト エディター\) ドロップダウン リストから、 **[Visual Studio]** が一覧にある場合はそれを選び、ない場合は **[Browse]\(参照\)** を選びます。

   ![Visual Studio を選ぶ](media/setup-vsmac-tools-unity-image5.png)

4. **[Browse]\(参照\)** を選んだ場合は、[Applications]\(アプリケーション\) ディレクトリに移動し、Visual Studio を選んで、 **[Open]\(開く\)** をクリックします。

   ![[Open]\(開く\) を選択する](media/setup-vsmac-tools-unity-image6.png)

5. **[External Script Editor]\(外部スクリプト エディター\)** ボックスの一覧で Visual Studio を選んだ後、[Preferences]\(ユーザー設定\) ダイアログを閉じて構成プロセスを完了します。
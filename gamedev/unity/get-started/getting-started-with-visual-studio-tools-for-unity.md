---
title: Visual Studio Tools for Unity の使用を開始する | Microsoft Docs
description: Visual Studio for Unity の開発をインストールしてセットアップする方法について説明します。
ms.custom: ''
ms.date: 07/13/2020
ms.technology: vs-unity-tools
ms.prod: visual-studio-dev16
ms.topic: how-to
ms.assetid: 66b5b4eb-13b5-4071-98d2-87fafa4598a8
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
zone_pivot_groups: platform
ms.openlocfilehash: 1f8cbe1629aab6a177a46888fe25cf8e3565d91d
ms.sourcegitcommit: 620d30c60da8f9805fce524fe4951cf40f28297d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97903754"
---
# <a name="get-started-with-visual-studio-and-unity"></a>Visual Studio と Unity を使ってみる

> [!NOTE]
> このガイドでは、unity Hub プログラムを使用して Unity が既にインストールされていることを前提としています。 Unity を初めて使用する場合は、unity の学習と、 [unity でのはじめにに関するチュートリアル](https://learn.unity.com/course/getting-started-with-unity) を最初に実行することをお勧めします。

## <a name="install-unity-support-for-visual-studio"></a>Unity support for Visual Studio のインストール

Visual Studio Tools for Unity は、C# などの記述とデバッグをサポートする無料の拡張機能です。 拡張機能に含まれる内容の完全な一覧については、 [「Tools For Unity の概要」](./visual-studio-tools-for-unity.md) を参照してください。

:::zone pivot="windows"

> [!NOTE]
> このインストールガイドは、Visual Studio を対象としています。 Visual Studio Code を使用している場合は、 [VS Code のドキュメントを使用した Unity 開発に関する](https://code.visualstudio.com/docs/other/unity)ページを参照してください。

1. [Visual Studio インストーラーをダウンロードする](/visualstudio/docs/install/install-visual-studio.md)か、既にインストールされている場合は実行します。
2. **[変更]** をクリックします (既にインストールされている場合)。または、 **[インストール]** をクリックして、目的のバージョンの Visual Studio をインストールします (新規インストール)。
3. [ **ワークロード** ] タブで、[ **ゲーム** ] セクションまでスクロールし、[ **Unity を使用したゲーム開発** ] ワークロードを選択します。

    ![インストーラーの [Unity を使用したゲーム開発] ワークロードボックス](../media/vs/unity-workload.png)

:::zone-end
:::zone pivot="macos"

> [!NOTE]
> このインストールガイドは Visual Studio for Mac を対象としています。 Visual Studio Code を使用している場合は、 [VS Code のドキュメントを使用した Unity 開発に関する](https://code.visualstudio.com/docs/other/unity)ページを参照してください。

Tools for Unity は Visual Studio for Mac のインストールに含まれており、個別のインストール手順は必要ありません。 これは、[ **Visual Studio for Mac > 拡張機能 > ゲーム開発** ] メニューで確認できます。 **Visual Studio for Mac Tools For Unity** が有効になっている必要があります。

![Visual Studio for Mac Tools for Unity が有効になっている拡張機能マネージャービュー](../media/vsm/unity-workload.png)

:::zone-end

## <a name="check-for-updates"></a>更新プログラムをチェックする

最新のバグ修正、機能、および Unity サポートを利用できるように、Visual Studio と Visual Studio for Mac を更新しておくことをお勧めします。 これには、Unity バージョンの更新は必要ありません。

:::zone pivot="windows"

1. [ **ヘルプ > [更新プログラムの確認** ] メニューをクリックします。

    ![Visual Studio 2019 の [更新プログラムの確認] メニュー](../media/vs/check-for-updates.png)

2. 利用可能な更新プログラムがある場合は、Visual Studio インストーラーに新しいバージョンが表示されます。 **[更新]** ボタンをクリックします。

:::zone-end
:::zone pivot="macos"

1. [ **Visual Studio for Mac > [更新プログラムの確認** ] メニューをクリックして、 **Visual Studio の更新** ダイアログを開きます。
2. 利用可能な更新プログラムがある場合は、[ **インストール** ] ボタンをクリックします。

:::zone-end

## <a name="configure-unity-to-use-visual-studio"></a>Visual Studio を使用するように Unity を構成する

既定では、Unity は、Visual Studio または Visual Studio for Mac をスクリプトエディターとして使用するように構成されている必要があります。 これを確認するか、Unity エディターから外部スクリプトエディターを Visual Studio の特定のバージョンに変更することができます。

:::zone pivot="windows"

1. Unity エディターで、[ **> 設定の編集** ] メニューを選択します。
2. 左側の [ **外部ツール** ] タブを選択します。
3. [ **外部スクリプトエディター** ] ドロップダウンリストには、Visual Studio のさまざまなインストールを選択する方法が用意されています。 ドロップダウンリストから [ **参照...** ] をクリックして、一覧にないバージョンを追加することもできます。

    ![Windows 上の Unity エディターの [外部ツール] 基本設定メニュー](../media/vs/preferences-external-tools.png)

4. **[Browse...]\(参照...\)** を選択した場合は、Visual Studio インストール ディレクトリの中の **Common7/IDE** ディレクトリに移動し、**devenv.exe** を選択します。 次に、[ **開く**] をクリックします。
5. **[External Script Editor]\(外部スクリプト エディター\)** の一覧から Visual Studio を選択した後、 **[Editor Attaching]\(エディターのアタッチ\)** チェックボックスがオンになっていることを確認します。
6. **[Preferences]\(ユーザー設定\)** ダイアログを閉じて、構成プロセスを完了します。

:::zone-end
:::zone pivot="macos"

1. Unity エディターで、[ **unity > 基本設定** ] メニューを選択します。
2. 左側の [ **外部ツール** ] タブを選択します。
3. [ **外部スクリプトエディター** ] ドロップダウンリストには、Visual Studio のさまざまなインストールを選択する方法が用意されています。 ドロップダウンリストから [ **参照...** ] をクリックして、一覧にないバージョンを追加することもできます。

    ![MacOS の Unity エディターの [外部ツール] 基本設定メニュー](../media/vsm/preferences-external-tools.png)

4. **[Preferences]\(ユーザー設定\)** ダイアログを閉じて、構成プロセスを完了します。

:::zone-end

## <a name="next-steps"></a>次のステップ

 Visual Studio で Unity プロジェクトを操作およびデバッグする方法については、 [Visual Studio Tools for Unity の使用](using-visual-studio-tools-for-unity.md)に関するページを参照してください。

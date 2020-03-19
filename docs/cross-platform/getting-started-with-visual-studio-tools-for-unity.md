---
title: Visual Studio Tools for Unity の使用を開始する | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2018
ms.technology: vs-unity-tools
ms.topic: conceptual
ms.assetid: 66b5b4eb-13b5-4071-98d2-87fafa4598a8
author: conceptdev
ms.author: crdun
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: c22b9c25f95ea26f2cdaf5c2035fb7a373123241
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79306963"
---
# <a name="get-started-with-visual-studio-tools-for-unity"></a>Visual Studio Tools for Unity の使用を開始する

## <a name="install-visual-studio"></a>Visual Studio のインストール

### <a name="unity-bundled-installation"></a>Unity バンドル済みインストール

Unity 2018.1 以降、Visual Studio は Unity の既定の C# スクリプト エディターであり、Unity Download Assistant および Unity Hub インストール ツールに含まれます。

- [store.unity.com](https://store.unity.com/) から Unity をダウンロードします。

インストールのとき、Unity でインストールするコンポーネントの一覧で Visual Studio がオンになっていることを確認します。

#### <a name="unity-hub"></a>Unity Hub

![Unity Hub のインストール](media/vstu_unity-hub.png)

#### <a name="unity-download-assistant"></a>Unity Download Assistant

![Unity Download Assistant のインストール](media/vstu_download-assistant.png)

#### <a name="check-for-updates-to-visual-studio"></a>Visual Studio の更新プログラムを確認する

Unity のインストールに含まれる Visual Studio のバージョンが、最新でない場合があります。 更新プログラムを調べて、最新のツールと機能にアクセスできることを確認することをお勧めします。

- [Visual Studio の更新](../install/update-visual-studio.md)

### <a name="manual-installation"></a>手動のインストール

Visual Studio 2017 が既にインストールされている場合、または手動でインストールする場合は、Visual Studio インストーラーを実行します。

1. [Visual Studio インストーラーをダウンロード](../install/install-visual-studio.md)します。既にインストールされている場合は、それを開きます。

1. **[変更]** をクリックします (既にインストールされている場合)。または、 **[インストール]** をクリックして、目的のバージョンの Visual Studio をインストールします (新規インストール)。

1. **[ワークロード]** タブで、 **[モバイルとゲーム]** セクションまでスクロールし、 **[Unity によるゲーム開発]** ワークロードを選択します。

    ![Unity ワークロード](media/vstu_unity-workload.png)

1. **[変更]** をクリックします (既にインストールされている場合)。または、インストーラー ウィンドウの右下にある **[インストール]** をクリックします (新規インストール)。

## <a name="configure-unity-for-use-with-visual-studio"></a>Visual Studio で使用するために Unity を構成する

Unity 2018.1 以降では、Visual Studio を Unity の既定の外部スクリプト エディターにする必要があります。 以下の手順で、これを確認したり、外部スクリプト エディターを特定のバージョンの Visual Studio に変更したりできます。

1. **[Edit]\(編集\)** メニューから **[Preferences]\(ユーザー設定\)** を選びます。

   ![[Preferences]\(ユーザー設定\) を選ぶ](media/vstu_unity-preferences.png)

2. [Preferences]\(ユーザー設定\) ダイアログで、 **[External Tools]\(外部ツール\)** タブを選びます。

3. **[External Script Editor]\(外部スクリプト エディター\)** ドロップダウン リストから、目的のバージョンの Visual Studio が一覧にある場合はそれを選び、ない場合は **[Browse]\(参照\)** を選びます。

   ![Visual Studio を選ぶ](media/vstu_unity-external-tools.png)

4. **[Browse...]\(参照...\)** を選択した場合は、Visual Studio インストール ディレクトリの中の **Common7/IDE** ディレクトリに移動し、**devenv.exe** を選択します。 次に、 **[Open]** をクリックします。

   ![[Open]\(開く\) を選ぶ](media/vstu_browse-for-application.png)

5. **[External Script Editor]\(外部スクリプト エディター\)** の一覧から Visual Studio を選択した後、 **[Editor Attaching]\(エディターのアタッチ\)** チェックボックスがオンになっていることを確認します。

6. **[Preferences]\(ユーザー設定\)** ダイアログを閉じて、構成プロセスを完了します。

## <a name="support-for-older-versions"></a>古いバージョンのサポート

 Visual Studio Tools for Unity を Visual Studio Marketplace からダウンロードしてインストールします。 ご使用の Visual Studio バージョンに適したパッケージをインストールする必要があります。

- Visual Studio 2015 Community、Visual Studio 2015 Professional、または Visual Studio 2015 Enterprise の場合:

   [Visual Studio 2015 Tools for Unity をダウンロード](https://marketplace.visualstudio.com/items?itemName=SebastienLebreton.VisualStudio2015ToolsforUnity)

> [!NOTE]
> Visual Studio Tools for Unity では、Unity 5.2 以降と、拡張機能をサポートしているバージョンの Visual Studio (Visual Studio Community、Professional、Premium、Enterprise など) が必要です。 お使いの Unity のインストールで Visual Studio Tools for Unity が有効になっていることを確認するには、 **[Help]\(ヘルプ\)** メニューから **[About Unity]\(Unity について\)** を選び、ダイアログの左下に [Microsoft Visual Studio Tools for Unity enabled]\(Microsoft Visual Studio Tools for Unity は有効です\) と表示されていることを確認します。
> ![Unity について](media/vstu_about-unity.png)

## <a name="next-steps"></a>次のステップ

 Visual Studio で Unity プロジェクトを操作およびデバッグする方法については、「[Visual Studio Tools for Unity](../cross-platform/using-visual-studio-tools-for-unity.md)」をご覧ください。

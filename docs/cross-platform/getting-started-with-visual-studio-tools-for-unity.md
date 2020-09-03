---
title: Visual Studio Tools for Unity の使用を開始する | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2020
ms.technology: vs-unity-tools
ms.topic: how-to
ms.assetid: 66b5b4eb-13b5-4071-98d2-87fafa4598a8
author: indiesaudi
ms.author: crdun
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: a8f3e183bd72e9894eae55a5ed7c4f9322d44953
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "88250096"
---
# <a name="get-started-with-visual-studio-tools-for-unity"></a>Visual Studio Tools for Unity の使用を開始する

## <a name="install-visual-studio"></a>Visual Studio のインストール

### <a name="unity-bundled-installation"></a>Unity バンドル済みインストール

Unity 2018.1 以降、Visual Studio は Unity の既定の C# スクリプト エディターであり、Unity Download Assistant および Unity Hub インストール ツールに含まれます。

- [store.unity.com](https://store.unity.com/) から Unity をダウンロードします。

インストールのとき、Unity でインストールするコンポーネントの一覧で Visual Studio がオンになっていることを確認します。

#### <a name="unity-hub"></a>Unity Hub

:::moniker range="vs-2017"
![Unity Hub のインストール](media/vs-2017/vstu-unity-hub.png)
:::moniker-end
:::moniker range=">=vs-2019"
![Unity Hub のインストール](media/vs-2019/vstu-unity-hub.png)
:::moniker-end

:::moniker range="vs-2017"

#### <a name="unity-download-assistant"></a>Unity Download Assistant

![Unity Download Assistant のインストール](media/vs-2017/vstu-download-assistant.png)

Unity のインストールに含まれる Visual Studio のバージョンが、最新でない場合があります。 Visual Studio 2017 をインストールするように求められた場合は、新しいバージョンの Visual Studio を手動でインストールすることをお勧めします。
:::moniker-end

### <a name="manual-installation"></a>手動インストール

Visual Studio が既にインストールされている場合、または手動でインストールする場合は、Visual Studio インストーラーを実行します。

1. [Visual Studio インストーラーをダウンロード](../install/install-visual-studio.md)します。既にインストールされている場合は、それを開きます。

1. **[変更]** をクリックします (既にインストールされている場合)。または、 **[インストール]** をクリックして、目的のバージョンの Visual Studio をインストールします (新規インストール)。

1. **[ワークロード]** タブで、 **[モバイルとゲーム]** セクションまでスクロールし、 **[Unity によるゲーム開発]** ワークロードを選択します。

   :::moniker range="vs-2017"
   ![Unity ワークロード](media/vs-2017/vstu-unity-workload.png)
   :::moniker-end
   :::moniker range=">=vs-2019"
   ![Unity ワークロード](media/vs-2019/vstu-unity-workload.png)
   :::moniker-end

1. **[変更]** をクリックします (既にインストールされている場合)。または、インストーラー ウィンドウの右下にある **[インストール]** をクリックします (新規インストール)。

#### <a name="check-for-updates-to-visual-studio"></a>Visual Studio の更新プログラムを確認する

Visual Studio 内の更新プログラムを調べて、最新のツールと機能にアクセスできることを確認することをお勧めします。 これによって Unity プロジェクトが破損することはありません。

- [Visual Studio の更新](../install/update-visual-studio.md)

## <a name="configure-unity-for-use-with-visual-studio"></a>Visual Studio で使用するために Unity を構成する

Unity 2018.1 以降では、Visual Studio を Unity の既定の外部スクリプト エディターにする必要があります。 以下の手順で、これを確認したり、外部スクリプト エディターを特定のバージョンの Visual Studio に変更したりできます。

1. **[Edit]\(編集\)** メニューから **[Preferences]\(ユーザー設定\)** を選びます。

   :::moniker range="vs-2017"
   ![[Preferences]\(ユーザー設定\) を選ぶ](media/vs-2017/vstu-unity-preferences.png)
   :::moniker-end
   :::moniker range=">=vs-2019"
   ![[Preferences]\(ユーザー設定\) を選ぶ](media/vs-2019/vstu-unity-preferences.png)
   :::moniker-end

2. [Preferences]\(ユーザー設定\) ダイアログで、 **[External Tools]\(外部ツール\)** タブを選びます。

3. **[External Script Editor]\(外部スクリプト エディター\)** ドロップダウン リストから、目的のバージョンの Visual Studio が一覧にある場合はそれを選び、ない場合は **[Browse]\(参照\)** を選びます。

   :::moniker range="vs-2017"
   ![Visual Studio を選ぶ](media/vs-2017/vstu-unity-external-tools.png)
   :::moniker-end
   :::moniker range=">=vs-2019"
   ![Visual Studio を選ぶ](media/vs-2019/vstu-unity-external-tools.png)
   :::moniker-end

4. **[Browse...]\(参照...\)** を選択した場合は、Visual Studio インストール ディレクトリの中の **Common7/IDE** ディレクトリに移動し、**devenv.exe** を選択します。 次に、 **[Open]\(開く\)** をクリックします。

   :::moniker range="vs-2017"
   ![[Open]\(開く\) を選ぶ](media/vs-2017/vstu-browse-for-application.png)
   :::moniker-end
   :::moniker range=">=vs-2019"
   ![[Open]\(開く\) を選ぶ](media/vs-2019/vstu-browse-for-application.png)
   :::moniker-end

5. **[External Script Editor]\(外部スクリプト エディター\)** の一覧から Visual Studio を選択した後、 **[Editor Attaching]\(エディターのアタッチ\)** チェックボックスがオンになっていることを確認します。

6. **[Preferences]\(ユーザー設定\)** ダイアログを閉じて、構成プロセスを完了します。

## <a name="support-for-older-versions"></a>古いバージョンのサポート

Visual Studio Tools for Unity を Visual Studio Marketplace からダウンロードしてインストールします。 ご使用の Visual Studio バージョンに適したパッケージをインストールする必要があります。

- Visual Studio 2015 Community、Visual Studio 2015 Professional、または Visual Studio 2015 Enterprise の場合:

   [Visual Studio 2015 Tools for Unity をダウンロード](https://marketplace.visualstudio.com/items?itemName=SebastienLebreton.VisualStudio2015ToolsforUnity)

> [!NOTE]
> Visual Studio Tools for Unity では、Unity 5.2 以降と、拡張機能をサポートしているバージョンの Visual Studio (Visual Studio Community、Professional、Premium、Enterprise など) が必要です。 お使いの Unity のインストールで Visual Studio Tools for Unity が有効になっていることを確認するには、 **[Help]\(ヘルプ\)** メニューから **[About Unity]\(Unity について\)** を選び、ダイアログの左下に [Microsoft Visual Studio Tools for Unity enabled]\(Microsoft Visual Studio Tools for Unity は有効です\) と表示されていることを確認します。
> ![Unity について](media/vs-2019/vstu-about-unity.png)

## <a name="next-steps"></a>次の手順

 Visual Studio で Unity プロジェクトを操作およびデバッグする方法については、「[Visual Studio Tools for Unity](../cross-platform/using-visual-studio-tools-for-unity.md)」をご覧ください。

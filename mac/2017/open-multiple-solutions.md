---
title: '方法: 複数のソリューションを開く'
description: Visual Studio for Mac で複数のソリューションを開く方法、およびアプリケーションの複数のインスタンスを開く方法について説明します。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 07/19/2018
ms.assetid: 592BA4E3-8DEF-4FCD-8BA0-519A4CEEE03E
ms.custom: video
ms.openlocfilehash: 3568ab8dd68deb83d668c6e46f556516e29a81ae
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "74984999"
---
# <a name="open-multiple-solutions-or-instances-of-visual-studio-for-mac"></a>Visual Studio for Mac の複数のソリューションまたはインスタンスを開く

既定では、Visual Studio for Mac など、Mac のすべてのアプリケーションは、"_単一インスタンス_" アプリです。 つまり、使用するアプリケーションが既に開かれている場合 (ドック内でアイコンの下のドットによって示されます)、アイコンを再び選択すると、新しいインスタンスではなく、実行中のインスタンスが開かれます。 [次のセクション](#open-a-second-instance-of-visual-studio-for-mac)で説明するように、アプリケーションのインスタンスを追加する必要がある場合は、インスタンスを開くようシステムに指示できます。

さらに、ソリューションを開くときは、新しいワークスペースでソリューションを開き、現在のワークスペースを閉じる (必要な場合) のが既定の動作です。 「[単一のインスタンス内で 2 つ目のソリューションを開く](#open-a-second-solution-inside-a-single-instance)」セクションで説明されているように、現在のワークスペースを開いたままにすることで、この既定の動作をオーバーライドできます。

## <a name="open-a-second-instance-of-visual-studio-for-mac"></a>Visual Studio for Mac の 2 つ目のインスタンスを開く

統合開発環境 (IDE) の 2 つ目のインスタンスを開くには、**ターミナル** アプリケーションを開いて、次の行を入力します。

```bash
open -n "/Applications/Visual Studio.app"
```

## <a name="open-a-second-solution-inside-a-single-instance"></a>単一のインスタンス内で 2 つ目のソリューションを開く

1 つ目のソリューションをそのままにして 2 つ目のソリューションを開くには、次の手順を使います。

1. 1 つ目のソリューションを既に開いた状態で、 **[ファイル]**  >  **[開く]** の順に選択します。
2. ファイル システムを参照して、既存のソリューションを検索します。
3. **.sln** ファイルを選択し、 **[オプション]** を選択します。

    ![.sln ファイルとオプションが強調表示されている Visual Studio for Mac のスクリーンショット](media/open-multiple-solutions-image3.png)

4. **[現在のワークスペースを閉じる]** ボックスをクリアします。

    ![[現在のワークスペースを閉じる] ボックスがクリアされた [オプション] ダイアログ ボックスのスクリーンショット](media/open-multiple-solutions-image1.png)

5. **[開く]** ボタンを選択して、Solution Pad で 2 つ目のソリューションを開きます。

または、最近ソリューションを開いた場合は、次の手順を使うこともできます。

1. **[ファイル]**  >  **[最近のソリューション]** の順に移動します。

    ![[最近のソリューション] メニューのスクリーンショット](media/open-multiple-solutions-image2.png)

1. **Ctrl** キーを押しながら、ソリューションを選択します。 この組み合わせにより、Solution Pad で 2 つ目のソリューションが開きます。

## <a name="related-video"></a>関連ビデオ

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Work-With-Multiple-Solutions/player]

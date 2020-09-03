---
title: '方法: IDE 内で移動する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- environments [Visual Studio], navigation
- documents [Visual Studio], navigating
- IDE, navigation
- navigation [Visual Studio]
- files [Visual Studio], navigating between
- windows [Visual Studio], navigating
- Window.NextDocumentWindowNav
- IDE navigator
ms.assetid: 6c36b6eb-c93f-496b-af08-4199f7afd8bd
caps.latest.revision: 33
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 89c4447eb6bbc4b2ae9f7667672626d5119c61d6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72651798"
---
# <a name="how-to-move-around-in-the-visual-studio-ide"></a>方法: Visual Studio IDE 内で移動する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

統合開発環境 (IDE) は、ユーザー設定やプロジェクトの要件に応じて、いくつかの異なる方法で、ウィンドウからウィンドウへ、またはファイルからファイルへ移動できるように設計されています。 エディターで開いているファイルを順番に表示することも、IDE 内でアクティブなすべてのツール ウィンドウを順番に表示することもできます。 また、最後にアクセスした順序に関係なく、エディターで開いている任意のファイルに直接切り替えることもできます。 これらの機能は、IDE で作業するときの生産性を向上するのに役立ちます。

> [!NOTE]
> 使用している設定またはエディションによっては、ダイアログ ボックスで使用可能なオプションや、メニュー コマンドの名前や位置がヘルプに記載されている内容と異なる場合があります。 このヘルプ ページは、**全般的な開発設定**を考慮して記述されています。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

## <a name="keyboard-shortcuts"></a>キーボード ショートカット
 Visual Studio のほぼすべてのメニュー コマンドにはショートカット キーがあります。 独自のカスタム ショートカットを作成することもできます。 詳細については、「[Visual Studio でのキーボード ショートカットの識別とカスタマイズ](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)」をご覧ください。

## <a name="navigating-among-files-in-the-editor"></a>エディターでファイル間を移動する
 エディターで開いているファイル間を移動する方法はいくつかあります。 アクセス順に基づいてファイル間を移動する、IDE Navigator を使用して現在開いている任意のファイルをすばやく見つける、あるいはお気に入りのファイルをタブにピン留めして常に表示されているようにする、などです。

 [戻る] と [次に進む] を使うと、Microsoft Internet Explorer で [戻る] と [進む] で履歴を表示するのと同じように、開いているファイルをアクセスした順番に基づいて切り替えることができます。

#### <a name="to-move-through-open-files-in-order-of-use"></a>使用順に開いているファイル内を移動するには

- 最も最近使用した順序で開いているドキュメントを表示するには、Ctrl キーを押しながらマイナス記号キーを押します。

- 逆の順序で開いているドキュメントを表示するには、Ctrl キーと Shift キーを押しながらマイナス記号キーを押します。

  > [!NOTE]
  > **[戻る]** と **[次に進む]** は **[表示]** メニューにもあります。

  また、ファイルを最後にアクセスしたときに関係なく、**IDE Navigator**、エディターの **[アクティブなファイル]** リスト、または **[Windows]** ダイアログ ボックスを使って、エディターで開いている特定のファイルを切り替えることができます。

  **IDE Navigator** は、Windows アプリケーションのスイッチャーのように動作します。 メニューからは利用できず、ショートカット キーを使用してのみアクセスできます。 2 つのコマンドのいずれかを使って **IDE Navigator** にアクセスし (下記参照)、表示したい順番でファイルを切り替えることができます。

  ![Visual Studio IDE ナビゲーター](../ide/media/vs2015-ide-navigator.png "VS2015_IDE_Navigator")

  `Window.PreviousDocumentWindowNav` では最後にアクセスしたファイルに移動することができ、`Window.NextDocumentWindowNav` では逆の順序で移動することができます。 [全般的な開発設定] では、Ctrl + Shift + Tab キーが `Window.PreviousDocumentWindowNav` に、Ctrl + Tab キーが `Window.NextDocumentWindowNav` に割り当てられてています。

> [!NOTE]
> 使っている設定の組み合わせの中に、このコマンドに割り当てられているショートカット キーの組み合わせがない場合は、**[オプション]** ダイアログ ボックスの **[キーボード]** ページを使って、独自のカスタム コマンドを割り当てることができます。 詳細については、「[Visual Studio でのキーボード ショートカットの識別とカスタマイズ](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)」をご覧ください。

#### <a name="to-switch-to-specific-files-in-the-editor"></a>エディターで特定のファイルに切り替えるには

- Ctrl + Tab キーを押して、**IDE Navigator** を表示します。 切り替える対象のファイルが選択されるまで、Ctrl キーを押さえたまま繰り返し Tab キーを押します。

    > [!TIP]
    > **[アクティブなファイル]** リストの順番を逆に切り替えるには、Ctrl キーと Shift キーを押さえたまま Tab キーを押します。

     \- または

- エディターの右上隅で、**[アクティブなファイル]** ボタンを選び、切り替え先のファイルをリストから選びます。

     \- または

- メニュー バーで、**[ウィンドウ]**、**[ウィンドウ]** の順に選びます。

- 一覧で表示するファイルを選び、**[開く]** を選びます。

## <a name="navigating-among-tool-windows-in-the-ide"></a>IDE のツール ウィンドウ間を移動する
 **IDE Navigator** では、IDE で開いているツール ウィンドウを順番に表示することもできます。 2 つのコマンドのいずれかを使って **IDE Navigator** にアクセスし、表示したい順番でツール ウィンドウを切り替えることができます。 `Window.PreviousToolWindowNav` では最後にアクセスしたファイルに移動することができ、`Window.NextToolWindowNav` では逆の順序で移動することができます。 [全般的な開発設定] では、Shift + Alt + F7 が `Window.PreviousDocumentWindowNav` に、Alt + F7 が `Window.NextDocumentWindowNav` に割り当てられています。

> [!NOTE]
> 使っている設定の組み合わせの中に、このコマンドに割り当てられているショートカット キーの組み合わせがない場合は、**[オプション]** ダイアログ ボックスの **[キーボード]** ページを使って、独自のカスタム コマンドを割り当てることができます。 詳細については、「[Visual Studio でのキーボード ショートカットの識別とカスタマイズ](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)」をご覧ください。

#### <a name="to-switch-to-a-specific-tool-window-in-the-ide"></a>IDE で特定のツール ウィンドウに切り替えるには

- Alt + F7 キーを押して、**IDE Navigator** を表示します。 切り替える対象のウィンドウが選択されるまで、Alt キーを押したまま繰り返し F7 キーを押します。

    > [!TIP]
    > **[アクティブなツール ウィンドウ]** リストの順番を逆に切り替えるには、Shift キーと Alt キーを押したまま F7 キーを押します。

## <a name="see-also"></a>参照
 [ウィンドウ レイアウトをカスタマイズする](../ide/customizing-window-layouts-in-visual-studio.md) [既定のキーボード ショートカット](../ide/default-keyboard-shortcuts-in-visual-studio.md)

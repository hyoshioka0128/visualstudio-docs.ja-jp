---
title: IDE 内で移動する方法
description: Visual Studio IDE 内で、ウィンドウ間、およびファイル間を移動するいくつかの方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
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
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 384a6252ef17709970f6e902dfdf83a157b0460a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99968048"
---
# <a name="how-to-move-around-in-the-visual-studio-ide"></a>方法: Visual Studio IDE 内で移動する

統合開発環境 (IDE) は、ユーザー設定やプロジェクトの要件に応じて、いくつかの異なる方法で、ウィンドウからウィンドウへ、またはファイルからファイルへ移動できるように設計されています。 エディターで開いているファイルを順番に表示することも、IDE 内でアクティブなすべてのツール ウィンドウを順番に表示することもできます。 また、最後にアクセスした順序に関係なく、エディターで開いている任意のファイルに直接切り替えることもできます。 これらの機能は、IDE で作業するときの生産性を向上するのに役立ちます。

> [!NOTE]
> 使用している設定またはエディションによっては、ダイアログ ボックスで使用可能なオプションや、メニュー コマンドの名前や位置がこの記事に記載されている内容と異なる場合があります。 この記事は、**[全般]** 設定を念頭に置いて書かれています。 設定を、たとえば、 **[全般]** や **[Visual C++]** に変更するには、 **[ツール]** 、 **[設定のインポートとエクスポート]** 、 **[すべての設定をリセット]** の順に選択します。

## <a name="keyboard-shortcuts"></a>キーボード ショートカット

Visual Studio のほぼすべてのメニュー コマンドにはショートカット キーがあります。 独自のカスタム ショートカットを作成することもできます。 詳しくは、「[キーボード ショートカットの識別とカスタマイズ](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)」をご覧ください。

## <a name="navigate-among-files-in-the-editor"></a>エディターでファイル間を移動する

エディターで開いているファイル間を移動する方法はいくつかあります。 アクセス順に基づいてファイル間を移動する、IDE Navigator を使用して現在開いている任意のファイルをすばやく見つける、あるいはお気に入りのファイルをタブにピン留めして常に表示されているようにする、などです。

[戻る] と [次に進む] を使うと、Microsoft Internet Explorer で [戻る] と [進む] で履歴を表示するのと同じように、開いているファイルをアクセスした順番に基づいて切り替えることができます。

### <a name="to-move-through-open-files-in-order-of-use"></a>使用順に開いているファイル内を移動するには

- 最近使用した順序で開いているドキュメントをアクティブにするには、**Ctrl**+ **-** (ハイフン) キーを押します。

- 逆の順序で開いているドキュメントをアクティブにするには、**Ctrl**+**Shift**+ **-** (ハイフン) キーを押します。

    > [!NOTE]
    > **[戻る]** と **[次に進む]** は **[表示]** メニューにもあります。

また、ファイルを最後にアクセスしたときに関係なく、**IDE Navigator**、エディターの **[アクティブなファイル]** リスト、または **[Windows]** ダイアログ ボックスを使って、エディターで開いている特定のファイルを切り替えることができます。

**IDE Navigator** は、Windows アプリケーションのスイッチャーのように動作します。 メニューからは利用できず、ショートカット キーを使用してのみアクセスできます。 2 つのコマンドのいずれかを使って **IDE Navigator** にアクセスし (下記参照)、表示したい順番でファイルを切り替えることができます。

![Visual Studio IDE ナビゲーター](../ide/media/vs2015_ide_navigator.png)

`Window.PreviousDocumentWindowNav` では最後にアクセスしたファイルに移動することができ、`Window.NextDocumentWindowNav` では逆の順序で移動することができます。 **[全般的な開発設定]** では、**Shift**+**Alt**+**F7** が `Window.PreviousDocumentWindowNav` に、**Alt**+**F7** が `Window.NextDocumentWindowNav` に割り当てられています。

> [!NOTE]
> 使っている設定の組み合わせの中に、このコマンドに割り当てられているショートカット キーの組み合わせがない場合は、**[オプション]** ダイアログ ボックスの **[キーボード]** ページを使って、独自のカスタム コマンドを割り当てることができます。 詳しくは、「[キーボード ショートカットの識別とカスタマイズ](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)」をご覧ください。

### <a name="to-switch-to-specific-files-in-the-editor"></a>エディターで特定のファイルに切り替えるには

- **Ctrl**+**Tab** キーを押して、**IDE Navigator** を表示します。 切り替える対象のファイルが選択されるまで、**Ctrl** キーを押さえたまま繰り返し **Tab** キーを押します。

    > [!TIP]
    > **[アクティブなファイル]** リストの順番を逆に切り替えるには、**Ctrl**+**Shift** キーを押したまま **Tab** キーを押します。

    \- または

- エディターの右上隅で、**[アクティブなファイル]** ボタンを選び、切り替え先のファイルをリストから選びます。

    \- または

- メニュー バーで **[ウィンドウ]**  >  **[ウィンドウ]** の順に選択します。

- 一覧で表示するファイルを選び、**[開く]** を選びます。

## <a name="navigate-among-tool-windows-in-the-ide"></a>IDE のツール ウィンドウ間を移動する

**IDE Navigator** では、IDE で開いているツール ウィンドウを順番に表示することもできます。 2 つのコマンドのいずれかを使って **IDE Navigator** にアクセスし、表示したい順番でツール ウィンドウを切り替えることができます。 `Window.PreviousToolWindowNav` では最後にアクセスしたファイルに移動することができ、`Window.NextToolWindowNav` では逆の順序で移動することができます。 **[全般的な開発設定]** では、**Shift**+**Alt**+**F7** が `Window.PreviousDocumentWindowNav` に、**Alt**+**F7** が `Window.NextDocumentWindowNav` に割り当てられています。

> [!NOTE]
> 使っている設定の組み合わせの中に、このコマンドに割り当てられているショートカット キーの組み合わせがない場合は、**[オプション]** ダイアログ ボックスの **[キーボード]** ページを使って、独自のカスタム コマンドを割り当てることができます。 詳しくは、「[キーボード ショートカットの識別とカスタマイズ](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)」をご覧ください。

### <a name="to-switch-to-a-specific-tool-window-in-the-ide"></a>IDE で特定のツール ウィンドウに切り替えるには

- **Alt**+**F7** キーを押して、**IDE Navigator** を表示します。 切り替える対象のウィンドウが選択されるまで、**Alt** キーを押したまま繰り返し **F7** キーを押します。

    > [!TIP]
    > **[アクティブなツール ウィンドウ]** リストの順番を逆に切り替えるには、**Shift**+**Alt** キーを押したまま **F7** キーを押します。

## <a name="see-also"></a>関連項目

- [ウィンドウ レイアウトをカスタマイズする](../ide/customizing-window-layouts-in-visual-studio.md)
- [既定のキーボード ショートカット](../ide/default-keyboard-shortcuts-in-visual-studio.md)

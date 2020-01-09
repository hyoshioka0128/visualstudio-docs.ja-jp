---
title: Visual Studio をマウスなしで使用する
titleSuffix: ''
description: Visual Studio の統合開発環境 (IDE) でキーボードだけを使って移動したりコードを記述したりする方法について説明します。
ms.date: 05/10/2019
ms.topic: conceptual
helpviewer_keywords:
- Toolbox, shortcut keys
- shortcut keys [Visual Studio]
- windows [Visual Studio], accessibility
- dialog boxes [Visual Studio], shortcut keys
- accessibility [Visual Studio]
ms.assetid: d71a4cc1-d352-4164-8538-3f9fa070a331
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3b1beb2ccb6b3e3e2b74ed7deaf2f31443ee2466
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75569024"
---
# <a name="how-to-use-the-keyboard-exclusively"></a>キーボードだけを使用する方法

キーボード ショートカットを利用すれば、Visual Studio IDE 内での移動やコードの記述が簡単になります。 この記事では、キーボード ショートカットをさらに効果的に使用するための方法をいくつか紹介します。

Visual Studio のすべてのコマンド ショートカット キーの一覧については、[既定のキーボード ショートカット](../../ide/default-keyboard-shortcuts-in-visual-studio.md)に関する記事をご覧ください。

::: moniker range="vs-2017"

> [!TIP]
> アクセシビリティの更新の詳細については、ブログ記事「[Accessibility improvements in Visual Studio 2017](https://devblogs.microsoft.com/visualstudio/accessibility-improvements-in-visual-studio-2017-version-15-3/)」 (Visual Studio 2017 でのアクセシビリティの機能強化) をご覧ください。

::: moniker-end

> [!NOTE]
> 使用している設定または Visual Studio のエディションによっては、ヘルプの記載と異なるダイアログ ボックスやメニュー コマンドが表示される場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[リセット設定](../environment-settings.md#reset-settings)」を参照してください。

## <a name="toolbox-controls"></a>ツールボックス コントロール

マウスを使わずに、ツールボックスのコントロールをフォームまたはデザイナーに追加するには:

1. メニュー バーで **[表示]** 、 **[ツールボックス]** の順にクリックします。

2. **[ツールボックス]** タブでセクション間を移動するには、**Ctrl** キーを押しながら**上方向**キーを押すか、**Ctrl** キーを押しながら**下方向**キーを押します。

3. セクション内のコントロール間を移動するには、**上方向キー**または**下方向キー**を使います。

4. コントロールを選択したら、**Enter** キーを使用し、コントロールをフォームまたはデザイナーに追加します。

## <a name="dialog-box-options"></a>ダイアログ ボックス オプション

キーボードだけを使って、ダイアログ ボックスのオプション間を移動し、オプションの設定を変更するには:

1. **Tab** キーまたは **Shift**+**Tab** キーを使って、ダイアログ ボックス内のコントロール間を上下に移動します。

2. オプションの設定を変更するには:

   - ラジオ ボタンの場合は、**上方向**キーと**下方向**キーを使って、選択を変更します。

   - チェック ボックスの場合は、**Space キー**を押してオンまたはオフにします。

   - ドロップダウン リストの場合は、**Alt** キーを押しながら**下方向**キーを押して項目を表示し、**上方向**キーと**下方向**キーを使って選択した項目を変更します。

   - ボタンの場合は、**Enter** キーを選択して呼び出します。

   - グリッドの場合は、方向キーを使って移動します。 グリッド内のドロップダウン リストの場合は、**Shift** キーと **Alt** キーを押しながら**下方向キー**を押して項目を表示し、**上方向**キーと**下方向**キーを使って選択した項目を変更します。

## <a name="navigate-between-windows-and-files"></a>ウィンドウ間およびファイル間を移動する

- エディターまたはデザイナー内でファイル間を移動するには、**Ctrl**+**Tab** ショートカット キーボードを選択し、 **[アクティブなファイル]** が選択された IDE ナビゲーターを表示します。 強調表示されているファイルに移動するには、**Enter** キーを押します。

- ドッキングされたツール ウィンドウ間を移動するには、**Alt**+**F7** キーボード ショートカットを選択し、 **[アクティブなツール ウィンドウ]** が選択された IDE ナビゲーターを表示します。 強調表示されているウィンドウに移動するには、**Enter** キーを押します。

## <a name="move-and-dock-tool-windows"></a>ツール ウィンドウを移動およびドッキングする

1. 移動するツール ウィンドウに移動し、フォーカスを設定します。

2. **[ウィンドウ]** メニューで **[ドッキング可能]** オプションを選択します。

3. **Alt**+**Space キー**を押し、 **[移動]** を選択します。

   ドッキング ガイドのひし形が表示されます。

4. 方向キーを押して、ウィンドウを新しい場所に移動します。

   方向キーを押すと、ウィンドウと共にマウス ポインターが移動します。

5. 新しい場所に到達したら、方向キーを押して、ガイドのひし形の適切な部分にマウス ポインターを移動します。

   新しいドッキング場所にツール ウィンドウの輪郭が表示されます。

6. **Enter** キーを押します。

   ツール ウィンドウが、新しいドッキング場所の所定の位置にスナップされます。

## <a name="see-also"></a>関連項目

* [キーボード ショートカットの識別とカスタマイズ](../../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)
* [アクセシビリティのヒントとテクニック](../../ide/reference/accessibility-tips-and-tricks.md)
* [既定のキーボード ショートカット](../../ide/default-keyboard-shortcuts-in-visual-studio.md)
* [Microsoft 製品のアクセシビリティ](https://www.microsoft.com/accessibility/)

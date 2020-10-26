---
title: '方法: キーボード主体で操作する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Toolbox, shortcut keys
- shortcut keys [Visual Studio]
- windows [Visual Studio], accessibility
- dialog boxes [Visual Studio], shortcut keys
- keyboard shortcuts [Visual Studio]
- accessibility [Visual Studio]
ms.assetid: d71a4cc1-d352-4164-8538-3f9fa070a331
caps.latest.revision: 30
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c9a9ec5f83a6df3dab262e24aac5c36b2d65ef00
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75852374"
---
# <a name="how-to-use-the-keyboard-exclusively"></a>方法: キーボード主体で操作する
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] で提供されているさまざまな既定のショートカット キーの組み合わせを使うと、統合開発環境 (IDE) 内で移動やコーディングを簡単に行うことができます。 Visual Studio で使用されるショートカットキーの完全な一覧については、「 [既定のキーボードショートカット](../../ide/default-keyboard-shortcuts-in-visual-studio.md)」を参照してください。 その他の Microsoft 製品で使用できるキーボードショートカットの詳細については、「」を参照してください [http://www.microsoft.com/enable/products/keyboard.aspx](https://www.microsoft.com/enable/products/keyboard.aspx) 。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

## <a name="toolbox-controls"></a>ツールボックス コントロール
 キーボードを使って、ツールボックスのコントロールをフォームまたはデザイナーに追加できます。

#### <a name="to-add-controls-from-the-toolbox-to-a-designer-from-the-keyboard"></a>キーボードを使ってツールボックスからデザイナーにコントロールを追加するには

1. メニュー バーで **[表示]**、**[ツールボックス]** の順に選択します。

2. 現在の [ツールボックス] タブのセクション間を移動するには、Ctrl + 上方向キーまたは Ctrl + 下方向キーを押します。

3. コントロール間を移動するには、上方向キーまたは**下方向**キーを押します。

4. コントロールを選択した後、Enter キーを押します。

   コントロールがフォームまたはデザイナーに追加されます。

## <a name="dialog-box-options"></a>ダイアログ ボックス オプション
 キーボードを使って、ダイアログ ボックスのオプション間を移動し、オプションの設定を変更できます。

#### <a name="to-set-dialog-box-options-from-the-keyboard"></a>キーボードを使ってダイアログ ボックスのオプションを設定するには

1. **Tab** キーまたは **Shift + Tab** キーを使って、ダイアログ ボックス内のコントロール間を上下に移動します。

2. オプションの設定を変更するには:

    - ラジオ ボタンの場合は、**上方向**キーと**下方向**キーを使って、選択を変更します。

    - チェック ボックスの場合は、**Space キー**を使ってオンまたはオフにします。

    - ドロップダウンリストの場合は、 **ALT キーを押し**ながら下方向キーを使用し  +  **DOWNARROW**て項目を表示し、 **uparrow**と**下方向キー**を使用して選択した項目を変更します。

    - ボタンの場合は、 **enter** キーを押してを呼び出します。

    - グリッドの場合は、方向キーを使って移動します。 グリッド内のドロップダウンリストの場合は、 **SHIFT**ALT ↓キーを使用して項目を表示し、  +  **ALT**  +  **DOWNARROW** **uparrow**と**下方向**キーを使用して、選択した項目を変更します。

## <a name="window-and-file-navigation"></a>ウィンドウおよびファイルに関する移動
 IDE では、キーボードを使って開いているツール ウィンドウやドキュメント ウィンドウ間を移動するための方法が複数用意されています。 また、キーボードを使って、ツール ウィンドウを別の場所に移動してドッキングすることもできます。

#### <a name="to-navigate-among-windows-and-files-in-the-ide-from-the-keyboard"></a>キーボードを使って IDE 内のウィンドウ間およびファイル間を移動するには

- エディターまたはデザイナー内でファイル間を移動するには、Ctrl + Tab キーを押して、**[アクティブなファイル]** が選択された IDE ナビゲーターを表示します。 強調表示されているファイルに移動するには、Enter キーを押します。

- ドッキングされたツール ウィンドウ間を移動するには、Alt + F7 キーを押して、**[アクティブなツール ウィンドウ]** が選択された IDE ナビゲーターを表示します。 強調表示されているウィンドウに移動するには、Enter キーを押します。

#### <a name="to-move-and-dock-tool-windows-from-the-keyboard"></a>キーボードを使ってツール ウィンドウを移動してドッキングするには

1. 移動するツール ウィンドウに移動し、フォーカスを設定します。

2. **[ウィンドウ]** メニューの **[ドッキング可能]** をクリックします。

3. **ALT**Space キーを押して  +  **Space** 、[**移動**] を選択します。

     ドッキング ガイドのひし形が表示されます。

4. **方向**キーを使用して、ウィンドウを新しい場所に移動します。

     **方向**キーを使用すると、マウスポインターがウィンドウと一緒に移動します。

5. 新しい場所に到達したら、**方向**キーを押して、ガイドのひし形の適切な部分にマウス ポインターを移動します。

     新しいドッキング場所にツール ウィンドウの輪郭が表示されます。

6. **Enter**キーを押します。

     ツール ウィンドウが、新しいドッキング場所の所定の位置にスナップされます。

## <a name="see-also"></a>参照
 [キーボードショートカットの識別とカスタマイズの](../../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)[アクセシビリティのヒントとテクニック既定の](../../ide/reference/accessibility-tips-and-tricks.md)[キーボードショートカット](../../ide/default-keyboard-shortcuts-in-visual-studio.md)

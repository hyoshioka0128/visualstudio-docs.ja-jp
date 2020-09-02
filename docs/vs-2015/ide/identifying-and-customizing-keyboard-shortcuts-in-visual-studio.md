---
title: キーボード ショートカットの識別とカスタマイズ
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Environment.Keyboard
helpviewer_keywords:
- keyboard shortcuts [Visual Studio], customizing
- importing shortcut keys [Visual Studio]
- shortcut key combinations [Visual Studio]
- commands [Visual Studio], shortcut keys
- custom shortcut keys [Visual Studio]
- customizing keyboard shortcuts [Visual Studio]
- exporting shortcut keys [Visual Studio]
ms.assetid: d2774be2-60a4-4d6f-95f1-79d0d9e55b56
caps.latest.revision: 30
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e63395838d7d91170d54edbb07c0b38db548ccdf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670491"
---
# <a name="identifying-and-customizing-keyboard-shortcuts-in-visual-studio"></a>Visual Studio でのキーボード ショートカットの識別とカスタマイズ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio のコマンドのショートカット キーを確認し、カスタマイズしたら、他の人が使用できるようにエクスポートできます。 多くのショートカット キーは常に同じコマンドを起動しますが、その動作は次の条件によって異なることがあります。

- Visual Studio を初めて実行したときに選択した既定の環境設定 ([全般的な開発設定] または [Visual C#] など)。

- ショートカット キーの動作をカスタマイズしたかどうか。

- ショートカット キーを選択するときのコンテキスト。 たとえば、F2 ショートカット キーでは、設定デザイナーを使用している場合は Edit.EditCell コマンドが呼び出され、チーム エクスプローラーを使用している場合は File.Rename コマンドが呼び出されます。

  設定、カスタマイズ、コンテキストにかかわらず、**[オプション]** ダイアログ ボックスでいつでもショートカット キーを変更できます。 数十のコマンドの既定のキーボード ショートカットについては、「[Visual Studio で頻繁に使用するコマンドに対応する既定のキーボード ショートカット](../ide/default-keyboard-shortcuts-for-frequently-used-commands-in-visual-studio.md)」でも確認できます。また、既定のショートカット キー ([全般的な開発設定] に基づく) の完全な一覧については、「[Visual Studio の既定のキーボード ショートカット](../ide/default-keyboard-shortcuts-in-visual-studio.md)」で確認できます。

  **このトピックの内容**

- [ショートカット キーの確認](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md#bkmk_identify)

- [ショートカットキーのカスタマイズ](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md#bkmk_assign)

- [カスタム ショートカット キーの共有](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md#bkmk_transfer)

  ショートカット キーを [全体] コンテキストに割り当て、他のコンテキストに割り当てていない場合、そのショートカット キーによって常にそのコマンドが呼び出されます。 しかし、ショートカット キーは [全体] コンテキストの 1 つのコマンドに割り当て、特定のコンテキストの別のコマンドに割り当てることができます。 そのようなショートカット キーを特定のコンテキストで使用すると、ショートカット キーによって [全体] コンテキストではなく特定のコンテキストのコマンドが呼び出されます。

> [!NOTE]
> 使用している Visual Studio の設定とエディションによって、メニューに表示されるコマンドやダイアログ ボックスに表示されるオプションの名前や位置が異なる場合があります。 このトピックは **[全般的な開発設定]** に基づいています。

## <a name="identifying-a-keyboard-shortcut"></a><a name="bkmk_identify"></a> ショートカットキーの識別

1. メニューバーで、[ **ツール**]、[ **オプション**] の順に選択します。

2. **[環境]** を展開し、**[キーボード]** を選択します。

     ![[オプション] ダイアログ ボックスにキーボード ショートカットを表示](../ide/media/optionskeyboard.png "オプションキーボード")

3. **[以下の文字列を含むコマンドを表示]** ボックスに、コマンド名の全体または一部を、空白を含めずに入力し始めます。

     たとえば、**solutionexplorer** のコマンドを検索できます。

4. 一覧から該当するコマンドを選択します。

     たとえば、**View.SolutionExplorer** を選択できます。

5. コマンドにショートカット キーが既に割り当てられている場合は、**[選択したコマンドへのショートカット]** ボックスの一覧に表示されます。

     ![指定されたコマンドのショートカットを表示](../ide/media/viewshortcut.png "ViewShortcut")

## <a name="customizing-a-keyboard-shortcut"></a><a name="bkmk_assign"></a> ショートカットキーのカスタマイズ

1. メニューバーで、[ **ツール**]、[ **オプション**] の順に選択します。

2. **[環境]** フォルダーを展開し、**[キーボード]** を選択します。

     ![[オプション] ダイアログ ボックスにキーボード ショートカットを表示](../ide/media/optionskeyboard.png "オプションキーボード")

3. **[以下の文字列を含むコマンドを表示]** ボックスに、コマンド名の全体または一部を、空白を含めずに入力し始めます。

     たとえば、**solutionexplorer** のコマンドを検索できます。

4. ショートカット キーを割り当てるコマンドを一覧から選択します。

5. **[ショートカットの使用場所]** ボックスの一覧で、ショートカット キーを使用する機能領域を選択します。

     たとえば、ショートカットをすべてのコンテキスト内で機能させる場合は、**[全体]** をクリックします。 他のエディターで同じショートカットが ([全体] として) 割り当てられていなければ、そのショートカット キーを使用できます。 それ以外の場合は、既存のショートカットがオーバーライドされます。

    > [!NOTE]
    > 次のキーは、ショートカット キーの一部として **[全体]** に割り当てることができません: Print Screen/Sys Rq、Scroll Lock、Pause/Break、Tab、Caps Lock、Insert、Home、End、Page Up、Page Down、Windows ロゴ キー、アプリケーション キー、すべての方向キー、Enter キーのほか、数値キーパッドの Num Lock、Delete、または Clear、さらに Ctrl + Alt + Delete。

6. **[ショートカット キー]** ボックスで、使用するショートカット キーを入力します。

    > [!NOTE]
    > 文字と Alt キー、Ctrl キー、またはその両方を組み合わせたショートカット キーを作成できます。 Shift キーおよび文字と Alt キー、Ctrl キー、またはその両方を組み合わせたショートカット キーを作成することもできます。

     ショートカット キーが別のコマンドに既に割り当てられている場合は、**[現在使用されているショートカット]** ボックスに表示されます。 その場合は、Backspace キーを押してそのショートカット キーを削除してから、別のショートカット キーを試します。

     ![コマンドに異なるショートカットを指定](../ide/media/reassignshortcut.png "ショートカットの再割り当て")

7. **[割り当て]** ボタンをクリックします。

    > [!NOTE]
    > コマンドに別のショートカット キーを指定し、**[割り当て]** ボタンをクリックした後に、**[キャンセル]** ボタンをクリックしても、ダイアログ ボックスは閉じますが、変更は元に戻りません。

## <a name="sharing-custom-keyboard-shortcuts"></a><a name="bkmk_transfer"></a> カスタムショートカットキーの共有
 カスタム ショートカット キーを他のユーザーと共有できます。そのためには、ショートカット キーの情報をファイルにエクスポートし、そのファイルを他のユーザーに渡して、インポートしてもらう必要があります。

#### <a name="to-export-only-keyboard-shortcuts"></a>ショートカット キーのみをエクスポートするには

1. メニュー バーで、**[ツール]**、**[設定のインポートとエクスポート]** の順にクリックします。

2. **[選択された環境設定をエクスポート]** をクリックし、**[次へ]** ボタンをクリックします。

3. **[エクスポートする設定を指定してください]** で、**[すべての設定]** チェック ボックスをオフにし、**[オプション]**、**[環境]** の順に展開します。

4. **[キーボード]** チェック ボックスをオンにして、**[次へ]** ボタンをクリックします。

     ![カスタマイズされたキーボード ショートカットのみをエクスポート](../ide/media/exportshortcuts.png "ExportShortcuts カット")

5. **[設定ファイルの名前を指定してください]** と **[設定を次のディレクトリに格納する]** ボックスで、既定値のままにするか別の値を指定し、**[完了]** ボタンをクリックします。

     既定では、ショートカット キーは %USERPROFILE%\Documents\Visual Studio 2013\Settings フォルダーに保存されます。 ファイルの名前には設定のエクスポート時の日付が反映され、拡張子は .vssettings になります。

#### <a name="to-import-only-keyboard-shortcuts"></a>ショートカット キーのみをインポートするには

1. メニュー バーで、**[ツール]**、**[設定のインポートとエクスポート]** の順にクリックします。

2. **[選択された環境設定をインポート]** オプションをクリックし、**[次へ]** ボタンをクリックします。

3. **[いいえ、現在の設定を上書きして新しい設定をインポートします]** オプション ボタンをクリックし、**[次へ]** ボタンをクリックします。

4. **[ユーザーの設定]** で、インポートするショートカット キーを含む設定ファイルを選択するか、**[参照]** ボタンをクリックして適切な設定ファイルを見つけます。

5. **[次へ]** ボタンをクリックします。

6. **[インポートする設定を指定してください]** で、**[すべての設定]** チェック ボックスをオフにし、**[オプション]**、**[環境]** の順に展開します。

7. **[キーボード]** チェック ボックスをオンにして、**[完了]** ボタンをクリックします。

     ![カスタマイズされたキーボード ショートカットのみをインポート](../ide/media/importshortcuts.png "ImportShortcuts カット")

## <a name="see-also"></a>参照
 [Visual Studio のユーザー補助機能](../ide/reference/accessibility-features-of-visual-studio.md)

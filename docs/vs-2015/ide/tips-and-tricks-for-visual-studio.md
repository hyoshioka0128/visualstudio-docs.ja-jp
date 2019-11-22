---
title: ヒントとテクニック | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 20489db9-7441-4f8b-97de-c72070d569b1
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 432a0eddece867972e5c5159f734b4589c22e218
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299924"
---
# <a name="tips-and-tricks-for-visual-studio"></a>Visual Studio のヒントとテクニック

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio では、このトピックのショートカットを使用してより簡単に移動できます。 全般的な情報については、[Visual Studio のキーボード ショートカット](default-keyboard-shortcuts-in-visual-studio.md)に関するページをご覧ください。 ユーザー補助について Visual Studio を最適化する方法の詳細については、「[アクセシビリティのヒントとテクニック](../ide/reference/accessibility-tips-and-tricks.md)」を参照してください。

- [ウィンドウ管理](../ide/tips-and-tricks-for-visual-studio.md#BKMK_WindowMgmt)

- [ウィンドウのショートカット](../ide/tips-and-tricks-for-visual-studio.md#BKMK_WindowShortcuts)

- [Visual Studio での検索](../ide/tips-and-tricks-for-visual-studio.md#BKMK_Search)

- [エディター検索](../ide/tips-and-tricks-for-visual-studio.md#BKMK_EditorFind)

- [コード エディター](../ide/tips-and-tricks-for-visual-studio.md#BKMK_CodeEditor)

- [ツールバー](../ide/tips-and-tricks-for-visual-studio.md#BKMK_Toolbars)

- [デバッグ](../ide/tips-and-tricks-for-visual-studio.md#BKMK_Debugging)

- [アプリケーション ライフサイクル管理](../ide/tips-and-tricks-for-visual-studio.md#BKMK_ALM)

## <a name="BKMK_WindowMgmt"></a>ウィンドウ管理

|||
|-|-|
|フローティング タブ ウェルを外にドラッグ|複数選択は Ctrl キーを押しながらクリック|
|フローティング ウィンドウの最大化|タイトル バーをダブルクリック|
|フローティング ウィンドウの再ドッキング|Ctrl キーを押しながらタイトル バーをダブルクリック|
|アクティブなドキュメントを閉じる|Ctrl + F4|
|開いているファイル リストを表示|Ctrl + Alt + Down|
|すべてのフローティング ウィンドウを表示|Ctrl+Shift+M|

## <a name="BKMK_WindowShortcuts"></a> ウィンドウのショートカット

|||
|-|-|
|フローティング ウィンドウの移動またはドッキング|Win + Left / Win + Right|
|ウィンドウの最大化または最小化|Win + Up / Win + Down|
|ジャンプ リストを表示|Win + Alt + n|
|新しいインスタンスを開始|Win + Shift + n|
|ウィンドウの切り替え|Win + n|

## <a name="BKMK_Search"></a> Visual Studio での検索

|||
|-|-|
|ソリューション エクスプローラーの検索|Ctrl + ;|
|任意のツール ウィンドウの検索ボックスへのフォーカスの移動|ツール ウィンドウにフォーカスがあるときに Alt + `|
|クイック起動|Ctrl + Q|
|スコープ結果のクイック起動|-   @opt オプション<br />-   @cmd コマンド<br />-   @mru 直前に使用<br />-   @doc ドキュメントを開く|
|ツール オプションの検索|Ctrl+E|

## <a name="BKMK_EditorFind"></a>エディター検索

|||
|-|-|
|クイック検索|Ctrl + F|
|クイック検索の次の結果|Enter|
|クイック検索の前の結果|Shift + Enter|
|クイック検索でドロップダウンを展開|Alt + Down|
|検索を消去|Esc|
|[クイック置換]|Ctrl + H|
|クイック置換で次を置換|Alt + R|
|クイック置換ですべて置換|Alt+A|
|[フォルダーを指定して検索]|Ctrl + Shift + F|
|[フォルダーを指定して置換]|Ctrl + Shift + H|

## <a name="BKMK_CodeEditor"></a> コード エディター

|||
|-|-|
|IntelliSense 候補提示モード|Ctrl + Alt + Space (切り替え)|
|IntelliSense の強制表示|Ctrl + J|
|スマート タグ|Ctrl + .|
|スニペットの選択|Ctrl + K、X、または ?、Tab (VB)|
|ブロックの挿入|Ctrl + K、S|
|クイック ヒントの表示|Ctrl + K、I|
|移動|Ctrl + ,|
|定義へ移動|F12|
|定義をここに表示|Alt + F12|
|定義スタックへ移動|Ctrl + Shift + 8 (戻る)、Ctrl +Shift + 7 (進む)|
|強調表示された参照間の移動|Ctrl + Shift + Up (前へ)、Ctrl + Shift + Down (次へ)|
|エディターのズーム|Ctrl + Shift + > (イン)、Ctrl + Shift + < (アウト)|
|ブロック選択|Alt を押したままマウスをドラッグ、Shift + Alt + 方向キー|
|行を上下に移動|Alt + Up / Alt + Down|
|定義をここに表示|Alt + F12|
|[ピークの定義] ウィンドウを閉じる|Esc|
|[ピークの定義] ウィンドウを通常のドキュメント タブに昇格する|Ctrl + Alt + Home|
|複数の [定義をここに表示] ウィンドウ間を移動する|Ctrl + Alt + マイナス記号 (-) と Ctrl + Alt + 等号 (=)|
|複数のピーク結果の間を移動する|F8 と Shift + F8|
|コード エディター ウィンドウと [定義をここに表示] ウィンドウの間で切り替える|Shift + Esc|

## <a name="BKMK_Toolbars"></a> ツールバー

|||
|-|-|
|ボタンを追加する|ツール バーのオーバーフロー ボタンをクリック|
|標準ツール バーのコンボの検索|Ctrl + D|
|テキストボックス コマンド モードの検索|「>」と入力|
|新しいエイリアスの作成|>alias NewAlias コマンド|

## <a name="BKMK_Debugging"></a> デバッグ

|||
|-|-|
|デバッグの開始|F5|
|デバッグ中に診断ツールを有効にします|Shift + F5|
|デバッグの再起動|Ctrl + Shift + F5|
|[ステップ オーバー]|F10|
|[ステップ イン]|F11|
|[ステップ アウト]|Shift + F11|
|カーソル行の前まで実行|Ctrl + F10|
|次のステートメントの設定|Ctrl + Shift + F10|
|ブレークポイントの設定と切り替え|F9|
|ブレークポイントの無効化|Ctrl + F9|
|イミディエイト ウィンドウ|Ctrl + Alt + I|
|イミディエイト ウィンドウ コマンド モード|「>」と入力|
|イミディエイト ウィンドウのバッファーをクリア|>cls|
|イミディエイト ウィンドウの値の印刷|?varname|

## <a name="BKMK_ALM"></a>アプリケーション ライフサイクル管理

「[キーボード ショートカット: Visual Studio Online、TFS Web ポータル、およびチーム エクスプローラー](/azure/devops/project/navigation/keyboard-shortcuts?view=vsts)」を参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio ブログ](https://devblogs.microsoft.com/visualstudio/)
- [Visual Studio のヒントとテクニックに関するブログ](https://blogs.msdn.microsoft.com/zainnab/)
- [Visual Studio ツールボックス (チャネル 9)](https://channel9.msdn.com/Shows/Visual-Studio-Toolbox)

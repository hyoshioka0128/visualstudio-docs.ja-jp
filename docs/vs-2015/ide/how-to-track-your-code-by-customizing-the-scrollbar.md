---
title: '方法 : ScrollBar のカスタマイズによるコードの追跡 | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: a9ebe7ec-4b6f-4ba2-a79e-80fab3db485b
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a852b0e5ac6c6a677caab97279a0b0cb0299d27f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670629"
---
# <a name="how-to-track-your-code-by-customizing-the-scrollbar"></a>方法 : ScrollBar のカスタマイズによるコードの追跡
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

長いコード ファイルで作業していると、すべてを頭に入れておくことは困難です。 コード ウィンドウのスクロール バーをカスタマイズして、コード全体を見渡せるようにすることができます。

### <a name="to-show-annotations-on-the-scroll-bar"></a>スクロール バーにコメントを表示するには

1. コードの変更、ブレークポイント、エラー、およびブックマークを表示するようにスクロール バーを設定できます。

     **スクロールバー**のオプションページ ([**ツール]、[オプション]、[テキストエディター]) を開きます。すべての言語**または特定の言語、または [クイック起動] ウィンドウに「**スクロールバー** 」と入力します)。

2. **[垂直スクロール バーへのコメントの表示]** を選択し、表示するコメントを選択します  (**[マーク]** オプションには、ブレークポイントとブックマークが含まれています)。

3. では、試してみましょう。大きなコードファイルを開き、ファイル内の複数の場所で発生したものを置き換えます。 スクロール バーに置き換えた結果が表示されるため、置き換えるべきでないものを置き換えた場合は変更を取り消すことができます。

     次の図は、文字列を検索した後のスクロール バーです。 文字列のすべてのインスタンスが表示されています。

     ![文字列の検索後のスクロール バー。](../ide/media/enhancedscrollbarsearch.png "EnhancedScrollbarSearch")

     次の図は、文字列のすべてのインスタンスを置き換えた後のスクロール バーです。 この操作で問題が発生したことがわかります。

     ![文字列の置換でエラーが発生した後のスクロール バー](../ide/media/enhancedscrollbarreplace.png "EnhancedScrollbarReplace")

### <a name="to-set-the-display-mode-for-the-scroll-bar"></a>スクロール バーの表示モードを設定するには

1. スクロール バーには、バー モード (既定) とマップ モードの 2 つのモードがあります。 バー モードでは、コメントのインジケーターだけがスクロール バーに表示されます。 マップ モードでは、スクロール バーにコード行が表示されます。 コード行の幅を選択でき、コード行の上にポインターを置いたときに基になるコードを表示するかどうかを選択できます。 スクロール バー上のある位置をクリックすると、カーソルがコード内のその位置に移動します。 折りたたまれた部分は他と異なる影付きで表示され、ダブルクリックすると展開されます。

     **スクロール バー**のオプション ページで、**[垂直スクロール バーでのバー モードの使用]** または **[垂直スクロール バーでのマップ モードの使用]** を選択します。 **[ソースの概要]** ドロップダウンで幅を選択できます。

     マップ モードが有効で、幅が [中] に設定されているときの検索例を示します。

     ![マップ モードのスクロール バー](../ide/media/enhancedscrollbar.png "EnhancedScrollbar")

2. マップ モードで、スクロール バーの上下にポインターを移動したときのコードのプレビューを有効にするには、**[プレビュー ツール ヒントの表示]** オプションを選択します。 しくみは次のとおりです。

     ![ツールヒント付きのスクロール バー](../ide/media/enhancedscrollbarsearchtooltip.png "EnhancedScrollbarSearchTooltip")

     マップ モードのスクロール動作とプレビュー ツール ヒントはそのままで、ソース コードの概要を表示しない場合は、**[ソースの概要]** を **[オフ]** に設定できます。

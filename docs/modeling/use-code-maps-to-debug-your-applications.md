---
title: コード マップを使用してアプリケーションをデバッグする
description: コードマップを使用して、大規模なコードベース、見慣れないコード、またはレガシコードで失われないようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 09/28/2018
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio Ultimate, visualizing code
- Visual Studio Ultimate, navigating code visually
- Visual Studio Ultimate, understanding code
- Visual Studio Ultimate, mapping code relationships
- Visual Studio Ultimate, code maps
- mapping code relationships
- code maps
- mapping relationships in code
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7af24dbbb510fb1d5c9c62b40d5986ea5c74d35b
ms.sourcegitcommit: 4d394866b7817689411afee98e85da1653ec42f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2020
ms.locfileid: "97361652"
---
# <a name="use-code-maps-to-debug-your-applications"></a>コード マップを使用してアプリケーションをデバッグする

コード マップを使用すると、大規模なコード ベース、よく知らないコード、またはレガシ コードでの見失いを回避できます。 たとえば、デバッグ中に多くのファイルやプロジェクトのコードを確認する必要がある場合があります。 コード マップを使用すると、これらのコード内を移動して、コード間の関係を確認できます。 これにより、このコードを頭の中で追跡したり、別の図を描画したりする必要はありません。 コード マップがあれば、作業を中断しても作業中のコードを思い出すのに役立ちます。

![コード内のマップリレーションシップ &#45; コードマップ](../modeling/media/codemapstoryboardpaint.png)

**緑色の矢印は、エディターでカーソルが表示される場所を示します。**

コードマップを操作するときに使用できるコマンドとアクションの詳細については、「 [コードマップの参照および再配置](../modeling/browse-and-rearrange-code-maps.md)」を参照してください。

> [!NOTE]
> コードマップを作成および編集するには Visual Studio Enterprise エディションが必要です。 Visual Studio Community および Professional エディションでは、Enterprise edition で生成されたダイアグラムを開くことができますが、編集することはできません。

## <a name="understand-the-problem"></a>問題を理解する
 作業中の描画プログラムにバグがあるとします。 バグを再現するには、Visual Studio でソリューションを開き、 **F5** キーを押してデバッグを開始します。

 線を描画し、[ **最後のストロークを元に戻す**] を選択すると、次の行を描画するまで何も起こりません。

 ![バグの再現 &#45; コードマップ](../modeling/media/codemapstoryboardpaint0.png)

 したがって、`Undo` メソッドを検索して調査を開始します。 `PaintCanvas` クラスでこれが見つかります。

 ![コードマップ &#45; コードの検索](../modeling/media/codemapstoryboardpaint1.png)

## <a name="start-mapping-the-code"></a>コードのマップを開始する
 ここで、`undo` メソッドとその関係のマップを開始します。 コード エディターで、`undo` メソッドとその参照するフィールドを、新しいコード マップに追加します。 新しいマップを作成するときは、コードにインデックスを付けるのに時間がかかる場合があります。 インデックスを付けることで、後の操作をより速く実行できるようになります。

 ![メソッドと関連フィールドを表示 &#45; コードマップ](../modeling/media/codemapstoryboardpaint3.png)

> [!TIP]
> 緑色の強調表示は、マップに追加された最後の項目を示します。 緑色の矢印は、コード内のカーソルの位置を示しています。 項目間の矢印は、さまざまな関係を表します。 マップの項目に関する詳細情報は、項目の上にマウスを移動してツールヒントを調べることで確認できます。

 ![コードマップ &#45; ツールヒントを表示する](../modeling/media/codemapstoryboardpaint4.png)

## <a name="navigate-and-examine-code-from-the-map"></a>マップからコードを移動して調査する
 各フィールドのコード定義を表示するには、マップのフィールドをダブルクリックするか、フィールドを選択して **F12** キーを押します。 緑色の矢印がマップの項目間を移動します。 コード エディターのカーソルも自動的に移動します。

 ![コードマップ &#45; フィールド定義を確認する](../modeling/media/codemapstoryboardpaint5.png)

 ![コードマップ &#45; フィールド定義を確認する](../modeling/media/codemapstoryboardpaint5a.png)

> [!TIP]
> また、コード エディターでカーソルを動かすと、マップの緑色の矢印を移動できます。

## <a name="understand-relationships-between-pieces-of-code"></a>コード間のリレーションシップを把握する
 ここで、他のどのコードが `history` フィールドおよび `paintObjects` フィールドとやり取りしているのかを把握する必要があります。 これらのフィールドを参照するすべてのメソッドをマップに追加できます。 この操作は、マップまたはコード エディターから行うことができます。

 ![すべての参照を検索 &#45; コードマップ](../modeling/media/codemapstoryboardpaint6.png)

 ![コード エディターからコード マップを開く](../modeling/media/codemapstoryboardpaint6a.png)

> [!NOTE]
> Windows Phone や Windows ストアなどの複数のアプリで共有されるプロジェクトから項目を追加すると、それらの項目は常に、現在アクティブなアプリ プロジェクトと共にマップに表示されます。 そのため、コンテキストを別のアプリ プロジェクトに変更すると、マップ上のコンテキストも、共有プロジェクトから新たに追加した項目に変更されます。 マップ上の項目に実行する操作は、同じコンテキストを共有する項目にのみ適用されます。

 関係のフローを再配置してマップを読みやすくするために、レイアウトを変更します。 項目をドラッグすることにより、マップ上で項目を移動することもできます。

 ![レイアウトの変更 &#45; コードマップ](../modeling/media/codemapstoryboardpaint7a.png)

> [!TIP]
> 既定では、 **インクリメンタルレイアウト** はオンになっています。 この設定では、新しい項目の追加時にマップの再配置は最小限に抑えられます。 新しい項目を追加するたびにマップ全体を再配置するには、[ **インクリメンタルレイアウト**] をオフにします。

 ![レイアウトの変更 &#45; コードマップ](../modeling/media/codemapstoryboardpaint7.png)

 これらのメソッドを調べます。 マップで、 **paintcanvas]** メソッドをダブルクリックするか、この方法を選択して **F12** キーを押します。 このメソッドにより、`history` と `paintObjects` が空のリストとして作成されることがわかります。

 ![コードマップ &#45; メソッド定義を調べる](../modeling/media/codemapstoryboardpaint8.png)

 ここで、同じ手順を繰り返して、`clear` メソッドの定義を調べます。 `clear` が `paintObjects` と `history`を使用して一部のタスクを実行することがわかります。 次に、このメソッドは `Repaint` メソッドを呼び出します。

 ![コードマップ &#45; メソッド定義を調べる](../modeling/media/codemapstoryboardpaint9.png)

 ここで、`addPaintObject` メソッドの定義を調べます。 このメソッドも、`history` と `paintObjects` を使用して一部のタスクを実行します。 また、このメソッドは `Repaint` を呼び出します。

 ![コードマップ &#45; メソッド定義を調べる](../modeling/media/codemapstoryboardpaint10.png)

## <a name="find-the-problem-by-examining-the-map"></a>マップを調べて問題を見つける
 `history` と `paintObjects` を変更するすべてのメソッドが `Repaint` を呼び出すと考えられます。 ただし、`undo` メソッドは `Repaint` を呼び出しませんが、`undo` メソッドは同じフィールドを変更します。 したがって、`Repaint` で `undo` を呼び出すことにより、この問題を解決できると考えられます。

 ![コードマップ &#45; 見つからないメソッド呼び出しの検索](../modeling/media/codemapstoryboardpaint11.png)

 この失われている呼び出しを示すマップがない場合、特にコードが複雑になると、この問題を見つけることがより困難になる可能性があります。

## <a name="share-your-discovery-and-next-steps"></a>探索と次のステップを共有する
 自分または他のユーザーがこのバグを修正する前に、問題と問題の解決方法に関するメモをマップに記載できます。

 ![コメントとフラグ項目を &#45; コードマップ](../modeling/media/codemapstoryboardpaint12.png)

 たとえば、マップにコメントを追加し、色を使用して項目にフラグを設定できます。

 ![コメント付きの項目とフラグが設定された項目 &#45; コードマップ](../modeling/media/codemapstoryboardpaint12a.png)

 Microsoft Outlook をインストール済みの場合は、他のユーザーに電子メールでマップを送信できます。 マップをイメージまたはその他の形式でエクスポートすることもできます。

 ![コードマップ &#45; 共有、エクスポート、メール](../modeling/media/codemapstoryboardpaint13.png)

## <a name="fix-the-problem-and-show-what-you-did"></a>問題を修正して操作内容を表示する
 このバグを修正するには、`Repaint`に `undo` の呼び出しを追加します。

 ![不足しているメソッド呼び出しを追加 &#45; コードマップ](../modeling/media/codemapstoryboardpaint14.png)

 修正を確認するには、デバッグ セッションを再開して、バグの再現を試みます。 ここで、 **[最後のストロークを元に戻す** ] を選択すると、適切な修正が行われたことが確認できます。

 ![コードマップ &#45; コード修正の確認](../modeling/media/codemapstoryboardpaint15.png)

 マップを更新すると、実行した修正を示すことができます。

 ![メソッド呼び出しがないコードマップ &#45; 更新マップ](../modeling/media/codemapstoryboardpaint16.png)

 マップには、 **undo** と **Repaint** の間のリンクが表示されるようになりました。

 ![コードマップ &#45; 更新されたマップのメソッド呼び出し](../modeling/media/codemapstoryboardpaint17.png)

> [!NOTE]
> マップを更新するときに、マップの作成に使用したコード インデックスが更新されたことを示すメッセージが表示される場合があります。 これは、他のだれかがコードを変更し、マップが現在のコードに一致しなくなっていることを意味します。 このことでマップの更新が停止されることはありませんが、コードとの一致を確認するためにマップを作成し直すことが必要になる場合があります。

 これで、調査が完了しました。 コードのマップにより、問題を正常に検出して修正しました。 また、コード内を移動することや確認したことの記憶に役立ち、問題を解決するための手順を示すマップも備わりました。

## <a name="see-also"></a>関連項目

- [デバッグを行うときの呼び出し履歴に対するメソッドのマップ](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)
- [コードの視覚化](../modeling/visualize-code.md)

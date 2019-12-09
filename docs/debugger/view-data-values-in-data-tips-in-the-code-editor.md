---
title: DataTips | の変数の値を表示するMicrosoft Docs
ms.custom: seodec18
ms.date: 11/21/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugging [Visual Studio], DataTips
- DataTips tool
ms.assetid: ffa7bd18-439b-4685-a9b3-c7884b5de41f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f121c7aadb605e6eb87089556ddaf1b1f4999dbb
ms.sourcegitcommit: 0b90e1197173749c4efee15c2a75a3b206c85538
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2019
ms.locfileid: "74903886"
---
# <a name="view-data-values-in-datatips-in-the-code-editor"></a>コードエディターでデータヒントのデータ値を表示する

DataTips は、デバッグ中にプログラムの変数に関する情報を確認するときに便利です。 データヒントは、中断モードのときにのみ機能します。また、実行の現在のスコープ内にある変数に対してだけ使用できます。 コードを初めてデバッグする場合は、この記事を読む前に、[絶対初心者向けのデバッグ](../debugger/debugging-absolute-beginners.md)や[手法とツール](../debugger/write-better-code-with-visual-studio.md)のデバッグをお読みになることをお勧めします。

## <a name="work-with-datatips"></a>DataTips を操作する

DataTips は、中断モードでのみ表示され、現在の実行スコープ内にある変数にのみ表示されます。

### <a name="display-a-datatip"></a>DataTip を表示する

1. コードにブレークポイントを設定し、 **F5**キーを押すか **、[デバッグ**] を > 選択してデバッグを**開始**し、デバッグを開始します。

1. ブレークポイントで一時停止したときに、現在のスコープ内の任意の変数にポインターを合わせます。 [DataTip] が表示され、変数の名前と現在の値が示されます。

### <a name="make-a-datatip-transparent"></a>DataTip を透過的にする

DataTip を透過的にして、その下にあるコードを表示するには、DataTip の中で、 **ctrl**キーを押します。 **Ctrl**キーを押したままにしておくと、ヒントは透過的なままになります。 これは、ピンされたまたはフローティングの DataTips に対しては機能しません。
### <a name="pin-a-datatip"></a>DataTip をピン留めする

開いたままになるように DataTip をピン留めするには、[**ソースにピン留め**する] アイコンを選択します。

![DataTip をピン留めする](../debugger/media/dbg-tips-data-tips-pinned.png "DataTip をピン留めする")

ピン留めされた DataTip は、コードウィンドウの周囲でドラッグすることによって移動できます。 コードヒントが固定されている行の横にある余白にプッシュピンアイコンが表示されます。

>[!NOTE]
>DataTips は、現在のカーソルまたは DataTip の場所ではなく、実行が中断されたコンテキストで常に評価されます。 現在のコンテキストで変数と同じ名前を持つ別の関数内の変数にマウスポインターを置くと、現在のコンテキストの変数の値が表示されます。

### <a name="unpin-a-datatip-from-source"></a>ソースからの DataTip の固定解除

ピン留めされた DataTip をフローティングするには、[DataTip] の上にマウスポインターを移動し、ショートカットメニューからプッシュピンアイコンを選択します。

プッシュピンアイコンが固定されていない位置に変わり、DataTip がフローティング状態になるか、開いているすべてのウィンドウの上にドラッグできるようになりました。 デバッグセッションが終了すると、浮動 DataTips が閉じます。

### <a name="repin-a-datatip"></a>DataTip の再ピン

フローティングヒントをソースに再ピン留めするには、コードエディターでその上にマウスポインターを移動し、プッシュピンアイコンを選択します。 画鋲アイコンがピン留めされた位置に変わり、DataTip はコードウィンドウだけに固定されます。

非ソースコードウィンドウに対して DataTip がフローティングの場合、プッシュピンアイコンは使用できず、DataTip は再ピン化できません。 プッシュピンアイコンにアクセスするには、コードエディターウィンドウにドラッグするか、コードウィンドウにフォーカスを与えることによって、DataTip をコードエディターウィンドウに返します。

### <a name="close-a-datatip"></a>DataTip を閉じる

DataTip を閉じるには、[DataTip] の上にマウスポインターを移動し、ショートカットメニューの [閉じる] (**x**) アイコンをクリックします。

### <a name="close-all-datatips"></a>すべての DataTips を閉じる

すべての DataTips を閉じるには、 **[デバッグ]** メニューの **[すべての datatips をクリア]** を選択します。

### <a name="close-all-datatips-for-a-specific-file"></a>特定のファイルのすべての DataTips を閉じる

特定のファイルのすべての DataTips を閉じるには、 **[デバッグ]** メニューの [ **\<Filename > にピン留め**されているすべての datatips をクリア] を選択します。

## <a name="expand-and-edit-information"></a>情報の展開と編集
データヒントを使用すると、配列、構造体、またはオブジェクトを展開して、メンバーを表示できます。 DataTip の変数値を編集することもできます。

### <a name="expand-a-variable"></a>変数を展開する

DataTip 内のオブジェクトを展開してその要素を表示するには、項目名の前にある展開矢印をポイントして、要素をツリー形式で表示します。 ピン留めされた DataTip の場合は、変数名の前の **+** を選択し、ツリーを展開します。

![DataTip を展開する](../debugger/media/dbg-tour-data-tips.png "DataTip を展開する")

キーボードのマウスまたは方向キーを使用して、展開されたビュー内を上下に移動することができます。

ピン留めされたアイテムの上にマウスポインターを置いてプッシュピンアイコンを選択することにより、展開されたアイテムをピン留めすることもできます。 ツリーが折りたたまれた後、ピン留めされたヒントに要素が表示されます。

### <a name="edit-the-value-of-a-variable"></a>変数の値を編集する

DataTip の変数または要素の値を編集するには、値を選択し、新しい値を入力して、 **enter**キーを押します。 読み取り専用の値の選択は無効になっています。

::: moniker range=">= vs-2019"

## <a name="pin-properties-in-datatips-supported-in-visual-studio-2019-version-164-preview-3-or-higher"></a>DataTips でプロパティをピン留めする (Visual Studio 2019 バージョン 16.4 Preview 3 以降でサポート)

> [!NOTE]
> この機能は、.NET Core 3.0 以降でサポートされています。

**Pinnable properties**ツールを使用すると、DataTips のプロパティでオブジェクトをすばやく調べることができます。  このツールを使用するには、プロパティの上にマウスポインターを移動し、表示されるピンアイコンを選択するか、右クリックして、結果のコンテキストメニューで [**お気に入りとしてメンバーをピン留め**する] オプションを選択します。  これにより、そのプロパティがオブジェクトのプロパティリストの先頭にバブルされ、プロパティの名前と値が DataTip の右側の列に表示されます。  プロパティの固定を解除するには、ピンアイコンをもう一度選択するか、コンテキストメニューの [**メンバーをお気に入りにピン留め**する] オプションを選択します。

![プロパティを DataTip にピン留めする](../debugger/media/basic-pin-datatip.gif "プロパティを DataTip にピン留めする")

また、オブジェクトのプロパティリストを datatip で表示するときに、プロパティ名を切り替えたり、ピン留めされていないプロパティを除外したりすることもできます。  いずれかのオプションにアクセスするには、プロパティを含む行を右クリックし、[ピン留めされた**メンバーのみを表示**] またはショートカットメニューの [**値のオプション] でピン留めされたメンバー名を非表示**にします。

::: moniker-end

## <a name="visualize-complex-data-types"></a>複合データ型を視覚化する

DataTip の変数または要素の横にある虫眼鏡アイコンは、[テキストビジュアライザー](../debugger/string-visualizer-dialog-box.md)など、1つまたは複数の[ビジュアライザー](../debugger/create-custom-visualizers-of-data.md)が変数に使用できることを意味します。 ビジュアライザーでは、より意味のある、グラフィカルな方法で情報が表示されます。

データ型の既定のビジュアライザーを使用して要素を表示するには、虫眼鏡アイコン![ビジュアライザーアイコン](../debugger/media/dbg-tips-visualizer-icon.png "ビジュアライザーアイコン")を選択します。 虫眼鏡アイコンの横にある矢印を選択して、データ型のビジュアライザーの一覧から選択します。

## <a name="add-a-variable-to-a-watch-window"></a>ウォッチウィンドウに変数を追加する

変数のウォッチを続行する場合は、DataTip から**ウォッチ**ウィンドウに追加することができます。 DataTip の変数を右クリックし、**ウォッチ式の追加** を選択します。

変数が **[ウォッチ]** ウィンドウに表示されます。 Visual Studio のエディションが複数の **[ウォッチ]** ウィンドウをサポートしている場合は、**ウォッチ 1**に変数が表示されます。

## <a name="import-and-export-datatips"></a>DataTips のインポートとエクスポート

DataTips を XML ファイルにエクスポートすることができます。これは、テキストエディターを使用して共有または編集することができます。 また、受け取った、または編集した DataTip XML ファイルをインポートすることもできます。

**データヒントをエクスポートするには**

1. **デバッグ** > **DataTips をエクスポート** を選択します。

1. **[Datatip のエクスポート]** ダイアログボックスで、XML ファイルを保存する場所に移動し、ファイルの名前を入力して、 **[保存]** を選択します。

**データヒントをインポートするには**

1. **デバッグ** > **DataTips をインポート** を選択します。

1. **[Datatip のインポート]** ダイアログボックスで、開く datatips XML ファイルを選択し、 **[開く]** を選択します。

## <a name="see-also"></a>参照
- [デバッグとは](../debugger/what-is-debugging.md)
- [デバッグの技術とツール](../debugger/write-better-code-with-visual-studio.md)
- [デバッグに関する最初の確認](../debugger/debugger-feature-tour.md)
- [デバッガーでのデータ表示](../debugger/viewing-data-in-the-debugger.md)
- [ウォッチ ウィンドウと [クイック ウォッチ] ウィンドウ](../debugger/watch-and-quickwatch-windows.md)
- [カスタム ビジュアライザーを作成する](../debugger/create-custom-visualizers-of-data.md)

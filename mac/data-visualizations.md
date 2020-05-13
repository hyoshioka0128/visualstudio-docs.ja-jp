---
title: デバッグ - データの視覚化
description: デバッグは、プログラミングの中でも一般的で必要な部分です。 Visual Studio for Mac には、デバッグが簡単になる機能一式が備わっています。 この記事では、デバッガーでオブジェクトを検査するときに表示できるさまざまなデータの視覚化について説明します。
author: jmatthiesen
ms.author: jomatthi
ms.date: 05/06/2018
ms.technology: vs-ide-debug
ms.assetid: 527E6BEC-EF15-4002-ACB5-62AE1C16F6B7
ms.openlocfilehash: 14696040160dfc33f89b7647fb73b116b41afa16
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "67691728"
---
# <a name="data-visualizations"></a>データ可視化

Visual Studio for Mac では、デバッガー用の UI がサポートされているため、デバッグ中に変数、フィールド、プロパティの値を視覚化できます。 これらのデータ ビジュアライザーには拡張されたバージョンのデータが表示され、color 構造体の色など、既知の構造を開発時に検査できます。

行にマウス カーソルを移動したときに値の右に表示されるプレビュー アイコンをクリックすると、デバッグのビジュアライザーである **[ローカル]** パッドが表示されます。

![[ローカル] パッド](media/data-visualizations-image9.png)

ここでは、Visual Studio for Mac でデバッグするときに使用できる多数の新しい視覚化について説明します。

## <a name="point"></a>ポイント
Point/PointF (iOS と Mac では CGPoint) は、X 値と Y 値を示すタプルとしてデバッグ パッドにレンダリングされます。

![ポイントの視覚化](media/data-visualizations-image10.png)

## <a name="size"></a>Size
Size/SizeF (iOS と Mac では CGSize) は、四角形としてレンダリングされます。 250 px を超えるディメンションまで拡大縮小して描画され、そこに 250 px の最大ディメンションに拡大縮小して四角形が表示されます。

[サイズの視覚化](media/data-visualizations-image11.png)

## <a name="rectangle"></a>Rectangle
Rectangle/RectangleF (iOS と Mac では CGRect) は、ディメンションと原点を表示します。 Size と同様に、250 px を超えるディメンションまで拡大縮小して描画されます。

![四角形の視覚化](media/data-visualizations-image12.png)

## <a name="coordinate"></a>座標
中央の位置にピン留めされた状態で、座標がマップにプロットされます。

[座標の視覚化](media/data-visualizations-image13.png)

## <a name="color"></a>Color
色のプレビュー、RGBA コンポーネント、色相値-彩度値-輝度値、および色の 16 進値を示す UIColor、CGColor、および Color のプロパティが表示されます。

![色の視覚化](media/data-visualizations-image14.png)

## <a name="images"></a>イメージ

メディアは、250 px の最大ディメンションまで拡大縮小してレンダリングされ、画像が 250 px を超える場合は 250 px に合わせて縮小表示されます。

![画像の視覚化](media/data-visualizations-image15.png)

## <a name="bezier-curves"></a>ベジエ曲線

ビジュアライザーには `NSBezierPath` が表示されます。

![ベジエ曲線の視覚化](media/data-visualizations-image16.png)

## <a name="string"></a>String

100 文字未満の文字列は、プレビューを使用せずに完全に表示されます。 100 文字以上の文字列は、プレビューで完全に表示されます。 文字列は編集可能で、ビジュアライザーには編集ボタンが表示されます。ボタンをクリックすると、以下のようにプレビューまたは文字列値エディターで文字列値を編集できます。

![文字列の視覚化](media/data-visualizations-image17.png)

### <a name="small-strings"></a>短い文字列:
![短い文字列の視覚化](media/data-visualizations-image18.png)]

### <a name="medium-length-strings"></a>中くらいの長さの文字列:
![中くらいの長さの文字列の視覚化](media/data-visualizations-image19.png)

### <a name="editor"></a>エディター:

![エディターの視覚化](media/data-visualizations-image21.png)

## <a name="ienumerable"></a>IEnumerable

IEnumerable はすべての値を列挙します。各値は、 **[値の表示]** ボタンをクリックして表示できます。 `Array`、`ArrayList`、`List<>`、`Dictionary<,>` などのオブジェクトの場合は独自のデバッガー ビジュアライザーがあるため、IEnumerable オプションではオブジェクト値が表示されません。

![IEnumerable の視覚化](media/data-visualizations-image22.png)

## <a name="other-visualizers"></a>その他のビジュアライザー

独自のインライン ビジュアライザーがあるその他の種類を紹介します。

![その他の視覚化](media/data-visualizations-image23.png)

* **Primitives**
  * 基本型の生の値が表示されます。
* **Enum**
  * enum Type 修飾子がないフィールド値が表示されます。
* **Tuple**
  * (,) の形式で表示されます
* **Null**
  * "null" 値が表示されます。
* **[URL]**
  * クリック可能なハイパーリンクが表示されます。
* **IntPtr**
  * IntPtr の 16 進表現が表示されます。

## <a name="see-also"></a>参照

- [[自動変数] ウィンドウと [ローカル] ウィンドウの変数の検査 (Windows 上の Visual Studio)](/visualstudio/debugger/autos-and-locals-windows)
- [ビジュアライザーで文字列を表示する (Windows 上の Visual Studio)](/visualstudio/debugger/string-visualizer-dialog-box)
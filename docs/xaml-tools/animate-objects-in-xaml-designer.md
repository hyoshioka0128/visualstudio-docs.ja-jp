---
title: XAML デザイナーでのオブジェクトのアニメーション化
titleSuffix: Blend for Visual Studio
ms.date: 07/31/2019
ms.topic: conceptual
ms.assetid: fb88fa26-e835-47f5-9771-2f279441c83c
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: ab5be23d2756c1afc38f5ea071fe10a621c5cf2e
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "82921209"
---
# <a name="animate-objects-in-xaml-designer"></a>XAML デザイナーでのオブジェクトのアニメーション化

Blend for Visual Studio では、オブジェクトを動かしたり、フェードイン/フェードアウトしたりする短いアニメーションを簡単に作成できます。

アニメーションを作成するには、*ストーリーボード*が必要です。 ストーリー ボードには、1 つ以上の *タイムライン*があります。 タイムライン上で *キーフレーム* を設定してプロパティの変更をマークします。 次に、アニメーションの実行時に、Blend for Visual Studio は、指定した期間全体でプロパティの変更を補間します。 結果として、移行がスムーズになります。 オブジェクトに属する任意のプロパティをアニメーション化できます。非視覚プロパティでも同様です。

次の図は、**Storyboard1** という名前のストーリーボードを示しています。 タイムラインには、四角形の X と Y 位置をマークするキーフレームが含まれています。 このアニメーションを実行すると、四角形はある位置から別の位置にスムーズに移動します。

![Blend for Visual Studio のアニメーションのストーリーボード](media/storyboard-timeline.png)

## <a name="create-an-animation"></a>アニメーションを作成する

1. ストーリーボードを作成するには、**[オブジェクトとタイムライン]** ウィンドウの **[ストーリーボード オプション]** ボタンを選択し、**[新規]** を選択します。

   ![Blend for Visual Studio でストーリーボードを追加する](media/new-storyboard.png)

2. **[ストーリーボード リソースの作成]** ダイアログ ボックスで、ストーリーボードの名前を入力します。

3. デザイン ビューの **[アセット]** パネルで、ページの左下に四角形を追加します。

   ![XAML デザイナーの [アセット] パネルの四角形](media/add-rectangle.PNG)

4. **[オブジェクトとタイムライン]** ウィンドウで、黄色のタイム ポインターを **3** 秒のところまで動かします。

   ![タイムラインのタイム インジケーター](media/timeline-indicator.PNG)

5. ページのデザイン ビューで、四角形をページの右側にドラッグします。

6. **[再生]** を押すと、ページの左側から右側に四角形が移動します。

四角形の変更を他にもさまざまな時点で試してみてください。 たとえば、塗りつぶしの色を変更したり、プロパティ ウィンドウの向きを反転したりすることができます。

## <a name="see-also"></a>関連項目

- [Blend for Visual Studio を使用して UI を作成する](../xaml-tools/creating-a-ui-by-using-blend-for-visual-studio.md)

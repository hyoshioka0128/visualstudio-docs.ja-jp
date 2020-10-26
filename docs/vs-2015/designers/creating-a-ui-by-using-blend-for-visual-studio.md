---
title: Blend を使用した UI の作成
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
f1_keywords:
- Blend.Start.Dev12
ms.assetid: efd12263-cc2d-4081-a2bb-9a2cc17c442c
caps.latest.revision: 33
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1a65f42dafca696bfa638964b825410b576d4845
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85544288"
---
# <a name="creating-a-ui-by-using-blend-for-visual-studio"></a>Blend for Visual Studio を使用して UI を作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Blend for Visual Studio は、XAML ベースの Windows デスクトップ アプリ、Web アプリ、[Windows Phone](https://msdn.microsoft.com/library/windowsphone/develop/jj683071.aspx) アプリ、[Windows Store](https://msdn.microsoft.com/library/windows/apps/jj129478.aspx) アプリの設計を支援します。 Visual Studio と同じ基本的な XAML デザイン環境を提供しているほか、アニメーションやビヘイビアーなどの高度なタスクを視覚的にデザインする機能が追加されています。

 Blend for Visual Studio は Visual Studio に含まれているので、ダウンロードする必要はありません。 ただし、Visual Studio インストーラーで選択し、システムにインストールする必要があります。

 Blend for Visual Studio を初めてご使用になる場合は、このワークスペース特有の機能に慣れるために少し時間を取ってください。 このトピックでは、短いツアーにお連れします。

> [!NOTE]
> アートボード、[ドキュメント アウトライン] ウィンドウ、[デバイス] ウィンドウなどの共有デザイン機能のツアーについては、「[XAML デザイナーを使用した UI の作成](../designers/creating-a-ui-by-using-xaml-designer-in-visual-studio.md)」を参照してください。

 **このトピックの**内容:

- [[ツール] パネルのツアー](#Tools)

- [[アセット] パネルのツアー](#Assets)

- [[オブジェクトとタイムライン] パネルのツアー](#Objects)

- [[プロパティ] パネルのツアー](#Properties)

## <a name="tour-of-the-tools-panel"></a><a name="Tools"></a> [ツール] パネルのツアー
 Blend for Visual Studio の **[ツール]** パネルは、アプリケーションのオブジェクトの作成と変更に使用します。 パネルにあるツールを選択してアートボード上でマウスを動かすと、オブジェクトを描画できます。

 ![ツール パネル](../designers/media/blend5toolspanel.png "Blend5Toolspanel")

|Image|ツールの種類|Image|ツールの種類|
|-|-|-|-|
|![](../designers/media/b1-1.png "B1_1")|**選択ツール** オブジェクトとパスを選択します。<br /><br /> **個別選択**ツールを使用すると、入れ子状のオブジェクトやパス セグメントを選択できます。|![吹き出し A](../designers/media/b5-label-a.png "b5_label_A")|**グラデーション ツールとブラシ ツール**|
|![](../designers/media/b1-2.png "B1_2")|**表示ツール** 手のひらツールでの移動、ズームなど、アートボードの表示の調整を行います。|![吹き出し B](../designers/media/b5-label-b.png "b5_label_B")|**パス ツール**|
|![](../designers/media/b1-3.png "B1_3")|**ブラシ ツール** ブラシの変換や、オブジェクトのペイントを行ったり、あるオブジェクトの属性を選択して別のオブジェクトに適用するなど、オブジェクトの表示属性を操作します。|![吹き出し C](../designers/media/b5-label-c.png "b5_label_C")|**シェイプ ツール**|
|![](../designers/media/b1-4.png "B1_4")|**オブジェクト ツール** パス、図形、レイアウト パネル、テキスト、コントロールなど、よく使用するオブジェクトをアートボード上で描画します。|![吹き出し D](../designers/media/b5-label-d.png "b5_label_D")|**レイアウト パネル**|
|![](../designers/media/b1-5.png "B1_5")|**アセット ツール****[アセット]** パネルにアクセスし、ライブラリから最近使用したアセットを表示します。|![吹き出し E](../designers/media/b5-label-e.png "b5_label_E")|**テキスト コントロール**|
|||![吹き出し F](../designers/media/b5-label-f.png "b5_label_F")|**コモン コントロール**|

 **短いビデオを見る:** ![インストール済みフィーチャーの構成](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [ツール バー](https://www.youtube.com/watch?v=VkdUJcvoo54&list=PLBDF977B2F1DAB358&index=4)。

## <a name="tour-of-the-assets-panel"></a><a name="Assets"></a> [アセット] パネルのツアー
 **[アセット]** パネルには、すべてのコントロールが用意されています (Visual Studio の **[ツールボックス]** に似ています)。 また、コントロールのほかに、スタイル、メディア、ビヘイビアー、効果など、アートボードに追加できるすべてのものが **[アセット]** パネルに用意されています。

 ![アセット パネル](../designers/media/blend5-assets-panel.png "Blend5_Assets_panel")

|Image|説明|
|-|-|
|![](../designers/media/b1-1.png "B1_1")|**[検索] ボックス****[検索]** ボックスに入力することにより、アセットの一覧を絞り込みます。|
|![](../designers/media/b1-2.png "B1_2")|**グリッド モードとリスト モード** アセットの表示モードを、**グリッド モード**または**リスト モード**に切り替えます。|
|![](../designers/media/b1-3.png "B1_3")|**アセットのカテゴリ** カテゴリまたはサブカテゴリをクリックすると、そのカテゴリに属するアセットが表示されます。|
|![](../designers/media/b1-4.png "B1_4")|**スタイル** リソース ディクショナリに含まれるすべてのスタイルを表示します。|
|![](../designers/media/b1-5.png "B1_5")|**説明** 選択したカテゴリまたはサブカテゴリの説明が表示されます。|

## <a name="tour-of-the-objects-and-timeline-panel"></a><a name="Objects"></a> [オブジェクトとタイムライン] パネルのツアー
 このパネルを使用すると、アートボード上のオブジェクトを整理して、必要な場合はアニメーション化できます。

 ![アニメーション モードの [オブジェクトとタイムライン] パネル](../designers/media/b5-object-timeline-animation.png "b5_object_timeline_animation")

|Image|説明|
|-|-|
|![](../designers/media/b1-1.png "B1_1")|**オブジェクト ビュー** ドキュメントをツリー表示します。 さまざまなレベルの詳細にドリル ダウンできます。 さらに、アートボード上のオブジェクトを整理するレイヤーを追加することもできます。 そのように、グループとしてロックし、非表示にすることができます。|
|![](../designers/media/b1-2.png "B1_2")|**記録モード インジケーター** タイムラインでプロパティの変更を記録中かどうかを表示します。|
|![](../designers/media/b1-3.png "B1_3")|**ストーリーボードの一覧** 作成済みのストーリーボードが一覧表示されます。|
|![](../designers/media/b1-4.png "B1_4")|**ストーリー ボードを閉じる** 現在のストーリー ボードを閉じます。|
|![](../designers/media/b1-5.png "B1_5")|**ストーリー ボードのオプション** ストーリー ボードの作成、複製、動作の取り消し、削除、名前の変更を行ったり、ストーリー ボードを閉じます。|
|![](../designers/media/b1-6.png "B1_6")|**再生コントロール** タイムライン上を移動します。 再生ヘッドは、ドラッグしてタイムライン上を移動する (*スクラブする*) こともできます。|
|![](../designers/media/b1-7.png "B1_7")|**スコープを戻す** オブジェクト ビューのスコープを前のルート オブジェクトまたは前のスコープに戻します。 スタイルまたはテンプレートを変更する場合にのみ、これを実行できます。|
|![](../designers/media/b1-8.png "B1_8")|**キーフレームの記録** 現時点で選択されているオブジェクトのプロパティのスナップショットを記録します。|
|![](../designers/media/b1-9.png "B1_9")|**スナップ オプション** タイムラインのスナップ、スナップの精度を設定し、タイムラインのスナップをオフにします。|
|![](../designers/media/97fa60b9-0caf-4387-9225-b57510d32209.png "97fa60b9-0caf-4387-9225-b57510d32209")|**表示/非表示**、**ロック/ロック解除** オブジェクト ビューの表示と非表示、ロックとロック解除を切り替えます。|
|![](../designers/media/b1-11.png "B1_11")|**タイムライン上の再生ヘッドの位置** 現在の時刻をミリ秒単位で表示します。 このフィールドに時間値を直接入力し、特定の時点に移動することもできます。 精度は **[スナップ オプション]** に設定したスナップ精度によって決まります。|
|![](../designers/media/b1-12.png "B1_12")|**再生ヘッド** アニメーションがどの時点にあるかを示します。 タイムラインで再生ヘッドをドラッグして、アニメーションをプレビューできます。|
|![](../designers/media/b1-13.png "B1_13")|**タイムラインに設定されたキーフレーム** 特定の時点でのプロパティの値を変更します。|
|![](../designers/media/d839d12c-07a1-4127-a830-4a8e7069f4fe.png "d839d12c-07a1-4127-a830-4a8e7069f4fe")|**オブジェクトの順序の変更** オブジェクトの表示順序を設定します。 構造ビューのオブジェクトを Z 軸を基準 (手前から奥)、またはマークアップ順 (**XAML** での表示順) に整列させるには、このボタンをクリックします。|
|![](../designers/media/b1-15.png "B1_15")|**タイムラインのズーム** タイムラインのズーム解像度を設定します。 ズーム インでは、アニメーションを詳細に編集できます。ズーム アウトすると、長い再生時間にわたる動作の概要が表示されます。 ズーム インしても、目的の位置にキーフレームを設定できない場合は、スナップ精度が十分高く設定されていることを確認してください。|
|![吹き出し 16](../designers/media/b5-label-16.png "b5_label_16")|**タイムライン構成領域** タイムラインを表示するとともに、キーフレームをドラッグするかショートカット メニューを使用してキーフレームを移動します。|

## <a name="tour-of-the-properties-panel"></a><a name="Properties"></a> [プロパティ] パネルのツアー
 オブジェクトのプロパティを表示して変更するには、このパネルを使用します。 また、アートボード上で直接設定することもできます。 この場合、プロパティの変更が **[プロパティ]** パネルに反映されます。

 ![プロパティ パネル](../designers/media/blend5-properties-panel.png "Blend5_properties_panel")

 **[カテゴリ]** プロパティのカテゴリを展開し、折りたたみます。 カテゴリの詳細を表示するには **[展開]** ![](../designers/media/6375953d-074c-421a-bbb3-6f5055b67b64.png "6375953d-074c-421a-bbb3-6f5055b67b64") をクリックし、非表示にするには **[折りたたみ]** ![折りたたみ](../designers/media/b5-collapse-button.png "b5_collapse_button") をクリックします。

|                                                                                                         |                                                                                                                                                                                                                                  |
|---------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                 ![](../designers/media/b1-1.png "B1_1")                                 |                                                                              **[名前] と [種類]** 選択したオブジェクトのアイコン、名前、種類が表示されます。                                                                              |
|                                 ![](../designers/media/b1-2.png "B1_2")                                 |                                                                          **[並べ替え]** プロパティを名前、ソース、またはカテゴリごとにアルファベット順に並べ替えます。                                                                          |
|                                 ![](../designers/media/b1-3.png "B1_3")                                 |                                                        **ブラシのプロパティ** Fill、Stroke、Foreground など、ブラシの視覚的なプロパティを設定します。                                                        |
|                                 ![](../designers/media/b1-4.png "B1_4")                                 |                                                                                    **カラー エディター** 単色ブラシおよびグラデーション ブラシで使用します。                                                                                    |
|                                 ![](../designers/media/b1-5.png "B1_5")                                 |                                                                                                 **カラー ピッカー** 色を選択します。                                                                                                 |
|                                 ![](../designers/media/b1-6.png "B1_6")                                 |                                                                              **カラー チップ** 初期の色、現在の色、および最後の色が表示されます。                                                                               |
|                                 ![](../designers/media/b1-7.png "B1_7")                                 | **スポイト ツール** 画面上の任意の要素の色を使用します。 **色スポイト**は、**単色ブラシ**が選択されているときに使用できます。 **[グラデーションのスポイト]** は、**[グラデーション ブラシ]** が選択されているときに使用できます。 |
|                                 ![](../designers/media/b1-8.png "B1_8")                                 |                                                                        **プロパティとイベント** 選択された要素に対してプロパティを設定したり、イベントを選択します。                                                                         |
|                                 ![](../designers/media/b1-9.png "B1_9")                                 |                                                         **[検索] ボックス** プロパティを検索します。 **[検索]** ボックスに入力することで、表示されるプロパティをフィルター処理します。                                                          |
| ![](../designers/media/97fa60b9-0caf-4387-9225-b57510d32209.png "97fa60b9-0caf-4387-9225-b57510d32209") |                                **ブラシ エディターのタブ** ブラシ エディターを選択する場合に使用します。 **ブラシなし**、**単色ブラシ**、**グラデーション ブラシ**、**タイル ブラシ**、または**ブラシ リソース**から選択できます。                                |
|                                ![](../designers/media/b1-11.png "B1_11")                                |                                    **色リソース** 異なるプロパティにまったく同じ色を適用します。 **[色リソース]** タブには、**[ローカル リソース]** と **[システム リソース]** が表示されます。                                    |
|                                ![](../designers/media/b1-12.png "B1_12")                                |                                                 **RGB 色空間****[R]**、**[G]**、または **[B]** (赤、緑、青) の各数値エディターの値を調整して色を変更します。                                                  |
|                                ![](../designers/media/b1-13.png "B1_13")                                |                                                                        **アルファ チャネル****[A]** の横にある数値エディターを使用してアルファ値を変更します。                                                                        |
| ![](../designers/media/d839d12c-07a1-4127-a830-4a8e7069f4fe.png "d839d12c-07a1-4127-a830-4a8e7069f4fe") |                                       **色をリソースに変換** 選択した色を色リソースに変換します。 色リソースは、[色リソース] タブをクリックした場合に使用できます。                                        |
|                                ![](../designers/media/b1-15.png "B1_15")                                |                                                                                 **16 進数値** 表示されている色を表す 16 進数値が表示されます。                                                                                 |
|                     ![吹き出し 16](../designers/media/b5-label-16.png "b5_label_16")                     |                                                                                **グラデーション スライダー** グラデーション ブラシが選択されている場合にのみ表示されます。                                                                                 |
| ![](../designers/media/d50027a1-6824-4ad8-8b4e-558b0756dcf8.png "d50027a1-6824-4ad8-8b4e-558b0756dcf8") |                                                                     **詳細設定プロパティの表示** 使用頻度が低いプロパティのカテゴリを表示します。                                                                      |

 **短いビデオを見る:** ![インストール済みフィーチャーの構成](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [[プロパティ] パネル](https://www.youtube.com/watch?v=HCqQfiobdag&list=PLBDF977B2F1DAB358&index=7)。

## <a name="see-also"></a>参照
 [コントロールを挿入し、その動作を変更する](../designers/insert-controls-and-modify-their-behavior-in-xaml-designer.md)[オブジェクトをアニメーション化](../designers/animate-objects-in-xaml-designer.md)する[図形とパスの描画](../designers/draw-shapes-and-paths.md) [Visual Studio での XAML のデザインと Blend for Visual Studio](../designers/designing-xaml-in-visual-studio.md)

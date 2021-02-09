---
title: Blend for Visual Studio 機能ツアー
titleSuffix: ''
description: XAML ベースの Windows および Web アプリケーションを設計するためのコンポーネントである、ワークスペースの UI と Blend for Visual Studio の機能について説明します。
ms.custom: SEO-VS-2020
ms.date: 07/31/2019
ms.topic: overview
f1_keywords:
- Blend.Start.Dev12
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9fdc3fc2241807cd1b36ec64d620c7b46a498918
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889266"
---
# <a name="blend-for-visual-studio-overview"></a>Blend for Visual Studio 概要

Blend for Visual Studio を使用すると、XAML ベースの Windows および Web アプリケーションを設計できます。 Visual Studio と同じ基本的な XAML デザイン環境を提供しているほか、アニメーションやビヘイビアーなどの高度なタスクを視覚的にデザインする機能が追加されています。 Blend と Visual Studio の比較については、[Visual Studio と Blend for Visual Studio で XAML をデザインする](../xaml-tools/designing-xaml-in-visual-studio.md)方法に関するページを参照してください。

Blend for Visual Studio は、Visual Studio のコンポーネントです。 Blend をインストールするには、**Visual Studio インストーラー** で、**[ユニバーサル Windows プラットフォーム開発]** または **[.NET デスクトップ開発]** のいずれかのワークロードを選択します。 これらの両方のワークロードに、Blend for Visual Studio コンポーネントが含まれます。

![UWP のワークロード コンポーネント](media/installer-uwp.png)&nbsp;&nbsp;&nbsp;&nbsp;![.NET デスクトップ開発のワークロード コンポーネント](media/installer-dotnet-desktop.png)

Blend for Visual Studio を初めてご使用になる場合は、このワークスペース特有の機能に慣れるために少し時間を取ってください。 このトピックでは、短いツアーにお連れします。

## <a name="tools-panel"></a>ツール パネル

Blend for Visual Studio の **[ツール]** パネルは、アプリケーションのオブジェクトの作成と変更に使用します。 *.xaml* ファイルを開くと、XAML デザイナーの左側に **[ツール]** パネルが表示されます。

パネルにあるツールを選択してアートボード上でマウスを動かすと、オブジェクトを描画できます。

![Blend for Visual Studio の [ツール] パネル](media/blend-tools-panel.png)

> [!TIP]
> **[ツール]** パネルの一部のツールにはバリエーションがあります。たとえば、四角形の代わりに、楕円形や線を選択することができます。 これらのバリエーションにアクセスするには、ツールを右クリックするか、長押しします。
>
> ![Blend for Visual Studio のシェイプ ツールのバリエーション](media/blend-rectangle-tool-variations.png)

### <a name="selection-tools"></a>選択ツール

オブジェクトとパスを選択します。 **個別選択** ツールを使用すると、入れ子状のオブジェクトやパス セグメントを選択できます。

### <a name="view-tools"></a>ビュー ツール

手のひらツールでの移動やズームなど、アートボードの表示の調整を行います。

### <a name="brush-tools"></a>ブラシ ツール

ブラシの変換やグラデーションの適用など、オブジェクトのビジュアル属性を操作します。

### <a name="object-tools"></a>オブジェクト ツール

パス、図形、レイアウト パネル、テキスト、コントロールなど、よく使用するオブジェクトをアートボード上で描画します。

### <a name="asset-tools"></a>アセット ツール

[アセット] ウィンドウにアクセスし、ライブラリから最近使用したアセットを表示します。

## <a name="assets-window"></a>[アセット] ウィンドウ

**[アセット]** ウィンドウには、使用できるすべてのコントロールが表示されます (Visual Studio の **[ツールボックス]** に似ています)。 また、コントロールのほかに、スタイル、メディア、ビヘイビアー、効果など、アートボードに追加できるすべてのものが **[アセット]** ウィンドウに用意されています。 **[アセット]** ウィンドウを開くには、**[表示]** > **[アセット] ウィンドウ** を選択するか、**Ctrl**+**Alt**+**X** キーを押します。

![Blend for Visual Studio の [アセット] ウィンドウ](media/blend-assets-window.png)

- **[検索]** ボックスに入力し、アセットの一覧を絞り込みます。
- 右上のボタンを使用し、アセットの表示方法としてグリッド モードとリスト モードを切り替えます。

## <a name="objects-and-timeline-window"></a>[オブジェクトとタイムライン] ウィンドウ

このウィンドウを使用すると、アートボード上のオブジェクトを整理して、必要な場合はアニメーション化できます。 **[オブジェクトとタイムライン]** ウィンドウを開くには、 **[表示]** 、 **[ドキュメント アウトライン]** の順に選択します。 Visual Studio の [[ドキュメント アウトライン]](creating-a-ui-by-using-xaml-designer-in-visual-studio.md#document-outline-window) ウィンドウで与えられる機能に加え、Blend for Visual Studio の [オブジェクトとタイムライン] ウィンドウには右側にタイムライン作成領域があります。 アニメーションを作成し、編集するときにタイムラインを使用します。

![アニメーション モードの [オブジェクトとタイムライン] ウィンドウ](media/storyboard-timeline.png)

ストーリーボード関連のボタンを使用する ![Blend for Visual Studio のストーリーボード ボタン](media/storyboard-buttons.png) ストーリーボードを作成、削除、閉じる、または選択します。 右側にあるタイムライン作成領域を使用し、タイムラインを表示し、キーフレームを動かします。

ウィンドウの各ボタンの上にカーソルを合わせると、利用できる機能の詳細が表示されます。

## <a name="see-also"></a>関連項目

- [オブジェクトのアニメーション化](../xaml-tools/animate-objects-in-xaml-designer.md)
- [図形とパスの描画](../xaml-tools/draw-shapes-and-paths.md)
- [Visual Studio および Blend for Visual Studio での XAML の設計](../xaml-tools/designing-xaml-in-visual-studio.md)

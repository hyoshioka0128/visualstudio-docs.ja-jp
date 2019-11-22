---
title: XAML デザイナーでコントロールを挿入し、そのビヘイビアーを変更する | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: a80fff74-bf01-41c9-ab85-ada7a873c3a9
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 02d51c5799391863262d285e1cda209a3b7938d7
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300845"
---
# <a name="insert-controls-and-modify-their-behavior-in-xaml-designer"></a>XAML デザイナー でコントロールを挿入し、そのビヘイビアーを変更する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コントロールは、ユーザーとアプリとの対話を可能にします。 コントロールを使用すると、情報を収集できるとともに、オブジェクトのアニメーション化や、データ ソースのクエリなどのアクションを実行できます。

 **このトピックの内容**

- [アートボードにコントロールを追加する](#Insert)

- [コントロールの操作を行う](#Modify)

## <a name="Insert"></a> アートボードにコントロールを追加する
 コントロールは、 **[アセット]** パネルから **アートボード**にドラッグし、 **[プロパティ]** ウィンドウで修正できます。

 ![Blend &#45; Assets &#45; FlipView](../designers/media/blend-assetsflipview-xaml.png "blend_AssetsFlipView_XAML")

 次のビデオは、いくつかの一般的なコントロールの使用方法を示しています。

|Control|短いビデオを見る|
|-------------|-------------------------|
|`Menu` ![](../designers/media/015a263c-0b2b-4253-ac57-b86fcb8c9591.png "015a263c-0b2b-4253-ac57-b86fcb8c9591")|![Configure Installed Features](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Add the controls](https://www.youtube.com/watch?v=ra4AHfgD4Ys&list=PLBDF977B2F1DAB358&index=45)|
|`Button` ![](../designers/media/05df1779-a68f-436b-b834-a91b7995a3ec.png "05df1779-a68f-436b-b834-a91b7995a3ec")|![Configure Installed Features](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Design a button](http://www.popscreen.com/v/6A4gb/Microsoft-Expression-Blend-Designing-a-Button)|
|`Textblock` ![](../designers/media/42165963-00f7-4a33-abcd-b0849edebada.png "42165963-00f7-4a33-abcd-b0849edebada")|![Configure Installed Features](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Add images to a textblock](http://www.popscreen.com/v/6A4du/Microsoft-Expression-Blend-Adding-Images-to-a-TextBlock)|
|`Slider` ![](../designers/media/bf689d92-3c74-4218-815c-e98c930ac189.png "bf689d92-3c74-4218-815c-e98c930ac189")|![Configure Installed Features](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Build a Slider with a  ToolTip](https://www.bing.com/videos/search?q=slider%20expression%20blend&qs=n&form=QBVR&pq=slider%20expression%20blend&sc=1-23&sp=-1&sk=#view=detail&mid=F1BB7DB91B2772A8CA2AF1BB7DB91B2772A8CA2A)|
|`GridSplitter` ![](../designers/media/d08d529f-a27e-4a8f-95aa-8a4e8b4ee7be.png "d08d529f-a27e-4a8f-95aa-8a4e8b4ee7be")|![Configure Installed Features](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Work with a GridSplitter](https://www.youtube.com/watch?v=bf4t6c8ms2w)|

### <a name="make-a-control-out-of-an-image-shape-or-path"></a>イメージ、図形、またはパスからコントロールを作成する
 あらゆるオブジェクトをコントロールにすることができます。

 ![Blend Make Into Control dialog box](../designers/media/blend-makeintocontrol-xaml.png "blend_MakeIntoControl_XAML")

 たとえば、ページの中央にテレビの画像があるところを想像してください。 テレビのボタンのような小さいイメージからコントロールを作成できます。 次に、このボタンをクリックしてチャンネルを変更します。

 これが可能なのは、ボタンがコントロールになったためです。 コントロールを使用すると;、ユーザーの操作に応答することができます。この場合は、ユーザーがボタンをクリックしたときです。

 コントロールを作成するには、オブジェクトを選択します。 **[ツール]** メニューで **[コントロールの作成]** をクリックします。

## <a name="Modify"></a> コントロールの操作を行う
 コントロールは、ユーザーが操作したときにアクションを実行します。 たとえば、アニメーションの開始、データ ソースの更新、またはビデオの再生を行えます。

 *トリガー*、 *ビヘイビアー*、 *イベント* を使用して、コントロールの操作を実行します。

### <a name="triggers"></a>トリガー
 *トリガー* は、プロパティを変更したり、イベントまたは別のプロパティの変更に応じてタスクを実行できます。 たとえば、ユーザーがボタンの上にマウスのポインタを置くとボタンの色が変化するなどです。

 ![The "Triggers" panel](../designers/media/custom-button-blend-propertytriggerinfo.png "custom_button_blend_PropertyTriggerInfo")

 **Watch a short video:** ![Configure Installed Features](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Add a property trigger](http://www.popscreen.com/v/6A4gO/Microsoft-Expression-Blend-Adding-a-Property-Trigger).

### <a name="behaviors"></a>ビヘイビアー
 *ビヘイビアー* は再利用可能なコードのパッケージです。 ビヘイビアーは、プロパティの変更より少し多くのことができます。 データ サービスのクエリなどのアクションを実行できます。 Blend には小さなアクションのコレクションが付属していますが、さらに追加することができます。 ビヘイビアーをアートボード内のオブジェクトにドラッグしてから、プロパティを設定してビヘイビアーをカスタマイズします。

 ![FluidMoveBehavior in the Properties panel](../designers/media/b4-fluidmovebehaviorproperties-sample.png "b4_FluidMoveBehaviorProperties_Sample")

 **Watch a short video:** ![Configure Installed Features](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Blend tips: Intro to using behaviors Part 1](https://www.bing.com/videos/search?q=Expression%20blend%20behaviors&qs=n&form=QBVR&pq=expression%20blend%20behavior&sc=4-25&sp=-1&sk=#view=detail&mid=CF0DD797ED84DE740904CF0DD797ED84DE740904).

### <a name="events"></a>イベント
 柔軟性を最大にするため、 *イベント*を処理します。 いくらかのコードを記述する必要があります。

 **Watch a short video:** ![Configure Installed Features](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Add a Mouse event](https://www.youtube.com/watch?v=2PMxAlb-x_E).

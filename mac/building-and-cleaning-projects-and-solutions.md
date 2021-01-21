---
title: プロジェクトとソリューションのビルドおよびクリーン
description: この記事では、Visual Studio for Mac でプロジェクトをビルドする方法について説明します
author: heiligerdankgesang
ms.author: dominicn
ms.date: 09/19/2019
ms.assetid: E4B6CB42-9FE2-43B9-93B7-BD4BD50518B1
ms.topic: how-to
ms.openlocfilehash: de6be4b509eff8a013f7367614e0016f810b3657
ms.sourcegitcommit: 2cf3a03044592367191b836b9d19028768141470
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2020
ms.locfileid: "94492699"
---
# <a name="building-and-cleaning-projects-and-solutions"></a>プロジェクトとソリューションのビルドおよびクリーン

この記事の手順に従うと、ソリューションに含まれるプロジェクトの全部または一部をビルド、リビルド、クリーンする方法が理解できます。

> [!NOTE]
> このトピックは、Visual Studio for Mac に適用されます。 Windows での Visual Studio については、[Visual Studio のプロジェクトとソリューションのビルドおよびクリーン](/visualstudio/ide/building-and-cleaning-projects-and-solutions-in-visual-studio)に関するページを参照してください。

## <a name="to-build-rebuild-or-clean-an-entire-solution"></a>ソリューション全体のビルド、リビルド、またはクリーン

1. **[ソリューション] ウィンドウ** でソリューション ノードを選択します。

    ![ソリューション ノードの選択](media/compiling-and-building-image1.png)

2. メニュー バーで **[ビルド]** メニューを選択し、次のいずれかのオプションを選択します。

    ![[すべてビルド] メニュー項目の選択](media/compiling-and-building-image2.png)

    * **[すべてビルド]** を選択すると、プロジェクトに含まれるファイルとコンポーネントのうち、一番新しいビルド以降に変更されたものがコンパイルされます。

    * **[すべてリビルド]** を選択すると、ソリューションが "クリーン" されてから、すべてのプロジェクト ファイルとコンポーネントがビルドされます。

    * **[すべてクリーン]** を選択すると、中間ファイルと出力ファイルがすべて削除されます。 その後、プロジェクト ファイルとコンポーネント ファイルのみを残して、中間ファイルと出力ファイルの新しいインスタンスをビルドできます。

## <a name="to-build-or-rebuild-a-single-project"></a>1 つのプロジェクトをビルドまたはリビルドするには

1. **[ソリューション] ウィンドウ** でプロジェクトを選択します。

2. メニュー バーから **[ビルド]** メニューを選択します。

3. [<プロジェクト名> のビルド]、[<プロジェクト名> のリビルド]、[<プロジェクト名> のクリーン] のいずれかを選択します。

## <a name="to-stop-a-build"></a>ビルドを停止するには

ビルドを停止するには、次のいずれかのオプションを使用します。

* ステータス領域の赤い正方形を押します。

    ![赤い正方形を押し、ビルドを停止する](media/compiling-and-building-image3.png)

* **[ビルド]** メニューの **[停止]** 項目を使用します。

* **Cmd + Shift + Return** を押します。

## <a name="see-also"></a>関連項目

- [プロジェクトとソリューションのビルドおよびクリーン (Windows の Visual Studio)](/visualstudio/ide/building-and-cleaning-projects-and-solutions-in-visual-studio)
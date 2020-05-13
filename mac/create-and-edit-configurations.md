---
title: ビルド構成の作成と編集
description: この記事では、Visual Studio for Mac でビルド構成を作成する方法について説明します。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 09/18/2019
ms.assetid: CC1B72D6-12FF-4CCC-A9D4-00F2DC14589F
ms.custom: video
ms.openlocfilehash: 26f6e25bfe1284fc31bcd484b905bf5d75c2ba15
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "71128433"
---
# <a name="creating-and-editing-build-configurations"></a>ビルド構成の作成と編集

ビルド構成を利用すると、ビルドを厳密に制御し、さまざまなテスト状況や配布状況に合わせた構成を作成できます。 ビルド構成は、個々のプロジェクトに対して作成するか、ソリューション全体に対して作成できます。

[プロジェクト オプション] ダイアログを利用し、プロジェクトとソリューションの両方に対して新しい構成を作成したり、既存の構成を編集したりできます。

>[!NOTE]
>このトピックは、Visual Studio for Mac に適用されます。 Windows の Visual Studio については、「[方法:構成を作成および編集する](/visualstudio/ide/how-to-create-and-edit-configurations)」を参照してください。

## <a name="creating-a-project-build-configuration"></a>プロジェクトのビルド構成の作成

プロジェクトのビルド構成は次の手順で作成します。

1. プロジェクト ノードを右クリックし、 **[オプション]** を選択します。 プロジェクト ノードをダブルクリックして [プロジェクト オプション] ダイアログを表示することもできます。

2. [プロジェクト オプション] ダイアログで、 **[ビルド]、[構成]** の順に選択します。

    ![プロジェクト オプションの構成マネージャー](media/create-and-edit-configurations-image2.png)

3. 新しい構成を作成するには **[追加]** を選択します。 既存の構成をコピーすることもできます。

構成が作成されたら、プロジェクト オプションの **[ビルド]** セクションを利用し、構成に合わせてプロパティを調整できます。

![ビルド オプションの構成](media/create-and-edit-configurations-image3.png)

## <a name="creating-a-solution-build-configuration"></a>ソリューションのビルド構成の作成

ソリューションのビルド構成は次の手順で作成します。

1. ソリューション ノードを右クリックし、 **[オプション]** を選択します。 ソリューション ノードをダブルクリックして [ソリューション オプション] ダイアログを表示することもできます。

2. [ソリューション オプション] ダイアログで、 **[ビルド]、[構成]** の順に選択します。

    ![ソリューション オプションの構成マネージャー](media/create-and-edit-configurations-image1.png)

3. 新しい構成を作成するには **[追加]** を選択します。 既存の構成をコピーすることもできます。

構成が作成されたら、各プロジェクトの [プロジェクト オプション] ダイアログの **[ビルド]** セクションを利用し、構成に合わせてプロパティを調整できます。

![ビルド オプションの構成](media/create-and-edit-configurations-image3.png)

## <a name="renaming-a-build-configuration"></a>ビルド構成の名前変更

構成の名前を変更するには、プロジェクトまたはソリューション オプションで **[ビルド]、[構成]** の順に選択し、構成一覧から構成を選択します。

![構成一覧](media/create-and-edit-configurations-image4.png)

**[名前の変更]** ボタンを選択します。

![[名前の変更] ダイアログ](media/create-and-edit-configurations-image5.png)

次に、 **[OK]** をクリックして確定します。

## <a name="related-video"></a>関連ビデオ

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Launch-Multiple-Projects/player]

## <a name="see-also"></a>関連項目

- [ビルド構成を作成して編集する (Windows の Visual Studio)](/visualstudio/ide/how-to-create-and-edit-configurations)
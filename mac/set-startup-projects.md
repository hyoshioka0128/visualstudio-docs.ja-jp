---
title: 複数のスタートアップ プロジェクトを設定する
description: この記事では、実行時またはデバッグ時に開始する複数のプロジェクトを設定する方法について説明します。
author: jmatthiesen
ms.author: jomatthi
ms.date: 11/09/2020
ms.topic: how-to
ms.prod: visual-studio-mac
ms.assetid: fd354fff-ce6b-4505-a815-84a2311e39ba
ms.openlocfilehash: df1e088a5e2d0f65d8b72dad0895f1edb1740f1f
ms.sourcegitcommit: 2cf3a03044592367191b836b9d19028768141470
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2020
ms.locfileid: "94493570"
---
# <a name="set-multiple-startup-projects"></a>複数のスタートアップ プロジェクトを設定する

Visual Studio for Mac では、ソリューションをデバッグまたは実行するときに、複数のプロジェクトを開始する必要があることを指定できます。

## <a name="to-set-multiple-startup-projects"></a>複数のスタートアップ プロジェクトを設定するには

1. [ソリューション] ウィンドウでソリューション (一番上のノード) を選択します。

2. ソリューション ノードを右クリックし、 **[スタートアップ プロジェクトの設定]** を選択します。

   ![[スタートアップ プロジェクトの設定] を選択する](media/startup-proj-ctx-menu.png)

3. **[ソリューション実行構成の作成]** ダイアログ ボックスが開きます。 このダイアログ ボックスでは、ソリューションに対して新しい名前付きソリューション実行構成を作成できます。 任意の名前を使用することができます。 既定の名前は `Multiple Projects` です。

   ![[ソリューション実行構成の作成] ダイアログ ボックス](media/create-sln-run-config.png)

4. **[実行構成の作成]** を選択します。 **[ソリューション オプション]** ダイアログ ボックスが開き、新しいソリューション実行構成が選択されます。

   ![[ソリューション オプション] ダイアログ ボックス](media/sln-options-run-config-multi-projects.png)

5. Visual Studio for Mac からアプリをデバッグまたは実行するときに開始するプロジェクトを選択します。

   ![プロジェクトが選択されている [ソリューション オプション] ダイアログ ボックス](media/sln-options-run-config-multi-projects-configured.png)

6. **[OK]** を選択します。 新しいソリューション実行構成がアクティブな実行構成として設定されます。

   ![デバッグまたは実行時に複数のプロジェクトが開始するように構成されたソリューション](media/startup-project-configured.png)

   これで 2 つのプロジェクトの開始が構成されました。[ソリューション] ウィンドウには、いずれのプロジェクトも **太字** で表示されています。 ツール バーでは、新しい実行構成が現在のソリューション実行構成として設定されます。

## <a name="next-steps"></a>次の手順

- [Visual Studio for Mac のコンパイルとビルド](compiling-and-building.md)
- [ビルド構成について](configurations.md)

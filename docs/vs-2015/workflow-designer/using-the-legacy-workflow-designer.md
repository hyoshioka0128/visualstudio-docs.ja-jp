---
title: Using the Legacy Workflow Designer | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- Visual Studio 2005 Extensions for Windows Workflow Foundation, about
ms.assetid: 7af53077-afd7-465f-9c1d-b387e9d4f216
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2fa11cd0b29f3b8ee6008b8c0b3369b16812f0e5
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74302786"
---
# <a name="using-the-legacy-workflow-designer"></a>従来のワークフロー デザイナーの使用
[!INCLUDE[wfd2](../includes/wfd2-md.md)] が備えている従来の[!INCLUDE[vs2010](../includes/vs2010-md.md)]を使用すると、[!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] または [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] を対象とすることができます。

 It is accessed by selecting either the **.NET Framework 3.0** option or the **.NET Framework 3.5** option in the drop down list at the top of the **New Project** window. The default option in [!INCLUDE[vs2010](../includes/vs2010-md.md)] is **.NET Framework 4** which is used to create [!INCLUDE[wf](../includes/wf-md.md)] applications that target the [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)].

 [!INCLUDE[wfd2](../includes/wfd2-md.md)] では、使い慣れた [!INCLUDE[wf](../includes/wf-md.md)] ユーザー インターフェイスを使用して [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] アプリケーションをグラフィカルに作成できます。 [!INCLUDE[wf](../includes/wf-md.md)] アプリケーションは、アクティビティと呼ばれるワークフロー プロセス ステップで構成されます。 To create a workflow, compose activities on the design surface by dragging their respective activity designers from **Toolbox** onto the design surface.

 次の表に、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] for Windows Workflow Foundation の主な機能を示します。

|特性|説明|
|-------------|-----------------|
|アクティビティのドラッグ アンド ドロップ|Drag activities from the **Toolbox** onto the design surface to create a workflow.|
|プロパティ ブラウザー|The standard **Properties** window in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] is used to configure the properties of an activity.|
|ズーム|The binoculars **Zoom Level** icon is located below the vertical scroll bar on the right side of the design surface. Click the binoculars and select a zoom percentage to cause the workflow graphic to zoom in or out. You can also use the **Pan** icon magnifying glass cursor options to zoom in and out.|
|パン|The **Pan** icon, a circle that contains four crossed arrows pointing in four directions, is located below the vertical scroll bar on the right side of the design surface just below the binoculars zoom icon. パン アイコンをクリックすると、次のようなカーソル オプションがポップアップ メニューに表示されます。<br /><br /> -   The **Zoom In** magnifying glass cursor lets you zoom in by clicking the design surface.<br />-   The **Zoom Out** magnifying glass cursor lets you zoom out by clicking the design surface.<br />-   The **Navigation Tool** hand cursor lets you "grab" and shift the view of a workflow in the design surface.<br />-   The **Default** arrow cursor lets you switch from the other cursors back to the default arrow cursor.|
|自動スクロール|ワークフローが大きいために、デザイン サーフェイスの表示領域外にアクティビティを配置する必要が生じる場合があります。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のデザイン サーフェスでは、アクティビティを配置したい方向に最も近い側の端にアクティビティをドラッグすることができます。 デザイン サーフェイスの表示が、その方向に自動的にスクロールされます。|
|スマート タグ|構成が完了していないアクティビティ、または構成が有効でないアクティビティは、感嘆符アイコン付きで表示されます。 このアイコンをクリックして表示されるドロップダウン リストで、アクティビティに存在する、必要な構成を確認できます。 You can then use the **Properties** window to configure the activity appropriately. アクティビティのすべてのプロパティが正しく構成されれば、感嘆符アイコンは表示されなくなります。|

## <a name="in-this-section"></a>このセクションの内容
 [Visual Studio ワークフローのウィンドウ (レガシ)](../workflow-designer/visual-studio-workflow-windows-legacy.md)

 [従来のワークフロー プロジェクトの作成](../workflow-designer/creating-legacy-workflow-projects.md)

 [シーケンシャル ワークフロー ビュー (レガシ)](../workflow-designer/sequential-workflow-views-legacy.md)

 [従来のワークフロー アクティビティ](../workflow-designer/legacy-workflow-activities.md)

 [ワークフロー内でのテーマの使用 (レガシ)](../workflow-designer/using-themes-in-workflows-legacy.md)

 [従来のステート マシン ワークフロー デザイナーの使用](../workflow-designer/using-the-legacy-state-machine-workflow-designer.md)

 [従来のアクティビティ デザイナーの使用](../workflow-designer/using-the-legacy-activity-designer.md)

 [従来の Designer for Windows Workflow Foundation UI ヘルプ](../workflow-designer/legacy-designer-for-windows-workflow-foundation-ui-help.md)

## <a name="see-also"></a>参照
 [Developing Workflows](https://go.microsoft.com/fwlink?LinkID=65010)
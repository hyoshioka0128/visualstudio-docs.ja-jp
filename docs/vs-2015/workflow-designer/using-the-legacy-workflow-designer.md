---
title: 従来のワークフローデザイナーを使用する |Microsoft Docs
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
ms.openlocfilehash: 72c92b4431c21c27bc1fe2ff86b24c850cc34694
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75846082"
---
# <a name="using-the-legacy-workflow-designer"></a>従来のワークフロー デザイナーの使用
[!INCLUDE[wfd2](../includes/wfd2-md.md)] が備えている従来の[!INCLUDE[vs2010](../includes/vs2010-md.md)]を使用すると、[!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] または [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] を対象とすることができます。

 これにアクセスするには、 **[新しいプロジェクト]** ウィンドウの上部にあるドロップダウンリストの **[.NET Framework 3.0]** オプションまたは **[.NET Framework 3.5]** オプションを選択します。 [!INCLUDE[vs2010](../includes/vs2010-md.md)] の既定のオプションは **.NET Framework 4**で、[!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)]を対象とする [!INCLUDE[wf](../includes/wf-md.md)] アプリケーションを作成するために使用されます。

 [!INCLUDE[wfd2](../includes/wfd2-md.md)] では、使い慣れた [!INCLUDE[wf](../includes/wf-md.md)] ユーザー インターフェイスを使用して [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] アプリケーションをグラフィカルに作成できます。 [!INCLUDE[wf](../includes/wf-md.md)] アプリケーションは、アクティビティと呼ばれるワークフロー プロセス ステップで構成されます。 ワークフローを作成するには、それぞれのアクティビティデザイナーを **[ツールボックス]** からデザインサーフェイスにドラッグして、デザイン画面でアクティビティを作成します。

 次の表に、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] for Windows Workflow Foundation の主な機能を示します。

|特性|説明|
|-------------|-----------------|
|アクティビティのドラッグ アンド ドロップ|アクティビティを **[ツールボックス]** からデザイン画面にドラッグして、ワークフローを作成します。|
|プロパティ ブラウザー|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の標準**プロパティ**ウィンドウは、アクティビティのプロパティを構成するために使用されます。|
|[ズーム]|[双眼鏡**ズームレベル**] アイコンは、デザインサーフェイスの右側の垂直スクロールバーの下に配置されます。 双眼鏡をクリックし、ズーム率を選択すると、ワークフローグラフィックが拡大または縮小されます。**パン**アイコン虫眼鏡のカーソルオプションを使用して、拡大と縮小を行うこともできます。|
|パン|**パン**アイコン (4 方向を指す4つの交差矢印を含む円) は、デザインサーフェイス右側の垂直スクロールバーの下 (双眼鏡ズームアイコンのすぐ下) にあります。 パン アイコンをクリックすると、次のようなカーソル オプションがポップアップ メニューに表示されます。<br /><br /> **[ズームイン]** 虫眼鏡カーソルを使用すると、デザイン画面をクリックしてズームインできます。<br />**[ズームアウト]** 虫眼鏡カーソルを使用すると、デザイン画面をクリックしてズームアウトできます。<br />-**ナビゲーションツール**ハンドカーソルを使用すると、デザインサーフェイスでワークフローのビューを "グラブ" して、そのビューをシフトすることができます。<br />-**既定**の矢印カーソルを使用すると、他のカーソルから既定の矢印カーソルに戻ることができます。|
|自動スクロール|ワークフローが大きいために、デザイン サーフェイスの表示領域外にアクティビティを配置する必要が生じる場合があります。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のデザイン サーフェスでは、アクティビティを配置したい方向に最も近い側の端にアクティビティをドラッグすることができます。 デザイン サーフェイスの表示が、その方向に自動的にスクロールされます。|
|スマート タグ|構成が完了していないアクティビティ、または構成が有効でないアクティビティは、感嘆符アイコン付きで表示されます。 このアイコンをクリックして表示されるドロップダウン リストで、アクティビティに存在する、必要な構成を確認できます。 その後、 **[プロパティ]** ウィンドウを使用して、アクティビティを適切に構成できます。 アクティビティのすべてのプロパティが正しく構成されれば、感嘆符アイコンは表示されなくなります。|

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
 [ワークフローの開発](https://msdn2.microsoft.com/library/bb628448.aspx)

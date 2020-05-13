---
title: 'チュートリアル: グラフィックス情報のキャプチャ |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 48f12f6e-57b4-48ec-a145-89fa71a42424
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: aab86d42cd158ad64ebb16497b8d2d9f5a7002df
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72734726"
---
# <a name="walkthrough-capturing-graphics-information"></a>チュートリアル: グラフィックス情報のキャプチャ
このチュートリアルでは、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のグラフィックス診断を使用して、Direct3D アプリケーションから手動でグラフィックス情報をキャプチャする方法を示します。

 このチュートリアルでは、次の作業について説明します。

- グラフィックス診断をアプリケーションにフックする

- グラフィックス情報をキャプチャする

## <a name="capturing-graphics-information"></a>グラフィックス情報をキャプチャする
 グラフィックス診断ツールを使用するには、まず依存するグラフィックス情報をキャプチャする必要があります。 キャプチャを有効にするには、 **[診断の開始]** を使用してアプリケーションの起動時にグラフィックス診断をフックします。

#### <a name="to-enable-the-capture-of-graphics-information-after-a-project-or-solution-is-loaded"></a>プロジェクトまたはソリューションの読み込み後にグラフィックス情報のキャプチャを有効にするには

1. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]で、グラフィックス情報をキャプチャするアプリケーションのプロジェクト ファイルまたはソリューション ファイルを読み込みます。

2. グラフィックス診断ツール バーで、 **[診断の開始]** を選択します。

#### <a name="to-enable-the-capture-of-graphics-information-without-loading-a-project-or-solution"></a>プロジェクトまたはソリューションを読み込まずにグラフィックス情報のキャプチャを有効にするには

1. メニュー バーで **[ファイル]** 、 **[開く]** 、 **[プロジェクト/ソリューション]** の順に選択します。 **[プロジェクトを開く]** ダイアログ ボックスが表示されます。

2. プロジェクト ファイルまたはソリューション ファイルの代わりに、グラフィックス情報をキャプチャするアプリケーションの実行可能ファイルを指定し、 **[開く]** を選択します。

3. メニュー バーで、 **[デバッグ]** 、 **[グラフィックス]** 、 **[診断の開始]** の順に選択します。

   アプリを開始して、フレームがレンダリングされると、グラフィックス情報をキャプチャすることができます。

#### <a name="to-capture-graphics-information"></a>グラフィックス情報をキャプチャするには

- グラフィックス診断ツール バーで、 **[キャプチャ]** ボタンをクリックします。 ![[グラフィックスのキャプチャ] ボタンアイコン](media/debuggingdirectxgraphics.png "DebuggingDirectXGraphics")

   -または-

   アプリケーションにフォーカスを置いた状態で、 **PrintScreen**キーを押します。

  フレームに関する情報をキャプチャするたびに、グラフィックス診断は Direct3D イベントおよび関連付けられた状態を記録し、グラフィックス ログにデータを追加します。 グラフィックス ログは、グラフィックス診断のセッションごとに新しく作成されます。 グラフィックスログの詳細については、「[概要](overview-of-visual-studio-graphics-diagnostics.md)」を参照してください。

## <a name="next-steps"></a>次のステップ
 このチュートリアルでは、手動でグラフィックス情報をキャプチャする方法を示しました。 次の手順では、次のオプションを検討します。

- グラフィックス診断ツールを使用してキャプチャされたグラフィックス情報を解析する方法について学習します。 「[概要](overview-of-visual-studio-graphics-diagnostics.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [Capturing Graphics Information](capturing-graphics-information.md)

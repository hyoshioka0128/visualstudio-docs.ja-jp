---
title: 'チュートリアル: グラフィックス情報のキャプチャ | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 48f12f6e-57b4-48ec-a145-89fa71a42424
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9ebd0453347084d1662c6bc7837fc1e96f498fbd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68151468"
---
# <a name="walkthrough-capturing-graphics-information"></a>チュートリアル: グラフィックス情報をキャプチャする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のグラフィックス診断を使用して、Direct3D アプリケーションから手動でグラフィックス情報をキャプチャする方法を示します。  
  
 このチュートリアルでは、次の作業について説明します。  
  
- グラフィックス診断をアプリケーションにフックする  
  
- グラフィックス情報をキャプチャする  
  
## <a name="capturing-graphics-information"></a>グラフィックス情報をキャプチャする  
 グラフィックス診断ツールを使用するには、まず依存するグラフィックス情報をキャプチャする必要があります。 キャプチャを有効にするには、 **[診断の開始]** を使用してアプリケーションの起動時にグラフィックス診断をフックします。  
  
#### <a name="to-enable-the-capture-of-graphics-information-after-a-project-or-solution-is-loaded"></a>プロジェクトまたはソリューションの読み込み後にグラフィックス情報のキャプチャを有効にするには  
  
1. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]で、グラフィックス情報をキャプチャするアプリケーションのプロジェクト ファイルまたはソリューション ファイルを読み込みます。  
  
2. グラフィックス診断ツール バーで、 **[診断の開始]** を選択します。  
  
#### <a name="to-enable-the-capture-of-graphics-information-without-loading-a-project-or-solution"></a>プロジェクトまたはソリューションを読み込まずにグラフィックス情報のキャプチャを有効にするには  
  
1. メニュー バーで **[ファイル]** 、 **[開く]** 、 **[プロジェクト/ソリューション]** の順に選択します。 **[プロジェクトを開く]** ダイアログ ボックスが表示されます。  
  
2. プロジェクト ファイルまたはソリューション ファイルの代わりに、グラフィックス情報をキャプチャするアプリケーションの実行可能ファイルを指定し、 **[開く]** を選択します。  
  
3. メニュー バーで、 **[デバッグ]** 、 **[グラフィックス]** 、 **[診断の開始]** の順に選択します。  
  
   アプリを開始して、フレームがレンダリングされると、グラフィックス情報をキャプチャすることができます。  
  
#### <a name="to-capture-graphics-information"></a>グラフィックス情報をキャプチャするには  
  
- グラフィックス診断ツール バーで、 **[キャプチャ]** ボタンをクリックします。 ![グラフィックス キャプチャ ボタン アイコン](../debugger/media/debuggingdirectxgraphics.png "DebuggingDirectXGraphics")  
  
   \- または -  
  
   アプリケーションにフォーカスを置いた状態で、 **PrintScreen**キーを押します。  
  
  フレームに関する情報をキャプチャするたびに、グラフィックス診断は Direct3D イベントおよび関連付けられた状態を記録し、グラフィックス ログにデータを追加します。 グラフィックス ログは、グラフィックス診断のセッションごとに新しく作成されます。 グラフィックス ログについては、「[概要](../debugger/overview-of-visual-studio-graphics-diagnostics.md)」をご覧ください。  
  
## <a name="next-steps"></a>次の手順  
 このチュートリアルでは、手動でグラフィックス情報をキャプチャする方法を示しました。 次の手順では、次のオプションを検討します。  
  
- グラフィックス診断ツールを使用してキャプチャされたグラフィックス情報を解析する方法について学習します。 「[概要](../debugger/overview-of-visual-studio-graphics-diagnostics.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Capturing Graphics Information](../debugger/capturing-graphics-information.md)

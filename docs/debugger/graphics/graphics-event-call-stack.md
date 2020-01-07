---
title: グラフィックスイベント呼び出し履歴 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.graphics.callstack
ms.assetid: 8a30168d-8b39-4de1-b094-c7356ba101a3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c221a572264bf6a6aaed9edbec66fb3c0c3ff4b9
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72735511"
---
# <a name="graphics-event-call-stack"></a>グラフィックス イベント呼び出し履歴
Visual Studio Graphics Analyzer のグラフィックス イベント呼び出し履歴を使用すると、問題のあるグラフィックス イベントとアプリのソース コードとの間の関係をマップできます。

 [イベント呼び出し履歴] ウィンドウを次に示します。

 ![DrawIndexed イベントの前のコールスタック。](media/gfx_diag_demo_graphics_event_call_stack_orientation.png "gfx_diag_demo_graphics_event_call_stack_orientation")

## <a name="understanding-the-graphics-event-call-stack"></a>グラフィックス イベント呼び出し履歴について
 [イベント呼び出し履歴] を使用すると、特定の Direct3D イベントが発生するまでの実行フローを理解できます。 これは Visual Studio の呼び出し履歴ウィンドウに似ていますが、実行中のアプリにおいて現在のスレッドの現在の呼び出し履歴を表示するのではなく、選択した Direct3D イベントが発生した時点の呼び出し履歴を表示する点が異なります。 [イベント呼び出し履歴] から、選択した Direct3D イベントの呼び出しサイトに移動して、前後のコードを確認できます。

 [イベント呼び出し履歴] を使用して、問題のイベントの発生元であるコード パスを識別することにより、コードベースの知識に基づき、問題の原因を推測できるようになります。また、アプリのソース コードにブレークポイントを追加して、従来のデバッグ手法で、アプリまたはイベント パラメーターの状態によって、どのようにイベントの不適切な動作が発生しているかを調査することもできます。 この調査は、問題がレンダリングに関連していることのみがわかっている場合に、ソース コード内の問題を見つけるのに役立ちます。

### <a name="graphics-event-call-stack-information"></a>グラフィックス イベント呼び出し履歴の情報
 イベント呼び出し履歴では、フレーム前イベントまたはユーザー定義イベントはサポートされていません。 グラフィックス イベントの呼び出し履歴は、表形式で表示されます。

|Column|説明|
|------------|-----------------|
|**Name**|呼び出しサイトを含む関数を一意に識別するための記号。 関数のデバッグ シンボルは、その関数が使用可能な場合に表示されます。それ以外の場合は、関数のオフセットが表示されます。|
|**ファイル**|呼び出しサイトを含むソース コード ファイルまたはライブラリ ファイルのファイル名。|
|**場所**|呼び出しサイトの行番号。|

### <a name="links-to-graphics-objects"></a>グラフィックス オブジェクトへのリンク
 選択したグラフィックス イベントについて理解するために、そのイベントが関連付けられている Direct3D オブジェクトに関する情報が必要になる場合があります。 **[グラフィックス イベント呼び出し履歴]** ウィンドウで、この情報へのリンクが提供されます。

## <a name="see-also"></a>関連項目
- [チュートリアル: 頂点の網かけによるオブジェクトの不足](walkthrough-missing-objects-due-to-vertex-shading.md)

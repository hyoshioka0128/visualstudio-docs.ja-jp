---
title: Visual Studio Graphics Diagnostics | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.graphics
ms.assetid: fa69c550-62a7-41b5-bb1f-7eb04af1a6e8
caps.latest.revision: 42
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 29ca6b2110038a427c76622d50f769321cda9ff9
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74296914"
---
# <a name="visual-studio-graphics-diagnostics"></a>Visual Studio グラフィックス診断
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio*Graphics Diagnostics* is a set of tools for recording and then analyzing rendering and performance problems in Direct3D apps. グラフィックス診断は、Windows PC でローカルに実行されているアプリ、Windows デバイス エミュレーターで実行されているアプリ、あるいはリモート PC またはデバイスで実行されているアプリに対して使用できます。  
  
 グラフィックス診断のワークフローは、アプリが Direct3D を使用する方法の記録を、アプリの実行中にライブでキャプチャすることから始まります。記録したアプリの動作は、直ちに分析し、共有し、後で使用するために保存できます。 Capture sessions can be initiated and controlled manually from Visual Studio or with the command-line capture tool **dxcap.exe**. Capture sessions can also be initiated and controlled programmatically by using the Graphics Diagnostics capture APIs.  
  
 キャプチャ セッションによる記録が終わったら、Visual Studio の *Graphics Analyzer* を使用して、いつでもその内容を再生できます。その際、アプリが使用したのと正確に同じリソースとレンダリング コマンドを使用して、キャプチャされたフレームが再作成されます。 Then, using the tools provided in the Graphics Analyzer window, any of the captured frames can be analyzed in detail. これらのツールを使用して、任意の Direct3D API 呼び出し、リソース、パイプライン状態オブジェクト、パイプライン ステージ、またはキャプチャしたフレーム内の任意のピクセルの完全な履歴さえも、調べることができます。 これらのツールを連携して使用すれば、レンダリングの問題を直感的に調査できます。キャプチャされたフレームにその問題が現れた地点から始めて、アプリのソース コード、シェーダー、またはグラフィックス アセットにある根本原因にまで掘り下げていきます。  
  
 パフォーマンスの問題を診断するには、キャプチャしたフレームを*フレーム分析*ツールを使用して分析できます。 このツールは、アプリが Direct3D を使用する方法を自動的に変更して、さらに最適なパフォーマンスを実現できないかどうか探索し、すべてのバリエーションのベンチマークを提供します。 以前は、このような変更を手動で設定してベンチマークを取り、いちばん違いの大きいものを見つけるだけでした。 フレーム分析を利用する場合は、有効であることが既に分かっている変更を加える必要があるだけです。  
  
 グラフィックス診断は、Direct3D アプリの外観を視覚的に優れたものにし、パフォーマンスを最大にするために役立ちます。  
  
 Continue to [Overview](../debugger/overview-of-visual-studio-graphics-diagnostics.md) to learn more about what Visual Studio Graphics Diagnostics offers.  
  
## <a name="in-this-section"></a>このセクションの内容  
 [概要](../debugger/overview-of-visual-studio-graphics-diagnostics.md)  
 グラフィックス診断のワークフローおよびツールについて説明します。  
  
 [はじめに](../debugger/getting-started-with-visual-studio-graphics-diagnostics.md)  
 Visual Studio のグラフィックス診断をインストールする方法と、Direct3D アプリに対してグラフィックス診断の使用を開始する方法を説明します。  
  
 [Capturing Graphics Information](../debugger/capturing-graphics-information.md)  
 グラフィックス診断を使用してアプリのレンダリングの問題を調べるには、まず、アプリが DirectX を使用する方法に関する情報を記録する必要があります。 アプリが通常どおりに実行されているときの記録セッション中に関心があるフレームを "*キャプチャ*" (つまり、選択) します。 キャプチャには、フレームがレンダリングされる方法に関する詳細情報が含まれています。 キャプチャした情報をグラフィックス ログのドキュメントとして保存し、後で調べたり、チームの他のメンバーと共有したりできます。  
  
 [GPU 使用率](../debugger/gpu-usage.md)  
 グラフィックス診断を使用してアプリのプロファイリングを行うには、GPU 使用率ツールを使用します。 GPU 使用率ツールを、CPU 使用率など、他のプロファイリング ツールと連携して使用すると、アプリのパフォーマンスの問題を引き起こしている可能性のある CPU および GPU のアクティビティを、問題と関連付けることができます。  
  
 [グラフィックス ログ ドキュメント](../debugger/graphics-log-document.md)  
 記録したグラフィックス ログの調査を開始するには、グラフィックス ログのドキュメント ウィンドウを使用して、キャプチャしたフレームまたは特定のピクセルを選択し、影響を及ぼす "*イベント*" (つまり、DirectX API 呼び出し) を詳細に調べることができるようにします。  
  
 [フレーム分析](../debugger/graphics-frame-analysis.md)  
 フレームを選択したら、グラフィックス フレーム分析を使用してレンダリング パフォーマンスを調べて調整することができます。  
  
 [イベント一覧](../debugger/graphics-event-list.md)  
 フレームを選択した後、 **[グラフィックス イベント一覧]** を使用して、そのイベントを調べ、レンダリングの問題に関連しているかどうかを判別します。  
  
 [状態](../debugger/graphics-state.md)  
 [状態] ウィンドウは、現在のイベントの時点でアクティブになっているグラフィックスの状態を理解するために役立ちます。  
  
 [パイプライン ステージ](../debugger/graphics-pipeline-stages.md)  
 **[グラフィックス パイプライン ステージ]** ウィンドウで、現在選択しているイベントがグラフィックス パイプラインの各ステージで処理される方法を調査することにより、レンダリングの問題が最初に表示される場所を特定します。 パイプライン ステージの調査は、正しくない変換のためにオブジェクトが表示されない場合、または次のステージで期待される出力と一致しない出力が 1 つのステージで生成された場合に特に便利です。  
  
 [イベント呼び出し履歴](../debugger/graphics-event-call-stack.md)  
 **[グラフィックス イベント呼び出し履歴]** を使用して、現在選択しているイベントの呼び出し履歴を調べ、レンダリングの問題に関連するアプリ コードに移動します。  
  
 [ピクセル履歴](../debugger/graphics-pixel-history.md)  
 **[グラフィックス ピクセル履歴]** ウィンドウを使用して、現在選択しているピクセルがどのようにイベントに影響されるかを分析することにより、特定の種類のレンダリングの問題を発生させるイベントまたはイベントの組み合わせを特定できます。 ピクセル履歴は、ピクセル シェーダー出力が正しくないか、フレーム バッファーと不適切に組み合わされているためにオブジェクトが正しくレンダリングされない場合、または、オブジェクトのピクセルがフレーム バッファーに到達する前に破棄されているためにオブジェクトが表示されない場合に特に便利です。  
  
 [オブジェクト テーブル](../debugger/graphics-object-table.md)  
 **[グラフィックス オブジェクト テーブル]** を使用して、現在選択しているイベントに対して有効な特定の Direct3D オブジェクトおよびリソースのプロパティと内容を調べます。 オブジェクト テーブルを使用すると、イベントの発生時にアクティブであるグラフィックス デバイス コンテキストを特定し、定数バッファー、頂点バッファー、テクスチャなどのグラフィックス リソースの内容を調べることが容易になります。  
  
 [HLSL デバッガー](../debugger/hlsl-shader-debugger.md)  
 現在選択しているイベントおよびグラフィックス パイプライン ステージのシェーダー コードが動作する方法を調べるには、**HLSL デバッガー**を使用して、コードをステップ実行して、変数の内容を調べ、その他の一般的なデバッグ タスクを実行します。 また、結果がグラフィックス パイプラインによってさらに処理されるか、アプリによって再び読み取られるかに関係なく、HLSL デバッガーを使用して計算シェーダー コードを調べることができます。  
  
 [コマンド ライン キャプチャ ツール](../debugger/command-line-capture-tool.md)  
 コマンド ライン キャプチャ ツールを使用すると、Visual Studio またはプログラムによるキャプチャを使用せずに、グラフィックス情報を簡単にキャプチャして再生できます。 具体的には、オートメーションを行う場合や、テスト環境でコマンド ライン キャプチャ ツールを使用できます。  
  
 [例](../debugger/graphics-diagnostics-examples.md)  
 いくつかの例によって、複数のグラフィックス診断ツールを一緒に使用して、さまざまな種類のレンダリングの問題を診断する方法が示されています。  
  
## <a name="related-sections"></a>関連項目  
  
|Title|説明|  
|-----------|-----------------|  
|[Visual Studio でのデバッグ](../debugger/debugging-in-visual-studio.md)|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のデバッグ機能を紹介します。|  
|[DirectX のグラフィックスとゲーム](https://go.microsoft.com/fwlink/?LinkId=256498)|DirectX グラフィックスの手法を説明する文書を提供します。|

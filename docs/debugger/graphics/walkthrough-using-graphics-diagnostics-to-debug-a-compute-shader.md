---
title: 'チュートリアル: グラフィックス診断を使用して計算シェーダーをデバッグする |Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 69287456-644b-4aff-bd03-b1bbb2abb82a
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 62c92a8b24dd3d932eedfcb122b4da9294dd3418
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49949878"
---
# <a name="walkthrough-using-graphics-diagnostics-to-debug-a-compute-shader"></a>Walkthrough: Using Graphics Diagnostics to Debug a Compute Shader (チュートリアル: 計算シェーダーをデバッグするためのグラフィックス診断の使用)
このチュートリアルでは、Visual Studio のグラフィックス診断ツールを使用して、正しくない結果を生成する計算シェーダーを調査する方法を説明します。  
  
 このチュートリアルでは、次の作業について説明します。  
  
-   **[グラフィックス イベント一覧]** を使用して、問題の原因となる可能性がある部分を検索します。  
  
-   使用して、**グラフィックス イベント呼び出し履歴**、DirectCompute によって実行されるシェーダー計算を決定する`Dispatch`イベント。  
  
-   使用して、**グラフィックス パイプライン ステージ**ウィンドウと HLSL デバッガーを問題のソースでは、計算シェーダーを調査します。  
  
## <a name="scenario"></a>シナリオ  
 このシナリオでは、シミュレーション更新の計算量が最も多い部分を実行するために DirectCompute を使用する流体力学シミュレーションを記述しました。 アプリを実行したときに、データセットと UI は正しくレンダリングされますが、シミュレーションが想定どおりに動作しません。 グラフィックス診断を使用すると、グラフィックス ログに問題をキャプチャして、アプリのデバッグを実行できます。 問題は、アプリケーションでは次のように見えます。  
  
 ![シミュレートされた液体は正しく動作します。](media/gfx_diag_demo_compute_shader_fluid_problem.png "gfx_diag_demo_compute_shader_fluid_problem")  
  
 グラフィックスの問題をグラフィックス ログにキャプチャする方法については、「 [Capturing Graphics Information](capturing-graphics-information.md)」をご覧ください。  
  
## <a name="investigation"></a>調査  
 グラフィックス診断ツールを使用して、グラフィックス ログ ファイルを読み込み、キャプチャされたフレームを検査することができます。  
  
#### <a name="to-examine-a-frame-in-a-graphics-log"></a>グラフィックス ログのフレームを調査するには  
  
1. Visual Studio で、正しくないシミューレーション結果を表すフレームを含むグラフィックス ログを読み込みます。 新しいグラフィックス診断タブが Visual Studio に表示されます。 このタブの上部に、選択されたフレームのレンダー ターゲットが出力されます。 部分は、下、**フレーム一覧**、キャプチャされた各フレームのサムネイルが表示されます。  
  
2. **フレーム一覧**、正しくないシミュレーション動作を示すフレームを選択します。 DirectCompute イベントは Direct3D イベントと共にフレームごとにキャプチャされるため、エラーがレンダリング コードではなくシミュレーション コードに表示されたとしても、フレームを選択する必要があります。 このシナリオでは、グラフィックス ログのタブは次のように表示されます。  
  
    ![Visual Studio に使用される、グラフィックス ログ ドキュメント。](media/gfx_diag_demo_compute_shader_fluid_step_1.png "gfx_diag_demo_compute_shader_fluid_step_1")  
  
   問題を示しているフレームを選択したら、 **[グラフィックス イベント一覧]** を使用してそのフレームを診断できます。 **グラフィックス イベント一覧**DirectCompute 呼び出しと、アクティブなフレームの中に実行された Direct3D API 呼び出しごとにイベントが含まれています —、GPU で計算を実行したり、データセットまたは UI を表示するために、たとえば、API が呼び出します。 この場合、GPU で実行されたシミュレーションの一部を表す `Dispatch` イベントに注目します。  
  
#### <a name="to-find-the-dispatch-event-for-the-simulation-update"></a>シミュレーション更新の Dispatch イベントを見つけるには  
  
1. **グラフィックス診断**ツールバーで、選択**イベント一覧**を開く、**グラフィックス イベント一覧**ウィンドウ。  
  
2. 検査、**グラフィックス イベント一覧**のデータセットをレンダリングする描画イベント。 簡単にするには、次のように入力します。`Draw`で、**検索**の右上隅にあるボックス、**グラフィックス イベント一覧**ウィンドウ。 これによって一覧がフィルター処理され、タイトルに "Draw" を含むイベントのみが一覧に表示されます。 このシナリオでは、これらの描画イベントが発生したことがわかります。  
  
    ![イベント一覧&#40;EL&#41;描画イベントを示しています。](media/gfx_diag_demo_compute_shader_fluid_step_2.png "gfx_diag_demo_compute_shader_fluid_step_2")  
  
3. グラフィックス ログのドキュメント タブでレンダー ターゲットを観察しながら、各描画イベント間を移動します。  
  
4. レンダリングされたデータセットがレンダー ターゲットによって最初に表示されたら移動を停止します。 このシナリオでは、データセットは最初の描画イベントでレンダリングされます。 シミュレーションのエラーが表示されます。  
  
    ![これは、イベントのレンダリングに、シミュレーション データ セットを描画します。](media/gfx_diag_demo_compute_shader_fluid_step_3.png "gfx_diag_demo_compute_shader_fluid_step_3")  
  
5. ここで、**グラフィックス イベント一覧**の`Dispatch`シミュレーションを更新するイベントです。 シミュレーションはレンダリングされる前に更新される可能性が高いため、結果をレンダリングする描画イベントの前に発生する `Dispatch` イベントに最初に集中できます。 簡単にするには、変更、**検索**ボックス`Draw;Dispatch;CSSetShader(`します。 これによって一覧がフィルター処理され、描画イベントに加えて、`Dispatch` イベントおよび `CSSetShader` イベントも一覧に表示されます。 このシナリオでは、描画イベントの前にいつくかの `Dispatch` イベントが発生したことがわかります。  
  
    ![EL は描画、ディスパッチ、CSSetShader のイベント](media/gfx_diag_demo_compute_shader_fluid_step_4.png "gfx_diag_demo_compute_shader_fluid_step_4")  
  
   これで、多数になる可能性のある `Dispatch` イベントのうち、問題に該当するいくつかのイベントを特定できるので、これらのイベントを詳しく調べることができます。  
  
#### <a name="to-determine-which-compute-shader-a-dispatch-call-executes"></a>Dispatch 呼び出しが実行する計算シェーダーを確認するには  
  
1. **グラフィックス診断**ツールバーで、選択**イベント呼び出し履歴**を開く、**グラフィックス イベント呼び出し履歴**ウィンドウ。  
  
2. シミュレーションの結果をレンダリングする描画イベントから開始し、前の各 `CSSetShader` イベント間を後方に移動します。 次に、**グラフィックス イベント呼び出し履歴**ウィンドウ、呼び出しサイトに移動する最上位の関数を選択します。 呼び出しサイトでの最初のパラメーターを使用することができます、 [CSSetShader](/windows/desktop/api/d3d11/nf-d3d11-id3d11devicecontext-cssetshader)関数シェーダーは、次によって実行される計算を確認する呼び出し`Dispatch`イベント。  
  
   このシナリオでは、各フレームに `CSSetShader` イベントと `Dispatch` イベントのペアが 3 つあります。 最後から説明すると、3 番目のペアは統合ステップ (ここで、流体パーティクルが実際に動かされます) を、2 番目のペアはフォース計算ステップ (ここで、各パーティクルに影響を及ぼすフォースが計算されます) を、最初のペアは密度計算ステップをそれぞれ表します。  
  
#### <a name="to-debug-the-compute-shader"></a>計算シェーダーをデバッグするには  
  
1. **グラフィックス診断**ツールバーで、選択**パイプライン ステージ**を開く、**グラフィックス パイプライン ステージ**ウィンドウ。  
  
2. 3 番目の選択`Dispatch`イベント (描画イベントの直前にあるもの) し、、**グラフィックス パイプライン ステージ**ウィンドウで、**計算シェーダー**ステージで、選択**デバッグを開始**します。  
  
    ![EL. の 3 つ目のディスパッチ イベントを選択](media/gfx_diag_demo_compute_shader_fluid_step_6.png "gfx_diag_demo_compute_shader_fluid_step_6")  
  
    統合ステップを実行するシェーダーで HLSL デバッガーが開始されます。  
  
3. 統合ステップの計算シェーダー ソース コードを調べて、エラーの原因を探します。 グラフィックス診断を使用して、HLSL 計算シェーダー コードをデバッグする場合は、コードをステップ実行したり、ウォッチ ウィンドウなどの他の一般的なデバッグ ツールを使用したりできます。 このシナリオでは、統合ステップを実行する計算シェーダーにエラーがないことを確認します。  
  
    ![IntegrateCS 計算シェーダーをデバッグします。](media/gfx_diag_demo_compute_shader_fluid_step_7.png "gfx_diag_demo_compute_shader_fluid_step_7")  
  
4. 計算シェーダーのデバッグを停止する、**デバッグ**ツールバーで、選択**デバッグの停止** (キーボード: shift + f5)。  
  
5. 次に、2 番目の `Dispatch` イベントを選択し、前のステップで実行したように、計算シェーダーのデバッグを開始します。  
  
    ![2 番目のディスパッチ イベントを選択する、EL. で](media/gfx_diag_demo_compute_shader_fluid_step_8.png "gfx_diag_demo_compute_shader_fluid_step_8")  
  
    各流体パーティクルに対して作用するフォースを計算するシェーダーで HLSL デバッガーが開始されます。  
  
6. フォース計算ステップの計算シェーダー ソース コードを調べます。 このシナリオでは、エラーの原因がここにあることを確認します。  
  
    ![デバッグ、ForceCS&#95;単純な計算シェーダー。](media/gfx_diag_demo_compute_shader_fluid_step_9.png "gfx_diag_demo_compute_shader_fluid_step_9")  
  
   エラーが発生した場所を確認した後、デバッグを停止して、計算シェーダー ソース コードを変更すると、相互作用するパーティクル間の距離を正しく計算できます。 このシナリオでは、行 `float2 diff = N_position + P_position;` を `float2 diff = N_position - P_position;` に変更するだけです。  
  
   ![修正されたコンピューティング&#45;シェーダー コード。](media/gfx_diag_demo_compute_shader_fluid_step_10.png "gfx_diag_demo_compute_shader_fluid_step_10")  
  
   このシナリオでは、計算シェーダーが実行時にコンパイルされるため、変更を加えた後、アプリを再起動するだけで、変更がシミュレーションに及ぼす影響を確認できます。 アプリをリビルドする必要はありません。 アプリを実行すると、シミュレーションが正しく動作していることが確認できます。  
  
   ![シミュレートされた液体は正しく動作します。](media/gfx_diag_demo_compute_shader_fluid_resolution.png "gfx_diag_demo_compute_shader_fluid_resolution")
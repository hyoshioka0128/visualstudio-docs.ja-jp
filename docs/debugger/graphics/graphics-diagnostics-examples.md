---
title: グラフィックス診断例 | Microsoft Docs
description: Visual Studio グラフィックス診断を利用し、DirectX ベース アプリのレンダリング問題をデバッグする方法の例を紹介します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 45dd86b2-801e-4b07-a8c4-7bd25641d7f8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2ab1c01ef0f0b82f80a521929f90e90c6a4e4bc7
ms.sourcegitcommit: fcfd0fc7702a47c81832ea97cf721cca5173e930
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2020
ms.locfileid: "97727805"
---
# <a name="graphics-diagnostics-examples"></a>グラフィックス診断例
これらの例は、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] グラフィックス診断を使用して、DirectX ベースのアプリで発生するレンダリングの問題をデバッグする方法を示しています。

## <a name="capturing-graphics-information"></a>グラフィックス情報をキャプチャする
 グラフィックス診断を使用してアプリケーションのレンダリングの問題を診断するには、まず実行中のアプリケーションからグラフィックス情報を取得する必要があります。 グラフィックス情報は、ローカルに実行しているアプリケーション、またはリモート コンピューターや他のデバイス上で実行しているアプリケーションからキャプチャできます。 これらのチュートリアルでは、アプリケーションから手動で、またはプログラムを使用してグラフィックス情報をキャプチャする方法を示しています。

- [チュートリアル: グラフィックス情報をキャプチャする](walkthrough-capturing-graphics-information.md)

- [チュートリアル: プログラムによるグラフィックス情報のキャプチャ](walkthrough-capturing-graphics-information-programmatically.md)

## <a name="use-graphics-diagnostics-with-an-arm-based-device"></a>ARM ベースのデバイスでのグラフィックス診断の使用
 グラフィックス診断を使用すると、リモート デバッギングを使用することによって、ARM ベースのデバイス上で Direct3D アプリケーションをデバッグできます。 詳細については、「[方法: ARM デバイスでグラフィックス診断を使用する](graphics-diagnostics-examples.md)

## <a name="playing-back-graphics-information"></a>グラフィックス情報を再生する
 実行中のアプリからグラフィックス情報をキャプチャした後、キャプチャしたイベントを再生してレンダリングの問題を診断することができます。 再生するには、開発用コンピューターを使用するか、接続されているリモート コンピューターまたはリモート デバイスを使用できます。 詳細については、[グラフィックス診断再生マシンを変更する](how-to-change-the-graphics-diagnostics-playback-machine.md)」を参照してください。

## <a name="debugging-missing-objects"></a>不足しているオブジェクトをデバッグする
 1 つ以上のオブジェクトの不足は、グラフィックス開発者が経験する最も一般的なレンダリングの問題の 1 つです。 さまざまな種類のエラーが原因でオブジェクトが見かけ上消滅する可能性があるため、このような問題の診断は困難な場合があります。 オブジェクトが欠落する一般的な原因としては、デバイス状態の誤った構成、オブジェクトのジオメトリ変換の問題、グラフィックス パイプラインの誤った構成が挙げられます。

 これらのシナリオは、グラフィックス診断を使用して、オブジェクトが欠落している原因を特定し、責任のあるコードを見つけるための方法を示しています。

- [チュートリアル: デバイス状態によるオブジェクトの不足](walkthrough-missing-objects-due-to-device-state.md)

- [チュートリアル: 頂点の網かけによるオブジェクトの不足](walkthrough-missing-objects-due-to-vertex-shading.md)

- [チュートリアル: ピクセル シェーディングによるオブジェクトの不足](walkthrough-missing-objects-due-to-misconfigured-pipeline.md)

## <a name="debugging-rendering-errors"></a>レンダリングのエラーをデバッグする
 外観が正しくないオブジェクトは、グラフィックス開発者が遭遇するもう 1 つの一般的な問題です。 正しくない外観とその原因は、誤ったテクスチャのバインドなどの非常に明白なものから、シェーダー コードのバグやシェーダー間の予期しない相互作用などの非常にわかりにくいものにまで及ぶため、このような問題の診断は困難な場合があります。 いくつかの問題は、エラーの組み合わせにより起きる場合があります。

 次のシナリオは、グラフィックス診断を使用して、シェーダーの軽微なバグによって引き起こされる、それほどわかりにくくないレンダリングの問題を追跡する方法を示しています。

- [チュートリアル: 網かけによるレンダリング エラーのデバッグ](walkthrough-debugging-rendering-errors-due-to-shading.md)

## <a name="debugging-compute-shaders"></a>計算シェーダーをデバッグする
 グラフィックス診断を使用して、正しくない結果を生成する DirectCompute 計算シェーダー カーネルをデバッグできます。 DirectCompute を使用すると、GPU 計算能力を使用して、多数のデータ要素に対して並列に計算を実行できます。 問題の種類によっては、GPU を利用することにより、適切に最適化された CPU コードの何倍も高速に実行できる場合があります。 ただし、従来のデバッガーでは、GPU で実行されるコードを検出できません。 この種のコードをデバッグするには、多くの場合販売元固有の専用ツールが必要であり、Visual Studio と密接に統合されない場合があります。 計算シェーダーのデバッグを、さまざまな GPU にまたがってより一貫したものにするために、グラフィックス診断は、Direct3D レンダリング イベントに加えて DirectCompute の Dispatch イベントをキャプチャし、使い慣れたツールを使用して計算シェーダー コードの問題をデバッグできるようにします。

 計算シェーダーのバグによって引き起こされるシミュレーションの問題をデバッグする方法を示すシナリオについては、「[チュートリアル: 計算シェーダーをデバッグするためのグラフィックス診断の使用](walkthrough-using-graphics-diagnostics-to-debug-a-compute-shader.md)」を参照してください。
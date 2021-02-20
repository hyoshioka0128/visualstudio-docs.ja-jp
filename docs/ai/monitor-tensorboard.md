---
title: TensorBoard で監視する
description: Visual Studio を使用して TensorBoard でモデルのトレーニングの進行状況を視覚化する方法について説明します。
ms.custom: SEO-VS-2020
author: jillre
ms.author: jillfra
manager: jmartens
monikerRange: vs-2017
ms.date: 11/13/2017
ms.topic: how-to
ms.workload:
- multiple
ms.openlocfilehash: edb6fe17902ad84ec6d7a6e5b9929bd965e7c29b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99841394"
---
# <a name="monitor-with-tensorboard"></a>TensorBoard で監視する

TensorBoard では、モデルのトレーニングの進行状況を視覚化することができます。

1. プロジェクトを右クリックし、**[Run TensorBoard]\(TensorBoard の実行\)** をクリックして、TensorBoard の出力ログのディレクトリを選択します。

    ![Visual Studio ソリューション エクスプローラーのスクリーンショット。MNIST プロジェクトが選択されています。 コンテキスト メニューが開いています。[Run TensorBoard]\(TensorBoard の実行\) コマンドが選択されています。](media/monitor-tensorboard/run-tensorboard.png)

2. 時間の経過に伴いエラーが減少していることに注目してください。これは品質が改善していることを意味します。

    ![メイン TensorBoard ウィンドウのスクリーンショット。TensorBoard ログのデータでグラフを作成しています。](media/monitor-tensorboard/tensorboard.png)

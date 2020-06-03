---
title: Azure Batch AI でモデルをトレーニングするためのジョブを送信する
description: モデル クラウドをトレーニングする
keywords: AI, Visual Studio, モデルのトレーニング, クラウド
author: jillre
ms.author: jillfra
manager: jillfra
monikerRange: vs-2017
ms.date: 11/13/2017
ms.topic: conceptual
ms.workload:
- azure
ms.openlocfilehash: 083b2cb191d627ced936ead6a90b363970a9e7e0
ms.sourcegitcommit: 9c1cecaff4d9955276eee7865b78d47679dd1e2a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/03/2020
ms.locfileid: "80638772"
---
# <a name="train-ai-models-in-azure-batch-ai"></a>Azure Batch AI での AI モデルのトレーニング

Batch AI は、データ サイエンティストおよび AI 研究者が、Azure 仮想マシン (GPU がサポートされた VM など) のクラスター上で AI やその他の Machine Learning モデルをトレーニングするための管理対象サービスです。 目的のジョブの要件を記述すると (入力を検索し、出力を格納)、Batch AI が残りの部分を処理します。 Azure Batch AI の詳細については、[こちら](/azure/batch-ai/overview)を参照してください。

Azure Batch AI は、Visual Studio Tools for AI に統合されているため、Azure にてトレーニング モデルを動的にスケールアウトすることができます。  [Visual Studio Tools for AI をインストール](installation.md)すれば、Azure Machine Learning サンプル ギャラリーにある事前に定義されたレシピを使用して新しい Python プロジェクトを容易に作成することができます。

1. Visual Studio を起動します。 **[AI Tools]\(AI Tools\)** メニューを開き、 **[Select Cluster]\(クラスターの選択\)** を選択して、**サーバー エクスプローラー**を開きます

    ![クラスターの選択](media/train-model/select-cluster.png)

2. **[AI Tools]\(AI Tools\)** を選択します。 所有している Batch AI リソースが自動的に検出され、サーバー エクスプローラーに表示されます。

    ![サンプル ギャラリー](media/train-model/batchai.png)

3. **[表示] > [チーム エクスプローラー]** の順に選択し、 **[チーム エクスプローラー]** ウィンドウを開きます。ここでは、GitHub または Azure DevOps に接続したり、リポジトリを複製したりすることができます。

    ![Azure DevOps、GitHub、リポジトリの複製を示すチーム エクスプローラー ウィンドウ](media/train-model/team-explorer-devops.png)

4. **[Local Git Repositories]\(ローカル Git リポジトリ\)** の下の [URL] フィールドに、`https://github.com/Microsoft/samples-for-ai` と入力し、複製されたファイル用のフォルダーを入力し、 **[複製]** を選択します。

    > [!Tip]
    > チーム エクスプローラーで指定したフォルダーは、複製されたファイルを受け取る特定のフォルダーです。 `git clone` コマンドとは異なり、チーム エクスプローラーで複製を作成しても、リポジトリの名前のサブフォルダーは自動作成されません。

5. 複製が完了したら、 **[ファイル]、[ソリューションを開く]、[プロジェクト/ソリューション]** の順にクリックします。

    ![サンプル ギャラリー](media/train-model/open-solution.png)

6. リポジトリを複製したディレクトリで、**samples-for-ai\TensorFlowExamples\TensorFlowExamples.sln** を開きます。

    ![サンプル ギャラリー](media/train-model/tensorflowexamples.png)

7. MNIST プロジェクトを**スタートアップ プロジェクト**として設定します

    ![サンプル ギャラリー](media/train-model/mnist-startup.png)

8. <strong>**MNIST プロジェクト**を右クリックし、 **[ジョブの送信]** をクリックします</strong>

    ![サンプル ギャラリー](media/train-model/submit-job.png)
9. 目的の **Azure Batch AI** クラスターを選択し、 **[インポート]** をクリックします。 `AzureBatchAI_TF_MNIST.json` ファイルを選択します。これにより、使用する Docker イメージなど、いくつかの既定値がすぐに入力されます。 **[送信]** をクリックします。

    ![サンプル ギャラリー](media/train-model/submit-batch.png)

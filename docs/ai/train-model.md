---
title: モデルをトレーニングするためのジョブを送信する
description: Azure Batch AI でモデルをトレーニングするためのジョブを送信する
ms.custom: SEO-VS-2020
keywords: AI, Visual Studio, モデルのトレーニング, クラウド
author: jillre
ms.author: jillfra
manager: jmartens
monikerRange: vs-2017
ms.date: 11/13/2017
ms.topic: how-to
ms.workload:
- azure
ms.openlocfilehash: e1bb1d0bde1b564fe9a35f3527c7b3803c7e9d78
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99841303"
---
# <a name="train-ai-models-in-azure-batch-ai"></a>Azure Batch AI での AI モデルのトレーニング

Batch AI は、データ サイエンティストおよび AI 研究者が、Azure 仮想マシン (GPU がサポートされた VM など) のクラスター上で AI やその他の Machine Learning モデルをトレーニングするための管理対象サービスです。 目的のジョブの要件を記述すると (入力を検索し、出力を格納)、Batch AI が残りの部分を処理します。 Azure Batch AI の詳細については、[こちら](/azure/batch-ai/overview)を参照してください。

Azure Batch AI は、Visual Studio Tools for AI に統合されているため、Azure にてトレーニング モデルを動的にスケールアウトすることができます。  [Visual Studio Tools for AI をインストール](installation.md)すれば、Azure Machine Learning サンプル ギャラリーにある事前に定義されたレシピを使用して新しい Python プロジェクトを容易に作成することができます。

1. Visual Studio を起動します。 **[AI Tools]\(AI Tools\)** メニューを開き、 **[Select Cluster]\(クラスターの選択\)** を選択して、**サーバー エクスプローラー** を開きます

    ![クラスターの選択](media/train-model/select-cluster.png)

2. **[AI Tools]\(AI Tools\)** を選択します。 所有している Batch AI リソースが自動的に検出され、サーバー エクスプローラーに表示されます。

    ![サーバー エクスプローラーで AI Tools のフォルダー ツリーを展開した画面のスクリーンショット。Azure Batch AI と Azure Machine Learning のサブフォルダーが展開されています。](media/train-model/batchai.png)

3. **[表示] > [チーム エクスプローラー]** の順に選択し、 **[チーム エクスプローラー]** ウィンドウを開きます。ここでは、GitHub または Azure DevOps に接続したり、リポジトリを複製したりすることができます。

    ![Azure DevOps、GitHub、リポジトリの複製を示すチーム エクスプローラー ウィンドウ](media/train-model/team-explorer-devops.png)

4. **[Local Git Repositories]\(ローカル Git リポジトリ\)** の下の [URL] フィールドに、`https://github.com/Microsoft/samples-for-ai` と入力し、複製されたファイル用のフォルダーを入力し、 **[複製]** を選択します。

    > [!Tip]
    > チーム エクスプローラーで指定したフォルダーは、複製されたファイルを受け取る特定のフォルダーです。 `git clone` コマンドとは異なり、チーム エクスプローラーで複製を作成しても、リポジトリの名前のサブフォルダーは自動作成されません。

5. 複製が完了したら、 **[ファイル]、[ソリューションを開く]、[プロジェクト/ソリューション]** の順にクリックします。

    ![サーバー エクスプローラーのファイル メニューの一部を示すスクリーンショット。[開く] コマンドとコンテキスト メニューの [プロジェクト/ソリューション] が選択されています。](media/train-model/open-solution.png)

6. リポジトリを複製したディレクトリで、**samples-for-ai\TensorFlowExamples\TensorFlowExamples.sln** を開きます。

    ![samples-for-ai リポジトリで TensorflowExamples フォルダーのコンテンツの一覧にあるソリューション ファイル TensorflowExamples.sln を示すスクリーンショット。](media/train-model/tensorflowexamples.png)

7. MNIST プロジェクトを **スタートアップ プロジェクト** として設定します

    ![ソリューション エクスプローラーで MNIST プロジェクトのコンテキスト メニューで選択されている [スタートアップ プロジェクトに設定] のスクリーンショット。](media/train-model/mnist-startup.png)

8. <strong>**MNIST プロジェクト** を右クリックし、 **[ジョブの送信]** をクリックします</strong>

    ![ソリューション エクスプローラーで MNIST プロジェクトのコンテキスト メニューで選択されている [ジョブの送信] のスクリーンショット。](media/train-model/submit-job.png)
9. 目的の **Azure Batch AI** クラスターを選択し、 **[インポート]** をクリックします。 `AzureBatchAI_TF_MNIST.json` ファイルを選択します。これにより、使用する Docker イメージなど、いくつかの既定値がすぐに入力されます。 **[送信]** をクリックします。

    ![[ジョブの送信] ダイアログのスクリーンショット。クラスターの使用、スタートアップ スクリプト、ジョブ名、画像名、StdOutErr パス プレフィックス、CLI パラメーターに値が入力されています。](media/train-model/submit-batch.png)

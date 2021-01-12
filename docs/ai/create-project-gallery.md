---
title: プロジェクトを作成する
description: Azure Machine Learning ギャラリーのサンプルを使ってプロジェクトを作成します
keywords: AI, Visual Studio, Azure Machine Learning
author: jillre
ms.author: jillfra
manager: jillfra
monikerRange: vs-2017
ms.date: 11/13/2017
ms.topic: how-to
ms.workload:
- multiple
ms.openlocfilehash: a6813e834af00330b4018f16d4a19be945be2be9
ms.sourcegitcommit: fcfd0fc7702a47c81832ea97cf721cca5173e930
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2020
ms.locfileid: "97726645"
---
# <a name="create-an-ai-project-from-the-azure-machine-learning-gallery-in-visual-studio"></a>Visual Studio で Azure Machine Learning ギャラリーから AI プロジェクトを作成する

Azure Machine Learning は Visual Studio Tools for AI と統合されています。 これを使って、Azure 仮想マシンや Spark クラスターなどのリモート マシン ターゲットに Machine Learning ジョブを送信できます。 

[Visual Studio Tools for AI をインストール](installation.md)すれば、Azure Machine Learning サンプル ギャラリーにある事前に定義されたレシピを使用して新しい Python プロジェクトを容易に作成することができます。

> [!NOTE]
> Azure Machine Learning ワークベンチをインストールする必要があります。 

1. Visual Studio を起動します。 **[AI Tools]\(AI Tools\)** メニューを開き、 **[Select Cluster]\(クラスターの選択\)** を選択して、**サーバー エクスプローラー** を開きます

    ![クラスターの選択](media/create-project-gallery/select-cluster.png)

2. サーバー エクスプローラーで **[Azure Machine Learning]** ノードを右クリックし、 **[ログイン]** を選択して指示に従い、Azure Machine Learning サブスクリプションにサインインします。

    ![ログイン](media/create-project-gallery/azureml-login.png)

3. **[AI Tools]\(AI Tools\)、[Azure Machine Learning Sample Gallery]\(Azure Machine Learning サンプル ギャラリー\)** の順に選びます。

    ![サンプル ギャラリー](media/create-project-gallery/gallery.png)

4. このクイック スタートでは "**MNIST using TensorFlow**" サンプルを選び、 **[インストール]** をクリックします。 次の内容を指定します。

   - **リソース グループ**:メタデータを格納する Azure リソース グループ
   - **アカウント**:Azure Machine Learning の実験アカウント
   - **ワークスペース**:Azure Machine Learning のワークスペース
   - **プロジェクトの種類**:機械学習のフレームワーク。 この例では、 **[TensorFlow]** を選びます。
   - **ソリューションに追加**: 現在の Visual Studio ソリューションに追加するか、新しいソリューションを作成して開くかを指定します。
   - **プロジェクトのパス**:コードを保存する場所
   - **プロジェクト名**:「**TensorFlowMNIST**」と入力します。

   ![Python アプリケーション テンプレートを使用した結果のプロジェクト](media/create-project-gallery/new-AzureSampleProject.png)

5. Visual Studio によって、プロジェクト ファイル (ディスク上の `.pyproj` ファイル) と、サンプルで定義されている他のファイルが作成されます。 "MNIST" テンプレートでは、プロジェクトに複数のファイルが含まれます。

    ![Visual Studio ソリューション エクスプローラーのスクリーンショット。TensorFlowMNIST プロジェクトのファイルが表示されています。 tf_mnist.py のコードがメイン ウィンドウに表示されています。](media/create-project-gallery/azml-mnist.png)

6. Azure Machine Learning にジョブを送信します。

    ![Visual Studio ソリューション エクスプローラーのスクリーンショット。TensorFlowMNIST プロジェクトのコンテキスト メニューが表示されています。[ジョブの送信...] が選択されています。](media/create-project-gallery/submit-azml.png)

7. Docker コンテナーまたはローカル コンピューターで実行します

    ![[ジョブの送信] ダイアログのスクリーンショット。[クラスターの使用] が "azureml:/local" に、[起動スクリプト] が "tf_mnist.py" に設定されています。](media/create-project-gallery/azml-local.png)

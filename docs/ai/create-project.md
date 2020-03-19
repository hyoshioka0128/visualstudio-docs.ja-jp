---
title: テンプレートから AI プロジェクトを作成する
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 11/13/2017
ms.topic: conceptual
ms.workload:
- multiple
ms.openlocfilehash: 0b537d80b8db9150c6804aff2ee3de0e6c879bb9
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "62546727"
---
# <a name="create-an-ai-project-from-a-template-in-visual-studio"></a>Visual Studio のテンプレートから AI プロジェクトを作成する

[Visual Studio Tools for AI をインストール](installation.md)すれば、さまざまなテンプレートを使って新しい AI プロジェクトを簡単に作成できます。

1. Visual Studio を起動します。

2. **[ファイル]、[新規]、[プロジェクト]** (Ctrl + Shift + N) の順に選択します。 **[新しいプロジェクト]** ダイアログで、"**AI Tools**" を検索し、希望のテンプレートを選択します。 テンプレートを選択すると、テンプレートの簡単な説明が表示されます。

    ![VS2017 Python テンプレートの [新しいプロジェクト] ダイアログ](media/create-project/new-ai-project.png)

3. このクイック スタートでは、"**TensorFlow アプリケーション**" テンプレートを選択し、("MNIST" などの) プロジェクト名を付け、場所を指定し、 **[OK]** を選択します。

4. Visual Studio によってプロジェクト ファイル (ディスク上に 1 つの `.pyproj` ファイル) と、テンプレートに記述されているその他のファイルが作成されます。 "TensorFlow アプリケーション" テンプレートでは、プロジェクトと同じ名前の 1 つのファイルがプロジェクトに含まれます。 このファイルは、既定で Visual Studio エディタで開きます。

    ![Python アプリケーション テンプレートを使用した結果のプロジェクト](media/create-project/new-tensorflowapp.png)

5. TensorFlow、numpy、sys、os を含むいくつかのライブラリがコードで既にインポートされていることに注目してください。 また、いくつかの入力変数が指定され準備ができているアプリケーションが開始されています。これにより、入力トレーニング データ、出力モデル、ログ ファイルの場所を簡単に切り替えることができます。 これらのパラメーターは、複数の計算コンテキスト (つまり、Azure ファイル共有とは異なる、ローカル開発ボックスのディレクトリ) にジョブを送信する場合に役立ちます。

6. プロジェクトではいくつかのプロパティも作成されています。コマンドライン引数をこれらの入力パラメーターに自動的に渡すことで、アプリのデバッグが簡単になります。 プロジェクトを**右クリック**してから **[プロパティ]** を選択します。

    ![プロパティ](media/create-project/project-properties.png)

7. **[デバッグ]** タブをクリックして、自動的に追加された [スクリプト引数] を表示します。 必要に応じて、それらを入力データが配置される場所や出力の格納先に変更することができます。

    ![プロパティ](media/create-project//project-properties_1.png)

8. Ctrl + F5 キーを押すか、メニューを **[デバッグ]、[デバッグなしで開始]** の順に選択して、プログラムを実行します。 結果は、コンソール ウィンドウに表示されます。

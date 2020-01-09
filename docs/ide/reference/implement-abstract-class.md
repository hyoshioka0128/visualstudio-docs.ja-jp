---
title: 抽象クラスの実装
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 6fcfdc06a055df28159f9d1ddc440aaf113f3264
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75568907"
---
# <a name="implement-an-abstract-class-in-visual-studio"></a>Visual Studio で抽象クラスを実装する

このコード生成は以下に適用されます。

- C#

- Visual Basic

**概要:** 抽象クラスを実装するために必要なコードをすぐに生成できます。

**条件:** 抽象クラスから継承したいとき。

**理由:** すべての抽象メンバーは 1 つずつ手動で実装できますが、この機能ではすべてのメソッド シグネチャが自動的に生成されます。

## <a name="how-to"></a>方法

1. 抽象クラスを継承しているが、必要なすべてのメンバーを実装していないことを示す赤い波線がある行に、カーソルを置きます。

   - C#:

       ![強調表示された C# のコード](media/abstract-highlight-cs.png)

   - Visual Basic:

       ![強調表示された VB のコード](media/abstract-highlight-vb.png)

2. 次に、以下のいずれかを実行します。

   - **キーボード**
      - 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。
   - **マウス**
      - 右クリックして **[クイック アクションとリファクタリング]** メニューを選択します。
      - 赤い波線をポイントし、表示された ![エラー電球](media/error-bulb.png) アイコンをクリックします。
      - テキスト カーソルが既に赤い波線の行にある場合は、左余白に表示されている ![エラー電球](media/error-bulb.png) アイコンをクリックします。

   ![クラス実装のプレビュー](media/abstract-preview-cs.png)

3. ドロップダウン メニューから **[抽象クラスの実装]** を選びます。

   > [!TIP]
   > - プレビュー ウィンドウの下部にある **[変更のプレビュー]** リンクを使うと、選択する前に、行われる[すべての変更を確認する](../../ide/preview-changes.md)ことができます。
   > - 抽象クラスから継承する複数のクラスにまたがる適切なメソッド シグネチャを作成するには、プレビュー ウィンドウの下部にある **[ドキュメント]** 、 **[プロジェクト]** 、 **[ソリューション]** の各リンクを使います。

   抽象メソッドのシグネチャが作成され、実装する準備が整います。

   - C#:

       ![クラス実装の結果 C#](media/abstract-result-cs.png)

   - Visual Basic:

       ![クラス実装の結果 VB](media/abstract-result-vb.png)

## <a name="see-also"></a>関連項目

- [コード生成](../code-generation-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)

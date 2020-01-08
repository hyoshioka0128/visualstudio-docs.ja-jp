---
title: インターフェイスの実装
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 7d420bd0d42e89476696966f7eda94a19893fc23
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75595554"
---
# <a name="implement-an-interface-in-visual-studio"></a>Visual Studio でインターフェイスを実装する

このコード生成は以下に適用されます。

- C#

- Visual Basic

**概要:** インターフェイスを実装するために必要なコードをすぐに生成できます。

**条件:** インターフェイスから継承したいとき。

**理由:** すべてのインターフェイスは 1 つずつ手動で実装できますが、この機能ではすべてのメソッド シグネチャが自動的に生成されます。

## <a name="how-to"></a>方法

1. インターフェイスを参照しているが、必要なすべてのメンバーを実装していないことを示す赤い波線がある行にカーソルを置きます。

   - C#:

       ![強調表示された C# のコード](media/interface-highlight-cs.png)

   - Visual Basic:

       ![強調表示された VB のコード](media/interface-highlight-vb.png)

2. 次に、以下のいずれかを実行します。

   - **キーボード**
      - 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。
   - **マウス**
      - 右クリックして **[クイック アクションとリファクタリング]** メニューを選択します。
      - 赤い波線をポイントし、表示された ![エラー電球](media/error-bulb.png) アイコンをクリックします。
      - テキスト カーソルが既に赤い波線の行にある場合は、左余白に表示されている ![エラー電球](media/error-bulb.png) アイコンをクリックします。

3. ドロップダウン メニューから **[インターフェイスの実装]** を選択します。

   ![インターフェイス実装のプレビュー](media/interface-preview-cs.png)

   > [!TIP]
   > - プレビュー ウィンドウの下部にある **[変更のプレビュー]** リンクを使うと、選択する前に、行われる[すべての変更を確認する](../../ide/preview-changes.md)ことができます。
   > - インターフェイスを実装する複数のクラスにまたがる適切なメソッド シグネチャを作成するには、プレビュー ウィンドウの下部にある **[ドキュメント]** 、 **[プロジェクト]** 、 **[ソリューション]** の各リンクを使います。

   インターフェイスのメソッド シグネチャが作成され、実装する準備が整います。

   - C#:

       ![インターフェイスの実装の結果 (C#)](media/interface-result-cs.png)

   - Visual Basic:

       ![インターフェイスの実装の結果 (VB)](media/interface-result-vb.png)

   > [!TIP]
   > (C# のみ) **[インターフェイスを明示的に実装]** オプションを使うと、生成される各メソッドの先頭にインターフェイス名を付けて、名前の衝突を避けることができます。
   >
   > ![インターフェイスの明示的な実装の結果](media/interface-explicitresult-cs.png);

## <a name="see-also"></a>関連項目

- [コード生成](../code-generation-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)

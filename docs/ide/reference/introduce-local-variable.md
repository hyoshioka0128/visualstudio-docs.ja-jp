---
title: ローカル変数の導入
description: ローカル変数を生成して、既存の式を置き換えます。 式を選択し、右クリックして [クイックアクションとリファクタリング] メニューを選択し、['expression' のすべての発生に対してローカルを導入します] を選択します。
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 564ba133074af3749bd909f1b0a7fe32822f5d75
ms.sourcegitcommit: d526af3642163180e0cc3e1e73b0a00f02542683
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2020
ms.locfileid: "97833261"
---
# <a name="introduce-a-local-variable-in-visual-studio"></a>Visual Studio でローカル変数を導入する

このコード生成は以下に適用されます。

- C#

- Visual Basic

**機能:** 既存の式を置換するローカル変数をすぐに生成できます。

**条件:** ローカル変数内で使用されていれば、後で簡単に再利用できるコードがあるとき。

**理由:** コードは複数回コピーして貼り付け、さまざまな場所で使用できるが、一度の実行で、結果を 1 つのローカル変数に格納し、そのローカル変数を全体で使用する方が良いため。

## <a name="how-to"></a>操作方法

1. 新しいローカル変数に割り当てる式を強調表示します。

   - C#:

       ![強調表示された C# のコード](media/local-highlight-cs.png)

   - Visual Basic:

       ![強調表示された VB のコード](media/local-highlight-vb.png)

2. 次に、以下のいずれかを実行します。

   - **[キーボード]**
      - 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。
   - **マウス**
      - 右クリックして **[クイック アクションとリファクタリング]** メニューを選択します。
      - テキスト カーソルが既にクラスの空の行にある場合は、左余白に表示されている ![[クイック アクションとリファクタリング] メニューの左余白に表示されるねじ回しアイコンのスクリーンショット。](media/screwdriver.png) アイコンをクリックします。

   ![ローカル導入のプレビュー](media/local-preview-cs.png)

3. ドロップダウン メニューから **['<式>' のすべての発生に対してローカルを導入します]** を選択します。

   > [!TIP]
   > プレビュー ウィンドウの下部にある **[変更のプレビュー]** リンクを使うと、選択する前に、行われる [すべての変更を確認する](../../ide/preview-changes.md)ことができます。

   ローカル変数と、その使用法から推論された型が作成されます。 新しいローカル変数に新しい名前を付けます。

   - C#:

       ![インターフェイスの実装の結果 (C#)](media/local-result-cs.png)

   - Visual Basic:

       ![インターフェイスの実装の結果 (VB)](media/local-result-vb.png)

   > [!NOTE]
   > **[...のすべての発生に対して]** メニュー オプションを使うと、明示的に強調表示したインスタンスだけでなく、選択した式のすべてのインスタンスを置換できます。

## <a name="see-also"></a>参照

- [コード生成](../code-generation-in-visual-studio.md)
- [変更のプレビュー](../../ide/preview-changes.md)

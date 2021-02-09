---
title: 'ワークフローデザイナー-方法: 式エディターを使用する'
description: 式エディターが、式を入力および評価するために多くのワークフローアクティビティで使用できるワークフローデザイナーコントロールであることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- System.Activities.Presentation.View.ExpressionTextBox.UI
ms.assetid: b5f961dd-6dda-41a9-9cae-0383d479ef3d
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 192418439bc25e6ac1b969483c0c48a030caa024
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894076"
---
# <a name="how-to-use-the-expression-editor"></a>式エディターを使用する方法

式エディターは、式を入力および評価するために多くのワークフローアクティビティで使用されるワークフローデザイナーコントロールです。 式エディターでは、IntelliSense、色付け、ParamInfo、エラーの波線など、豊富な機能を備えた IDE 編集エクスペリエンスが提供されます。 入力した式は、コンパイラによって検証されます。 式が無効な場合は、エラー アイコンが表示されます。 エディターは、[ **式エディター** ] ダイアログボックスとして開くこともできます。

式は、引数またはプロパティにバインドされたリテラル値または Visual Basic コードです。 これらには、新しい値を生成するために操作と結合される値要素 (変数、定数、リテラル、プロパティなど) が含まれています。 アプリケーションが C# を使用したプログラムに含まれている場合でも、式の記述には VB.NET 構文が使用されます。 つまり、大文字小文字は区別されません。比較は、1つの等号 ("= =" ではなく "=") を使用して実行されます。ブール演算子は、記号 "&&" および "| |" ではなく "and" と "or" で、 **null** ではなく、**何も** 使用されません。 Visual Basic の式と演算子の詳細およびいくつかのサンプルについては、「 [Visual Basic の演算子と式](/previous-versions/visualstudio/visual-studio-2010/a1w3te48(v=vs.100))」を参照してください。

**式エディター** は次のように動作します。

- フォーカスがない場合、式エディターは通常の TextBlock コントロールと同様の外観になります。

- フォーカスが式エディターに移ると、式エディター コントロールと同様の外観と動作になります。 フォーカスが失われると、式エディターは通常の TextBlock のようになります。

- 再ホストされたワークフロー デザイナーで式エディターにフォーカスを設定した場合は、TextBox と同じように動作します。 再ホストされたワークフロー デザイナーでフォーカスが失われると、式エディターは、通常の TextBlock と同様の外観に戻ります。

> [!NOTE]
> 式エディターの IntelliSense は、Visual Studio 内でのみ使用できます。 Visual Studio と再ホストされるシナリオでは、入力後に式が検証され、式が無効な場合は式エディターにエラーアイコンが表示されます。

## <a name="use-the-expression-editor"></a>式エディターを使用する

1. Visual Studio で、新規または既存のワークフロープロジェクトを開きます。

2. ワークフローに <xref:System.Activities.Statements.Assign> などのアクティビティを追加します。

    > [!NOTE]
    > 式エディターを使用できるワークフロー アクティビティは複数あります。 変数デザイナー、引数デザイナー、および動的引数デザイナーには、式 TextBlock も表示されます。 ここでは、例として <xref:System.Activities.Statements.Assign> アクティビティを使用しています。

3. <xref:System.Activities.Statements.Assign> アクティビティのアクティビティ デザイナーで、左側の式エディターをクリックします。

     灰色のウォーターマーク文字列 **\<To>** と **\<Enter a VB Expression>** は、アクティビティの式エディターの既定のテキスト文字列です <xref:System.Activities.Statements.Assign> 。

4. 式を入力します。 文字列を入力する場合は、文字列を引用符で囲みます。 式の引数を変数にバインドする場合は、引用符を省略してください。

     完了したら、式エディターの外部の領域を選択して、デザイナーの別の部分にフォーカスを移動します。 フォーカスを移動すると、前に説明したように、コンパイラによって式が検証されます。

     式を入力または編集する別の方法として、プロパティグリッドでプロパティ名の横にある省略記号をクリックする方法もあります。 省略記号を選択すると、 **式エディター** がダイアログボックスとして開きます。

## <a name="see-also"></a>関連項目

- <xref:System.Activities.Presentation.View.ExpressionTextBox>

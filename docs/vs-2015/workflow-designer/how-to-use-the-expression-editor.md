---
title: '方法: 式エディターを使用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Presentation.View.ExpressionTextBox.UI
ms.assetid: b5f961dd-6dda-41a9-9cae-0383d479ef3d
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 54099bc5c0f249cdb3697715d153a94a596ac344
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75849231"
---
# <a name="how-to-use-the-expression-editor"></a>式エディターを使用する方法
式エディターは、式を入力および評価する手段として、多くのワークフロー アクティビティで使用される[!INCLUDE[wfd1](../includes/wfd1-md.md)] コントロールです。 式エディターには、IntelliSense、色付け、パラメーター情報、エラーを示す波線などの、本格的な IDE 編集機能が用意されています。 入力した式はコンパイラによって検証されます。 式が無効な場合は、エラー アイコンが表示されます。 エディターは、[ **式エディター** ] ダイアログボックスとして開くこともできます。

 式は、引数またはプロパティにバインドされたリテラル値または [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] コードです。 式には、新しい値を生成するための操作と組み合わされた値要素 (変数、定数、リテラル、プロパティなど) が含まれます。 アプリケーションが C# を使用したプログラムに含まれている場合でも、式の記述には VB.NET 構文が使用されます。 つまり、大文字小文字は区別されません。比較は、("= =") ではなく1つの等号 ("=") を使用して実行されます。ブール演算子は、記号 "&&" および "&#124;&#124;" ではなく "and" と "or" で、 **null**の代わり**には使用**されません。 の式と演算子、およびいくつかのサンプルについては [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 、「 [Visual Basic の演算子と式](https://msdn.microsoft.com/library/a1w3te48(VS.100).aspx)」を参照してください。

 **式エディター**は次のように動作します。

- フォーカスがない場合、式エディターは通常の TextBlock コントロールと同様の外観になります。

- フォーカスが式エディターに移ると、式エディター コントロールと同様の外観と動作になります。 フォーカスが失われると、通常の TextBlock と同様の外観に戻ります。

- 再ホストされたワークフロー デザイナーで式エディターにフォーカスを設定した場合は、TextBox と同じように動作します。 再ホストされたワークフロー デザイナーでフォーカスが失われると、式エディターは、通常の TextBlock と同様の外観に戻ります。

> [!NOTE]
> 式エディター用の IntelliSense は、[!INCLUDE[vs2010](../includes/vs2010-md.md)] 内でのみ使用できます。 [!INCLUDE[vs2010](../includes/vs2010-md.md)] および再ホストのシナリオではいずれも、入力した式がコンパイラによって検証され、式が無効な場合は、式エディターにエラー アイコンが表示されます。

### <a name="using-the-expression-editor"></a>式エディターの使用

1. [!INCLUDE[vs2010](../includes/vs2010-md.md)] で新規または既存のワークフロー プロジェクトを開きます。

2. ワークフローに <xref:System.Activities.Statements.Assign> などのアクティビティを追加します。

    > [!NOTE]
    > 式エディターを使用できるワークフロー アクティビティは複数あります。 変数デザイナー、引数デザイナー、および動的引数デザイナーには、式 TextBlock も表示されます。 ここでは、例として <xref:System.Activities.Statements.Assign> アクティビティを使用しています。

3. <xref:System.Activities.Statements.Assign> アクティビティのアクティビティ デザイナーで、左側の式エディターをクリックします。

     灰色のウォーターマークの文字列 **\<To>** と **\<Enter a VB Expression>** は、アクティビティの式エディターの既定のテキスト文字列です <xref:System.Activities.Statements.Assign> 。

4. 式を入力します。 文字列を入力する場合は、文字列を引用符で囲みます。 式の引数を変数にバインドする場合は、引用符を省略してください。

     式を入力し終えたら、式エディターの外部を選択して、デザイナーの他の部分にフォーカスを移動させます。 この操作により、既に説明したように、コンパイラによって式が検証されます。

     式を入力または編集する方法として、プロパティ グリッドのプロパティ名の横にある省略記号をクリックするという方法もあります。 これにより、[ **式エディター** ] ダイアログボックスが開きます。

## <a name="see-also"></a>参照
 <xref:System.Activities.Presentation.View.ExpressionTextBox>

---
title: '手順 2: Random オブジェクトおよびアイコンのリストの追加'
ms.date: 11/04/2016
ms.topic: tutorial
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.assetid: 95faea28-eddc-4cfa-95fb-3b34b5a976d7
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1f4731778ebb3acbdc3bb7d9b5827c1015541d98
ms.sourcegitcommit: 2ae2436dc3484b9dfa10e0483afba1e5a02a52eb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2020
ms.locfileid: "77579423"
---
# <a name="step-2-add-a-random-object-and-a-list-of-icons"></a>手順 2: Random オブジェクトおよびアイコンのリストの追加

このステップでは、絵合わせゲームに使用する一連のアイコンを作成します。 各アイコンは、フォーム上の TableLayoutPanel 内の 2 つのランダムなセルに追加されます。 そのために、2 つの `new` ステートメントを使用して 2 つのオブジェクトを作成します。 1 つ目は、計算クイズ ゲームで使用したオブジェクトに似た <xref:System.Random> オブジェクトです。 このコードでは、TableLayoutPanel 内のセルをランダムに選択するために使用します。 2 つ目は、初めての使用になるかもしれませんが、<xref:System.Collections.Generic.List%601> オブジェクトです。ランダムに選択されたアイコンを格納するために使用します。

## <a name="to-add-a-random-object-and-a-list-of-icons"></a>Random オブジェクトおよびアイコンのリストを追加するには

1. **ソリューション エクスプローラー**で、C# の場合は *Form1.cs*、Visual Basic の場合は *Form1.vb* を選択し、メニュー バーの **[表示]**  >  **[コード]** の順に選択します。 別の方法として、**F7** キーを押すか、**ソリューション エクスプローラー**で **[Form1]** をダブルクリックすることもできます。

     これにより、Form1 のコード モジュールが表示されます。

2. 既存のコードに次のコードを追加します。

     [!code-csharp[VbExpressTutorial4Step2_3_4#1](../ide/codesnippet/CSharp/step-2-add-a-random-object-and-a-list-of-icons_1.cs)]
     [!code-vb[VbExpressTutorial4Step2_3_4#1](../ide/codesnippet/VisualBasic/step-2-add-a-random-object-and-a-list-of-icons_1.vb)]

      > [!IMPORTANT]
      > このページの右上にあるプログラミング言語のコントロールを使用して、C# コード スニペットまたは Visual Basic コード スニペットのいずれかを表示します。<br><br>![Docs.Microsoft.com のプログラミング言語コントロール](../ide/media/docs-programming-language-control.png)

      C# を使用している場合は、必ず開始中かっこの後の、クラス宣言 (`public partial class Form1 : Form`) のすぐ後に、コードを配置してください。 Visual Basic を記述している場合は、クラス宣言 (`Public Class Form1`) のすぐ後にコードを配置します。

3. List オブジェクトを追加するときに、表示される **IntelliSense** ウィンドウに注目します。 次に示すのは C# の例ですが、Visual Basic でリストを追加するときも同様のテキストが表示されます。

     ![Click イベントが表示された [プロパティ] ウィンドウ](../ide/media/express_listintellisense.png)<br/>***IntelliSense** ウィンドウ*

    > [!NOTE]
    > [IntelliSense] ウィンドウは、手動でコードを入力する場合にのみ表示されます。 コードをコピーして貼り付ける場合は表示されません。

     小さなセクションのコード (およびコメント) を見ると、より容易に理解できます。 プログラムでは、list オブジェクトを使用してさまざまな項目を追跡できます。 リストでは、数値、true/false 値、テキスト、またはその他のオブジェクトを保持できます。 他の list オブジェクトを保持している list オブジェクトを持つこともできます。 リスト内の項目は要素と呼ばれ、各リストで保持される要素は 1 種類のみです。 そのため、数値のリストでは数値しか保持できません。数値のリストにテキストを追加することはできません。 同様に、true/false 値のリストに数値を追加することもできません。

     `List` ステートメントを使用して `new` オブジェクトを作成するときは、リストに格納するデータの種類を指定する必要があります。 **IntelliSense** ウィンドウの上部のツールヒントがリスト内の要素の種類を示すのはそのためです。 また、`List<string>` (C# の場合) および `List(Of String)` (Visual Basic の場合) は、`List` オブジェクトが `string` データ型の要素を保持することを意味します。 string は、プログラムがテキストの格納に使用するものであり、**IntelliSense** ウィンドウの右側のツールヒントが示しているものです。

4. Visual Basic では最初に一時配列を作成する必要があるのに対し、C# では 1 つのステートメントでリストを作成できる理由を考えます。 これは、C# 言語には "*コレクション初期化子*" があるためです。この初期化子により値を受け取るリストが作成されます。 Visual Basic では、コレクション初期化子を使用できます。 ただし、以前のバージョンの Visual Basic との互換性を確保するため、先に示されているコードを使用することをお勧めします。

     `new` ステートメントでコレクション初期化子を使用した場合は、新しい List オブジェクトを作成すると、中かっこ内に指定しているデータがプログラムによってリストに格納されます。 ここでは、icons という名前の文字列のリストが生成され、そのリストは、16 の文字列を格納できるように初期化されます。 これらの各文字列は、1 つの文字であり、それらすべてがラベルで表示されるアイコンと対応しています。 そのためゲームには、感嘆符のペア、大文字の N のペア、コンマのペアなどが存在することになります (これらの文字は Webdings フォントに設定されると、バス、バイク、クモなどのアイコンとして表示されます)。list オブジェクトは、TableLayoutPanel パネルのセルごとに 1 つの、合計 16 の文字列を保持することになります。

    > [!NOTE]
    > Visual Basic では、結果は同じになりますが、最初に一時配列に文字列が格納されてから、この一時配列が list オブジェクトに変換されます。 配列はリストと似ていますが、配列は固定サイズで作成されるなどの例外があります。 リストは、必要に応じて縮小および拡大できます。このプログラムではこの点が重要になります。

## <a name="to-continue-or-review"></a>続行または確認するには

- チュートリアルの次の手順に進むには、「[**手順 3:各ラベルへのランダムなアイコンの割り当て**](../ide/step-3-assign-a-random-icon-to-each-label.md)」を参照してください。

- チュートリアルの前の手順に戻るには、「[手順 1: プロジェクトの作成とフォームへのテーブルの追加](../ide/step-1-create-a-project-and-add-a-table-to-your-form.md)」をご覧ください。

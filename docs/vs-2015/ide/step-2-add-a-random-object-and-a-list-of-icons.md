---
title: '手順 2: Random オブジェクトおよびアイコンのリストの追加 | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 95faea28-eddc-4cfa-95fb-3b34b5a976d7
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7370bf956fd79f5568737af5d9a96b9c64a5316b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667310"
---
# <a name="step-2-add-a-random-object-and-a-list-of-icons"></a>手順 2: Random オブジェクトおよびアイコンのリストの追加
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このステップでは、絵合わせゲームに使用する一連のアイコンを作成します。 各アイコンは、フォーム上の TableLayoutPanel 内の 2 つのランダムなセルに追加されます。 そのために、2 つの `new` ステートメントを使用して 2 つのオブジェクトを作成します。 1 つ目は、計算クイズ ゲームで使用したオブジェクトに似た `Random` オブジェクトです。 このコードでは、TableLayoutPanel 内のセルをランダムに選択するために使用します。 2 つ目は、初めての使用になるかもしれませんが、`List` オブジェクトです。ランダムに選択されたアイコンを格納するために使用します。

### <a name="to-add-a-random-object-and-a-list-of-icons"></a>Random オブジェクトおよびアイコンのリストを追加するには

1. **ソリューション エクスプローラー**で、Visual C# の場合は **[Form1.cs]**、Visual Basic の場合は **[Form1.vb]** をダブルクリックします。次に、メニュー バーで **[表示]**、**[コード]** の順にクリックします。 別の方法として、**F7** キーを押すか、**ソリューション エクスプローラー**で **[Form1]** をダブルクリックすることもできます。

     これにより、Form1 のコード モジュールが表示されます。

2. 既存のコードに次のコードを追加します。

     [!code-csharp[VbExpressTutorial4Step2_3_4#1](../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs#1)]
     [!code-vb[VbExpressTutorial4Step2_3_4#1](../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb#1)]

     Visual C# を使用している場合は、必ずクラス宣言 (`public partial class Form1 : Form`) のすぐ後の、始め中かっこの後にコードを配置してください。 Visual Basic を記述している場合は、クラス宣言 (`Public Class Form1`) のすぐ後にコードを配置します。

3. `List` オブジェクトを追加するときに、表示される **IntelliSense** ウィンドウに注目します。 次に示しているのは Visual C# の例ですが、Visual Basic でリストを追加するときも同様のテキストが表示されます。

     ![Click イベントが表示されたプロパティ ウィンドウ](../ide/media/express-listintellisense.png "Express_ListIntellisense") IntelliSense ウィンドウ

    > [!NOTE]
    > [Intellisense] ウィンドウは、手動でコードを入力する場合にのみ表示されます。 コードをコピーして貼り付ける場合は表示されません。

     小さなセクションのコード (およびコメント) を見ると、より容易に理解できます。 プログラムでは、`List` オブジェクトを使用してさまざまな項目を追跡できます。 リストでは、数値、true/false 値、テキスト、またはその他のオブジェクトを保持できます。 他の `List` オブジェクトを保持している `List` オブジェクトを持つこともできます。 リスト内の項目は*要素*と呼ばれ、各リストで保持される要素は 1 種類のみです。 そのため、数値のリストでは数値しか保持できません。数値のリストにテキストを追加することはできません。 同様に、true/false 値のリストに数値を追加することもできません。

     `List` ステートメントを使用して `new` オブジェクトを作成するときは、リストに格納するデータの種類を指定する必要があります。 **IntelliSense** ウィンドウの上部のツールヒントがリスト内の要素の種類を示すのはそのためです。 また、`List<string>` (Visual C# の場合) および `List(Of String)` (Visual Basic の場合) は、`List` オブジェクトが `string` データ型の要素を保持することを意味します。 string は、プログラムがテキストの格納に使用するものであり、**IntelliSense** ウィンドウの右側のツールヒントが示しているものです。

4. Visual Basic では最初に一時配列を作成する必要があるのに対し、Visual C# では 1 つのステートメントでリストを作成できる理由を考えます。 これは、Visual C# 言語には*コレクション初期化子*があるためです。この初期化子により値を受け取るリストが作成されます。 Visual Basic では、コレクション初期化子を使用できます。 ただし、以前のバージョンの Visual Basic との互換性を確保するため、先に示されているコードを使用することをお勧めします。

     `new` ステートメントでコレクション初期化子を使用した場合は、新しい `List` オブジェクトを作成すると、中かっこ内に指定しているデータがプログラムによってリストに格納されます。 ここでは、**icons** という名前の文字列のリストが生成され、そのリストは、16 の文字列を格納できるように初期化されます。 これらの各文字列は、1 つの文字であり、それらすべてがラベルで表示されるアイコンと対応しています。 そのためゲームには、感嘆符のペア、大文字の N のペア、コンマのペアなどが存在することになります  (これらの文字が Webdings フォントに設定されている場合、バス、自転車、スパイダーなどのシンボルとして表示されます)。 `List` オブジェクトには、TableLayoutPanel パネルの各セルに1つずつ、16個の文字列が含まれます。

    > [!NOTE]
    > Visual Basic では、結果は同じになりますが、最初に一時配列に文字列が格納されてから、この一時配列が `List` オブジェクトに変換されます。 配列はリストと似ていますが、配列は固定サイズで作成されるなどの例外があります。 リストは、必要に応じて縮小および拡大できます。このプログラムではこの点が重要になります。

### <a name="to-continue-or-review"></a>続行または確認するには

- チュートリアルの次の手順に進むには、「[手順 3: 各ラベルへのランダムなアイコンの割り当て](../ide/step-3-assign-a-random-icon-to-each-label.md)」を参照してください。

- チュートリアルの前の手順に戻るには、「[手順 1: プロジェクトの作成とフォームへのテーブルの追加](../ide/step-1-create-a-project-and-add-a-table-to-your-form.md)」を参照してください。

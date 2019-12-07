---
title: 変数の検査-自動変数とローカルウィンドウ |Microsoft Docs
ms.custom: seodec18
ms.date: 10/18/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.autos
- vs.debug.locals
helpviewer_keywords:
- debugger, variable windows
- debugging [Visual Studio], variable windows
ms.assetid: bb6291e1-596d-4af0-9f22-5fd713d6b84b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b159f631534135ac568fb03dbffa46ae0360fc47
ms.sourcegitcommit: 0b90e1197173749c4efee15c2a75a3b206c85538
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2019
ms.locfileid: "74904098"
---
# <a name="inspect-variables-in-the-autos-and-locals-windows"></a>[自動変数] ウィンドウと [ローカル] ウィンドウで変数を検査する

**[自動]** 変数 ウィンドウと **[ローカル]** ウィンドウには、デバッグ中の変数の値が表示されます。 ウィンドウは、デバッグセッション中にのみ使用できます。 **[自動変数]** ウィンドウには、現在のブレークポイントを囲む変数が表示されます。 [ローカル **] ウィンドウには、ローカル**スコープで定義されている変数が表示されます。これは通常、現在の関数またはメソッドです。 コードを初めてデバッグする場合は、この記事を読む前に、[絶対初心者向けのデバッグ](../debugger/debugging-absolute-beginners.md)や[手法とツール](../debugger/write-better-code-with-visual-studio.md)のデバッグをお読みになることをお勧めします。

 C# **[自動変数]** ウィンドウは、、Visual Basic C++、、および Python コードでは使用できますF#が、JavaScript やには使用できません。

**[自動変数]** ウィンドウを開くには、デバッグ中に [**デバッグ** > **Windows** > **自動変数**] を選択するか、 **ctrl**+**Alt**+**V** > **A**キーを押します。

**[ローカル]** ウィンドウを開くには、デバッグ中に [**デバッグ** > **Windows** > **ローカル**] を選択するか、 **Alt**+**4**キーを押します。

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、「 [Visual Studio for Mac でのデータの視覚化](/visualstudio/mac/data-visualizations)」を参照してください。

## <a name="use-the-autos-and-locals-windows"></a>[自動変数] ウィンドウと [ローカル] ウィンドウを使用する

配列とオブジェクトは、 **[自動変数]** ウィンドウと **[ローカル]** ウィンドウにツリーコントロールとして表示されます。 変数名の左側にある矢印を選択すると、ビューが展開され、フィールドとプロパティが表示されます。 **[ローカル]** ウィンドウの <xref:System.IO.FileStream?displayProperty=fullName> オブジェクトの例を次に示します。

![ローカル-FileStream](../debugger/media/locals-filestream.png "[ローカル]-FileStream")

**[ローカル]** または **[自動変数]** ウィンドウの赤の値は、最後の評価以降に値が変更されたことを意味します。 以前のデバッグセッションから、またはウィンドウの値を変更したために変更された可能性があります。

デバッガーウィンドウの既定の数値書式は decimal です。 16進数に変更するには、 **[ローカル]** または **[自動変数]** ウィンドウを右クリックし、 **[16 進数で表示]** を選択します。 この変更は、すべてのデバッガーウィンドウに影響します。

## <a name="edit-variable-values-in-the-autos-or-locals-window"></a>[自動変数] ウィンドウまたは [ローカル] ウィンドウで変数の値を編集する

**[自動]** 変数 ウィンドウまたは **[ローカル]** ウィンドウでほとんどの変数の値を編集するには、値をダブルクリックし、新しい値を入力します。

たとえば `a + b`のように、値に式を入力することもできます。 デバッガーは、正しい言語式であれば大部分を受け入れます。

ネイティブの C++ コードでは、変数名のコンテキストを修飾しなければならない場合があります。 詳細については、[コンテキスト演算子 (C++)](../debugger/context-operator-cpp.md) に関するページを参照してください。

>[!CAUTION]
>値と式を変更する前に、結果を理解しておく必要があります。 次のような問題が考えられます。
>
>- 式を評価すると、変数の値が変わる場合や、プログラムの状態に影響が及ぶ場合があります。 たとえば、`var1 = ++var2` を評価すると、`var1` と `var2`の両方の値が変更されます。 これらの式は、[副作用](https://en.wikipedia.org/wiki/Side_effect_\(computer_science\))があると言います。 副作用に気付いていない場合は、予期しない結果が発生する可能性があります。
>
>- 浮動小数点値を編集すると、小数部分の 10 進とバイナリの変換により、多少の誤差が発生する場合があります。 一見無害な編集でも、浮動小数点変数の一部のビットが変更される可能性があります。

::: moniker range=">= vs-2019" 
## <a name="search-in-the-autos-or-locals-window"></a>[自動変数] ウィンドウまたは [ローカル] ウィンドウで検索する

各ウィンドウの上にある検索バーを使用して、**自動変数** ウィンドウまたは **ローカル** ウィンドウの 名前、値、および 型 列でキーワードを検索できます。 ENTER キーを押すか、いずれかの矢印を選択して検索を実行します。 進行中の検索を取り消すには、検索バーの "x" アイコンを選択します。

検出された一致の間を移動するには、左矢印と右矢印 (Shift + F3 および F3 キー) を使用します。

![ローカルウィンドウで検索](../debugger/media/ee-search-locals.png "ローカルウィンドウで検索")

検索をさらに詳細に行うには、 **[自動変数]** ウィンドウまたは **[ローカル]** ウィンドウの上部にある 詳細の **[検索]** ドロップダウンを使用して、入れ子になったオブジェクトに検索するレベルの深さを選択します。 

## <a name="pin-properties-in-the-autos-or-locals-window"></a>[自動変数] ウィンドウまたは [ローカル] ウィンドウでプロパティをピン留めする

> [!NOTE]
> この機能は、.NET Core 3.0 以降でサポートされています。

**Pinnable properties**ツールを使用して、[自動変数] ウィンドウと [ローカル] ウィンドウでオブジェクトのプロパティをすばやく調べることができます。  このツールを使用するには、プロパティの上にマウスポインターを移動し、表示されるピンアイコンを選択するか、右クリックして、結果のコンテキストメニューで [**お気に入りとしてメンバーをピン留め**する] オプションを選択します。  これにより、そのプロパティがオブジェクトのプロパティリストの先頭にバブルされ、 **[値]** 列にプロパティの名前と値が表示されます。  プロパティの固定を解除するには、ピンアイコンをもう一度選択するか、コンテキストメニューの [**メンバーをお気に入りにピン留め**する] オプションを選択します。

![[ローカル] ウィンドウのプロパティを固定する](../debugger/media/basic-pin.gif "[ローカル] ウィンドウのプロパティを固定する")

また、[自動変数] ウィンドウまたは [ローカル] ウィンドウでオブジェクトのプロパティリストを表示するときに、プロパティ名を切り替えたり、ピン留めされていないプロパティを除外したりすることもできます。  各オプションにアクセスするには、[自動変数] ウィンドウまたは [ローカル] ウィンドウの上のツールバーにあるボタンを選択します。

![お気に入りのプロパティをフィルター処理](../debugger/media/filter-pinned-properties-locals.png "お気に入りのプロパティのフィルター処理")して![プロパティ名を切り替える](../debugger/media/toggle-property-names.gif "プロパティ名の切り替え")


::: moniker-end

## <a name="change-the-context-for-the-autos-or-locals-window"></a>[自動変数] ウィンドウまたは [ローカル] ウィンドウのコンテキストを変更する

**[デバッグの場所]** ツールバーを使用して、 **[自動変数]** ウィンドウと **[ローカル]** ウィンドウのコンテキストを変更する、必要な関数、スレッド、またはプロセスを選択できます。

デバッグの **[場所]** ツールバーを有効にするには、ツールバーの領域の空白部分をクリックし、ドロップダウンから **[デバッグの場所]** を選択するか、[ > **ツールバー** > **デバッグの場所** **] を選択**します。

ブレークポイントを設定し、デバッグを開始します。 ブレークポイントにヒットすると、実行が一時停止し、[デバッグの**場所**] ツールバーにその場所が表示されます。

![デバッグの場所ツールバー](../debugger/media/debuglocationtoolbar.png "[デバッグの場所] ツール バー")

## <a name="bkmk_whatvariables"></a>[自動変数] ウィンドウのC#変数C++(、、Visual Basic、Python)

コード言語が異なると、[**自動**変数] ウィンドウにさまざまな変数が表示されます。

- C# および Visual Basic では、 **[自動変数]** ウィンドウに現在の行または前の行に使用されている変数がすべて表示されます。 たとえば、またはC# Visual Basic コードで、次の4つの変数を宣言します。

   ```csharp
       public static void Main()
       {
          int a, b, c, d;
          a = 1;
          b = 2;
          c = 3;
          d = 4;
       }
   ```

   `c = 3;`行にブレークポイントを設定し、デバッガーを開始します。 実行が一時停止すると、 **[自動変数]** ウィンドウに次のように表示されます。

   ![自動変数-CSharp](../debugger/media/autos-csharp.png "Autos-CSharp")

   行 `c = 3` がまだ実行されていないため、`c` の値は0です。

- でC++は、実行が一時停止されている現在の行の少なくとも3行で使用されている変数が **[自動変数]** ウィンドウに表示されます。 たとえば、コードでC++は、次の6つの変数を宣言します。

   ```C++
       void main() {
           int a, b, c, d, e, f;
           a = 1;
           b = 2;
           c = 3;
           d = 4;
           e = 5;
           f = 6;
       }
   ```

    `e = 5;` 行にブレークポイントを設定し、デバッガーを実行します。 実行が停止すると、 **[自動変数]** ウィンドウに次のように表示されます。

    ![自動C++](../debugger/media/autos-cplus.png "自動C++")

    行 `e = 5` がまだ実行されていないため、`e` 変数は初期化されていません。

## <a name="bkmk_returnValue"></a> View return values of method calls
 .NET とC++コードでは、メソッド呼び出しのステップオーバーまたはステップアウト時に、 **[自動変数]** ウィンドウで戻り値を調べることができます。 メソッド呼び出しの戻り値を表示することは、ローカル変数に格納されていない場合に便利です。 メソッドは、パラメーターとして、または別のメソッドの戻り値として使用できます。

 たとえば、次C#のコードでは、2つの関数の戻り値が追加されます。

```csharp
static void Main(string[] args)
{
    int a, b, c, d;
    a = 1;
    b = 2;
    c = 3;
    d = 4;
    int x = sumVars(a, b) + subtractVars(c, d);
}

private static int sumVars(int i, int j)
{
    return i + j;
}

private static int subtractVars(int i, int j)
{
    return j - i;
}
```

[自動変数] ウィンドウで `sumVars()` および `subtractVars()` メソッドの呼び出しの戻り値を確認するには、次の手順を実行します。

1. `int x = sumVars(a, b) + subtractVars(c, d);` の行にブレークポイントを設定します。

1. デバッグを開始し、ブレークポイントで実行が一時停止したら、 **[ステップオーバー]** を選択するか、 **F10**キーを押します。 **[自動変数]** ウィンドウに次の戻り値が表示されます。

  ![自動変数の戻り値C#](../debugger/media/autosreturnvaluecsharp2.png "自動変数の戻り値C#")

## <a name="see-also"></a>参照

- [デバッグとは](../debugger/what-is-debugging.md)
- [デバッグの技術とツール](../debugger/write-better-code-with-visual-studio.md)
- [デバッグに関する最初の確認](../debugger/debugger-feature-tour.md)
- [デバッガー ウィンドウ](../debugger/debugger-windows.md)

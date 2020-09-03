---
title: 自動変数とローカルウィンドウ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.autos
- vs.debug.locals
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
helpviewer_keywords:
- debugger, variable windows
- debugging [Visual Studio], variable windows
ms.assetid: bb6291e1-596d-4af0-9f22-5fd713d6b84b
caps.latest.revision: 29
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 261c0c0bd8b48634c8d24d56ee4df7ea3bbcf135
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68161724"
---
# <a name="autos-and-locals-windows"></a>[自動変数] ウィンドウと [ローカル] ウィンドウ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**[自動変数]** ウィンドウ (デバッグ中に **CTRL+ALT+V キーを押し、A を押す**か、または **[デバッグ]、[Windows]、[自動変数]** を選択) および **[ローカル]** ウィンドウ (デバッグ中に **CTRL+ALT+V キーを押し、L を押す**か、または **[デバッグ]、[Windows]、[ローカル]** を選択) は、デバッグ中に変数の値を表示するときに、非常に役立ちます。 **[ローカル]** ウィンドウにはローカル スコープで定義されている変数が表示されます。これは一般に、現在実行されている関数またはメソッドです。 **[自動変数]** ウィンドウには、現在の行 (デバッガーが停止している場所) の付近で使用されている変数が表示されます。 正確にはどの変数が表示されるかは、言語によって異なります。 以下の「 What variables appear in the Autos Window?  
  
 基本的なデバッグの詳細については、「 [デバッガーでのはじめに](../debugger/getting-started-with-the-debugger.md)」を参照してください。  
  
## <a name="looking-at-objects-in-the-autos-and-locals-windows"></a>[自動変数] と [ローカル] ウィンドウ内のオブジェクトを調べる  
 配列とオブジェクトは、[自動変数] と [ローカル] ウィンドウにツリー コントロールで表示されます。 変数名の左側にある矢印をクリックするとビューが展開され、フィールドとプロパティが表示されます。 以下に、 **[ローカル]** ウィンドウに表示されている <xref:System.IO.FileStream> オブジェクトの例を示します。  
  
 ![ローカル&#45;FileStream](../debugger/media/locals-filestream.png "Locals-FileStream")  
  
## <a name="what-variables-appear-in-the-autos-window"></a>[自動変数] ウィンドウに表示される変数  
 **[自動変数]** ウィンドウは C#、Visual Basic、C++ のコードで使用できます。 **[自動変数]** ウィンドウでは JavaScript も F# もサポートされません。  
  
 C# および Visual Basic の場合、[ **自動変数** ] ウィンドウには、現在または前の行で使用されている任意の変数が表示されます。 たとえば、4 つの変数を宣言し、これらを次のように設定したとします。  
  
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
  
 行 `c = 3`にブレークポイントを設定した場合、デバッガーを実行して、実行が停止すると、 **[自動変数]** ウィンドウは次のようになります。  
  
 ![自動変数&#45;CSharp](../debugger/media/autos-csharp.png "Autos-CSharp")  
  
 `c` の値が 0 であることにご注意ください。これは、 `c = 3` 行目のコードがまだ実行されていないからです。  
  
 C++ では、最低でも現在の行 (実行が停止した行) の 3 行前で使用された変数が **[自動変数]** ウィンドウに表示されます。 6 つの変数を宣言するとします。  
  
```cpp  
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
  
 行 `e = 5;` にブレークポイントを設定した場合、デバッガーを実行して、実行が停止すると、 **[自動変数]** ウィンドウは次のようになります。  
  
 ![自動変数&#45;Cplus](../debugger/media/autos-cplus.png "[自動変数]-Cplus")  
  
 e の変数が初期化されていないことにご注意ください。これは `e = 5;` 行目のコードがまだ実行されていないからです。  
  
 ある状況では、関数やメソッドの戻り値が表示されることもあります。 以下の「 [View return values of method calls](#bkmk_returnValue) 」をご覧ください。  
  
## <a name="view-return-values-of-method-calls"></a><a name="bkmk_returnValue"></a> View return values of method calls  
 .NET および C++ のコードでは、メソッド呼び出しのステップ オーバーまたはステップ アウトをするときに戻り値を確認できます。 この機能が便利なのは、メソッド呼び出しの結果がローカル変数に格納されないときです。たとえば、メソッドが別のメソッドのパラメーターまたは戻り値として使用されるときなどです。  
  
 次の C# コードは、2 つの関数の戻り値を加算します。  
  
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
  
 int `x = sumVars(a, b) + subtractVars(c, d);` 行にブレークポイントを設定します。  
  
 デバッグを開始して、最初のブレークポイントで実行が中断したときに、 **F10 キー (ステップ オーバー)** を押します。 **[自動変数]** ウィンドウには次のように表示されます。  
  
 ![[自動変数]戻り値C##](../debugger/media/autosreturnvaluecsharp2.png "[自動変数]戻り値C##")  
  
## <a name="why-are-variable-values-sometimes-red-in-locals-and-autos-windows"></a>[ローカル] ウィンドウと [自動変数] ウィンドウで変数の値が時々赤色で表示される理由  
 **[ローカル]** ウィンドウと **[自動変数]** ウィンドウで時々、変数の値が赤色で表示されることがあります。 これらは、前回の評価以降、変化した変数の値です。 この変更は前のデバッグ セッションに由来する場合もあれば、ウィンドウで値が変更されたための場合もあります。  
  
## <a name="changing-the-numeric-format-of-a-variable-window"></a>変数ウィンドウの数値の形式の変更  
 既定の数値の形式は 10 進数ですが、これを 16 進数に変更することができます。 **[ローカル]** または **[自動変数]** ウィンドウ内で右クリックし、 **[16 進数で表示]** を選びます。 この変更は、すべてのデバッガー ウィンドウに反映されます。  
  
## <a name="editing-a-value-in-a-variable-window"></a>[変数] ウィンドウで値を編集する  
 **[自動変数]**、 **[ローカル]**、 **[ウォッチ]**、 **[クイック ウォッチ]** ウィンドウに表示される変数の大部分は、値を編集できます。 **[ウォッチ]** と **[クイック ウォッチ]** ウィンドウについては、「 [Watch and QuickWatch Windows](../debugger/watch-and-quickwatch-windows.md)」をご覧ください。 変更する値をダブルクリックするだけで、新しい値を追加できます。  
  
 たとえば `a + b`のように、値に式を入力することもできます。 デバッガーは、正しい言語式であれば大部分を受け入れます。  
  
 ネイティブの C++ コードでは、変数名のコンテキストを修飾しなければならない場合があります。 詳細については、「 [コンテキスト演算子 (C++)](../debugger/context-operator-cpp.md)」を参照してください。  
  
 ただし、値を変更するときには注意が必要です。 考えられる問題のいくつかを次に示します。  
  
- 式を評価すると、変数の値が変わる場合や、プログラムの状態に影響が及ぶ場合があります。 たとえば、 `var1 = ++var2` を評価すると `var1` と `var2`の値が変更されます。  
  
     データを変更する式は、 [副作用](https://en.wikipedia.org/wiki/Side_effect_\(computer_science\))があると言われています。気付かないうちに予期しない結果になる可能性があります。 変更を加える前に、そうした変更の結果を理解する必要があります。  
  
- 浮動小数点値を編集すると、小数部分の 10 進とバイナリの変換により、多少の誤差が発生する場合があります。 特に影響のないように見える編集でも、浮動小数点値の最下位バイトが変化する場合があります。  
  
## <a name="debug-location-toolbar"></a>[デバッグの場所] ツール バー  
 **[デバッグの場所]** ツール バーを使用して、必要な関数、スレッド、またはプロセスを選択できます。 ブレークポイントを設定し、デバッグを開始します。 (このツール バーが表示されていない場合は、ツール バーの領域の空白の場所をクリックして有効にできます。 ツール バーの一覧が表示されたら、 **[デバッグの場所]** を選びます。) ブレークポイントがヒットすると、実行が停止し、[デバッグの場所] ツール バーが表示されます (次の図の一番下の行)。  
  
 ![[デバッグの場所] ツール バー](../debugger/media/debuglocationtoolbar.png "[デバッグの場所] ツール バー")  
  
 **[呼び出し履歴]** ウィンドウ、 **[スレッド]** ウィンドウ、または **[プロセス]** ウィンドウで要素をダブルクリックすれば、コンテキストを別の関数呼び出し、スレッド、またはプロセスに変更することもできます。  
  
## <a name="see-also"></a>参照  
 [デバッガー ウィンドウ](../debugger/debugger-windows.md)

---
title: デバッグ履歴を使用したアプリの検査 |Microsoft Docs
description: IntelliTrace のデバッグ履歴を使用して C# コンソール アプリケーションのバグを追跡する調査について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 629b5d93-39b2-430a-b8ba-d2a47fdf2584
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d51327f67429071d08f6dfd02c0ec0a1fc55822f
ms.sourcegitcommit: 40d758f779d42c66cb02ae7face8a62763a8662b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97398702"
---
# <a name="inspect-your-app-with-intellitrace-historical-debugging-in-visual-studio-c-visual-basic-c"></a>Visual Studio で IntelliTrace のデバッグ履歴を使用してアプリを検査します (C#、Visual Basic、C++)

アプリケーションの実行を前後に移動して、その状態を調査するには、[デバッグ履歴](../debugger/historical-debugging.md)を使用できます。

IntelliTrace は Visual Studio Enterprise Edition で使用できますが、Professional Edition または Community Edition では使用できません。

## <a name="navigate-your-code-with-historical-debugging"></a>デバッグ履歴を使用したコードの移動

バグのあるシンプルなプログラムから始めましょう。 C# コンソール アプリケーションで次のコードを追加します。

```csharp
static void Main(string[] args)
{
    int testInt = 0;
    int resultInt = AddAll(testInt);
    Console.WriteLine(resultInt);
}
private static int AddAll(int j)
{
    for (int i = 0; i < 20; i++)
    {
        j = AddInt(j);
    }
    return j;
}

private static int AddInt(int add)
{
    if (add == 10)
    {
        return add += 25;
    }
    return ++add;
}
```

`AddAll()` を呼び出した後の `resultInt` の予想される値が 20 であるものとします (`testInt` を 20 回インクリメントした結果)。 (また、`AddInt()` 内のバグは確認できなものと想定します)。しかし、実際の結果は 44 です。 `AddAll()` を 10 回ステップ実行しないでバグを見つけるにはどうすればよいでしょう。 デバッグ履歴を使うと、迅速かつ簡単にバグを発見できます。 次の手順に従います。

1. **[ツール]、[オプション]、[IntelliTrace]、[全般]** で、IntelliTrace が有効になっていることを確認し、 **[IntelliTrace イベントと呼び出し情報]** を選択します。 このオプションを選択しないと、ナビゲーション余白が表示されません (後で説明します)。

2. `Console.WriteLine(resultInt);` の行にブレークポイントを設定します。

3. デバッグを開始します。 コードがブレークポイントまで実行されます。 **[ローカル]** ウィンドウで、`resultInt` の値が 44 であることを確認できます。

4. **[診断ツール]** ウィンドウを開きます ( **[デバッグ] > [診断ツールの表示]** )。 コード ウィンドウは、次のようになります。

    ![ブレークポイントでのコード ウィンドウ](../debugger/media/historicaldebuggingbreakpoint.png "HistoricalDebuggingBreakpoint")

5. ブレークポイントのすぐ上の左余白の横に双方向矢印が表示されます。 この領域はナビゲーション余白と呼ばれ、履歴デバッグに使用されます。 矢印をクリックします。

    コード ウィンドウでは、上記のコード行 (`int resultInt = AddIterative(testInt);`) がピンク色で表示されます。 ウィンドウの上には、現在デバッグ履歴中であることを示すメッセージが表示されます。

    コード ウィンドウは、次のようになります。

    ![デバッグ履歴モードでのコード ウィンドウ](../debugger/media/historicaldebuggingback.png "HistoricalDebuggingBack")

6. ここで、`AddAll()` メソッドにステップ インできます (**F11** キー、またはナビゲーション余白の **[ステップ イン]** ボタン)。 ステップ前進します (**F10** キー、またはナビゲーション余白の **[次の呼び出しへ移動]** )。 ピンクの行が `j = AddInt(j);` 行に移ります。 ここで **F10** キーを押しても、次のコード行には移動しません。 代わりに、次の関数呼び出しに移動します。 デバッグ履歴は呼び出しから呼び出しに移動し、関数呼び出しを含まないコード行はスキップされます。

7. ここで、`AddInt()` メソッドにステップ インします。 このコードにバグがあることがすぐにわかります。

## <a name="next-steps"></a>次の手順

この手順では、デバッグ履歴でできることの表面的な部分のみを見ています。

- デバッグ時にスナップショットを表示するには、[IntelliTrace を使用した以前のアプリの状態の調査](../debugger/view-historical-application-state.md)に関するページを参照してください。
- 他の設定およびナビゲーション余白の他のボタンの効果について詳しくは、「[IntelliTrace の機能](../debugger/intellitrace-features.md)」をご覧ください。

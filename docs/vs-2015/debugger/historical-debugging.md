---
title: デバッグ履歴 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 7cc5ddf2-2f7c-4f83-b7ca-58e92e9bfdd2
caps.latest.revision: 9
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c7db175535e0eebdcf1974f0f85123959ba5a3ed
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68192175"
---
# <a name="historical-debugging"></a>デバッグ履歴
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

デバッグ履歴は、IntelliTrace で収集された情報に依存するデバッグのモードです。 アプリケーションの実行内を前後に移動して、実行の状態を調べることができます。  
  
 IntelliTrace は Visual Studio Enterprise Edition で使用できます (Professional Edition または Community Edition の場合は使用できません)。  
  
## <a name="why-use-historical-debugging"></a>デバッグ履歴を使用する理由  
 ブレークポイントを設定してバグを探すのは、どちらかというと行き当たりばったりな方法です。 バグがありそうな場所のコードの近くにブレークポイントを設定し、デバッガーでアプリケーションを実行して、ブレークポイントがヒットし、実行が中断した場所でバグの原因が明らかになることを期待します。 原因がわからない場合は、コードの別の場所にブレークポイントを設定し、デバッガーを再実行して、問題が見つかるまで繰り返しテスト手順を実行する必要があります。  
  
 ![ブレークポイントの設定](../debugger/media/breakpointprocesa.png "BreakpointProcesa")  
  
 IntelliTrace とデバッグ履歴を使用すると、アプリケーション内を移動して状態を調べることができ (呼び出し履歴およびローカル変数)、ブレークポイントを設定し、デバッグを再実行し、テスト手順を繰り返す必要はありません。 これにより多くの時間を節約できます。実行に時間がかかるテスト シナリオの深い場所にバグがある場合は特に有効です。  
  
## <a name="how-do-i-start-using-historical-debugging"></a>デバッグ履歴の使用を始める方法  
 IntelliTrace は既定で有効になります。 決定する必要があるのは、調査対象のイベントと関数呼び出しだけです。 調べる対象の定義について詳しくは、「[IntelliTrace の機能](../debugger/intellitrace-features.md)」をご覧ください。 IntelliTrace を使用したデバッグの詳細な手順については、「 [チュートリアル: intellitrace の使用](../debugger/walkthrough-using-intellitrace.md)」を参照してください。  
  
## <a name="navigating-your-code-with-historical-debugging"></a>デバッグ履歴でのコード内の移動  
 バグのある単純なプログラムから始めましょう。 C# コンソール アプリケーションで次のコードを追加します。  
  
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
  
 `AddAll()` を呼び出した後の `resultInt` の予想される値が 20 であるものとします (`testInt` を 20 回インクリメントした結果)  (また、`AddInt()` 内のバグはわからないものします)。しかし、実際の結果は 44 です。 `AddAll()` を 10 回ステップ実行しないでバグを見つけるにはどうすればよいでしょう。 デバッグ履歴を使うと、迅速かつ簡単にバグを発見できます。 その方法は次のとおりです。  
  
1. [ツール]、[オプション]、[IntelliTrace]、[一般] で、IntelliTrace が有効になっていることを確認し、[IntelliTrace イベントと呼び出し情報] オプションを選択します。 このオプションを選択しないと、ナビゲーション余白が表示されません (後で説明します)。  
  
2. `Console.WriteLine(resultInt);` の行にブレークポイントを設定します。  
  
3. デバッグを開始します。 コードがブレークポイントまで実行されます。 **[ローカル]** ウィンドウで、`resultInt` の値が 44 であることを確認できます。  
  
4. [ **診断ツール** ] ウィンドウを開きます ([**デバッグ]/[診断ツールの表示**])。 コード ウィンドウは、次のようになります。  
  
    ![ブレークポイントでのコード ウィンドウ](../debugger/media/historicaldebuggingbreakpoint.png "HistoricalDebuggingBreakpoint")  
  
5. ブレークポイントのすぐ上の左余白の横に双方向矢印が表示されます。 この領域はナビゲーション余白と呼ばれ、履歴デバッグに使用されます。 矢印をクリックします。  
  
    コード ウィンドウでは、上記のコード行 (`int resultInt = AddIterative(testInt);`) がピンク色で表示されます。 ウィンドウの上には、現在デバッグ履歴中であることを示すメッセージが表示されます。  
  
    コード ウィンドウは、次のようになります。  
  
    ![デバッグ履歴モードでのコード ウィンドウ](../debugger/media/historicaldebuggingback.png "HistoricalDebuggingBack")  
  
6. ここで、`AddAll()` メソッドにステップ インできます (**F11** キー、またはナビゲーション余白の **[ステップ イン]** ボタン)。 ステップ前進します (**F10** キー、またはナビゲーション余白の **[次の呼び出しへ移動]** )。 ピンクの行が `j = AddInt(j);` 行に移ります。 ここで **F10** キーを押しても、次のコード行には移動しません。 代わりに、次の関数呼び出しに移動します。 デバッグ履歴は呼び出しから呼び出しに移動し、関数呼び出しを含まないコード行はスキップされます。  
  
7. ここで、`AddInt()` メソッドにステップ インします。 このコードにバグがあることがすぐにわかります。  
  
   この手順では、デバッグ履歴でできることの表面的な部分のみを見ています。 他の設定およびナビゲーション余白の他のボタンの効果について詳しくは、「[IntelliTrace の機能](../debugger/intellitrace-features.md)」をご覧ください。

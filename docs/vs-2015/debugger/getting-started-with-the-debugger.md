---
title: デバッガーを使用してはじめに |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: c763d706-3213-494f-b4d2-990b6e1ec456
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e093abd5e836bcb7ee236979c00d574a07ecfd3d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202305"
---
# <a name="getting-started-with-the-debugger"></a>デバッガーの使用開始
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio デバッガーは、どの言語でも簡単に使用できます。 ここでは、簡単な C# プログラムのデバッグ方法について説明しますが、C++、JavaScript などの他の言語のコードに同じ手順を適用することができます。  
  
## <a name="debug-a-basic-c-project"></a><a name="BKMK_Start_debugging_a_VS_project"></a> 基本的な C# プロジェクトのデバッグ  
 単純な C# コンソールアプリケーションから始めましょう ([ファイル]、[**新規作成**]、[プロジェクト] の順に選択し、[ **Visual C#** ]、[ **コンソールアプリケーション**] の順に選択します)。 以前に Visual Studio を使用したことがない場合は、「 [チュートリアル: 単純なアプリケーションを作成](../ide/walkthrough-create-a-simple-application-with-visual-csharp-or-visual-basic.md)する」を参照してください。 **Main**メソッドは、整数変数に1を10回追加するだけで、結果をコンソールに出力します。  
  
```csharp  
static void Main(string[] args)  
{  
    int testInt = 0;  
    for (int i = 1; i <= 10; i++)  
    {  
        testInt += 1;  
    }  
    Console.WriteLine(testInt);  
}  
```  
  
 **デバッグ**構成でこのコードをビルドします。 この構成は、既定で設定されています。 構成の詳細については、「 [ビルド構成](../ide/understanding-build-configurations.md)について」を参照してください。  
  
 [デバッグ]、[ **デバッグの開始** ] の順にクリックする **か、** ツールバーまたは **F5 キー**を押して、デバッガーでこのコードを実行します。 アプリケーションはほぼ即座に終了するため、実際に何かがコンソール ウィンドウに出力されたかどうかは分かりません。  
  
 ブレークポイントを設定してから先に進むことで、コンソール ウィンドウを確認する間実行を停止することができます。 ブレークポイントを設定するには、行にカーソルを置き、 `Console.WriteLine` [デバッグ]、[ブレークポイント]、[ **関数のブレークポイント**] の順にクリックするか、同じ行の左余白をクリックします。 ブレークポイントは次のように表示されます。  
  
 ![ブレークポイントを設定する](../debugger/media/getstartedbreakpoint.png "Geton ブレークポイント")  
  
 ブレークポイントの詳細については、「 [ブレークポイントの使用](../debugger/using-breakpoints.md)」を参照してください。  
  
## <a name="inspect-variables"></a><a name="BKMK_Inspect_Variables"></a> 変数の検査  
 多くの場合、デバッグでは、特定の時点で必要な値が含まれていない変数が検索されます。 変数を検査するいくつかの方法を紹介します。  
  
 デバッグを再度開始します。 `Console.WriteLine` のコードが実行される前に実行が停止します。 これを実行するには、ステップ実行する必要があります ([ **デバッグ]/[ステップオーバー** ] または [ **F10**] をクリックします)。 この場合、[ **ステップイン** ] (**F11**) を選択して、同じ結果を取得することができます。この違いについては、後で説明します。 メソッドの最後の中かっこの行が黄色に変わっているはずです。 コンソール ウィンドウを見てください。 **10**と表示します。  
  
 **Testint**変数の上にマウスポインターを置くと、データヒントの現在の値が表示されます。  
  
 ![DBG&#95;基本&#95;データ&#95;のヒント](../debugger/media/dbg-basics-data-tips.png "DBG_Basics_Data_Tips")  
  
 コードウィンドウのすぐ下には、[ **自動変数**]、[ **ローカル**]、[ **ウォッチ** ] の各ウィンドウが表示されます。 これらのウィンドウは、実行時における変数の現行値を表示します。 [**自動変数**] ウィンドウと [**ローカル**] ウィンドウの両方に、値が**10**の**testint**が表示されます。  
  
 ![デバッグ時の [自動変数] ウィンドウ](../debugger/media/getstartedwindows.png "Getの前のウィンドウ")  
  
 これらのウィンドウの詳細については、「 [自動変数とローカルウィンドウ](../debugger/autos-and-locals-windows.md)」を参照してください。  
  
 プログラムを進めながら、変数の値がどのように変化するかを見てみましょう。 行にブレークポイントを設定 `testInt += 1;` し、デバッグを再開します。 [**ローカル**] ウィンドウと [**自動変数**] ウィンドウに [ **testint** ] が**0**、 **i**が**1**になっていることがわかります。 デバッグを続行すると ([**デバッグ]/[続行**] をクリックするか、ツールバーまたは**F5 キー**を押して**続行**)、 **testint**の値が**1**に変更され、 **2**が続くことがわかります。 これらの変更を確認するのが面倒な場合は、ブレークポイントを削除します ([**デバッグ]/[ブレークポイント**の設定/解除] をクリックするか、余白内でクリックします)。デバッグを続行します。 すべてのブレークポイントを削除する場合は、[**デバッグ]/[すべてのブレークポイントの削除**] をクリックするか、 **CTRL + SHIFT + F9 キーを押し**て、[すべての**ブレークポイントを削除しますか?**] ダイアログボックスで [**はい**] をクリックします。  
  
## <a name="stepping-into-and-over-function-calls"></a>関数の呼び出しのステップ インとステップ オーバー  
 デバッガーでコードを実行したり (**ステップイン**)、デバッガーが関数 (**ステップオーバー**) をスキップするときにコードを実行して、関心のあるコード (関数コードがまだ実行されている) をすぐに取得することができます。 同じデバッグセッションで、両方のメソッドを切り替えることができます。  
  
 **ステップイン**と**ステップオーバー**の違いを確認するには、別のメソッドによって呼び出されるメソッドを追加する必要があります。 C# アプリケーションにメソッドを追加し、Main メソッドから呼び出します。 コードは次のようになります。  
  
```csharp  
static void Main(string[] args)  
{  
    Method1();  
    Console.WriteLine("end");  
}  
  
private static void Method1()  
{  
    Console.WriteLine("in Method1");  
}  
```  
  
 Main メソッド内の `Method1();` の呼び出しにブレークポイントを設定し、デバッグを開始します。 実行が中断したら、[ **デバッグ]/[ステップイン** ] (またはツールバーの [ **ステップイン** ]) をクリックするか、 **F11**キーを押します。 Method1() 内の最初の中かっこでもう一度実行が中断します。  
  
 ![コードへのステップイン](../debugger/media/getstartedstepinto.png "Getのステップイン")  
  
 デバッグを停止してからもう一度開始します。ブレークポイントで実行が中断したら、[ **デバッグ]/[ステップオーバー** ] をクリックします (または、ツールバーの [ **ステップオーバー** ] をクリックするか、 **F10**キーを押します)。 実行が `Console.WriteLine("end");` で再度中断します。  
  
 デバッガーでのコード間の移動の詳細については、「 [デバッガーでのコード間の移動](../debugger/navigating-through-code-with-the-debugger.md)」を参照してください。

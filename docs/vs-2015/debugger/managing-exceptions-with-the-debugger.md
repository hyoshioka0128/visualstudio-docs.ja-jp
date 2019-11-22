---
title: Managing Exceptions with the Debugger | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.exceptions
- vs.debug.exceptions.find
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
helpviewer_keywords:
- run-time errors
- exception handling, during debugging
- errors [debugger]
- debugger, runtime errors
- On Error-style error handlers
- exceptions, Win32
- run-time errors, debugging
- Win32, exceptions
- run time, exceptions
- error handling
- debugging [Visual Studio], exception handling
- common language runtime, exceptions
- native run-time checks
- exceptions, debugging
ms.assetid: 43a77fa8-37d0-4c98-a334-0134dbca4ece
caps.latest.revision: 40
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5303a8003d84af5e2a059d9f509e560204afa528
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74301089"
---
# <a name="managing-exceptions-with-the-debugger"></a>デバッガーでの例外の管理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

例外は、プログラムの実行中に発生したエラー状態を示します。 最も重要な例外に応答するハンドラーを提供できるようにする必要がありますが、確認したい例外が発生した場合に実行が中断されるようにデバッガーを設定する方法を理解することが重要です。  
  
 例外が発生すると、[出力] ウィンドウに例外メッセージが書き込まれます。 次のような場合、例外によって実行が中断される可能性があります。  
  
- 例外がスローされたが、処理されない場合。  
  
- 例外がスローされた直後、ハンドラーが呼び出される前に実行を中断するようにデバッガーが設定されている場合。  
  
- [ [Just My Code](../debugger/just-my-code.md)] を設定済みで、デバッガーが、ユーザー コードで処理されない例外に対して実行を中断するように設定されている場合。  
  
> [!NOTE]
> ASP.NET は、エラー ページをブラウザーに表示する最上位の例外ハンドラーを持っています。 **マイ コードのみ** が有効ではない場合、実行は中断されません。 例については、以下の「 [Setting the debugger to continue on user-unhandled exceptions](../debugger/managing-exceptions-with-the-debugger.md#BKMK_UserUnhandled) 」をご覧ください。  
  
> [!NOTE]
> Visual Basic アプリケーションのデバッガーでは、すべてのエラーが例外として管理されます。On Error 形式のエラー ハンドラーを使用している場合でもそうです。  
  
## <a name="managing-exceptions-with-the-exception-settings-window"></a>[例外設定] ウィンドウで例外を管理する  
 **[例外設定]** ウィンドウを使用すれば、デバッガーに実行を中断させる例外 (または例外のセット)、およびデバッガーに実行を中断させるポイントを指定することができます。 例外を追加または削除したり、実行を中断する例外を指定したりすることができます。 ソリューションが開いているときに、このウィンドウを開くには、 **[デバッグ] / [Windows] / [例外設定]** の順にクリックします。  
  
 特定の例外を見つけるには、 **[例外設定]** ツールバーの **[検索]** ウィンドウを使用するか、検索機能を使用して特定の名前空間 (たとえば **System.IO**) をフィルター処理します。  
  
### <a name="setting-the-debugger-to-break-when-an-exception-is-thrown"></a>例外がスローされたときに中断されるようにデバッガーを設定する  
 例外がスローされた時点でデバッガーは実行を中断することができます。これにより、例外ハンドラーが呼び出される前に例外を調査する機会が与えられます。  
  
 **[例外設定]** ウィンドウで、例外のカテゴリのノード (たとえば、 **[共通言語ランタイム例外]** 、すなわち、.NET に関する例外) を展開し、そのカテゴリ内の特定の例外 (たとえば、 **[System.AccessViolationException]** ) のチェックボックスをオンにします。 例外のカテゴリ全体を選択することもできます。  
  
 ![Checked AccessViolationException](../debugger/media/exceptionsettingscheckaccess.png "ExceptionSettingsCheckAccess")  
  
 特定の例外を選択した場合、その例外がスローされるたびに、処理するか処理しないかに関係なく、デバッガーの実行は停止されます。 この時点で、例外は初回例外と呼ばれます。 例として、いくつかのシナリオを以下に示します。  
  
1. 次の C# コンソール アプリケーションで、Main メソッドは **try/catch** ブロック内で `try/catch` をスローします。  
  
   ```csharp  
   static void Main(string[] args)  
   {  
       try  
       {  
           throw new AccessViolationException();  
           Console.WriteLine("here");  
       }  
       catch (Exception e)  
       {  
           Console.WriteLine("caught exception");  
       }  
       Console.WriteLine("goodbye");  
   }  
   ```  
  
    **try/catch** で **[例外設定]** のチェック ボックスをオンにした場合、このコードをデバッガーで実行すると、 `throw` 行で実行が中断されます。 実行は続行することができます。 コンソールには、次の行が両方とも表示される必要があります。  
  
   ```  
   caught exception  
   goodbye  
   ```  
  
    しかし、 `here` 行は表示されていません。  
  
2. C# コンソール アプリケーションは、2 つのメソッドを持つクラスが属するクラス ライブラリを参照します。1 つのメソッドは例外をスローし、それを処理します。もう 1 つのメソッドは同じ例外をスローしますが、その処理を行いません。  
  
   ```vb  
   public class Class1  
   {  
       public void ThrowHandledException()  
       {  
           try  
           {  
               throw new AccessViolationException();  
           }  
           catch (AccessViolationException ave)  
           {  
               Console.WriteLine("caught exception" + ave.Message);  
           }  
       }  
  
       public void ThrowUnhandledException()  
       {  
           throw new AccessViolationException();  
       }  
   }  
   ```  
  
    コンソール アプリケーションの Main() メソッドを次に示します。  
  
   ```csharp  
   static void Main(string[] args)  
   {  
       Class1 class1 = new Class1();  
       class1.ThrowHandledException();  
       class1.ThrowUnhandledException();  
   }  
   ```  
  
    If you have **AccessViolationException** checked in **Exception Settings**, when you run this code in the debugger execution will break on the `throw` line in both **ThrowHandledException()** and **ThrowUnhandledException()** .  
  
   例外設定を既定値に戻す場合は、ツールバーの **[復元]** ボタンをクリックします。  
  
   ![Restore defaults in Exception Settings](../debugger/media/restoredefaultexceptions.png "RestoreDefaultExceptions")  
  
### <a name="BKMK_UserUnhandled"></a> Setting the debugger to continue on user-unhandled exceptions  
 [ [Just My Code](../debugger/just-my-code.md)] を使用して .NET コードまたは JavaScript コードをデバッグする場合、ユーザー コードで処理されないが他の場所で処理される例外について、中断しないようにデバッガーを設定することができます。  
  
1. **[例外設定]** ウィンドウでコンテキスト メニューを開くには、ウィンドウで右クリックし、 **[列の表示]** を選択します ( **[マイ コードのみ]** を選択していない場合、このコマンドは表示されません)。  
  
2. **[追加のアクション]** という名前の 2 つ目の列が表示されます。 この列には、特定の例外に対して **[ユーザー コードで処理されない場合は続行]** が表示されます。すなわち、例外がユーザー コードで処理されないが外部コードで処理される場合、デバッガーは中断されません。  
  
3. この設定は、特定の例外に対して変更することも (例外を選択し、右クリックし、 **[ユーザー コードで処理されない場合は続行]** を選択または選択解除する)、例外のカテゴリ全体 (たとえば、すべての共通言語ランタイム例外) に対して変更することもできます。  
  
   たとえば、ASP.NET Web アプリケーションは、例外を HTTP 500 状態コードに変換して処理します ([ASP.NET API での例外の処理](https://docs.microsoft.com/aspnet/web-api/overview/error-handling/exception-handling))。この場合、例外の原因を特定できないことがあります。 次の例では、ユーザー コードは、 `String.Format()` をスローする <xref:System.FormatException>を呼び出します。 実行は次のように中断されます。  
  
   ![breaks on user&#45;unhanlded exception](../debugger/media/exceptionunhandledbyuser.png "ExceptionUnhandledByUser")  
  
### <a name="adding-and-deleting-exceptions"></a>例外の追加と削除  
 例外は追加および削除することができます。 任意のカテゴリから任意の種類の例外を削除するには、例外を選択し、 **[例外設定]** ツールバーの **[削除]** ボタン (マイナス記号) をクリックするか、または例外を右クリックし、コンテキスト メニューから **[削除]** をクリックします。 例外を削除することは、例外をオフにするのと同じ結果になります。すなわち、該当する例外がスローされたとき、デバッガーは中断されません。  
  
 例外を追加するには、 **[例外設定]** ウィンドウで、例外カテゴリの 1 つ (たとえば、 **[共通言語ランタイム]** ) を選択し、 **[追加]** ボタンをクリックします。 例外の名前を入力します (たとえば、 **System.UriTemplateMatchException**)。 例外は一覧 (アルファベット順の) に追加され、自動的にオンになります。  
  
 GPU メモリ アクセス例外、JavaScript ランタイム例外、または Win32 例外というカテゴリに例外を追加する場合は、エラー コードと説明を含める必要があります。  
  
> [!TIP]
> スペルを確認してください。 **[例外設定]** ウィンドウでは、追加された例外の存在について確認が行われません。 したがって、「 **Sytem.UriTemplateMatchException**」と入力した場合は、その例外のエントリ ( **System.UriTemplateMatchException**のエントリではなく) が表示されます。  
  
 例外の設定はソリューションの .suo ファイルに保持され、特定のソリューションに適用されます。 複数のソリューションの間で、特定の例外設定を再利用することはできません。 この時点では、追加された例外だけが保存されます。削除された例外は保持されません。 すなわち、例外を追加してから、ソリューションをいったん閉じて、再度開いた場合、その例外は表示されたままです。 しかし、例外を削除してから、ソリューションをいったん閉じて、再度開いた場合、例外は再表示されます。  
  
 **[例外設定]** ウィンドウでは、C# の汎用的な例外タイプをサポートしていますが、Visual Basic の汎用的な例外タイプはサポートしていません。 `MyNamespace.GenericException<T>`のような例外が発生したときに実行が中断されるようにするには、例外を **[MyNamespace.GenericException`1]** として追加する必要があります。 すなわち、例外を次のように作成した場合:  
  
```csharp  
public class GenericException<T> : Exception  
{  
    public GenericException() : base("This is a generic exception.")  
    {  
    }  
}  
```  
  
 **[例外設定]** に例外を次のように追加できます。  
  
 ![adding generic exception](../debugger/media/addgenericexception.png "AddGenericException")  
  
## <a name="see-also"></a>参照  
 [Continuing Execution After an Exception](../debugger/continuing-execution-after-an-exception.md)   
 [How to: Examine System Code After an Exception](../debugger/how-to-examine-system-code-after-an-exception.md)   
 [How to: Use Native Run-Time Checks](../debugger/how-to-use-native-run-time-checks.md)   
 [Using Run-Time Checks Without the C Run-Time Library](../debugger/using-run-time-checks-without-the-c-run-time-library.md)   
 [Exception Assistant](https://msdn.microsoft.com/library/992892ac-9d52-44cc-bf09-b44bfc5befeb)   
 [デバッガーの基本事項](../debugger/debugger-basics.md)

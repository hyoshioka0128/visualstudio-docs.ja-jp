---
title: デバッガーを使用して例外を管理する |Microsoft Docs
ms.custom: seodec18
ms.date: 10/09/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.exceptions
- vs.debug.exceptions.find
dev_langs:
- CSharp
- VB
- FSharp
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 00ad5b41dd0a11661d281f24474b7673ea0a342c
ms.sourcegitcommit: 257fc60eb01fefafa9185fca28727ded81b8bca9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72911503"
---
# <a name="manage-exceptions-with-the-debugger-in-visual-studio"></a>Visual Studio でデバッガーを使用して例外を管理する

例外は、プログラムの実行中に発生したエラー状態を示します。 デバッガーに対して、中断する例外または例外のセットと、デバッガーが中断するポイント (つまり、デバッガーで一時停止) を指定できます。 デバッガーが中断すると、例外がスローされた場所が示されます。 例外を追加または削除することもできます。 Visual Studio でソリューションを開いた状態で、 **[デバッグ > Windows > 例外設定]** を使用して **[例外設定]** ウィンドウを開きます。

最も重要な例外に応答するハンドラーを提供します。 例外のハンドラーを追加する方法を理解する必要がある場合は、「[よりC#適切なコードを記述してバグを修正](../debugger/write-better-code-with-visual-studio.md)する」を参照してください。 また、一部の例外に対して常に実行を中断するようにデバッガーを構成する方法についても説明します。

例外が発生すると、 **[出力]** ウィンドウに例外メッセージが書き込まれます。 次の場合に、実行が中断される可能性があります。

- 例外がスローされ、処理されません。
- デバッガーは、ハンドラーが呼び出される前に実行を中断するように構成されています。
- [マイコードのみ](../debugger/just-my-code.md)を設定しました。デバッガーは、ユーザーコードで処理されない例外で中断するように構成されています。

> [!NOTE]
> ASP.NET は、エラー ページをブラウザーに表示する最上位の例外ハンドラーを持っています。 **マイコードのみ**が有効になっていない限り、実行は中断されません。 例については、以下の「ユーザーによって処理され[ない例外で続行するようにデバッガーを指定する](#BKMK_UserUnhandled)」を参照してください。

<!-- Two consecutive notes are intentional here...-->

> [!NOTE]
> Visual Basic アプリケーションのデバッガーでは、すべてのエラーが例外として管理されます。On Error 形式のエラー ハンドラーを使用している場合でもそうです。

## <a name="tell-the-debugger-to-break-when-an-exception-is-thrown"></a>例外がスローされたときに中断するようにデバッガーに指示する

デバッガーは、例外がスローされた時点で実行を中断できます。そのため、ハンドラーが呼び出される前に例外を調べることができます。

<<<<<<< HEAD
**[例外設定]** ウィンドウ (**デバッグ > Windows > 例外設定**) で、例外のカテゴリ ( **[共通言語ランタイムの例外]** など) のノードを展開します。 次に、そのカテゴリ内の特定の例外のチェックボックスをオンにします。たとえば、「**system.string**」と入力します。 例外のカテゴリ全体を選択することもできます。
||||||| merged common ancestors
**[例外設定]** ウィンドウ (**デバッグ > Windows > 例外設定**) で、例外のカテゴリ ( **[共通言語ランタイムの例外]** など) のノードを展開します。 次に、そのカテゴリ内の特定の例外のチェックボックスをオンにします。たとえば、「system.string **」と入力**します。 例外のカテゴリ全体を選択することもできます。
=======
**[例外設定]** ウィンドウ (**デバッグ > Windows > 例外設定**) で、例外のカテゴリ ( **[共通言語ランタイムの例外]** など) のノードを展開します。 次に、そのカテゴリ内の特定の例外のチェックボックスをオンにします。たとえば、「**system.string **」と入力します。 例外のカテゴリ全体を選択することもできます。
>>>>>>> live

![チェックされた AccessViolationException](../debugger/media/exceptionsettingscheckaccess.png "ExceptionSettingsCheckAccess")

> [!TIP]
> 特定の例外を見つけるには、 **[例外設定]** ツールバーの **[検索]** ウィンドウを使用するか、検索を使用して特定の名前空間 ( **System.IO**など) をフィルター処理します。

**[例外設定]** ウィンドウで例外を選択すると、処理されているかどうかに関係なく、例外がスローされた箇所でデバッガーの実行が中断されます。 これで、例外は初回例外と呼ばれるようになりました。 例として、いくつかのシナリオを以下に示します。

- 次の C# コンソール アプリケーションで、Main メソッドは `try/catch` ブロック内で **AccessViolationException** をスローします。

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

  **例外設定**で **[access違反 ationexception]** がオンになっている場合、デバッガーでこのコードを実行すると、`throw` 行で実行が中断されます。 実行は続行することができます。 コンソールには、次の行が両方とも表示される必要があります。

  ```cmd
  caught exception
  goodbye
  ```

  ただし、`here` 線は表示されません。

- コンソールC#アプリケーションは、2つのメソッドを持つクラスを使用してクラスライブラリを参照します。 1つのメソッドが例外をスローし、それを処理しますが、2番目のメソッドは同じ例外をスローしますが、それを処理しません。

  ```csharp
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

  **例外設定**で**AccessThrowHandledException ationexception**がオンになっている場合、デバッガーでこのコードを実行すると、両方の **()** と**ThrowUnhandledException ()** の両方の `throw` 行で実行が中断されます。

例外設定を既定値に復元するには、 **[既定の設定に戻す]** ボタンを選択します。

![例外設定の既定値に戻す](../debugger/media/restoredefaultexceptions.png "RestoreDefaultExceptions")

## <a name="BKMK_UserUnhandled"></a>ユーザーにハンドルされない例外に対して続行するようにデバッガーに指示する

[マイコードのみ](../debugger/just-my-code.md)で .net コードまたは JavaScript コードをデバッグする場合は、ユーザーコードで処理されないが他の場所で処理される例外の中断を防ぐように、デバッガーに指示できます。

1. **[例外設定]** ウィンドウで、列ラベルを右クリックしてショートカットメニューを開き、[**列の表示] > [追加のアクション**] を選択します。 (**マイコードのみ**を無効にした場合、このコマンドは表示されません)。**追加アクション**という名前の3番目の列が表示されます。

   ![その他のアクション列](../debugger/media/additionalactionscolumn.png "Additionalactions 列")

   この列のユーザーコードで処理されない**ときに続行**を示す例外の場合、その例外がユーザーコードで処理されず、外部で処理される場合、デバッガーは続行されます。

2. 特定の例外に対してこの設定を変更するには、例外を選択し、右クリックしてショートカットメニューを表示し、[**ユーザーコードで処理されない場合は続行**する] を選択します。 また、共通言語ランタイムの例外全体など、例外のカテゴリ全体の設定を変更することもできます。

   ![* * ユーザーコード * * 設定で処理されない場合は続行します](../debugger/media/continuewhenunhandledinusercodesetting.png "ContinueWhenUnhandledInUserCodeSetting")

たとえば、ASP.NET web アプリケーションは、例外を HTTP 500 状態コード ([ASP.NET Web API での例外処理](/aspnet/web-api/overview/error-handling/exception-handling)) に変換することによって例外を処理しますが、例外の原因を特定するのには役立ちません。 次の例では、ユーザー コードは、 `String.Format()` をスローする <xref:System.FormatException>を呼び出します。 実行は次のように中断されます。

![ユーザー&#45;のハンドルされない例外で中断](../debugger/media/exceptionunhandledbyuser.png "ExceptionUnhandledByUser")

## <a name="add-and-delete-exceptions"></a>例外を追加および削除する

例外は追加および削除することができます。 カテゴリから例外の種類を削除するには、例外を選択し、 **[例外設定]** ツールバーの **[一覧から選択した例外を削除]** する (マイナス記号) を選択します。 または、例外を右クリックして、ショートカットメニューの **[削除]** をクリックすることもできます。 例外を削除すると、例外をオフにした場合と同じ効果があります。これは、スローされたときにデバッガーが中断しないことを意味します。

例外を追加するには:

1. **[例外設定]** ウィンドウで、例外カテゴリの1つ (たとえば、 **[共通言語ランタイム]** ) を選択します。

2. [**選択したカテゴリに例外を追加**します] ボタン (正符号) を選択します。

   ![* * 選択した [カテゴリ] * * ボタンに例外を追加します。](../debugger/media/addanexceptiontotheselectedcategorybutton.png "Addanexceptiontotheselected[カテゴリ] ボタン")

3. 例外の名前を入力します (たとえば、 **system.uritemplatematchexception**)。

   ![例外の名前を入力します](../debugger/media/typetheexceptionname.png "TypeTheExceptionName")

   例外が一覧に追加され (アルファベット順に)、自動的にチェックされます。

GPU メモリアクセス例外、JavaScript ランタイム例外、または Win32 例外カテゴリに例外を追加するには、エラーコードと説明を含めます。

> [!TIP]
> スペルを確認してください。 **[例外設定]** ウィンドウでは、追加された例外の存在について確認が行われません。 したがって、「**Sytem.UriTemplateMatchException**」と入力した場合は、その例外のエントリ (**System.UriTemplateMatchException** のエントリではなく) が表示されます。

例外の設定はソリューションの .suo ファイルに保持され、特定のソリューションに適用されます。 複数のソリューションの間で、特定の例外設定を再利用することはできません。 ここで、追加された例外だけが保存されます。削除された例外はありません。 例外を追加して、ソリューションを閉じてから再度開くことができます。例外は引き続き存在します。 しかし、例外を削除してから、ソリューションをいったん閉じて、再度開いた場合、例外は再表示されます。

**[例外設定]** ウィンドウでは、C# の汎用的な例外タイプをサポートしていますが、Visual Basic の汎用的な例外タイプはサポートしていません。 `MyNamespace.GenericException<T>`のような例外が発生したときに実行が中断されるようにするには、例外を **[MyNamespace.GenericException`1]** として追加する必要があります。 つまり、次のコードのような例外が作成されたとします。

```csharp
public class GenericException<T> : Exception
{
    public GenericException() : base("This is a generic exception.")
    {
    }
}
```

例外**設定**には、前の手順を使用して例外を追加できます。

![汎用例外を追加しています](../debugger/media/addgenericexception.png "AddGenericException")

## <a name="add-conditions-to-an-exception"></a>例外に条件を追加する

**[例外設定]** ウィンドウを使用すると、例外に関する条件を設定できます。 現在サポートされている条件には、例外に含めたり除外したりするモジュール名が含まれます。 モジュール名を条件として設定することにより、特定のコードモジュールでのみ例外の発生を中断するように選択できます。 また、特定のモジュールを中断しないように選択することもできます。

> [!NOTE]
> 例外への条件の追加は [!include[vs_dev15](../misc/includes/vs_dev15_md.md)]以降でサポートされています。

条件付き例外を追加するには:

1. 例外設定 ウィンドウで **条件の編集** ボタンを選択するか、例外を右クリックして **条件の編集** を選択します。

   ![例外の条件](../debugger/media/dbg-conditional-exception.png "DbgConditionalException")

2. 例外に必要な条件を追加するには、[新しい条件ごとに**条件を追加**する] を選択します。 その他の条件行が表示されます。

   ![例外の追加条件](../debugger/media/extraconditionsforanexception.png "ExtraConditionsForAnException")

3. 各条件行にモジュールの名前を入力し、比較演算子**リストを equals または** **Not equals**に変更します。 名前にワイルドカード ( **\\\*** ) を指定して、複数のモジュールを指定することもできます。

4. 条件を削除する必要がある場合は、条件行の最後にある **[X]** を選択します。

## <a name="see-also"></a>関連項目

- [例外後の実行の継続](../debugger/continuing-execution-after-an-exception.md)<br/>
- [方法 : 例外の後にシステム コードを調べる](../debugger/how-to-examine-system-code-after-an-exception.md)<br/>
- [方法 : ネイティブ ランタイム チェックを使用する](../debugger/how-to-use-native-run-time-checks.md)<br/>
- [C ランタイム ライブラリなしのランタイム チェックを使用する](../debugger/using-run-time-checks-without-the-c-run-time-library.md)<br/>
- [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)

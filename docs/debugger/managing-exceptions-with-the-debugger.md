---
title: デバッガを使用して例外を管理する |マイクロソフトドキュメント
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
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301123"
---
# <a name="manage-exceptions-with-the-debugger-in-visual-studio"></a>Visual Studio でデバッガーを使用して例外を管理します。

例外は、プログラムの実行中に発生したエラー状態を示します。 中断する例外または例外のセット、およびデバッガーを中断する (デバッガーで一時停止する) ポイントをデバッガーに知ることができます。 デバッガーが中断すると、例外がスローされた場所が表示されます。 例外を追加または削除することもできます。 Visual Studio でソリューションを開いた場合は **、[Windows >の例外設定] > [デバッグ**] を使用して **[例外設定]** ウィンドウを開きます。

最も重要な例外に応答するハンドラーを提供します。 例外のハンドラーを追加する方法を知る必要がある場合は、「[より良い C# コードを記述してバグを修正](../debugger/write-better-code-with-visual-studio.md)する」を参照してください。 また、一部の例外の実行を常に中断するようにデバッガーを構成する方法についても説明します。

例外が発生すると、デバッガーは **、出力**ウィンドウに例外メッセージを書き込みます。 次の場合に実行が中断される可能性があります。

- 処理されない例外がスローされます。
- デバッガーは、ハンドラーが呼び出される前に実行を中断するように構成されています。
- [マイ[コードのみを使用](../debugger/just-my-code.md)] を設定し、ユーザー コードで処理されない例外でデバッガーが中断するように構成されています。

> [!NOTE]
> ASP.NET は、エラー ページをブラウザーに表示する最上位の例外ハンドラーを持っています。 **[マイ コードだけ**] がオンになっていない限り、実行は中断されません。 例については、以下[の「ユーザーハンドルされない例外を続行するようにデバッガーに指示する」を](#BKMK_UserUnhandled)参照してください。

<!-- Two consecutive notes are intentional here...-->

> [!NOTE]
> Visual Basic アプリケーションのデバッガーでは、すべてのエラーが例外として管理されます。On Error 形式のエラー ハンドラーを使用している場合でもそうです。

## <a name="tell-the-debugger-to-break-when-an-exception-is-thrown"></a>例外がスローされたときにデバッガーを中断するように指示する

デバッガーは例外がスローされた時点で実行を中断できるため、ハンドラーが呼び出される前に例外を調べることができます。

[**例外の設定]** ウィンドウ (**[Windows >例外の設定**] > [ デバッグ ] ウィンドウ ) で、ノードを展開して 、例外のカテゴリ (**共通言語ランタイム例外**など) を展開します。 次に、そのカテゴリ内の特定の例外のチェック ボックス**をオンにします**。 例外のカテゴリ全体を選択することもできます。

![チェック済み AccessViolationException](../debugger/media/exceptionsettingscheckaccess.png "設定のチェック アクセス")

> [!TIP]
> [**例外の設定]** ツールバーの [**検索**] ウィンドウを使用して特定の例外を検索するか、検索を使用して特定の名前空間 **(System.IO**など) をフィルター処理します。

**[例外設定]** ウィンドウで例外を選択すると、例外が処理されるかどうかにかかわらず、例外がスローされた場合は、デバッガーの実行が中断されます。 ここで、例外は最初のチャンス例外と呼ばれます。 例として、いくつかのシナリオを以下に示します。

- 次の C# コンソール アプリケーションでは、Main メソッドはブロック内に`try/catch`**AccessViolationException**をスローします。

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

  **例外設定**で**AccessViolationException**がオンになっている場合、デバッガーでこの`throw`コードを実行すると、実行は行で中断されます。 実行は続行することができます。 コンソールには、次の行が両方とも表示される必要があります。

  ```cmd
  caught exception
  goodbye
  ```

  しかし、それは線を`here`表示しません。

- C# コンソール アプリケーションは、2 つのメソッドを持つクラス ライブラリを参照します。 1 つのメソッドは例外をスローして処理し、2 番目のメソッドは同じ例外をスローしますが、処理しません。

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

  **例外設定**で**AccessViolationException**がオンになっている場合、デバッガーでこのコード`throw`を実行すると、実行は**ThrowHandledException()** と**ThrowUnhandledException()** の両方の行で中断されます。

例外設定をデフォルトに戻すには、[**リストを既定の設定に戻す**] ボタンを選択します。

![例外設定の既定値に戻す](../debugger/media/restoredefaultexceptions.png "既定の例外を復元します。")

## <a name="tell-the-debugger-to-continue-on-user-unhandled-exceptions"></a><a name="BKMK_UserUnhandled"></a>ユーザーが処理できない例外を続行するようにデバッガーに指示する

[[マイ コードのみを使用して](../debugger/just-my-code.md).NET] または JavaScript コードをデバッグする場合は、ユーザー コードで処理されないが他の場所で処理される例外が発生しないようにデバッガーに指示できます。

1. [**例外設定]** ウィンドウで、列ラベルを右クリックしてショートカット メニューを開き、[**列>追加アクションを表示**] を選択します。 **([マイ コード]** をオフにしている場合は、このコマンドは表示されません)。**[追加アクション]** という名前の 3 番目の列が表示されます。

   ![[追加のアクション] 列](../debugger/media/additionalactionscolumn.png "追加アクション列")

   この列のユーザー**コードで処理されない場合に続行**を示す例外の場合、その例外はユーザー コードで処理されず、外部で処理される場合、デバッガーは続行されます。

2. 特定の例外に対してこの設定を変更するには、例外を選択し、右クリックしてショートカット メニューを表示し、[**ユーザー コードで未処理の場合に続行]** を選択します。 共通言語ランタイムの例外全体など、例外のカテゴリ全体の設定を変更することもできます。

   ![**ユーザーコードで処理されない場合に続行**設定](../debugger/media/continuewhenunhandledinusercodesetting.png "処理されていない場合の続行ユーザーコード設定")

たとえば、ASP.NET Web アプリケーションは、例外を HTTP 500 ステータス コード[(ASP.NET Web API の例外処理](/aspnet/web-api/overview/error-handling/exception-handling)) に変換して例外を処理します。 次の例では、ユーザー コードは、 `String.Format()` をスローする <xref:System.FormatException>を呼び出します。 実行は次のように中断されます。

![ユーザー&#45;ハンドルされない例外の中断](../debugger/media/exceptionunhandledbyuser.png "例外未処理のユーザー")

## <a name="add-and-delete-exceptions"></a>例外を追加および削除する

例外は追加および削除することができます。 カテゴリから例外の種類を削除するには、例外を選択し、[**例外設定]** ツールバーの [リスト] ボタン (マイナス記号) から **[選択した例外を削除**する] を選択します。 または、例外を右クリックして、ショートカット メニューから **[削除**] を選択することもできます。 例外を削除すると、例外がオフになっている場合と同じ結果が発生します。

例外を追加するには:

1. [**例外の設定]** ウィンドウで、例外カテゴリ (**たとえば、共通言語ランタイム**) のいずれかを選択します。

2. [**選択したカテゴリに例外を追加]** ボタン (プラス記号) を選択します。

   ![**選択したカテゴリ**ボタンに例外を追加します。](../debugger/media/addanexceptiontotheselectedcategorybutton.png "選択されたカテゴリボタンに追加します。")

3. 例外の名前を入力します (たとえば、**システム.UriTemplateMatchException)。**

   ![例外名を入力してください](../debugger/media/typetheexceptionname.png "タイプザ・例外名")

   例外はリストに追加され(アルファベット順に)自動的にチェックされます。

GPU メモリ アクセス例外、JavaScript ランタイム例外、または Win32 例外カテゴリに例外を追加するには、エラー コードと説明を含めます。

> [!TIP]
> スペルを確認してください。 **[例外設定]** ウィンドウでは、追加された例外が存在するかどうかをチェックしません。 したがって **、Sytem.UriTemplateMatchException**と入力すると、その例外のエントリが取得されます (**および、System.UriTemplateMatchException の**エントリではありません)。

例外の設定はソリューションの .suo ファイルに保持され、特定のソリューションに適用されます。 複数のソリューションの間で、特定の例外設定を再利用することはできません。 これで、追加された例外のみが永続化されます。削除された例外は、そうではありません。 例外を追加し、ソリューションを閉じて再度開くと、例外が発生します。 しかし、例外を削除してから、ソリューションをいったん閉じて、再度開いた場合、例外は再表示されます。

**[例外設定]** ウィンドウでは、C# の汎用的な例外タイプをサポートしていますが、Visual Basic の汎用的な例外タイプはサポートしていません。 `MyNamespace.GenericException<T>`のような例外が発生したときに実行が中断されるようにするには、例外を **[MyNamespace.GenericException`1]** として追加する必要があります。 つまり、次のような例外を作成した場合は、次のようになります。

```csharp
public class GenericException<T> : Exception
{
    public GenericException() : base("This is a generic exception.")
    {
    }
}
```

上記の手順を使用して**例外**設定に例外を追加できます。

![一般的な例外の追加](../debugger/media/addgenericexception.png "ジェネリック例外を追加します。")

## <a name="add-conditions-to-an-exception"></a>例外に条件を追加する

例外の条件を設定するには **、[例外設定]** ウィンドウを使用します。 現在サポートされている条件には、例外に含めるモジュール名または除外するモジュール名が含まれます。 モジュール名を条件として設定することで、特定のコード モジュールでのみ例外を中断するように選択できます。 また、特定のモジュールで破損を回避することもできます。

> [!NOTE]
> 例外への条件の追加は、 で[!include[vs_dev15](../misc/includes/vs_dev15_md.md)]始まるサポートされています。

条件付き例外を追加するには、次の手順に従います。

1. [例外設定] ウィンドウの **[条件の編集**] ボタンを選択するか、例外を右クリックして **[条件の編集**] を選択します。

   ![例外の条件](../debugger/media/dbg-conditional-exception.png "条件例外")

2. 例外に追加の必須条件を追加するには、新しい条件ごとに **[条件の追加]** を選択します。 追加の条件行が表示されます。

   ![例外に対する追加条件](../debugger/media/extraconditionsforanexception.png "例外の追加条件")

3. 各条件行に対して、モジュールの名前を入力し、比較演算子リストを **「等しい**」 または 「**不等号」** に変更します。 名前にワイルドカード (**\\**) を指定して、複数のモジュールを指定できます。

4. 条件を削除する必要がある場合は、条件行の最後にある**X**を選択します。

## <a name="see-also"></a>関連項目

- [例外後の実行の継続](../debugger/continuing-execution-after-an-exception.md)<br/>
- [方法 : 例外の後にシステム コードを調べる](../debugger/how-to-examine-system-code-after-an-exception.md)<br/>
- [方法 : ネイティブ ランタイム チェックを使用する](../debugger/how-to-use-native-run-time-checks.md)<br/>
- [C ランタイム ライブラリを使用せずにランタイム チェックを使用する](../debugger/using-run-time-checks-without-the-c-run-time-library.md)<br/>
- [まずデバッガを見てください](../debugger/debugger-feature-tour.md)

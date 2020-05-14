---
title: デザイン時にデバッグする |Microsoft Docs
ms.custom: ''
ms.date: 01/10/2019
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- debugging [Visual Studio], design-time
- breakpoints, design-time debugging
- Immediate window, design-time debugging
- design-time debugging
ms.assetid: 35bfdd2c-6f60-4be1-ba9d-55fce70ee4d8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: beb16ae52f880e31bd19a185d47b13c02026752f
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75916144"
---
# <a name="debug-at-design-time-in-visual-studio-c-ccli-visual-basic-f"></a>Visual Studio でのデザイン時のデバッグC#( C++、/cli、Visual Basic F#、)

アプリの実行中にではなく、デザイン時にコードをデバッグするには、 **[イミディエイト]** ウィンドウを使用します。

宣言型データバインディングのシナリオなど、アプリの背後にある XAML コードを XAML デザイナーからデバッグするには、 **[デバッグ]**  >  **[プロセスにアタッチ]** を使用できます。

## <a name="use-the-immediate-window"></a>[イミディエイト] ウィンドウを使用する

Visual Studio の **[イミディエイト]** ウィンドウを使用すると、アプリを実行せずに関数またはサブルーチンを実行できます。 関数またはサブルーチンにブレークポイントが含まれている場合、Visual Studio はブレークポイントで中断します。 デバッガー ウィンドウを使用して、プログラムの状態を確認できます。 この機能は、*デザイン時のデバッグ*と呼ばれます。

次の例は Visual Basic にあります。 F#、、およびC++/cli アプリでC#は、デザイン時に **[イミディエイト]** ウィンドウを使用することもできます。

1. 空の Visual Basic コンソールアプリに次のコードを貼り付けます。

   ```vb
   Module Module1

       Sub Main()
           MySub()
       End Sub

       Function MyFunction() As Decimal
           Static i As Integer
           i = i + 1
           Return i
       End Function

       Sub MySub()
           MyFunction()

       End Sub
   End Module
   ```

1. 行の**終わりの関数**にブレークポイントを設定します。

1. イミディエイトウィンドウ**を開くには、** [**デバッグ** > **Windows** > **イミディエイト**] を選択します。 ウィンドウに「`?MyFunction`」と入力し、 **enter キーを**押します。

   ブレークポイントにヒットし、 **[ローカル]** ウィンドウの**MyFunction**の値が**1**になります。 アプリが中断モードのときに、呼び出し履歴とその他のデバッグウィンドウを調べることができます。

1. Visual Studio ツールバーの **[続行]** を選択します。 アプリが終了し、 **[イミディエイト]** ウィンドウに**1**が返されます。 まだデザインモードになっていることを確認します。

1. **[イミディエイト]** ウィンドウでもう一度「`?MyFunction`」と入力し、 **enter**キーを押します。 ブレークポイントにヒットし、 **[ローカル]** ウィンドウの**MyFunction**の値は**2**になります。

1. **[続行]** を選択せずに、 **[イミディエイト]** ウィンドウに「`?MySub()`」と入力し、 **enter キーを**押します。 ブレークポイントにヒットし、 **[ローカル]** ウィンドウの**MyFunction**の値が**3**になります。 アプリが中断モードになっている間は、アプリの状態を確認できます。

1. **[続行]** を選択します。 ブレークポイントが再びヒットし、 **[ローカル]** ウィンドウの**MyFunction**の値が**2**になります。 **イミディエイト**ウィンドウは、**式が評価され、値がない**ことを返します。

1. **[続行]** を選択します。 アプリが終了し、 **[イミディエイト]** ウィンドウに**2**が返されます。 まだデザインモードになっていることを確認します。

1. **[イミディエイト]** ウィンドウの内容を消去するには、ウィンドウ内を右クリックし、 **[すべてクリア]** を選択します。

## <a name="debug-a-custom-xaml-control-at-design-time-by-attaching-to-xaml-designer"></a>XAML デザイナーにアタッチして、デザイン時にカスタム XAML コントロールをデバッグする

1. Visual Studio でソリューションまたはプロジェクトを開きます。

1. ソリューション/プロジェクトをビルドします。

1. デバッグするカスタムコントロールを含む XAML ページを開きます。

   Windows ビルド16299以降を対象とする UWP プロジェクトの場合、この手順では、 *Uwpsurface .exe*プロセスを開始します。 Windows ビルド16299より前の WPF または UWP バージョンの場合、この手順では*Xdesproc .exe*プロセスを開始します。

1. Visual Studio の 2 つ目のインスタンスを開きます。 2番目のインスタンスでは、ソリューションまたはプロジェクトを開かないでください。

1. Visual Studio の2番目のインスタンスで、 **[デバッグ]** メニューを開き、 **[プロセスにアタッチ...]** をクリックします。

1. プロジェクトの種類に応じて (前の手順を参照)、使用可能なプロセスの一覧から、 *Uwpsurface .exe*または*xdesproc .exe*プロセスを選択します。

1. **[プロセスにアタッチ]** ダイアログの **[アタッチ先]** フィールドで、デバッグするカスタムコントロールの適切なコードの種類を選択します。

   カスタムコントロールが .NET 言語で記述されている場合は、**マネージ (CoreCLR)** などの適切な .net コードの種類を選択します。 カスタムコントロールがにC++記述されている場合は、 **[ネイティブ]** を選択します。

1. **[アタッチ]** ボタンをクリックして、Visual Studio の2番目のインスタンスをアタッチします。

1. Visual Studio の2番目のインスタンスで、デバッグするカスタムコントロールに関連付けられているコードファイルを開きます。 ソリューションまたはプロジェクト全体ではなく、ファイルのみを開いてください。

1. 前に開いたファイルに必要なブレークポイントを設定します。

1. Visual Studio の最初のインスタンスで、デバッグするカスタムコントロール (前の手順で開いたものと同じページ) を含む XAML ページを閉じます。

1. Visual Studio の最初のインスタンスで、前の手順で閉じた XAML ページを開きます。 これにより、Visual Studio の2番目のインスタンスに設定した最初のブレークポイントでデバッガーが停止します。

1. Visual Studio の2番目のインスタンスでコードをデバッグします。

## <a name="see-also"></a>関連項目
- [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
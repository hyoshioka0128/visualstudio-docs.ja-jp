---
title: デザイン時にデバッグする | Microsoft Docs
description: '[イミディエイト] ウィンドウを使用し、アプリを実行せず、デザイン時にコードをデバッグします。 関数を実行し、ブレークポイントにヒットしたときの状態を調べることができます。'
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: f127c630cec0e0b64ab5602e81f2b314a3896b16
ms.sourcegitcommit: 957da60a881469d9001df1f4ba3ef01388109c86
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2021
ms.locfileid: "98148848"
---
# <a name="debug-at-design-time-in-visual-studio-c-ccli-visual-basic-f"></a>Visual Studio でデザイン時にデバッグする (C#、C++/CLI、Visual Basic、F#)

アプリの実行中にではなくデザイン時にコードをデバッグするには、 **[イミディエイト]** ウィンドウを使用できます。

宣言型データ バインディングのシナリオなど、XAML デザイナーからアプリの XAML 分離コードをデバッグするには、 **[デバッグ]**  >  **[プロセスにアタッチ]** を使用できます。

## <a name="use-the-immediate-window"></a>[イミディエイト] ウィンドウを使用する

Visual Studio の **[イミディエイト]** ウィンドウを使用すると、アプリを実行しなくても、関数やサブルーチンを実行できます。 関数またはサブルーチンにブレークポイントが含まれている場合、Visual Studio はブレークポイントで中断します。 デバッガー ウィンドウを使用して、プログラムの状態を確認できます。 この機能は、*デザイン時のデバッグ* と呼ばれます。

Visual Basic での例を次に示します。 C#、F#、および C++/CLI アプリでは、デザイン時に **[イミディエイト]** ウィンドウを使用することもできます。

1. 次のコードを空白の Visual Basic コンソール アプリに貼り付けます。

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

1. **End Function** という行にブレークポイントを設定します。

1. **[イミディエイト]** ウィンドウを開くには、 **[デバッグ]**  >  **[Windows]**  >  **[イミディエイト]** を選択します。 ウィンドウに「`?MyFunction`」と入力してから、**Enter** キーを押します。

   ブレークポイントにヒットし、 **[ローカル]** ウィンドウの **[MyFunction]** の値が **1** になります。 アプリが中断モードのときに、呼び出し履歴とその他のデバッグ ウィンドウを調べることができます。

1. Visual Studio ツール バーで **[続行]** を選択します。 アプリが終了し、 **[イミディエイト]** ウィンドウに **1** が返されます。 まだデザイン モードになっていることを確認します。

1. もう一度 **[イミディエイト]** ウィンドウに「`?MyFunction`」と入力し、**Enter** キーを押します。 ブレークポイントにヒットし、 **[ローカル]** ウィンドウの **[MyFunction]** の値が **2** になります。

1. **[続行]** を選択せずに、 **[イミディエイト]** ウィンドウに「`?MySub()`」と入力し、**Enter** キーを押します。 ブレークポイントにヒットし、 **[ローカル]** ウィンドウの **[MyFunction]** の値が **3** になります。 アプリが中断モードになっている間は、アプリの状態を確認できます。

1. **[続行]** を選択します。 もう一度ブレークポイントにヒットし、 **[ローカル]** ウィンドウの **[MyFunction]** の値が **2** になります。 **[イミディエイト]** ウィンドウによって、「**式は評価されましたが、値が指定されていません。** 」が返されます。

1. もう一度 **[続行]** を選択します。 アプリが終了し、 **[イミディエイト]** ウィンドウに **2** が返されます。 まだデザイン モードになっていることを確認します。

1. **[イミディエイト]** ウィンドウの内容を消去するには、ウィンドウ内を右クリックし、 **[すべてクリア]** を選択します。

## <a name="debug-a-custom-xaml-control-at-design-time-by-attaching-to-xaml-designer"></a>XAML デザイナーにアタッチしてデザイン時にカスタム XAML コントロールをデバッグする

1. Visual Studio でソリューションまたはプロジェクトを開きます。

1. ソリューションまたはプロジェクトをビルドします。

1. デバッグするカスタム コントロールを含む XAML ページを開きます。

   Windows ビルド 16299 以降を対象とする UWP プロジェクトの場合、この手順により *UwpSurface.exe* プロセスが開始します。 Windows ビルド 16299 以降を対象とする WPF プロジェクトの場合、この手順により *WpfSurface.exe* プロセスが開始します。 Windows ビルド 16299 より前の WPF または UWP バージョンの場合、この手順により *XDesProc.exe* プロセスが開始します。 

1. Visual Studio の 2 つ目のインスタンスを開きます。 2 番目のインスタンスでは、ソリューションまたはプロジェクトを開かないでください。

1. Visual Studio の 2 番目のインスタンスで、 **[デバッグ]** メニューを開き、 **[プロセスにアタッチ...]** を選択します。

1. プロジェクト タイプに応じて (前の手順を参照)、*UwpSurface.exe*、*WpfSurface.exe*、または *XDesProc.exe* プロセスを、使用可能なプロセスの一覧から選択します。

1. **[プロセスにアタッチ]** ダイアログの **[アタッチ先]** フィールドで、デバッグするカスタム コントロールに対して適切なコードの種類を選択します。

   カスタム コントロールが .NET 言語で記述されている場合は、 **[マネージド (CoreCLR)]** など、適切な .NET コードの種類を選択します。 カスタム コントロールが C++ で記述されている場合は、 **[ネイティブ]** を選択します。

1. **[アタッチ]** ボタンをクリックして、Visual Studio の 2 番目のインスタンスをアタッチします。

1. Visual Studio の 2 番目のインスタンスで、デバッグするカスタム コントロールに関連付けられているコード ファイルを開きます。 ソリューションまたはプロジェクト全体ではなく、ファイルのみを開いてください。

1. 前に開いたファイルに必要なブレークポイントを設定します。

1. Visual Studio の最初のインスタンス内で、デバッグするカスタム コントロール (前の手順で開いたものと同じページ) を含む XAML ページを閉じます。

1. Visual Studio の最初のインスタンスで、前の手順で閉じた XAML ページを開きます。 これにより、Visual Studio の 2 番目のインスタンスに設定した最初のブレークポイントでデバッガーが停止します。

1. Visual Studio の 2 番目のインスタンス内でコードをデバッグします。

## <a name="see-also"></a>関連項目
- [デバッガーでのはじめに](../debugger/debugger-feature-tour.md)
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
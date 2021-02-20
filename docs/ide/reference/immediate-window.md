---
title: イミディエイト ウィンドウ
description: '[イミディエイト] ウィンドウを使用して、式のデバッグと評価、ステートメントの実行、変数値の出力を行う方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 02/25/2019
ms.topic: reference
dev_langs:
- VB
f1_keywords:
- VS.ImmediateWindow
helpviewer_keywords:
- design-time expression evaluation
- Immediate window
- first-chance exception notifications
ms.assetid: d33e7937-73f3-4c69-9df0-777a8713c6f2
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 73d3d2cc42e958c59ef058a1f69921145ea18475
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99852480"
---
# <a name="immediate-window"></a>イミディエイト ウィンドウ

**[イミディエイト]** ウィンドウは、式のデバッグと評価、ステートメントの実行、変数値の出力のために使用します。 **[イミディエイト]** ウィンドウでは、現在選択されているプロジェクトをビルドして使用することで式を評価します。

**[イミディエイト]** ウィンドウを表示するには、編集用にプロジェクトを開いて、**[デバッグ]** > **[ウィンドウ]** > **[イミディエイト]** の順に選択するか、**Ctrl**+**Alt**+**I** キーを押します。 また、**[コマンド]** ウィンドウに「**Debug.Immediate**」と入力することもできます。

**[イミディエイト]** ウィンドウは、IntelliSense をサポートしています。

## <a name="display-the-values-of-variables"></a>変数の値を表示する

**[イミディエイト]** ウィンドウは、アプリをデバッグするときに特に役に立ちます。 たとえば、`varA` 変数の値を確認するには、[Print コマンド](../../ide/reference/print-command.md)を使用します。

```cmd
>Debug.Print varA
```

疑問符 (?) は`Debug.Print` のエイリアスであるため、このコマンドは次のように書き換えることもできます。

```cmd
? varA
```

コマンドをどちらで入力した場合でも、変数 `varA` の値が返されます。

> [!TIP]
> **[イミディエイト]** ウィンドウで Visual Studio コマンドを発行するには、コマンドの先頭に大なり記号 (>) を付ける必要があります。 複数のコマンドを入力するには、[コマンド ウィンドウ](command-window.md)に切り替えます。

## <a name="design-time-expression-evaluation"></a>デザイン時の式評価

**[イミディエイト]** ウィンドウを使用すると、デザイン時に関数またはサブルーチンを実行できます。

### <a name="execute-a-function-at-design-time"></a>デザイン時に関数を実行する

1. 次のコードを Visual Basic コンソール アプリにコピーします。

   ```vb
   Module Module1

       Sub Main()
           MyFunction(5)
       End Sub

       Function MyFunction(ByVal input as Integer) As Integer
           Return input * 2
       End Function

   End Module
   ```

2. **[デバッグ]** メニューの **[ウィンドウ]** > **[イミディエイト]** の順に選択します。

3. **[イミディエイト]** ウィンドウに「`?MyFunction(2)`」と入力し、**Enter** キーを押します。

    **[イミディエイト]** ウィンドウで `MyFunction` が実行され、`4` と表示されます。

関数またはサブルーチンにブレークポイントが含まれている場合、適切なポイントで実行が中断されます。 デバッガー ウィンドウを使用して、プログラムの状態を確認できます。 詳細については、「[チュートリアル:デザイン時のデバッグ](../../debugger/walkthrough-debugging-at-design-time.md)」をご覧ください。

デザイン時の式の評価は、実行時環境の起動を必要とするプロジェクトの種類 (Visual Studio Tools for Office プロジェクト、Web プロジェクト、スマート デバイス プロジェクト、SQL プロジェクトなど) には使用できません。

### <a name="design-time-expression-evaluation-in-multi-project-solutions"></a>デザイン時の式の評価 (複数のプロジェクトから成るソリューションの場合)

デザイン時の式の評価におけるコンテキストを設定する際、Visual Studio はソリューション エクスプローラーで現在選択されているプロジェクトを参照します。 ソリューション エクスプローラーでプロジェクトが選択されていない場合、Visual Studio はスタートアップ プロジェクトで関数を評価します。 現在のコンテキストで関数を評価できない場合は、エラー メッセージが表示されます。 ソリューションのスタートアップ プロジェクト以外のプロジェクトで関数を評価しようとしていたときにエラーを受け取った場合は、ソリューション エクスプローラーで評価対象プロジェクトを選択し、再度評価を試みてください。

## <a name="enter-commands"></a>コマンドを入力する

**[イミディエイト]** ウィンドウで Visual Studio コマンドを発行するときは、大なり記号 (>) を入力する必要があります。 **上方向** キーおよび **下方向** キーを使用して、以前に使用したコマンドの間をスクロールします。

|タスク|解決策|例|
|----------|--------------|-------------|
|式を評価する。|式の先頭に疑問符 (?) を付けます。|`? a+b`|
|イミディエイト モードの場合に、一時的にコマンド モードに移行して 1 つのコマンドを実行する。|先頭に不等号 (>) を付けてコマンドを入力します。|`>alias`|
|[コマンド] ウィンドウに切り替る。|先頭に不等号 (>) を付けて、ウィンドウに「`cmd`」と入力します。|`>cmd`|
|[イミディエイト] ウィンドウに戻る。|不等号 (>) を付けずにウィンドウに「`immed`」と入力します。|`immed`|

## <a name="mark-mode"></a>マーク モード

**[イミディエイト]** ウィンドウで、既に出力されている任意の行をクリックすると、自動的にマーク モードに切り替わります。 これにより、テキスト エディターでの操作と同じように、既に入力されたコマンドのテキストを選択、編集、およびコピーし、現在の行に貼り付けることができます。

## <a name="examples"></a>例

次の例は、Visual Basic プロジェクトの **[イミディエイト]** ウィンドウの 4 つの式とその結果を示しています。

```cmd
j = 2
Expression has been evaluated and has no value

? j
2

j = DateTime.Now.Day
Expression has been evaluated and has no value

? j
26
```

## <a name="first-chance-exception-notifications"></a>初回例外通知

設定の構成によっては、**[イミディエイト]** ウィンドウに初回例外通知が表示されることがあります。

### <a name="toggle-first-chance-exception-notifications-in-the-immediate-window"></a>[イミディエイト] ウィンドウで初回例外通知を切り替える

1. **[表示]** メニューの **[その他のウィンドウ]** をポイントし、**[出力]** をクリックします。

2. **[出力]** ウィンドウのテキスト領域で右クリックし、**[例外メッセージ]** をクリックして選択または選択解除します。

## <a name="see-also"></a>関連項目

- [デバッガーでのコード間の移動](../../debugger/navigating-through-code-with-the-debugger.md)
- [コマンド ウィンドウ](../../ide/reference/command-window.md)
- [デバッガーでのはじめに](../../debugger/debugger-feature-tour.md)
- [チュートリアル: デザイン時のデバッグ](../../debugger/walkthrough-debugging-at-design-time.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)
- [Visual Studio での正規表現の使用](../../ide/using-regular-expressions-in-visual-studio.md)

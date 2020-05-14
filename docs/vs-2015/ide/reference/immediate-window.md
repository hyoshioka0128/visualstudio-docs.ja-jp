---
title: イミディエイト ウィンドウ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ImmediateWindow
helpviewer_keywords:
- design-time expression evaluation
- Immediate window
- first-chance exception notifications
ms.assetid: d33e7937-73f3-4c69-9df0-777a8713c6f2
caps.latest.revision: 28
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3177c92713f6fdeb9b9b8a47a0da38608714174d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651279"
---
# <a name="immediate-window"></a>イミディエイト ウィンドウ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

**[イミディエイト]** ウィンドウは、式のデバックと評価、ステートメントの実行、変数値の出力などのために使用します。 このモードでは、デバッグ時に、開発言語で評価または実行される式を入力できます。 **[イミディエイト]** ウィンドウを表示するには、編集用にプロジェクトを開いて、 **[デバッグ]** メニューの **[ウィンドウ]** をポイントし、 **[イミディエイト]** をクリックするか、Ctrl キーと Alt キーを押しながら I キーを押します。

 このウィンドウは、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] コマンドを個別に実行するために使用できます。 使用できるコマンドには、`EvaluateStatement` があります。このコマンドは、変数に値を割り当てるのに使用できます。 **[イミディエイト]** ウィンドウは、IntelliSense もサポートしています。

## <a name="displaying-the-values-of-variables"></a>変数の値の表示
 このウィンドウはアプリケーションをデバッグするときに特に役に立ちます。 たとえば、`varA` 変数の値を確認するには、[Print コマンド](../../ide/reference/print-command.md)を使用します。

```
>Debug.Print varA
```

 疑問符 (?) は`Debug.Print` のエイリアスであるため、このコマンドは次のように書き換えることもできます。

```
>? varA
```

 コマンドをどちらで入力した場合でも、変数 `varA` の現在の値が返されます。

> [!NOTE]
> **[イミディエイト]** ウィンドウで [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] コマンドを実行するには、コマンドの先頭に不等号 (>) を付ける必要があります。 複数のコマンドを入力するには、 **[コマンド]** ウィンドウに切り替えます。

## <a name="design-time-expression-evaluation"></a>デザイン時の式の評価
 **[イミディエイト]** ウィンドウを使用すると、デザイン時に関数またはサブルーチンを実行できます。

#### <a name="to-execute-a-function-at-design-time"></a>デザイン時に関数を実行するには

1. 次のコードを [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] コンソール アプリケーションにコピーします。

   ```
   Module Module1

       Sub Main()
           MyFunction(5)
       End Sub

       Function MyFunction(ByVal input as Integer) As Integer
           Return input * 2
       End Function

   End Module
   ```

2. **[デバッグ]** メニューの **[ウィンドウ]** をポイントし、 **[イミディエイト]** をクリックします。

3. **[イミディエイト]** ウィンドウで「`?MyFunction(2)`」と入力し、Enter キーを押します。

    **[イミディエイト]** ウィンドウで `MyFunction` が実行され、`4` と表示されます。

   関数またはサブルーチンにブレークポイントが含まれているとき、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] は適切なポイントで実行を中断します。 デバッガー ウィンドウを使用して、プログラムの状態を確認できます。 詳細については、「[チュートリアル: デザイン時のデバッグ](../../debugger/walkthrough-debugging-at-design-time.md)」を参照してください。

   デザイン時の式の評価は、実行時環境の起動を必要とするプロジェクトの種類 ([!INCLUDE[trprVSTOshort](../../includes/trprvstoshort-md.md)] プロジェクト、Web プロジェクト、スマート デバイス プロジェクト、SQL プロジェクトなど) には使用できません。

### <a name="design-time-expression-evaluation-in-multi-project-solutions"></a>デザイン時の式の評価 (複数のプロジェクトから成るソリューションの場合)
 デザイン時の式の評価におけるコンテキストを設定する際、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] はソリューション エクスプローラーで現在選択されているプロジェクトを参照します。 ソリューション エクスプローラーでプロジェクトが選択されていない場合、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] はスタートアップ プロジェクトで関数を評価します。 現在のコンテキストで関数を評価できない場合は、エラー メッセージが表示されます。 ソリューションのスタートアップ プロジェクト以外のプロジェクトで関数を評価しようとしていたときにエラーを受け取った場合は、ソリューション エクスプローラーで評価対象プロジェクトを選択し、再度評価を試みてください。

## <a name="entering-commands"></a>コマンドの入力
 **[イミディエイト]** ウィンドウで [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] コマンドを実行するときは、不等号 (>) を入力する必要があります。 上方向キーおよび下方向キーを使用して、以前に入力したコマンドの間をスクロールします。

|タスク|解決策:|例|
|----------|--------------|-------------|
|式を評価する。|式の先頭に疑問符 (?) を付けます。|`? a+b`|
|イミディエイト モードの場合に、一時的にコマンド モードに移行して 1 つのコマンドを実行する。|先頭に不等号 (>) を付けてコマンドを入力します。|`>alias`|
|[コマンド] ウィンドウに切り替る。|先頭に不等号 (>) を付けて、ウィンドウに「`cmd`」と入力します。|`>cmd`|
|[イミディエイト] ウィンドウに戻る。|不等号 (>) を付けずにウィンドウに「`immed`」と入力します。|`immed`|

## <a name="mark-mode"></a>マーク モード
 **[イミディエイト]** ウィンドウで、既に出力されている任意の行をクリックすると、自動的にマーク モードに切り替わります。 これにより、テキスト エディターでの操作と同じように、既に入力されたコマンドのテキストを選択、編集、およびコピーし、現在の行に貼り付けることができます。

## <a name="the-equals--sign"></a>等号 (=)
 `EvaluateStatement` コマンドをどのウィンドウに入力するかによって、等号 (=) を比較演算子として解釈するのか、代入演算子として解釈するのかが決まります。

 **[イミディエイト]** ウィンドウの場合、等号 (=) は、代入演算子と解釈されます。 したがって、たとえば次のコマンド

```
>Debug.EvaluateStatement(varA=varB)
```

 では、変数 `varA` に変数 `varB` の値が代入されます。

 **[コマンド]** ウィンドウの場合、等号 (=) は、比較演算子と解釈されます。 **[コマンド]** ウィンドウでは、代入演算は使用できません。 したがって、たとえば変数 `varA` と変数 `varB` の値が異なる場合、次のコマンド

```
>Debug.EvaluateStatement(varA=varB)
```

 は、値 `False` を返します。

## <a name="first-chance-exception-notifications"></a>初回例外通知
 設定の構成によっては、 **[イミディエイト]** ウィンドウに初回例外通知が表示されることがあります。

#### <a name="to-toggle-first-chance-exception-notifications-in-the-immediate-window"></a>[イミディエイト] ウィンドウで初回例外通知を切り替えるには

1. **[表示]** メニューの **[その他のウィンドウ]** をポイントし、 **[出力]** をクリックします。

2. **[出力]** ウィンドウのテキスト領域で右クリックし、 **[例外メッセージ]** をクリックして選択または選択解除します。

## <a name="see-also"></a>参照
 デバッガー[コマンドウィンドウ](../../ide/reference/command-window.md)[を使用したコード内](../../debugger/navigating-through-code-with-the-debugger.md)での移動[visual Studio デバッガーでのデバッグ](../../debugger/debugging-in-visual-studio.md)の[基礎](../../debugger/debugger-basics.md)[チュートリアル: デザイン時のデバッグ](../../debugger/walkthrough-debugging-at-design-time.md) [visual studio コマンドエイリアス](../../ide/reference/visual-studio-command-aliases.md)([標準)Visual Studio での式](../../ide/using-regular-expressions-in-visual-studio.md)

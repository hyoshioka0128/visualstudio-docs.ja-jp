---
description: メッセージ テキスト全文:ターゲット プロセスがコード 'code' で終了しました (関数 'function' の評価中)。
title: ターゲット プロセスがコード &apos;code&apos; で終了しました (関数 &apos;function&apos; の評価中) | Microsoft Docs
ms.date: 4/06/2018
ms.topic: error-reference
f1_keywords:
- vs.debug.error.process_exit_during_func_eval
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ba1e2e258a12c6548317b272365db67503dc3d16
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102147004"
---
# <a name="error-the-target-process-exited-with-code-39code39-while-evaluating-the-function-39function39"></a>エラー :ターゲット プロセスがコード &#39;code&#39 で終了しました (関数 &#39;function&#39; の評価中)。

メッセージ テキスト全文:ターゲット プロセスがコード 'code' で終了しました (関数 'function' の評価中)。

デバッガーでは、.NET オブジェクトの状態が簡単に検査されるよう、デバッグ対象のプロセスで追加のコード (通常はプロパティの getter メソッドと `ToString` 関数) の実行が自動強制されます。 ほとんどのシナリオでは、これらの関数は正常に完了するか、例外がスローされてデバッガーによってキャッチされます。 ただし、カーネルの境界を越える場合や、ユーザー メッセージ ポンプが必要な場合、または回復できない場合など、例外がキャッチされない状況もあります。 結果として、(たとえば、`ExitProcess()` を呼び出して) プロセスを明示的に終了したり、キャッチできないハンドルされない例外(`StackOverflowException` など) をスローしたりするコードを実行するプロパティ getter または ToString メソッドによって、デバッグ対象のプロセスが終了され、デバッグ セッションが終了されてしまいます。 このエラー メッセージが表示された場合は、これが発生しています。

この問題の一般的な理由の 1 つは、デバッガーでそれ自体が呼び出されるプロパティが評価されるときに、スタック オーバーフローの例外が発生する可能性があるためです。 スタック オーバーフローの例外は復旧できないため、ターゲット プロセスは終了してしまいます。

## <a name="to-correct-this-error"></a>このエラーを解決するには

この問題には、次の 2 つの対応策があります。

### <a name="solution-1-prevent-the-debugger-from-calling-the-getter-property-or-tostring-method"></a>対応策 #1:デバッガーで getter プロパティまたは ToString メソッドが呼び出されないようにする 

エラー メッセージには、デバッガーが呼び出そうとした関数名が表示されます。 この関数名を使用し、**イミディエイト** ウィンドウからその関数を再評価し、評価をデバッグします。 **イミディエイト** ウィンドウから評価する場合は、 **[自動変数]、[ローカル]、[ウォッチ]** のウィンドウからの暗黙的に評価する場合とは異なり、ハンドルされない例外でデバッガーが中断されるため、デバッグを行うことが可能です。

この関数を変更できると、デバッガーによりプロパティ getter または `ToString` メソッドが呼び出されないようにすることができます。 次のいずれかの操作を試してください。

* このメソッドを、プロパティ getter または ToString メソッドではない他の種類のコードに変更すると、この問題を解消できます。
    \- または -
* (`ToString` の場合) 型に `DebuggerDisplay` 属性を定義し、デバッガーで `ToString` 以外のものを評価させます。
    \- または -
* (プロパティ getter の場合) `[System.Diagnostics.DebuggerBrowsable(DebuggerBrowsableState.Never)]` 属性をプロパティに配置します。 これは、API の互換性のために、実際はメソッドであるが、プロパティとして残す必要があるメソッドがある場合に便利です。

このメソッドを変更できない場合は、別の手順でターゲット プロセスを中断し、再度評価をしてください。

### <a name="solution-2-disable-all-implicit-evaluation"></a>対応策 #2:暗黙的な評価をすべて無効にする

前の対応策で問題が解決しない場合は、 **[ツール]**  >  **[オプション]** に移動し、 **[デバッグ]**  >  **[全般]**  >  **[プロパティの評価とその他の暗黙的な関数の呼び出しを有効にする]** の設定をオフにします。 これにより、暗黙的な関数のほとんどが評価されなくなり、問題が解決されるはずです。

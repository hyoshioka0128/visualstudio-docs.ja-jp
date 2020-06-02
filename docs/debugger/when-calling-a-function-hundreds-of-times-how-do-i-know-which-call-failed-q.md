---
title: 関数を複数回呼び出しているときにどの呼び出しが失敗したかを見つける |Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.functions
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- conditional breakpoints
- errors [debugger], function calls
- breakpoints, troubleshooting
- errors [debugger], finding which function call failed
- failures
- location breakpoint call failures
- errors [Visual Studio], function calls
- hit counts
- function calls, failure
- functions [debugger]
- Skip Count
ms.assetid: 66cfac86-f5be-4d3a-9329-d44cd74bc586
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4d054c60c45980b3d08b09987229febb99593090
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72728049"
---
# <a name="when-calling-a-function-hundreds-of-times-how-do-i-know-which-call-failed"></a>ある関数が何回も呼び出される場合、どの呼び出しでエラーが発生するのかを調べるには
## <a name="problem-description"></a>問題の説明
 `CnvtV` という関数を呼び出すとプログラムでエラーが発生します。 プログラムでエラーが発生するまでに、その関数は 200 回から 300 回は呼び出されているようです。 `CnvtV` に位置ブレークポイントを設定すると、この関数を呼び出すたびにプログラムが停止してしまうため、このブレークポイントは使用したくありません。 どのような条件で呼び出しが失敗するのかが不明なため、条件付きブレークポイントは設定できません。 どうしたらいいのでしょうか。

## <a name="solution"></a>ソリューション
 **[ヒット カウント]** フィールドを使って、関数のブレークポイントに、絶対に到達不可能な大きい値を設定できます。 この場合、`CnvtV` 関数が 200 回から 300 回は呼び出されているようなので、 **[ヒット カウント]** に 1000 以上の値を設定します。 その後、プログラムを実行し、エラーが発生するのを待ちます。 エラーが発生したら、[ブレークポイント] ウィンドウを開き、ブレークポイントの一覧を確認します。 `CnvtV` に設定されたブレークポイントは、次のように、後ろにヒット カウントと残りの繰り返し回数が付いた状態で表示されます。

```cpp
CnvtV(int) (no condition) when hit count is equal to 1000 (currently 101)
```

 この関数は、101 回目の呼び出しで失敗したことがわかります。 ヒット カウントを 101 にしてブレークポイントを設定し直し、プログラムを再び実行します。すると、エラーの原因となった `CnvtV` 呼び出しのところでプログラムが停止します。

## <a name="see-also"></a>関連項目
- [ネイティブ コードのデバッグに関する FAQ](../debugger/debugging-native-code-faqs.md)
- [ブレークポイントの設定](https://msdn.microsoft.com/library/fe4eedc1-71aa-4928-962f-0912c334d583)
- [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)

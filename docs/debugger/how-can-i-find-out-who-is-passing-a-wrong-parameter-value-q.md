---
title: 不正なパラメーター値が渡された原因を見つける | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.parameters
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [C++], parameters
- parameters [debugger]
- passing parameters, troubleshooting wrong values
- functions [debugger], detecting wrong parameter values
- parameter values, troubleshooting
ms.assetid: 1f1ae455-0e25-4e9d-b33f-53908f5bd6ce
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 42884cd6498f00cfe2df2d0396ff9ea6b03c2f98
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72734241"
---
# <a name="how-can-i-find-out-who-is-passing-a-wrong-parameter-value"></a>引数に不正な値が渡された原因を見つけるには
## <a name="problem-description"></a>問題の説明
 関数の 1 つに誤った引数値が渡されていることが判明しました。 この関数は頻繁に呼び出されます。 この関数に誤った値が渡されている場所を特定するにはどうしたらいいのでしょうか。

## <a name="solution"></a>ソリューション

#### <a name="to-resolve-this-problem"></a>この問題を解決するには

1. 関数の先頭に位置ブレークポイントを設定します。

2. ブレークポイントを右クリックし、 **[条件]** をクリックします。

3. **[ブレークポイントの条件]** ダイアログ ボックスで、 **[条件]** チェック ボックスをオンにします。 [高度なブレークポイント](../debugger/using-breakpoints.md#BKMK_Specify_a_breakpoint_condition_using_a_code_expression)に関する記事を参照してください。

4. テキスト ボックスに `Var==3` などの式を入力します (`Var` は不適切な値が格納されるパラメーターの名前、`3` はこのパラメーターに渡される不適切な値)。

5. **[true の場合]** オプション ボタンをクリックし、 **[OK]** をクリックします。

6. そして、再びプログラムを実行します。 `Var` パラメーターの値が `3` になると、ブレークポイントによって、その関数の先頭でプログラムの実行が停止します。

7. 次に、[呼び出し履歴] ウィンドウを使用して呼び出し元の関数を見つけ、その関数のソース コードに移動します。 詳細については、[[呼び出し履歴] ウィンドウを使用する](../debugger/how-to-use-the-call-stack-window.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ネイティブ コードのデバッグに関する FAQ](../debugger/debugging-native-code-faqs.md)
- [ブレークポイント](https://msdn.microsoft.com/library/fe4eedc1-71aa-4928-962f-0912c334d583)
- [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)
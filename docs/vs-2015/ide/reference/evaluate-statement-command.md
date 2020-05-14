---
title: Evaluate Statement コマンド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.evaluatestatement
helpviewer_keywords:
- Debug.EvaluateStatement command
- Evaluate Statement command
ms.assetid: 032039bc-9477-4f93-9b9d-66d4be0e90f4
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6e2db8596c1c16f5c9fb54a8c7c867b06e997b7b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72657710"
---
# <a name="evaluate-statement-command"></a>Evaluate Statement コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定したステートメントを評価し、表示します。

## <a name="syntax"></a>構文

```
Debug.EvaluateStatement text
```

## <a name="arguments"></a>引数
 `text` 必須。 評価するステートメント。

## <a name="remarks"></a>解説
 **EvaluateStatement** コマンドをどのウィンドウに入力するかによって、等号 (=) を比較演算子として解釈するのか、代入演算子として解釈するのかが決まります。

 **[コマンド]** ウィンドウの場合、等号 (=) は、比較演算子と解釈されます。 したがって、たとえば変数 `a` と変数 `b` の値が異なる場合、次のコマンド

```
>Debug.EvaluateStatement(a=b)
```

 は、値 `false` を返します。

 一方、 **[イミディエイト]** ウィンドウの場合、等号 (=) は、代入演算子と解釈されます。 したがって、たとえば次のコマンド

```
>Debug.EvaluateStatement(a=b)
```

 では、変数 `a` に変数 `b` の値が代入されます。

## <a name="example"></a>例

```
>Debug.EvaluateStatement(a+b)
```

## <a name="see-also"></a>関連項目
 [[印刷] コマンド](../../ide/reference/print-command.md) [Visual studio](../../ide/reference/visual-studio-commands.md)の [コマンド[] ウィンドウ](../../ide/reference/command-window.md)の[[検索]/[コマンド] ボックス](../../ide/find-command-box.md) [visual studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)

---
title: Print コマンド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.print
helpviewer_keywords:
- Debug.Print command
- Print method
- Print command
ms.assetid: 0412d381-590a-483f-bab4-6e1cca095645
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 136edf7fa91e4caeb9303edfd4441ee178fa6038
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72662152"
---
# <a name="print-command"></a>Print コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

式を評価するか、指定したテキストを表示します。

## <a name="syntax"></a>構文

```
Debug.Print text
```

## <a name="arguments"></a>引数
 `text` 必須。 評価対象の式または表示対象のテキストです。

## <a name="remarks"></a>解説
 このコマンドのエイリアスとして疑問符 (?) を使用できます。 したがって、たとえば次のコマンド

```
>Debug.Print expA
```

 は、次のように記述することもできます。

```
>? expA
```

 どちらのコマンドでも、式 `expA` の現在の値が返されます。

## <a name="example"></a>例

```
>Debug.Print varA
```

## <a name="see-also"></a>参照
 [Evaluate Statement コマンド](../../ide/reference/evaluate-statement-command.md) [visual Studio](../../ide/reference/visual-studio-commands.md)のコマンド [ウィンドウ](../../ide/reference/command-window.md)の [[検索]/[コマンド] ボックス](../../ide/find-command-box.md) [visual studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)

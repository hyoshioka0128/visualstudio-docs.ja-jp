---
title: SetRadix コマンド | Microsoft ドキュメント
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.setradix
helpviewer_keywords:
- Set Radix command
- Debug.SetRadix command
ms.assetid: 6ffd1554-7530-4da4-b5f5-e276a5034f3b
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 050cbe6e639f4177694d9af3ecbc0b768065b7d9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72665418"
---
# <a name="set-radix-command"></a>SetRadix コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

整数値を表示するために使用する基数値を設定または返します。

## <a name="syntax"></a>構文

```
Debug.SetRadix [10 | 16 | hex | dec]
```

## <a name="arguments"></a>引数
 `10` またはまたはまたは `16` `hex` `dec` 省略可能。 10 (10 または dec) 進数または 16 (16 または hex) 進数を示します。 引数を省略すると、現在の基数値が返されます。

## <a name="example"></a>例
 この例では、整数値を 16 進形式で表示するための環境を設定します。

```
>Debug.SetRadix hex
```

## <a name="see-also"></a>参照
 [Visual Studio コマンド](../../ide/reference/visual-studio-commands.md)の [コマンドウィンドウ](../../ide/reference/command-window.md)の [検索/コマンドボックス](../../ide/find-command-box.md) [visual studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)

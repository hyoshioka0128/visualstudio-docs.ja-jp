---
title: ListThreads コマンド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.listthreads
helpviewer_keywords:
- ListThreads command
- list threads command
- Debug.ListThreads command
ms.assetid: 34b665c0-d46f-4c1a-a066-b678eba5ac54
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: fc11479901785b19235e0962d3ae90e552e5b33b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671136"
---
# <a name="list-threads-command"></a>ListThreads コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

現在のプログラムのスレッド一覧を表示します。

## <a name="syntax"></a>構文

```
Debug.ListThreads [index]
```

## <a name="arguments"></a>引数
 `index` 省略可能。 スレッドをインデックスで選択して、現在のスレッドにします。

## <a name="remarks"></a>解説
 指定した場合、`index` 引数により、示されたスレッドが現在のスレッドとしてマークされます。 一覧の現在のスレッドの横にはアスタリスク (*) が表示されます。

## <a name="example"></a>例

```
>Debug.ListThreads
```

## <a name="see-also"></a>関連項目
 [呼び出し履歴の一覧表示](../../ide/reference/list-call-stack-command.md)[コマンドリストの逆アセンブリコマンド](../../ide/reference/list-disassembly-command.md) [visual Studio コマンド](../../ide/reference/visual-studio-commands.md)[コマンドウィンドウ](../../ide/reference/command-window.md)の[[検索]/[コマンド] ボックス](../../ide/find-command-box.md) [visual studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)

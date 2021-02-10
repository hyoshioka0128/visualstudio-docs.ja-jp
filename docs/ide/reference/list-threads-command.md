---
title: ListThreads コマンド
description: ListThreads コマンドと、それを使用して現在のプログラム内のスレッドの一覧を表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.listthreads
helpviewer_keywords:
- ListThreads command
- list threads command
- Debug.ListThreads command
ms.assetid: 34b665c0-d46f-4c1a-a066-b678eba5ac54
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f3abcd7182c8bb5b94b2f35a9463f845cc6bb5bd
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99919388"
---
# <a name="list-threads-command"></a>ListThreads コマンド
現在のプログラムのスレッド一覧を表示します。

## <a name="syntax"></a>構文

```
Debug.ListThreads [index]
```

## <a name="arguments"></a>引数
`index`

任意。 スレッドをインデックスで選択して、現在のスレッドにします。

## <a name="remarks"></a>注釈
指定した場合、`index` 引数により、示されたスレッドが現在のスレッドとしてマークされます。 一覧の現在のスレッドの横にはアスタリスク (*) が表示されます。

## <a name="example"></a>例

```
>Debug.ListThreads
```

## <a name="see-also"></a>関連項目

- [ListCallStack コマンド](../../ide/reference/list-call-stack-command.md)
- [ListDisassembly コマンド](../../ide/reference/list-disassembly-command.md)
- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [コマンド ウィンドウ](../../ide/reference/command-window.md)
- [検索コマンド ボックス](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)

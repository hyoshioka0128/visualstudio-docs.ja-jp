---
title: List Registers コマンド
description: List Registers コマンドと、これにより、選択したレジスタの値を表示する方法、および表示されるレジスタの一覧を変更する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.listregisters
helpviewer_keywords:
- list registers command
- Debug.ListRegisters command
- ListRegisters command
ms.assetid: 19a9d789-f6c9-46b3-b1f6-4934fc33e055
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5459ded60ea90ae00a3f943f829065a82548d160
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2020
ms.locfileid: "96305295"
---
# <a name="list-registers-command"></a>List Registers コマンド
選択したレジスタの値を表示するほか、表示されるレジスタの一覧を変更できます。

## <a name="syntax"></a>構文

```cmd
Debug.ListRegisters [/Display [{register|registerGroup}...]] [/List]
[/Watch [{register|registerGroup}...]]
[/Unwatch [{register|registerGroup}...]]
```

## <a name="switches"></a>スイッチ
/Display [{`register`&#124;`registerGroup`}...]

指定した `register` または `registerGroup` の値を表示します。 `register` も `registerGroup` も指定されていない場合は、レジスタの既定の一覧が表示されます。 スイッチが指定されていない場合、動作は同じです。 次に例を示します。

`Debug.ListRegisters /Display eax`

上記の式は、次の式と同じです。

`Debug.ListRegisters eax`

/List

すべてのレジスタ グループが一覧に表示されます。

/Watch [{`register`&#124;`registerGroup`}...]

1 つ以上の `register` または `registerGroup` の値が一覧に追加されます。

/Unwatch [{`register`&#124;`registerGroup`}...]

1 つ以上の `register` または `registerGroup` の値が一覧から削除されます。

## <a name="remarks"></a>注釈
エイリアス `r` を `Debug.ListRegisters` の代わりに使用できます。

## <a name="example"></a>例
この例では、`Debug.ListRegisters` のエイリアス `r` を使用して、レジスタ グループ `Flags` の値を表示します。

```cmd
r /Display Flags
```

## <a name="see-also"></a>関連項目

- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [デバッグの基礎:[レジスタ] ウィンドウ](../../debugger/debugging-basics-registers-window.md)
- [方法: [レジスタ] ウィンドウを使用する](../../debugger/how-to-use-the-registers-window.md)

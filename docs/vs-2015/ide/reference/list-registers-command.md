---
title: List Registers コマンド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.listregisters
helpviewer_keywords:
- list registers command
- Debug.ListRegisters command
- ListRegisters command
ms.assetid: 19a9d789-f6c9-46b3-b1f6-4934fc33e055
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3476244d3044eb80dbfce3559479421b012cc5fa
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659500"
---
# <a name="list-registers-command"></a>List Registers コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

選択したレジスタの値を表示するほか、表示されるレジスタの一覧を変更できます。

## <a name="syntax"></a>構文

```
Debug.ListRegisters [/Display [{register|registerGroup}...]] [/List]
[/Watch [{register|registerGroup}...]]
[/Unwatch [{register|registerGroup}...]]
```

## <a name="switches"></a>スイッチ
 /Display [{`register`&#124; `registerGroup`}...]指定した `register` または `registerGroup` の値を表示します。 `register` も `registerGroup` も指定されていない場合は、レジスタの既定の一覧が表示されます。 スイッチが指定されていない場合、動作は同じです。 (例:

 `Debug.ListRegisters /Display eax`

 上記の式は、次の式と同じです。

 `Debug.ListRegisters eax`

 /List すべてのレジスタグループを一覧に表示します。

 /Watch [{`register`&#124; `registerGroup`}...]リストに1つ以上の `register` または `registerGroup` 値を追加します。

 /Unwatch [{`register`&#124; `registerGroup`}...]1つ以上の `register` または `registerGroup` 値を一覧から削除します。

## <a name="remarks"></a>Remarks
 エイリアス `r` を `Debug.ListRegisters` の代わりに使用できます。

## <a name="example"></a>例
 この例では、`Debug.ListRegisters` のエイリアス `r` を使用して、レジスタ グループ `Flags` の値を表示します。

```
r /Display Flags
```

## <a name="see-also"></a>参照
 [Visual Studio コマンド](../../ide/reference/visual-studio-commands.md)の[デバッグの基本: レジスタウィンドウ](../../debugger/debugging-basics-registers-window.md)[方法: [レジスタ] ウィンドウを使用](../../debugger/how-to-use-the-registers-window.md)する

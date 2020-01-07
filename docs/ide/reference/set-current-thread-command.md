---
title: SetCurrentThread コマンド
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.setcurrentthread
helpviewer_keywords:
- Set Current Thread command
- Debug.SetCurrentThread command
ms.assetid: 9917ed1d-6c30-4d94-b2f0-69acce74f1b2
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0d782a507d57e459aa5735cf34717f13e41d4cde
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72748616"
---
# <a name="set-current-thread-command"></a>SetCurrentThread コマンド
指定したスレッドを現在のスレッドとして設定します。

## <a name="syntax"></a>構文

```
Debug.SetCurrentThread index
```

## <a name="arguments"></a>引数
`index`

必須です。 スレッドをそのインデックスで選択します。

## <a name="example"></a>例

```
>Debug.SetCurrentThread 1
```

## <a name="see-also"></a>関連項目

- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [コマンド ウィンドウ](../../ide/reference/command-window.md)
- [検索コマンド ボックス](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)

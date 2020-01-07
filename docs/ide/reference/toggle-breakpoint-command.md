---
title: ToggleBreakpoint コマンド
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.togglebreakpoint
helpviewer_keywords:
- ToggleBreakpoint command
- Debug.ToggleBreakPoint command
- Toggle Breakpoint command
ms.assetid: d50dfadb-ce79-4d5e-9c09-1cfddd57876d
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a8294c25bcf3b62f9d6480e170d4693a9be85079
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72748577"
---
# <a name="toggle-breakpoint-command"></a>ToggleBreakpoint コマンド
ファイル内の現在位置で、現在の状態に基づいてブレークポイントのオン/オフを切り替えます。

## <a name="syntax"></a>構文

```
Debug.ToggleBreakpoint [text]
```

## <a name="arguments"></a>引数

`text`\
任意。 テキストを指定すると、行が名前付きのブレークポイントとしてマークされます。 それ以外の場合は、行は名前のないブレークポイントとしてマークされ、これは F9 キーを押したときの動作に似ています。

## <a name="example"></a>例
次の例では、現在のブレークポイントを切り替えます。

```
>Debug.ToggleBreakpoint
```

## <a name="see-also"></a>関連項目

- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [コマンド ウィンドウ](../../ide/reference/command-window.md)
- [検索コマンド ボックス](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)

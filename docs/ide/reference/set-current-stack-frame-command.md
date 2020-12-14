---
title: SetCurrentStackFrame コマンド
description: SetCurrentStackFrame コマンドについて、およびそれを使用して特定のスタック フレームを設定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.setcurrentstackframe
helpviewer_keywords:
- Set Current Stack Frame command
- Debug.SetCurrentStackFrame command
ms.assetid: 3dcf52c0-6781-4598-bac2-0094dce67c20
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 032602744247ded5cb38d8a3ae3e1157ccbc5cee
ms.sourcegitcommit: 2cf87f79762906ccaa133a7645aa4c77a0bed7da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2020
ms.locfileid: "96616604"
---
# <a name="set-current-stack-frame-command"></a>SetCurrentStackFrame コマンド
特定のスタック フレームを設定できます。

## <a name="syntax"></a>構文

```cmd
Debug.SetCurrentStackFrame index
```

## <a name="arguments"></a>引数
`index`

必須です。 インデックスでスタック フレームを選びます。

## <a name="example"></a>例

```cmd
>Debug.SetCurrentStackFrame 1
```

## <a name="see-also"></a>関連項目

- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [コマンド ウィンドウ](../../ide/reference/command-window.md)
- [検索コマンド ボックス](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)
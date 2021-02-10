---
title: EvaluateStatement
description: Evaluate Statement コマンドと、これにより、指定したステートメントを評価して表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/25/2019
ms.topic: reference
f1_keywords:
- debug.evaluatestatement
helpviewer_keywords:
- Debug.EvaluateStatement command
- Evaluate Statement command
ms.assetid: 032039bc-9477-4f93-9b9d-66d4be0e90f4
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4aec65a1460203d3c02ed75c40e82256151703ba
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99907536"
---
# <a name="evaluate-statement-command"></a>ステートメントの評価コマンド

指定したステートメントを評価し、表示します。

## <a name="syntax"></a>構文

```cmd
>Debug.EvaluateStatement text
```

## <a name="arguments"></a>引数

`text`

必須です。 評価するステートメント。

## <a name="example"></a>例

```cmd
>Debug.EvaluateStatement args.Length
```

## <a name="see-also"></a>関連項目

- [Print コマンド](../../ide/reference/print-command.md)
- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [コマンド ウィンドウ](../../ide/reference/command-window.md)
- [検索コマンド ボックス](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)

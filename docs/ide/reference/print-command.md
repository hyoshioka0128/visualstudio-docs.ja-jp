---
title: Debug.Print
description: Print コマンドと、それを使用して式を評価したり、指定したテキストを表示したりする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.print
helpviewer_keywords:
- Debug.Print command
- Print method
- Print command
ms.assetid: 0412d381-590a-483f-bab4-6e1cca095645
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 08150654a7a4f062555a1d12382b9d51aacca25f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99932034"
---
# <a name="print-command"></a>Print コマンド

式を評価するか、指定したテキストを表示します。

## <a name="syntax"></a>構文

```cmd
>Debug.Print text
```

## <a name="arguments"></a>引数

`text`

必須です。 評価対象の式または表示対象のテキストです。

## <a name="remarks"></a>注釈

このコマンドのエイリアスとして疑問符 (?) を使用できます。 したがって、たとえば次のコマンド

```cmd
>Debug.Print expA
```

は、次のように記述することもできます。

```cmd
? expA
```

どちらのコマンドでも、式 `expA` の現在の値が返されます。

## <a name="example"></a>例

```cmd
>Debug.Print DateTime.Now.Day
```

## <a name="see-also"></a>関連項目

- [Evaluate Statement コマンド](../../ide/reference/evaluate-statement-command.md)
- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [コマンド ウィンドウ](../../ide/reference/command-window.md)
- [検索コマンド ボックス](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)

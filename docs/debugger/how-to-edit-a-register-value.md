---
title: レジスタ値を編集する | Microsoft Docs
description: '[レジスタ] ウィンドウで値を編集して、レジスタの内容を変更する方法について説明します (アドレス レベルのデバッグが有効になっている場合にのみ使用できます)。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.debug.register.edit
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- Registers window, editing register values
- register values
ms.assetid: e27b6bd8-e6d4-4f1d-8a86-9f4047bb1167
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4f83f67f57e67080f97a6df434f8dfc008e36892
ms.sourcegitcommit: 620d30c60da8f9805fce524fe4951cf40f28297d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97903546"
---
# <a name="how-to-edit-a-register-value-c-c-visual-basic-f"></a>方法: レジスタ値を編集する (C#、C++、Visual Basic、F#)

[レジスタ] ウィンドウは、 **[オプション]** ダイアログ ボックス、 **[デバッグ]** ノードで、アドレスレベルのデバッグが有効になっている場合にのみ、使用できます。

### <a name="to-change-the-value-of-a-register"></a>レジスタ値を変更するには

1. **[レジスタ]** ウィンドウで、Tab キーまたはマウスを使用して、変更する値にカーソルを置きます。 入力するときは、上書きする値の直前の位置にカーソルを置く必要があります。

2. 新しい値を入力します。

    > [!CAUTION]
    > レジスタ値を変更すると (特に EIP レジスタと EBP レジスタの場合は)、プログラムの実行に影響する場合があります。

    > [!CAUTION]
    > 浮動小数点値を編集すると、小数部分の 10 進とバイナリの変換により、多少の誤差が発生する場合があります。 特に影響のないように見える編集でも、浮動小数点レジスタの最下位バイトが変化する場合があります。

## <a name="see-also"></a>関連項目
- [方法: [レジスタ] ウィンドウを使用する](../debugger/how-to-use-the-registers-window.md)
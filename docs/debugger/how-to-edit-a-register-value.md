---
title: '方法: レジスタ値を編集する | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: b3ccaa124b64ad462f633e760695f931afaae531
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72733419"
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
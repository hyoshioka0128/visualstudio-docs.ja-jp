---
title: '方法: レジスタ値を編集する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.register.edit
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- Registers window, editing register values
- register values
ms.assetid: e27b6bd8-e6d4-4f1d-8a86-9f4047bb1167
caps.latest.revision: 29
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7f0cd04b054d51119f6f6c1b0275c4f781656bff
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841885"
---
# <a name="how-to-edit-a-register-value"></a>方法 : レジスタ値を編集する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[レジスタ] ウィンドウは、 **[オプション]** ダイアログ ボックス、 **[デバッグ]** ノードで、アドレスレベルのデバッグが有効になっている場合にのみ、使用できます。  
  
### <a name="to-change-the-value-of-a-register"></a>レジスタ値を変更するには  
  
1. **[レジスタ]** ウィンドウで、Tab キーまたはマウスを使用して、変更する値にカーソルを置きます。 入力するときは、上書きする値の直前の位置にカーソルを置く必要があります。  
  
2. 新しい値を入力します。  
  
    > [!CAUTION]
    > レジスタ値を変更すると (特に EIP レジスタと EBP レジスタの場合は)、プログラムの実行に影響する場合があります。  
  
    > [!CAUTION]
    > 浮動小数点値を編集すると、小数部分の 10 進とバイナリの変換により、多少の誤差が発生する場合があります。 特に影響のないように見える編集でも、浮動小数点レジスタの最下位バイトが変化する場合があります。  
  
## <a name="see-also"></a>参照  
 [方法: [レジスタ] ウィンドウを使用する](../debugger/how-to-use-the-registers-window.md)

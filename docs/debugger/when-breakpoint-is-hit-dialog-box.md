---
title: '[ブレークポイントのヒット時] ダイアログ ボックス | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.debug.whenbreakpointishit
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
- SQL
ms.assetid: 476e3d98-cf35-4338-b124-cd0f3010d854
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 53b19f4dd0d4b0cb97bb33e4895f36c4dc8f670c
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72728141"
---
# <a name="when-breakpoint-is-hit-dialog-box"></a>[ブレークポイントのヒット時] ダイアログ ボックス
このダイアログ ボックスでは、ブレークポイントにヒットしたときに発生するアクションをカスタマイズできます。

## <a name="uielement-list"></a>UIElement の一覧
 **メッセージの出力**: DebuggerDisplay 構文を使用してメッセージを出力します。 詳細については、「[DebuggerDisplay 属性の使用](../debugger/using-the-debuggerdisplay-attribute.md)」をご覧ください。

 このテキストボックスは、$ADDRESS などの特殊なキーワードもサポートしています。これらのキーワードはキーワード自身が使用することも、DebuggerDisplay 式の中かっこ ({}) 内で使用することもできます。 使用できるキーワードはダイアログ ボックスに一覧表示されます。

 **続けて実行する**: このコントロールは、 **[メッセージの出力]** が選択されている場合にだけ有効になります。 このコントロールを選択すると、ブレークポイントにヒットしたときに、これを中断するポイントとしてではなく、プログラムの実行をトレースするためのトレースポイントとして使用できます。

## <a name="see-also"></a>関連項目
- [ブレークポイントの使用](../debugger/using-breakpoints.md)
- [DebuggerDisplay 属性の使用](../debugger/using-the-debuggerdisplay-attribute.md)
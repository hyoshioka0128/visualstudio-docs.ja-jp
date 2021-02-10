---
title: '[ブレークポイントのヒット時] ダイアログ ボックス | Microsoft Docs'
description: '[ブレークポイントのヒット時] を使用して、中断するアクションを指定します。 メッセージを出力するように指定することができ、その後、その実行は続行されます。'
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: bfb5099bd0fab17cd983af4e16a435fd192a1668
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99883871"
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
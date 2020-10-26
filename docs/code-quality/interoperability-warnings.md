---
title: 移植性と相互運用性に関する警告
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.Portablityrules
- vs.codeanalysis.Interoperabilityrules
helpviewer_keywords:
- managed code analysis warnings, interoperability warnings, portability warnings
- portability warnings
- warnings, portability
- interoperability warnings
- warnings, interoperability
ms.assetid: 95de6eb3-40c4-4063-9f59-25cb70e3b2b3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 306c2477e6e5f731ed6dbf20b2cf4d03d4556467
ms.sourcegitcommit: 5caad925ca0b5d136416144a279e984836d8f28c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2020
ms.locfileid: "89509914"
---
# <a name="portability-and-interoperability-warnings"></a>移植性と相互運用性に関する警告

移植性の警告は、さまざまなプラットフォーム間での移植性をサポートします。 相互運用性の警告は、COM クライアントとの対話をサポートします。

## <a name="in-this-section"></a>このセクションの内容

| ルール | 説明 |
| - | - |
| [CA1401: P/Invoke を表示できません](../code-quality/ca1401.md) | パブリック型のパブリックメソッドまたはプロテクトメソッドには System.Runtime.InteropServices.DllImportAttribute 属性があります (Visual Basic で Declare キーワードによっても実装されています)。 このようなメソッドは公開しないでください。 |
| [CA1417: `OutAttribute` P/invoke に文字列パラメーターを使用しません](../code-quality/ca1417.md) | で値によって渡される文字列パラメーター `OutAttribute` は、文字列がインターン文字列である場合、ランタイムを不安定にする可能性があります。 |
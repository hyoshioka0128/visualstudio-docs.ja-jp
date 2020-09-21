---
title: 移植性と相互運用性に関する警告
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.Portablityrules
- vs.codeanalysis.Interoperabilityrules
helpviewer_keywords:
- managed code analysis rules, interoperability rules, portability rules
- portability rules
- rules, portability
- interoperability rules
- rules, interoperability
ms.assetid: 95de6eb3-40c4-4063-9f59-25cb70e3b2b3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b8a456f4a24339b6cba5aeec2c9fe64ad3ee278b
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2020
ms.locfileid: "90808601"
---
# <a name="portability-and-interoperability-rules"></a>移植性と相互運用性の規則

移植性ルールは、異なるプラットフォーム間での移植性をサポートします。 相互運用性規則は、COM クライアントとの対話をサポートします。

## <a name="in-this-section"></a>このセクションの内容

| ルール | 説明 |
| - | - |
| [CA1401: P/Invoke を表示できません](../code-quality/ca1401.md) | パブリック型のパブリックメソッドまたはプロテクトメソッドには System.Runtime.InteropServices.DllImportAttribute 属性があります (Visual Basic で Declare キーワードによっても実装されています)。 このようなメソッドは公開しないでください。 |
| [CA1416:プラットフォームの互換性を検証する](../code-quality/ca1416.md) | コンポーネントでプラットフォームに依存する Api を使用すると、コードがすべてのプラットフォームで動作しなくなります。 |
| [CA1417: `OutAttribute` P/invoke に文字列パラメーターを使用しません](../code-quality/ca1417.md) | で値によって渡される文字列パラメーター `OutAttribute` は、文字列がインターン文字列である場合、ランタイムを不安定にする可能性があります。 |

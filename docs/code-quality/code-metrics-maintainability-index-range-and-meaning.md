---
title: コードメトリックス-保守容易性インデックスの範囲と意味
ms.date: 1/8/2021
description: Visual Studio のコードメトリックスの保守容易性インデックス範囲メトリックについて説明します。
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 14bee6dcb522b7c1dd0475ca309b829a09c0d4ec
ms.sourcegitcommit: b1f7e7d7a0550d5c6f46adff3bddd44bc1d6ee1c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98069532"
---
# <a name="code-metrics---maintainability-index-range-and-meaning"></a>コードメトリックス-保守容易性インデックスの範囲と意味

質問: 保守容易性のインデックスが 0 ~ 100 の範囲にリセットされました。 この処理はどのように行われたのでしょうか。

メトリックは、最初は次のように計算されています。 `Maintainability Index = 171 - 5.2 * ln(Halstead Volume) - 0.23 * (Cyclomatic Complexity) - 16.2 * ln(Lines of Code)`

この数式を使用すると、171から無制限の負の数値になることが想定されていました。  コードを0にすると、コードの管理が明らかに難しくなり、0のコードと、負の値の違いは役に立たなかったということです。  負の数値の有用性が減少し、メトリックをできるだけ明確に維持するために、0個以上のインデックスを0として処理し、171以下の範囲を0から100に再設定することにしました。 このため、使用する式は次のとおりです。

   `Maintainability Index = MAX(0,(171 - 5.2 * ln(Halstead Volume) - 0.23 * (Cyclomatic Complexity) - 16.2 * ln(Lines of Code))*100 / 171)`

それに加えて、しきい値を慎重に決定することにしました。  インデックスが赤で示されている場合、コードに問題が発生したという確信度が高いということです。  これにより、次のしきい値が与えられました。

しきい値については、この0-100 の範囲80-20 を分割して、ノイズレベルを低くし、疑わしいと思われるフラグが設定されたコードのみを保持することにしました。 次のしきい値を使用しました。

- 0-9 = 赤
- 10-19 = 黄
- 20-100 = 緑

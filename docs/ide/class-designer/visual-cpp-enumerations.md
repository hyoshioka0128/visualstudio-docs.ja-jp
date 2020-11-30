---
title: クラス デザイナーの C++ 列挙体
description: クラス デザイナーで C++ 列挙型およびスコープを持つ enum クラス型がサポートされるしくみについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Class Designer [Visual Studio], enumerations
ms.assetid: 11e90ba1-18cd-44f8-9e26-e3746a7a19d1
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: b12d270884ca9877d6c1c80780a9ae96324f3af4
ms.sourcegitcommit: 86e98df462b574ade66392f8760da638fe455aa0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2020
ms.locfileid: "94903456"
---
# <a name="c-enumerations-in-class-designer"></a>クラス デザイナーの C++ 列挙体

**クラス デザイナー** では、C++ の `enum`、およびスコープを持つ `enum class` 型はサポートされていません。 たとえば次のようになります。

```cpp
enum CardSuit {
   Diamonds = 1,
   Hearts = 2,
   Clubs = 3,
   Spades = 4
};

// or...
enum class CardSuit {
   Diamonds = 1,
   Hearts = 2,
   Clubs = 3,
   Spades = 4
};
```

クラス ダイアグラムにおける C++ 列挙体の図形の形状と動作は構造体の図形に似ていますが、ラベルが **[Enum]** または **[Enum class]** である点と、青ではなくピンクである点、および左と上の余白に色つきの枠がある点が異なります。 列挙体の図形も構造体の図形も、角が直角になっています。

`enum` 型の使用法の詳細については、「[列挙型](/cpp/cpp/enumerations-cpp)」を参照してください。

## <a name="see-also"></a>参照

- [C++ のコードを操作する](working-with-visual-cpp-code.md)
- [列挙型](/cpp/cpp/enumerations-cpp)

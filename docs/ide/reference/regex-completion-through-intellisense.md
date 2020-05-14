---
title: IntelliSense メニューを使用した正規表現の入力
ms.date: 03/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 68b5cb480184a287d9fcb088b0a74ac9d607f3f2
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79093857"
---
# <a name="regex-completion-through-intellisense-menu"></a>IntelliSense メニューを使用した正規表現の入力

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**概要:** IntelliSense メニューを使用して正規表現 (regex) を入力します。

**条件:** IntelliSense を使用して正規表現を記述します。 IntelliSense によって、基本入力と、各正規表現文字の説明が示されます。 

**理由:** 正規表現の記述は簡単ではありませんが、IntelliSense を使用することで楽に記述できます。

## <a name="how-to"></a>方法

1. 正規表現文字列にカーソルを置きます。
2. **Ctrl**+**Space** キーを押して、**IntelliSense** メニューを表示します。
3. 正規表現文字列を追加する文字を選択します。

   ![IntelliSense を使用した正規表現の入力](../media/regex-completion-intellisense.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)

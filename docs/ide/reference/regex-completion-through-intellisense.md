---
title: IntelliSense メニューを使用した正規表現の入力
description: Intellisense メニューを使用して、IntelliSense を活用して正規表現を記述する方法について説明します。
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
ms.openlocfilehash: 750869abbad079f3c109113f8cd65b5e8f11c147
ms.sourcegitcommit: 2cf87f79762906ccaa133a7645aa4c77a0bed7da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2020
ms.locfileid: "96616695"
---
# <a name="regex-completion-through-intellisense-menu"></a>IntelliSense メニューを使用した正規表現の入力

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**概要:** IntelliSense メニューを使用して正規表現 (regex) を入力します。

**条件:** IntelliSense を使用して正規表現を記述します。 IntelliSense によって、基本入力と、各正規表現文字の説明が示されます。 

**理由:** 正規表現の記述は簡単ではありませんが、IntelliSense を使用することで楽に記述できます。

## <a name="how-to"></a>操作方法

1. 正規表現文字列にカーソルを置きます。
2. **Ctrl**+**Space** キーを押して、**IntelliSense** メニューを表示します。
3. 正規表現文字列を追加する文字を選択します。

   ![IntelliSense を使用した正規表現の入力](../media/regex-completion-intellisense.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)

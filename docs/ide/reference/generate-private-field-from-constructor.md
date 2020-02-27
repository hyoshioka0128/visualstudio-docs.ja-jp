---
title: コンストラクターからプライベートフィールドを生成する
ms.date: 02/19/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 8ef4188216b669b30b7af9bd725ec432bcd0a774
ms.sourcegitcommit: 3c105990656cd509062ce60e52e776c794f6305d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2020
ms.locfileid: "77529414"
---
# <a name="generate-private-field-from-constructor"></a>コンストラクターからプライベートフィールドを生成する

このリファクタリングは以下に適用されます。 

- C# 

**概要:** コンストラクターからプライベート フィールドを生成します。 

**条件:** コンストラクターからプライベート フィールドをすばやく追加したいとき。

**理由:** プライベート フィールドを記述することは、時間がかかり、反復的になることがあります。 このリファクタリングを使用すると、簡単でプログラムがより堅牢になります。

## <a name="how-to"></a>方法 

1. コンストラクター内のパラメーター名にカーソルを置きます。

2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。
   
3. **初期化フィールドを作成する**オプションを選択します。

   ![コンストラクターからプライベートフィールドを生成する](media/generate-private-field-from-constructor.png)

## <a name="see-also"></a>関連項目 

- [リファクタリング](../refactoring-in-visual-studio.md)

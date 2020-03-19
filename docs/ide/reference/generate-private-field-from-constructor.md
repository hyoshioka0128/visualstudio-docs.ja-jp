---
title: コンストラクターからプライベートフィールドを生成する
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
ms.openlocfilehash: 4eb5dd39d0fb2d4cd9ba8ade0d0408d6e36a4854
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79094019"
---
# <a name="generate-private-field-from-constructor"></a>コンストラクターからプライベートフィールドを生成する

このリファクタリングは以下に適用されます。 

- C# 

- Visual Basic

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

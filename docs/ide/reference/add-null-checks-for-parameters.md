---
title: すべて (パラメーター) に対して null チェックを追加する
ms.date: 09/17/2019
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 573a9e56d3aedd55bc571eaaa363b42a53019566
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74782343"
---
# <a name="add-null-checks-for-all-parameters"></a>すべてのパラメーターに対して null チェックを追加する 

このリファクタリングは以下に適用されます。 

- C# 

**概要:** Null 許容の、チェックされていないすべてのパラメーターに対して、null かどうかをチェックする `if` ステートメントを作成して追加します。 

**条件:** すべての適用可能なメソッド パラメーターに対して null チェックをすばやく追加する必要があります。

**理由:** 多くのパラメーターに対して null チェックを記述することは、時間がかかり、反復的になることがあります。 このリファクタリングを使用すると、簡単でプログラムがより堅牢になります。  

## <a name="how-to"></a>方法 

1. メソッド内の任意のパラメーターにカーソルを置きます。

2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

   ![クイック アクションとリファクタリング](media/add-null-checks-for-all-parameters.png)
   
3. **[Add null checks for all parameters]\(すべてのパラメーターに対して null チェックを追加する\)** オプションを選択します。

   ![すべてに対して null チェックを追加する](media/add-null-checks-for-all.png) 

## <a name="see-also"></a>関連項目 

- [リファクタリング](../refactoring-in-visual-studio.md)

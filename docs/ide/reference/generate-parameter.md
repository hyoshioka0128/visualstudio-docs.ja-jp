---
title: パラメーターの生成リファクタリング
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
ms.openlocfilehash: 372a3f705e5e85c0edb31a754105f61056402b9f
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79094348"
---
# <a name="generate-parameter"></a>パラメーターを生成する

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**概要:** メソッドのパラメーターを自動的に生成します。

**条件:** 現在のコンテキストに存在しないメソッドの変数を参照し、エラーを受け取ります。コード修正としてパラメーターを生成できます。 

**理由:** コンテキストを失わずに、メソッドのシグネチャをすばやく変更できます。

## <a name="how-to"></a>方法

1. 変数名内にカーソルを置き、**Ctrl**+ **.** キーを押して、 **[クイック アクションとリファクタリング]** メニューをトリガーします。
1. **[Generate parameter]\(パラメーターを生成する\)** を選択します。

   ![パラメーターを生成する](media/generate-parameter.png) 

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)

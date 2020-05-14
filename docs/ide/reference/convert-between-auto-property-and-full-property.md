---
title: auto プロパティと full プロパティの間で変換する
ms.date: 03/27/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 8950ce27e95a59f5425419dcac5bd807193d51b6
ms.sourcegitcommit: d6828e7422c8d74ec1e99146fedf0a05f757245f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2020
ms.locfileid: "80395737"
---
# <a name="convert-between-auto-property-and-full-property"></a>auto プロパティと full プロパティの間で変換する

このリファクタリングは以下に適用されます。

- C#

**概要:** 自動実装プロパティと完全なプロパティの変換を行います。

**条件:** プロパティのロジックが変更された。

**理由:** 自動実装プロパティと完全なプロパティの変換は手動で行うことができますが、この機能によって自動的に処理されます。 

## <a name="how-to"></a>方法

1. プロパティ名にカーソルを置きます。
2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。
3. 次の 2 つのオプションから選択します。 

    **[自動プロパティに変換する]** を選択します。

   ![自動プロパティを完全なプロパティに変換する](media/convert-auto-property-to-full-property.png) 

    **[自動プロパティを使用する]** を選択します。 

    ![完全なプロパティを自動プロパティに変換する](media/convert-full-property-to-auto-property.png) 

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)

---
title: auto プロパティと full プロパティの間で変換する
description: '[クイック アクションとリファクタリング] メニューを使用して、自動実装プロパティと完全なプロパティの間で変換を行う方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 03/27/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: b53f337b538ff1c0aef84272eea7d9e032eb2c1d
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96040837"
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

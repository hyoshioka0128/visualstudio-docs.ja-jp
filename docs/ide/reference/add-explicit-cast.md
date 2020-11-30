---
title: 明示的なキャストの追加
description: コードのコンテキストに基づいて、明示的なキャストを式に自動的に追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 03/26/2020
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: a8208ec9c84eb076ab5c313b3078d3853619fb06
ms.sourcegitcommit: 935e4d9a20928b733e573b6801a6eaff0d0b1b14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "95870847"
---
# <a name="add-explicit-cast"></a>明示的なキャストの追加

このコード生成は以下に適用されます。

- C#

**概要:** 使用に基づいて、明示的なキャストを式に自動的に追加できます。

**条件:** 明示的なキャストを式に追加する必要があり、これを自動的に適切に割り当てたい。

**理由:** 明示的なキャストを式に手動で追加することもできますが、この機能によりコード コンテキストに基づいて自動的に追加されます。

## <a name="how-to-use-it"></a>使用方法

1. エラーにキャレットを配置します。
2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。
3. **[明示的なキャストの追加]** を選択します。

   ![Visual Studio での [明示的なキャストの追加] のクイック アクション](media/add-explicit-cast.png)

## <a name="see-also"></a>関連項目

- [コード生成](../code-generation-in-visual-studio.md)
- [リファクタリング](../refactoring-in-visual-studio.md)

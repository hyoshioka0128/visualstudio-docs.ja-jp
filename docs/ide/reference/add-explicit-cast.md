---
title: 明示的なキャストの追加
description: コードのコンテキストに基づいて、明示的なキャストを式に自動的に追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 03/26/2020
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 93365ea32ce2ad0b07b8285e3787a7a7edefffbc
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99956660"
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

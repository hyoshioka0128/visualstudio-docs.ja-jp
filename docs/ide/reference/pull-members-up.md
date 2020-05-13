---
title: メンバーのプル アップ
ms.date: 02/13/2019
ms.topic: reference
author: kendrahavens
ms.author: kehavens
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 2d1f7deb7aca1fed7b75b66b17ce2e4d63768a0d
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "62969175"
---
# <a name="pull-members-up"></a>メンバーのプル アップ

このリファクタリングは以下に適用されます。

- C#

- Visual Basic

**概要:** 基本データ型にメンバーをプル アップできます。

**条件:** インターフェイスを実装し、メンバーを基本データ型に移動したい場合です。

**理由:** メンバーをプル アップすると、インターフェイスのその他の実装がそれらのメンバーを継承するようになります。

## <a name="how-to"></a>方法

1. 実装されているインターフェイスの任意のメンバーの上にカーソルを置きます。
2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。

   ![メンバーのプル アップ](media/pull-members-up.png)

2. **[Pull Members up to base type]** \(基本データ型にメンバーをプル アップする\) を選択します。

3. ダイアログで、選択したインターフェイスに追加するメンバーを選択します。

   ![メンバーのプル アップ](media/pull-members-up-dialog.png)

4. **[OK]** をクリックします。 選択したメンバーがインターフェイスにプル アップされます。

   ![メンバーのプル アップの完了](media/pull-members-up-completed.png)

## <a name="see-also"></a>関連項目

- [リファクタリング](../refactoring-in-visual-studio.md)

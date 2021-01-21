---
title: コンストラクターからプライベート フィールドとプロパティを生成する
description: '[クイックアクションとリファクタリング] メニューを使用して、コンストラクターからプライベート フィールドまたはプロパティを生成する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 06/20/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: e989efed8b58746312ed5f5a510efa049393f3db
ms.sourcegitcommit: 2cf87f79762906ccaa133a7645aa4c77a0bed7da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2020
ms.locfileid: "96617462"
---
# <a name="generate-private-field-and-property-from-constructor"></a>コンストラクターからプライベート フィールドとプロパティを生成する

このリファクタリングは以下に適用されます。 

- C# 

**概要:** コンストラクターからプライベート フィールドまたはプロパティを生成します。 

**条件:** コンストラクターからプライベート フィールドまたはプロパティをすばやく追加し、初期化する必要があります。

**理由:** プライベート フィールドとプロパティを記述することは、時間がかかり、反復的になることがあります。 このリファクタリングを使用すると、簡単でプログラムがより堅牢になります。

## <a name="how-to"></a>方法 

1. コンストラクター内のパラメーター名にカーソルを置きます。

2. 行の任意の場所で **Ctrl**+ **.** キーを押すと、 **[クイック アクションとリファクタリング]** メニューをトリガーします。
   
3. 次に、次のいずれかを選択します。

- **[フィールド '{0}' を作成して初期化する]** または **[プロパティ '{0}' を作成して初期化する]** 。

   ![コンストラクターからプライベートフィールドを生成する](media/generate-private-field-from-constructor.png)

## <a name="see-also"></a>関連項目 

- [リファクタリング](../refactoring-in-visual-studio.md)

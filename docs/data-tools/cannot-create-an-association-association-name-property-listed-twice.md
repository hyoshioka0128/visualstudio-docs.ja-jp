---
title: プロパティが2回表示されます
description: 関連付けを作成できません - プロパティが 2 回リストされています
ms.date: 11/04/2016
ms.topic: error-reference
ms.technology: vs-data-tools
ms.assetid: 3ced8bda-210e-4caf-9d8f-96cdbba19251
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 3c496a25b093c88cca68d31bd22ccc6deca9a33a
ms.sourcegitcommit: 2a201c93ed526b0f7e5848657500f1111b08ac2a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2020
ms.locfileid: "89743203"
---
# <a name="cannot-create-an-association-ltassociation-namegt---property-listed-twice"></a>関連付け &lt;関連付けの名前&gt; を作成できません - プロパティが 2 回リストされています

関連付けを作成できません \<association name> 。 同じプロパティが複数回表示されて \<property name> います:。

関連付けは、**[関連付けエディター]** ダイアログ ボックスで選択された **[関連付けのプロパティ]** によって定義されます。 プロパティは、関連付けのクラスごとに 1 回のみリストできます。

メッセージに示されているプロパティは、Parent クラスまたは Child クラスの **[関連付けのプロパティ]** に複数回表示されます。

## <a name="to-resolve-this-condition"></a>この状況の解決方法

- メッセージを確認し、メッセージで指定されているプロパティに注目します。

- **[OK]** をクリックしてメッセージ ボックスを閉じます。

- **[関連付けのプロパティ]** を調べて、重複エントリを削除します。

- **[OK]** をクリックします。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [方法: LINQ to SQL クラス間の関連付けを作成する (O/R デザイナー)](../data-tools/how-to-create-an-association-relationship-between-linq-to-sql-classes-o-r-designer.md)
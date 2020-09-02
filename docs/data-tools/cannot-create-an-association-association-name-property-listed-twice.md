---
title: 関連付けを作成できません - プロパティが 2 回リストされています
ms.date: 11/04/2016
ms.topic: error-reference
ms.technology: vs-data-tools
ms.assetid: 3ced8bda-210e-4caf-9d8f-96cdbba19251
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 50c9311ef09172ea082d2419495f26b51ff1d6a4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85536800"
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
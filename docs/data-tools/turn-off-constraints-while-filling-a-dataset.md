---
title: データセットの読み込み中に制約をオフにする
description: データセットの読み込み中に制約をオフにする方法について説明します。 プログラムによって、またはデータセットデザイナーを使用して、更新の制約を中断します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- DataRow.BeginEdit
- DataRow.EndEdit
- DataRow.CancelEdit
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- updating datasets, constraints
- constraints [Visual Basic], datasets
- datasets [Visual Basic], constraints
- constraints [Visual Basic], suspending during dataset update
ms.assetid: 553f7d0c-2faa-4c17-b226-dd02855bf1dc
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 8a4d1e17d2f6a0159a9c0187d5e1a3d16216d0ba
ms.sourcegitcommit: 72a49c10a872ab45ec6c6d7c4ac7521be84526ff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2020
ms.locfileid: "94998318"
---
# <a name="turn-off-constraints-while-filling-a-dataset"></a>データセットの読み込み中に制約をオフにする

データセットに制約 (外部キー制約など) が含まれている場合は、データセットに対して実行される操作の順序に関連するエラーが発生することがあります。 たとえば、関連する親レコードを読み込む前に子レコードを読み込むと、制約に違反してエラーが発生する可能性があります。 子レコードを読み込んだ直後に、関連する親があるかどうかが制約でチェックされ、エラーが生成されます。

一時的に制約を中断する機構がない場合は、レコードを子テーブルに読み込もうとするたびにエラーが生成されます。 データセットのすべての制約を中断する別の方法として、<xref:System.Data.DataRow.BeginEdit%2A> プロパティおよび <xref:System.Data.DataRow.EndEdit%2A> プロパティを使用できます。

> [!NOTE]
> 検証イベント ( <xref:System.Data.DataTable.ColumnChanging> やなど <xref:System.Data.DataTable.RowChanging> ) は、制約がオフになっている場合には発生しません。

## <a name="to-suspend-update-constraints-programmatically"></a>更新制約をプログラムによって中断するには

- 次の例は、データセットでの制約チェックを一時的に無効にする方法を示しています。

     [!code-csharp[VbRaddataEditing#10](../data-tools/codesnippet/CSharp/turn-off-constraints-while-filling-a-dataset_1.cs)]
     [!code-vb[VbRaddataEditing#10](../data-tools/codesnippet/VisualBasic/turn-off-constraints-while-filling-a-dataset_1.vb)]

## <a name="to-suspend-update-constraints-using-the-dataset-designer"></a>データセット デザイナーを使って更新制約を中断するには

1. **データセット デザイナー** でご自分のデータセットを開きます。 詳細については、「 [チュートリアル: データセットデザイナーでのデータセットの作成](walkthrough-creating-a-dataset-with-the-dataset-designer.md)」を参照してください。

2. **[プロパティ]** ウィンドウで、 <xref:System.Data.DataSet.EnforceConstraints%2A> プロパティを `false`に設定します。

## <a name="see-also"></a>こちらもご覧ください

- [TableAdapters を使用してデータセットを入力する](../data-tools/fill-datasets-by-using-tableadapters.md)
- [データセットのリレーションシップ](../data-tools/relationships-in-datasets.md)

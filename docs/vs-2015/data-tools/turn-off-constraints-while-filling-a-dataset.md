---
title: データセットの読み込み中に制約をオフにする |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
f1_keywords:
- DataRow.BeginEdit
- DataRow.EndEdit
- DataRow.CancelEdit
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- updating datasets, constraints
- constraints [Visual Basic], datasets
- datasets [Visual Basic], constraints
- constraints [Visual Basic], suspending during dataset update
ms.assetid: 553f7d0c-2faa-4c17-b226-dd02855bf1dc
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6646f669bf2c465d8e0f705f8fba956b979952ee
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667160"
---
# <a name="turn-off-constraints-while-filling-a-dataset"></a>データセットの読み込み中に制約をオフにする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

データセットに制約 (外部キー制約など) が含まれている場合は、データセットに対して実行される操作の順序に関連するエラーが発生する可能性があります。 たとえば、loadingrelated 親レコードの前に子レコードを読み込むと、制約に違反してエラーが発生する可能性があります。 子レコードを読み込んだ直後に、関連する親があるかどうかが制約でチェックされ、エラーが生成されます。

 一時的に制約を中断する機構がない場合は、レコードを子テーブルに読み込もうとするたびにエラーが生成されます。 データセットのすべての制約を中断する別の方法として、<xref:System.Data.DataRow.BeginEdit%2A> プロパティおよび <xref:System.Data.DataRow.EndEdit%2A> プロパティを使用できます。

> [!NOTE]
> 検証イベント ( <xref:System.Data.DataTable.ColumnChanging> やなど <xref:System.Data.DataTable.RowChanging> ) は、制約がオフになっている場合には発生しません。

### <a name="to-suspend-update-constraints-programmatically"></a>更新制約をプログラムによって中断するには

- 次の例は、データセットでの制約チェックを一時的に無効にする方法を示しています。

     [!code-csharp[VbRaddataEditing#10](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs#10)]
     [!code-vb[VbRaddataEditing#10](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb#10)]

### <a name="to-suspend-update-constraints-using-the-dataset-designer"></a>データセット デザイナーを使って更新制約を中断するには

1. データセット デザイナーでデータセットを開きます。 詳細については、「 [方法: データセットデザイナーでデータセットを開く](https://msdn.microsoft.com/library/36fc266f-365b-42cb-aebb-c993dc2c47c3)」を参照してください。

2. **[プロパティ]** ウィンドウで、 <xref:System.Data.DataSet.EnforceConstraints%2A> プロパティを `false`に設定します。

## <a name="see-also"></a>参照
 [データセット内の tableadapter リレーションシップ](../data-tools/relationships-in-datasets.md)[を使用してデータセットにデータを格納する](../data-tools/fill-datasets-by-using-tableadapters.md)

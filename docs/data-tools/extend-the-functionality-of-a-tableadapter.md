---
title: TableAdapter の機能を拡張する
description: Tableadapter の部分クラスファイルにコードを追加して、TableAdapter の機能を拡張する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], TableAdapters
- data [Visual Studio], extending TableAdapters
- TableAdapters, adding functionality
ms.assetid: 418249c8-c7f3-47ef-a94c-744cb6fe6aaf
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: bfc0f68f38f801d63367b1ee9150c723767ec667
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99858879"
---
# <a name="extend-the-functionality-of-a-tableadapter"></a>TableAdapter の機能を拡張する

Tableadapter の部分クラスファイルにコードを追加することにより、TableAdapter の機能を拡張できます。

TableAdapter を定義するコードは、 **データセットデザイナー** 内の tableadapter に変更が加えられた場合、またはウィザードによって tableadapter の構成が変更された場合に再生成されます。 TableAdapter の再生成時にコードが削除されないようにするには、TableAdapter の部分クラスファイルにコードを追加します。

部分クラスを使用すると、特定のクラスのコードを複数の物理ファイルに分割できます。 詳細については、「 [partial](/dotnet/visual-basic/language-reference/modifiers/partial) または [partial (型)](/dotnet/csharp/language-reference/keywords/partial-type)」を参照してください。

## <a name="locate-tableadapters-in-code"></a>コードでの Tableadapter の検索

Tableadapter は **データセットデザイナー** で設計されていますが、生成される tableadapter クラスは、の入れ子になったクラスではありません <xref:System.Data.DataSet> 。 Tableadapter は、TableAdapter に関連付けられたデータセットの名前に基づいて名前空間に配置されます。 たとえば、アプリケーションにという名前のデータセットが含まれている場合、 `HRDataSet` tableadapter は名前空間に配置され `HRDataSetTableAdapters` ます。 (名前付け規則は、次のパターンに従います: *DatasetName*  +  `TableAdapters` )。

次の例では、という名前の TableAdapter `CustomersTableAdapter` がプロジェクト内に存在することを前提としてい `NorthwindDataSet` ます。

### <a name="to-create-a-partial-class-for-a-tableadapter"></a>TableAdapter の部分クラスを作成するには

1. [ **プロジェクト** ] メニューの [ **クラスの追加**] をクリックして、新しいクラスをプロジェクトに追加します。

2. クラスに `CustomersTableAdapterExtended` という名前を付けます。

3. **[追加]** を選択します。

4. 次のように、プロジェクトの正しい名前空間と部分クラス名でコードを置き換えます。

     [!code-csharp[VbRaddataTableAdapters#2](../data-tools/codesnippet/CSharp/extend-the-functionality-of-a-tableadapter_1.cs)]
     [!code-vb[VbRaddataTableAdapters#2](../data-tools/codesnippet/VisualBasic/extend-the-functionality-of-a-tableadapter_1.vb)]

## <a name="see-also"></a>関連項目

- [TableAdapters を使用してデータセットを入力する](../data-tools/fill-datasets-by-using-tableadapters.md)

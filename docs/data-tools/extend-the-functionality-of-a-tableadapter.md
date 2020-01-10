---
title: TableAdapter の機能を拡張する
ms.date: 11/04/2016
ms.topic: conceptual
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
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 34a5c1601071a36ca11005503e2f443a72ca3dfe
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586641"
---
# <a name="extend-the-functionality-of-a-tableadapter"></a>TableAdapter の機能を拡張する

Tableadapter の部分クラスファイルにコードを追加することにより、TableAdapter の機能を拡張できます。

TableAdapter を定義するコードは、**データセットデザイナー**内の tableadapter に変更が加えられた場合、またはウィザードによって tableadapter の構成が変更された場合に再生成されます。 TableAdapter の再生成時にコードが削除されないようにするには、TableAdapter の部分クラスファイルにコードを追加します。

部分クラスを使用すると、特定のクラスのコードを複数の物理ファイルに分割できます。 詳細については、「 [partial](/dotnet/visual-basic/language-reference/modifiers/partial)または[partial (型)](/dotnet/csharp/language-reference/keywords/partial-type)」を参照してください。

## <a name="locate-tableadapters-in-code"></a>コードでの Tableadapter の検索

Tableadapter は**データセットデザイナー**で設計されていますが、生成される tableadapter クラスは <xref:System.Data.DataSet>の入れ子になったクラスではありません。 Tableadapter は、TableAdapter に関連付けられたデータセットの名前に基づいて名前空間に配置されます。 たとえば、アプリケーションに `HRDataSet`という名前のデータセットが含まれている場合、Tableadapter は `HRDataSetTableAdapters` 名前空間に配置されます。 (名前付け規則がこのパターンに従います: *DatasetName* + `TableAdapters`)。

次の例では、`NorthwindDataSet`のプロジェクトに `CustomersTableAdapter`という名前の TableAdapter があることを前提としています。

### <a name="to-create-a-partial-class-for-a-tableadapter"></a>TableAdapter の部分クラスを作成するには

1. **[プロジェクト]** メニューの **[クラスの追加]** をクリックして、新しいクラスをプロジェクトに追加します。

2. クラスに `CustomersTableAdapterExtended` という名前を付けます。

3. **[追加]** を選びます。

4. 次のように、プロジェクトの正しい名前空間と部分クラス名でコードを置き換えます。

     [!code-csharp[VbRaddataTableAdapters#2](../data-tools/codesnippet/CSharp/extend-the-functionality-of-a-tableadapter_1.cs)]
     [!code-vb[VbRaddataTableAdapters#2](../data-tools/codesnippet/VisualBasic/extend-the-functionality-of-a-tableadapter_1.vb)]

## <a name="see-also"></a>関連項目

- [TableAdapters を使用してデータセットを入力する](../data-tools/fill-datasets-by-using-tableadapters.md)

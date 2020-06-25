---
title: '方法: 複数形化をオンおよびオフにする (O-R デザイナー)'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 9b693bc3-303a-40a9-97ee-9cef5ca3ae81
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 6675a136b2bbdc1ef19d90ee19ecf7497053bfe1
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282048"
---
# <a name="how-to-turn-pluralization-on-and-off-or-designer"></a>方法: 複数形化をオンおよびオフにする (O/R デザイナー)
既定では、名前がで終わるか**サーバーエクスプローラー**からの名前を持つデータベースオブジェクト、または[Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)に**データベースエクスプローラー**されているデータベースオブジェクトをドラッグすると、生成されたエンティティクラスの名前が複数形から単数形に変更されます。 この処理は、インスタンス化されたエンティティ クラスが単一のデータ レコードにマップされるという事実をより正確に表すために行われます。 たとえば、 `Customers` **O/R デザイナー**にテーブルを追加すると、という名前のエンティティクラスが生成 `Customer` されます。これは、クラスが1人の顧客に対してのみデータを保持するためです。

> [!NOTE]
> 複数形化は、英語バージョンの Visual Studio でのみ、既定でオンになります。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-turn-pluralization-on-and-off"></a>複数形化をオンまたはオフにするには

1. **[ツール]** メニューの **[オプション]** をクリックします。

2. **[オプション]** ダイアログ ボックスの **[データベース ツール]** を展開します。

    > [!NOTE]
    > **[データベース ツール]** ノードが表示されない場合は、**[すべての設定を表示]** を選択します。

3. **[O/R デザイナー]** をクリックします。

4. クラス名を変更し**Enabled**ないように O/R デザイナーを設定するには、**複数形化の名前**を Enabled False に設定し  =  **False** **O/R Designer**ます。

5. **Pluralization of names** **Enabled**  =  **O/R デザイナー**に追加されたオブジェクトのクラス名に複数形化ルールを適用するに**は、** 複数形化の名前を Enabled に設定します。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)

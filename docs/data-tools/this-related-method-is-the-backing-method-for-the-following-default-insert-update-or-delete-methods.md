---
title: この関連メソッドは、次の既定の挿入、更新、または削除メソッドのバッキング メソッドです
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 62afa6da-97cf-48b9-8de3-33e4d72a0377
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 252303c4933501dd3a4672329d66ef4910238a08
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85535253"
---
# <a name="this-related-method-is-the-backing-method-for-the-following-default-insert-update-or-delete-methods"></a>この関連メソッドは、次の既定の挿入、更新、または削除メソッドのバッキング メソッドです

この関連メソッドは、次の既定のメソッド、 `Insert` `Update` メソッド、またはメソッドのバッキングメソッドです `Delete` 。 削除されると、これらのメソッドも削除されます。 続行しますか?

選択された `DataContext` メソッドは、現在、 `Insert` `Update` `Delete` **O/R デザイナー**のいずれかのエンティティクラスに対して、、、のいずれかのメソッドとして使用されています。 選択したメソッドを削除すると、このメソッドを使用していたエンティティクラスは、更新時に挿入、更新、または削除を実行する既定の実行時の動作に戻ります。

## <a name="selected-method-options"></a>選択されたメソッドのオプション

- 選択したメソッドを削除して、エンティティクラスがランタイムの更新プログラムを使用するようにするには、[ **はい**] をクリックします。

   選択したメソッドが削除され、このメソッドを使用して更新動作をオーバーライドしたクラスは、既定の LINQ to SQL の実行時の動作を使用するように戻されます。

- 選択した方法を変更せずにメッセージボックスを閉じるには、[ **いいえ**] をクリックします。

   メッセージ ボックスが閉じ、変更は行われません。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
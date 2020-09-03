---
title: この関連メソッドは、次の既定の insert、update、または delete メソッドのバッキングメソッドです。Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 62afa6da-97cf-48b9-8de3-33e4d72a0377
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 84d27dc6f5081a36a237748c091429cfdabbe841
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667182"
---
# <a name="this-related-method-is-the-backing-method-for-the-following-default-insert-update-or-delete-methods"></a>この関連メソッドは、次の既定の挿入、更新、または削除メソッドのバッキング メソッドです
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この関連メソッドは、次の既定の挿入、更新、または削除メソッドのバッキング メソッドです。 削除されると、これらのメソッドも削除されます。 続行しますか?

 選択した `DataContext` メソッドは、O/R デザイナーで、いずれかのエンティティ クラスの挿入、更新、または削除メソッドとして現在使用されています。 選択したメソッドを削除すると、このメソッドを使用していたエンティティ クラスの更新時の挿入、更新、または削除の動作は、既定のランタイムの動作に戻ることになります。

### <a name="to-delete-the-selected-method-causing-the-entity-class-to-use-runtime-updates"></a>選択したメソッドを削除して、エンティティ クラスでランタイムの更新動作が使用されるようにするには

- **[はい]** をクリックします。

     選択されたメソッドが削除され、このメソッドを使用して更新動作をオーバーライドしていたすべてのクラスは、既定の LINQ to SQL ランタイムの動作を使用するように戻されます。

### <a name="to-close-the-message-box-leaving-the-selected-method-unchanged"></a>メッセージ ボックスを閉じて、選択したメソッドが変更されないようにするには

- **[いいえ]** をクリックします。

     メッセージ ボックスが閉じ、変更は行われません。

## <a name="see-also"></a>参照
 [DataContext メソッド (o/r デザイナー)](../data-tools/datacontext-methods-o-r-designer.md)方法: [Visual Studio の LINQ to SQL ツールで](../data-tools/linq-to-sql-tools-in-visual-studio2.md) [、更新、挿入、および削除 (o/r デザイナー) を実行するストアドプロシージャを割り当てる](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)

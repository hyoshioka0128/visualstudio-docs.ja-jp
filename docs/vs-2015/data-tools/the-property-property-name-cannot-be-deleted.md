---
title: プロパティの &lt; プロパティ名を &gt; 削除することはできません |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 55873f74-7834-4ec1-8815-eeeb65618d87
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: aca36919cb4c82d6ca76e0f3eecbbacd48cde768
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72667243"
---
# <a name="the-property-ltproperty-namegt-cannot-be-deleted"></a>プロパティの &lt; プロパティ名を &gt; 削除できません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

プロパティは、 \<property name> との間の継承の識別子プロパティとして設定されているため、削除できません \<class name>\<class name>

 選択されたプロパティは、エラー メッセージに示されているクラス間の継承に対する**識別子のプロパティ**として設定されています。 プロパティがデータ クラス間の継承構成に関与している場合、そのプロパティを削除することはできません。

 **識別子のプロパティ**をデータ クラスの別のプロパティに設定して、目的のプロパティが正常に削除されるようにしてください。

### <a name="to-correct-this-error"></a>このエラーを解決するには

1. O/R デザイナーで、エラー メッセージに示されているデータ クラスを接続する継承線を選択します。

2. **識別子** プロパティを別のプロパティに設定します。

3. プロパティの削除を再試行します。

## <a name="see-also"></a>参照
 [方法: o/r デザイナーのデータクラスの継承を使用して継承を構成](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md)する [(o/r デザイナー)](../data-tools/data-class-inheritance-o-r-designer.md) [チュートリアル: 単一テーブル継承を使用した LINQ to SQL クラスの作成 (o/r デザイナー)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)

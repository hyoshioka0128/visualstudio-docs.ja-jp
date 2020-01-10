---
title: デザイナーに追加されたオブジェクトが別のデータ接続を使用する
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 332ed2f3-3377-4d51-8e3b-fdb98231978e
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 9a3a2e00ccdee20fd374c52235ba648f89a0faa1
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586160"
---
# <a name="the-objects-you-are-adding-to-the-designer-use-a-different-data-connection-than-the-designer"></a>デザイナーに追加しようとしているオブジェクトは、デザイナーとは異なるデータ接続を使用しています

デザイナーに追加する対象のオブジェクトは、デザイナーが現在使用しているのとは異なるデータ接続を使用しています。 デザイナーが使用している接続に置き換えますか?

**オブジェクトリレーショナルデザイナー** (**O/R デザイナー**) に項目を追加すると、すべての項目が1つの共有データ接続を使用します。 (デザインサーフェイスは、サーフェイス上のすべてのオブジェクトに対して単一の接続を使用する <xref:System.Data.Linq.DataContext>を表します)。デザイナーによって現在使用されているデータ接続とは異なるデータ接続を使用するオブジェクトをデザイナーに追加すると、このメッセージが表示されます。 このエラーを解決するために、既存の接続を維持するように選択できます。 その場合、選択したオブジェクトは追加されません。 別の方法として、オブジェクトを追加し、<xref:System.Data.Linq.DataContext> 接続を新しい接続にリセットすることもできます。

## <a name="connection-options"></a>接続オプション

- 既存の接続を、選択したオブジェクトによって使用されている接続に置き換えるには、[**はい]** をクリックします。

   選択したオブジェクトが**O/R デザイナー**に追加され、 *DataContext 接続*が新しい接続に設定されます。

   > [!NOTE]
   > **[はい]** をクリックすると、 **O/R デザイナー**のすべてのエンティティクラスが新しい接続にマップされます。

- 既存の接続を引き続き使用して、選択したオブジェクトの追加をキャンセルするには、 **[いいえ]** をクリックします。

   操作がキャンセルされます。 *DataContext.Connection* は、既存の接続に設定されたままになります。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
